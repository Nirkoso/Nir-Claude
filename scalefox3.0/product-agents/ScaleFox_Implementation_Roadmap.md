# ScaleFox Agent System - Implementation Roadmap
## Detailed Technical Specifications & Execution Plan

---

## Implementation Philosophy

**Core Principles:**
1. **Agent-First Design**: Each agent is independently deployable and testable
2. **Progressive Enhancement**: Start with core agents, add sophistication iteratively
3. **User Value First**: Prioritize agents that deliver immediate user value
4. **Learning Systems**: Build feedback loops from day one
5. **Scalable Architecture**: Design for scale even if starting small

---

## Phase 1: Foundation (Weeks 1-4)
*Goal: Get users from URL to basic company profile & personas*

### Week 1-2: Infrastructure & Discovery Agent

#### 1.1 Core Infrastructure Setup
**Database:**
```sql
-- Essential tables
CREATE TABLE users (
    user_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE companies (
    company_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(user_id),
    company_name VARCHAR(255) NOT NULL,
    company_url VARCHAR(500) NOT NULL,
    discovery_data JSONB,
    last_updated TIMESTAMP DEFAULT NOW()
);

CREATE TABLE agent_conversations (
    conversation_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(user_id),
    agent_name VARCHAR(50) NOT NULL,
    messages JSONB,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE agent_knowledge (
    knowledge_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    agent_name VARCHAR(50) NOT NULL,
    entity_type VARCHAR(50),
    entity_id UUID,
    knowledge_data JSONB,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);
```

**Agent Framework (Python):**
```python
# agents/base_agent.py
from abc import ABC, abstractmethod
from typing import Dict, List, Any
import logging

class BaseAgent(ABC):
    def __init__(self, agent_name: str, db_connection, llm_client):
        self.agent_name = agent_name
        self.db = db_connection
        self.llm = llm_client
        self.logger = logging.getLogger(agent_name)
        self.system_prompt = self.load_system_prompt()
        
    @abstractmethod
    def load_system_prompt(self) -> str:
        """Load agent-specific system prompt"""
        pass
    
    @abstractmethod
    async def process_message(self, user_message: str, context: Dict) -> Dict:
        """Process user message and return response"""
        pass
    
    async def get_knowledge(self, entity_id: str) -> Dict:
        """Retrieve agent's knowledge about entity"""
        query = """
            SELECT knowledge_data 
            FROM agent_knowledge 
            WHERE agent_name = %s AND entity_id = %s
            ORDER BY updated_at DESC LIMIT 1
        """
        result = await self.db.fetch_one(query, (self.agent_name, entity_id))
        return result['knowledge_data'] if result else {}
    
    async def store_knowledge(self, entity_id: str, entity_type: str, data: Dict):
        """Store agent's knowledge"""
        query = """
            INSERT INTO agent_knowledge 
            (agent_name, entity_type, entity_id, knowledge_data)
            VALUES (%s, %s, %s, %s)
            ON CONFLICT (agent_name, entity_id) 
            DO UPDATE SET knowledge_data = %s, updated_at = NOW()
        """
        await self.db.execute(query, (
            self.agent_name, entity_type, entity_id, data, data
        ))
    
    async def use_tool(self, tool_name: str, params: Dict) -> Any:
        """Execute tool with given parameters"""
        tool_func = getattr(self.tools, tool_name, None)
        if tool_func:
            return await tool_func(**params)
        raise ValueError(f"Tool {tool_name} not found")
    
    async def chat(self, messages: List[Dict], tools: List[Dict] = None) -> Dict:
        """LLM chat with function calling support"""
        return await self.llm.chat(
            messages=messages,
            system_prompt=self.system_prompt,
            tools=tools
        )
```

#### 1.2 Discovery Agent Implementation

**Tools Module:**
```python
# agents/tools/discovery_tools.py
import aiohttp
from bs4 import BeautifulSoup
from typing import Dict, List

class DiscoveryTools:
    def __init__(self):
        self.session = aiohttp.ClientSession()
    
    async def scrape_website(self, url: str) -> Dict:
        """Scrape company website for key information"""
        try:
            async with self.session.get(url, timeout=30) as response:
                html = await response.text()
                soup = BeautifulSoup(html, 'html.parser')
                
                return {
                    'title': soup.find('title').text if soup.find('title') else '',
                    'meta_description': self._get_meta_description(soup),
                    'headings': self._extract_headings(soup),
                    'text_content': self._extract_text_content(soup),
                    'internal_links': self._extract_links(soup, url)
                }
        except Exception as e:
            return {'error': str(e)}
    
    async def search_web(self, query: str, num_results: int = 3) -> List[Dict]:
        """Search web for company information"""
        # Integration with web_search tool
        pass
    
    async def get_industry_data(self, industry: str) -> Dict:
        """Fetch industry benchmarks and trends"""
        # Integration with industry databases
        pass
    
    def _get_meta_description(self, soup) -> str:
        meta = soup.find('meta', attrs={'name': 'description'})
        return meta.get('content', '') if meta else ''
    
    def _extract_headings(self, soup) -> List[str]:
        return [h.text.strip() for h in soup.find_all(['h1', 'h2', 'h3'])]
    
    def _extract_text_content(self, soup) -> str:
        # Remove script and style elements
        for script in soup(['script', 'style']):
            script.decompose()
        return ' '.join(soup.stripped_strings)
    
    def _extract_links(self, soup, base_url: str) -> List[Dict]:
        links = []
        for a in soup.find_all('a', href=True):
            href = a['href']
            if href.startswith('/'):
                href = base_url + href
            links.append({
                'url': href,
                'text': a.text.strip(),
                'is_internal': base_url in href
            })
        return links
```

**Discovery Agent:**
```python
# agents/discovery_agent.py
from agents.base_agent import BaseAgent
from agents.tools.discovery_tools import DiscoveryTools
import json

class DiscoveryAgent(BaseAgent):
    def __init__(self, db_connection, llm_client):
        self.tools = DiscoveryTools()
        super().__init__("discovery", db_connection, llm_client)
    
    def load_system_prompt(self) -> str:
        with open('prompts/1_company_info_prompt.md', 'r') as f:
            return f.read()
    
    async def process_message(self, user_message: str, context: Dict) -> Dict:
        """Handle user queries about company information"""
        
        # Get existing knowledge
        company_id = context.get('company_id')
        existing_knowledge = await self.get_knowledge(company_id) if company_id else {}
        
        # Build conversation with context
        messages = [
            {
                "role": "system",
                "content": self.system_prompt
            },
            {
                "role": "user",
                "content": f"Existing knowledge: {json.dumps(existing_knowledge)}\n\nUser query: {user_message}"
            }
        ]
        
        # Define available tools
        tools = [
            {
                "name": "scrape_website",
                "description": "Scrape a company website for information",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "url": {"type": "string", "description": "Website URL"}
                    },
                    "required": ["url"]
                }
            },
            {
                "name": "search_web",
                "description": "Search the web for company information",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "query": {"type": "string"},
                        "num_results": {"type": "integer", "default": 3}
                    },
                    "required": ["query"]
                }
            }
        ]
        
        # LLM decides what to do
        response = await self.chat(messages, tools)
        
        # Execute tool calls if needed
        if response.get('tool_calls'):
            for tool_call in response['tool_calls']:
                tool_name = tool_call['function']['name']
                tool_params = json.loads(tool_call['function']['arguments'])
                
                tool_result = await self.use_tool(tool_name, tool_params)
                
                # Add tool result to conversation
                messages.append({
                    "role": "function",
                    "name": tool_name,
                    "content": json.dumps(tool_result)
                })
            
            # Get final response after tool execution
            response = await self.chat(messages)
        
        # Extract and store knowledge
        if 'company_profile' in response:
            await self.store_knowledge(
                company_id, 
                'company', 
                response['company_profile']
            )
        
        return {
            "message": response.get('message', ''),
            "data": response.get('data', {}),
            "actions_taken": response.get('actions_taken', [])
        }
    
    async def initialize_company(self, company_name: str, company_url: str) -> Dict:
        """Initialize company research (onboarding trigger)"""
        
        self.logger.info(f"Initializing research for {company_name}")
        
        # Scrape website
        website_data = await self.tools.scrape_website(company_url)
        
        # Search for company info
        search_results = await self.tools.search_web(
            f"{company_name} company product offering"
        )
        
        # Build context for LLM
        context = {
            "company_name": company_name,
            "company_url": company_url,
            "website_data": website_data,
            "search_results": search_results
        }
        
        # Generate company profile
        messages = [
            {
                "role": "user",
                "content": f"Analyze this company and create a profile:\n{json.dumps(context)}"
            }
        ]
        
        response = await self.chat(messages)
        
        # Parse JSON response
        company_profile = json.loads(response['content'])
        
        # Store in database
        query = """
            INSERT INTO companies (user_id, company_name, company_url, discovery_data)
            VALUES (%s, %s, %s, %s)
            RETURNING company_id
        """
        result = await self.db.fetch_one(
            query, 
            (context['user_id'], company_name, company_url, company_profile)
        )
        
        company_id = result['company_id']
        
        # Store agent knowledge
        await self.store_knowledge(company_id, 'company', company_profile)
        
        return {
            "company_id": company_id,
            "company_profile": company_profile,
            "status": "completed"
        }
```

**Task Checklist Week 1-2:**
- [ ] Set up database with core schema
- [ ] Implement BaseAgent framework
- [ ] Create DiscoveryTools with web scraping
- [ ] Build DiscoveryAgent with company_info prompt
- [ ] Integrate web_search tool
- [ ] Test with 10+ real company URLs
- [ ] Handle edge cases (blocked sites, timeouts)

---

### Week 3-4: Brand Agent & ICP Agent

#### 1.3 Brand Agent Implementation

**Brand Tools:**
```python
# agents/tools/brand_tools.py
from PIL import Image
import requests
from io import BytesIO
import colorgram

class BrandTools:
    async def extract_logo_colors(self, logo_url: str) -> List[str]:
        """Extract dominant colors from logo"""
        response = requests.get(logo_url)
        img = Image.open(BytesIO(response.content))
        
        colors = colorgram.extract(img, 6)
        hex_colors = [self._rgb_to_hex(color.rgb) for color in colors]
        
        return hex_colors
    
    async def analyze_website_design(self, url: str) -> Dict:
        """Analyze website for design patterns"""
        # Scrape CSS, analyze layout, typography
        pass
    
    async def analyze_social_tone(self, linkedin_url: str) -> Dict:
        """Analyze tone from social media"""
        # Scrape recent posts, analyze language
        pass
    
    def _rgb_to_hex(self, rgb) -> str:
        return '#{:02x}{:02x}{:02x}'.format(rgb.r, rgb.g, rgb.b)
```

**Brand Agent:**
```python
# agents/brand_agent.py
class BrandAgent(BaseAgent):
    def __init__(self, db_connection, llm_client):
        self.tools = BrandTools()
        super().__init__("brand", db_connection, llm_client)
    
    def load_system_prompt(self) -> str:
        # Brand agent system prompt (new, to be created)
        return """
        You are a brand identity expert. Your mission is to analyze and codify 
        a company's visual and verbal brand identity.
        
        Extract:
        - Visual identity: colors, typography, design style
        - Verbal identity: tone of voice, messaging patterns
        - Brand personality: attributes and characteristics
        
        Output as structured JSON.
        """
    
    async def initialize_brand(self, company_id: str) -> Dict:
        """Initialize brand analysis"""
        
        # Get company data from Discovery Agent
        discovery_data = await self.db.fetch_one(
            "SELECT discovery_data FROM companies WHERE company_id = %s",
            (company_id,)
        )
        
        company_url = discovery_data['discovery_data']['company_url']
        
        # Extract visual elements
        logo_colors = await self.tools.extract_logo_colors(f"{company_url}/logo.png")
        design_analysis = await self.tools.analyze_website_design(company_url)
        
        # Generate brand identity with LLM
        context = {
            "company_data": discovery_data['discovery_data'],
            "logo_colors": logo_colors,
            "design_analysis": design_analysis
        }
        
        response = await self.chat([{
            "role": "user",
            "content": f"Create brand identity profile:\n{json.dumps(context)}"
        }])
        
        brand_identity = json.loads(response['content'])
        
        # Store brand knowledge
        await self.store_knowledge(company_id, 'brand', brand_identity)
        
        # Update company record
        await self.db.execute(
            "UPDATE companies SET brand_data = %s WHERE company_id = %s",
            (brand_identity, company_id)
        )
        
        return brand_identity
```

#### 1.4 ICP Agent Implementation

**ICP Agent:**
```python
# agents/icp_agent.py
class ICPAgent(BaseAgent):
    def __init__(self, db_connection, llm_client):
        super().__init__("icp", db_connection, llm_client)
    
    def load_system_prompt(self) -> str:
        with open('prompts/2_Target_audience_prompt.md', 'r') as f:
            return f.read()
    
    async def generate_personas(self, company_id: str, user_input: str = "") -> List[Dict]:
        """Generate persona suggestions"""
        
        # Get company context
        company_data = await self.db.fetch_one(
            "SELECT discovery_data FROM companies WHERE company_id = %s",
            (company_id,)
        )
        
        # Build prompt with company context
        prompt_data = {
            "user_input": user_input,
            **company_data['discovery_data']
        }
        
        # Use prompt template from 2a_ICP_suggest_prompt.md
        response = await self.chat([{
            "role": "user",
            "content": f"Generate 8 distinct personas:\n{json.dumps(prompt_data)}"
        }])
        
        personas = self._parse_personas(response['content'])
        
        # Store personas
        for persona in personas:
            await self.db.execute(
                """
                INSERT INTO personas 
                (company_id, persona_data, selected)
                VALUES (%s, %s, false)
                """,
                (company_id, persona)
            )
        
        return personas
    
    async def refine_personas(self, company_id: str, selected_persona_ids: List[str]) -> Dict:
        """Refine selected personas with deep research"""
        
        # Use detailed prompt from 2_Target_audience_prompt.md
        # Conduct deeper research on selected personas
        pass
    
    def _parse_personas(self, llm_response: str) -> List[Dict]:
        """Parse persona output into structured format"""
        # Parse the 8 personas from LLM response
        pass
```

**Task Checklist Week 3-4:**
- [ ] Implement BrandTools (color extraction, design analysis)
- [ ] Build BrandAgent with brand analysis logic
- [ ] Test brand extraction on 20+ company websites
- [ ] Implement ICPAgent with persona generation
- [ ] Create persona suggestion UI
- [ ] Test persona quality with real users
- [ ] Build persona selection interface

---

### Week 4: Onboarding Agent (Basic)

**Onboarding Agent:**
```python
# agents/onboarding_agent.py
class OnboardingAgent(BaseAgent):
    def __init__(self, db_connection, llm_client):
        super().__init__("onboarding", db_connection, llm_client)
        self.workflow_steps = [
            "company_setup",
            "brand_analysis",
            "persona_selection",
            "competitor_setup",
            "theme_selection",
            "campaign_creation"
        ]
    
    async def start_onboarding(self, user_id: str, company_name: str, company_url: str):
        """Initialize onboarding workflow"""
        
        # Create onboarding session
        session = await self.db.execute(
            """
            INSERT INTO onboarding_sessions 
            (user_id, current_step, status, metadata)
            VALUES (%s, 'company_setup', 'in_progress', %s)
            RETURNING session_id
            """,
            (user_id, {'company_name': company_name, 'company_url': company_url})
        )
        
        # Trigger Discovery Agent
        discovery_result = await self.trigger_agent(
            'discovery',
            'initialize_company',
            {'company_name': company_name, 'company_url': company_url}
        )
        
        company_id = discovery_result['company_id']
        
        # Update session
        await self.update_session(session['session_id'], {
            'company_id': company_id,
            'discovery_completed': True
        })
        
        # Trigger Brand Agent (parallel)
        await self.trigger_agent(
            'brand',
            'initialize_brand',
            {'company_id': company_id}
        )
        
        # Trigger ICP Agent (parallel)
        await self.trigger_agent(
            'icp',
            'generate_personas',
            {'company_id': company_id}
        )
        
        return {
            "session_id": session['session_id'],
            "next_step": "persona_selection",
            "message": "Company setup complete! Review your personas."
        }
    
    async def trigger_agent(self, agent_name: str, method: str, params: Dict):
        """Trigger another agent's method"""
        # Agent registry/factory pattern
        agent = AgentFactory.get_agent(agent_name)
        method_func = getattr(agent, method)
        return await method_func(**params)
    
    async def get_progress(self, session_id: str) -> Dict:
        """Get onboarding progress"""
        session = await self.db.fetch_one(
            "SELECT * FROM onboarding_sessions WHERE session_id = %s",
            (session_id,)
        )
        
        return {
            "current_step": session['current_step'],
            "completed_steps": session['metadata'].get('completed_steps', []),
            "blockers": session['metadata'].get('blockers', []),
            "next_action": self._determine_next_action(session)
        }
```

**Task Checklist Week 4:**
- [ ] Implement OnboardingAgent orchestration
- [ ] Create workflow state machine
- [ ] Build agent triggering system
- [ ] Design onboarding UI flow
- [ ] Test full onboarding flow end-to-end
- [ ] Add progress tracking
- [ ] Implement error handling & recovery

---

## Phase 2: Intelligence (Weeks 5-8)
*Goal: Add competitive intelligence and strategic insights*

### Week 5-6: Competitor Agent

**Scraper Implementation:**
```python
# agents/tools/ad_scraper.py
import asyncio
from playwright.async_api import async_playwright

class AdScraper:
    async def scrape_linkedin_ads(self, company_url: str) -> List[Dict]:
        """Scrape LinkedIn ads using Playwright"""
        async with async_playwright() as p:
            browser = await p.chromium.launch(headless=True)
            page = await browser.new_page()
            
            # Navigate to LinkedIn Ad Library
            search_url = f"https://www.linkedin.com/ad/library/?company={company_url}"
            await page.goto(search_url)
            
            # Wait for ads to load
            await page.wait_for_selector('.ad-card')
            
            # Extract ad data
            ads = await page.eval_on_selector_all('.ad-card', """
                elements => elements.map(el => ({
                    title: el.querySelector('.ad-title')?.textContent,
                    description: el.querySelector('.ad-description')?.textContent,
                    image_url: el.querySelector('img')?.src,
                    cta: el.querySelector('.cta-button')?.textContent,
                    impressions: el.querySelector('.impressions')?.textContent,
                    date: el.querySelector('.ad-date')?.textContent
                }))
            """)
            
            await browser.close()
            return ads
```

**Clustering Implementation:**
```python
# agents/tools/ad_clusterer.py
import numpy as np
from sklearn.cluster import HDBSCAN
import boto3

class AdClusterer:
    def __init__(self):
        self.bedrock = boto3.client('bedrock-runtime')
    
    async def generate_embeddings(self, texts: List[str]) -> np.ndarray:
        """Generate embeddings using AWS Bedrock Titan"""
        embeddings = []
        
        for text in texts:
            response = self.bedrock.invoke_model(
                modelId='amazon.titan-embed-text-v1',
                body=json.dumps({"inputText": text})
            )
            
            result = json.loads(response['body'].read())
            embeddings.append(result['embedding'])
        
        return np.array(embeddings)
    
    async def cluster_ads(self, ads: List[Dict]) -> List[Dict]:
        """Cluster similar ads using HDBSCAN"""
        
        # Create text representations
        ad_texts = [
            f"{ad['title']} {ad['description']} {ad['cta']}"
            for ad in ads
        ]
        
        # Generate embeddings
        embeddings = await self.generate_embeddings(ad_texts)
        
        # Cluster
        clusterer = HDBSCAN(
            min_cluster_size=2,
            metric='euclidean',
            cluster_selection_method='eom'
        )
        
        cluster_labels = clusterer.fit_predict(embeddings)
        
        # Organize ads by cluster
        clusters = {}
        for i, ad in enumerate(ads):
            cluster_id = int(cluster_labels[i])
            if cluster_id not in clusters:
                clusters[cluster_id] = []
            clusters[cluster_id].append(ad)
        
        # Rank clusters by performance
        ranked_clusters = self._rank_clusters(clusters)
        
        return ranked_clusters
    
    def _rank_clusters(self, clusters: Dict) -> List[Dict]:
        """Rank clusters by performance metrics"""
        ranked = []
        
        for cluster_id, ads in clusters.items():
            # Calculate cluster score
            total_reach = sum(self._parse_impressions(ad.get('impressions', '0')) for ad in ads)
            avg_reach = total_reach / len(ads)
            best_performer = max(ads, key=lambda ad: self._parse_impressions(ad.get('impressions', '0')))
            
            score = (
                (total_reach / 10000) * 0.4 +  # Total reach (40%)
                (avg_reach / 1000) * 0.25 +     # Average reach (25%)
                (self._parse_impressions(best_performer.get('impressions', '0')) / 1000) * 0.2 +  # Best performer (20%)
                len(ads) * 0.15                 # Cluster size (15%)
            )
            
            ranked.append({
                'cluster_id': cluster_id,
                'cluster_score': score,
                'ad_count': len(ads),
                'best_ad': best_performer,
                'all_ads': ads
            })
        
        return sorted(ranked, key=lambda x: x['cluster_score'], reverse=True)
    
    def _parse_impressions(self, impressions_str: str) -> int:
        """Parse impression string like '10K' to integer"""
        if 'K' in impressions_str:
            return int(float(impressions_str.replace('K', '')) * 1000)
        elif 'M' in impressions_str:
            return int(float(impressions_str.replace('M', '')) * 1000000)
        return int(impressions_str or 0)
```

**Competitor Agent:**
```python
# agents/competitor_agent.py
class CompetitorAgent(BaseAgent):
    def __init__(self, db_connection, llm_client):
        self.scraper = AdScraper()
        self.clusterer = AdClusterer()
        super().__init__("competitor", db_connection, llm_client)
    
    async def analyze_competitor(self, competitor_url: str, company_id: str) -> Dict:
        """Scrape and analyze competitor ads"""
        
        # Scrape ads
        ads = await self.scraper.scrape_linkedin_ads(competitor_url)
        
        # Store raw ads
        competitor_id = await self._store_competitor(company_id, competitor_url)
        for ad in ads:
            await self._store_ad(competitor_id, ad)
        
        # Cluster ads
        clusters = await self.clusterer.cluster_ads(ads)
        
        # Analyze top clusters
        analyzed_clusters = []
        for cluster in clusters[:30]:  # Top 30 clusters
            best_ad_analysis = await self._analyze_ad(cluster['best_ad'])
            
            analyzed_clusters.append({
                **cluster,
                'best_ad_analysis': best_ad_analysis
            })
        
        # Store cluster data
        await self._store_clusters(competitor_id, analyzed_clusters)
        
        return {
            "competitor_id": competitor_id,
            "total_ads": len(ads),
            "cluster_count": len(clusters),
            "top_clusters": analyzed_clusters[:10]
        }
    
    async def _analyze_ad(self, ad: Dict) -> Dict:
        """Analyze individual ad using prompt 4"""
        
        # Use 4_Analyze_ad_prompt.md
        response = await self.chat([{
            "role": "user",
            "content": f"Analyze this ad:\n{json.dumps(ad)}"
        }])
        
        return json.loads(response['content'])
```

**Task Checklist Week 5-6:**
- [ ] Implement ad scraping with Playwright
- [ ] Integrate AWS Bedrock for embeddings
- [ ] Build HDBSCAN clustering pipeline
- [ ] Test clustering quality on real ad data
- [ ] Implement CompetitorAgent
- [ ] Create ad analysis with prompt 4
- [ ] Build competitor management UI
- [ ] Handle rate limiting & errors

---

### Week 7-8: Insight Agent

**Insight Agent:**
```python
# agents/insight_agent.py
class InsightAgent(BaseAgent):
    def load_system_prompt(self) -> str:
        with open('prompts/7_Analyze_Insight_prompt.md', 'r') as f:
            return f.read()
    
    async def generate_insights(self, company_id: str) -> Dict:
        """Generate strategic insights from competitor data and ICP"""
        
        # Get clustered competitor data
        clusters = await self.db.fetch_all(
            """
            SELECT c.cluster_id, c.cluster_rank, c.cluster_score, c.cluster_data
            FROM ad_clusters c
            JOIN competitors comp ON c.competitor_id = comp.competitor_id
            WHERE comp.company_id = %s
            ORDER BY c.cluster_rank
            LIMIT 40
            """,
            (company_id,)
        )
        
        # Summarize across all competitors (prompt 8)
        market_summary = await self._summarize_market(clusters)
        
        # Get ICP data
        icp_data = await self.db.fetch_all(
            "SELECT persona_data FROM personas WHERE company_id = %s AND selected = true",
            (company_id,)
        )
        
        # Generate insights (prompt 7)
        context = {
            "market_summary": market_summary,
            "icp_data": icp_data
        }
        
        response = await self.chat([{
            "role": "user",
            "content": f"Generate strategic insights:\n{json.dumps(context)}"
        }])
        
        insights = json.loads(response['content'])
        
        # Store insights
        await self.store_knowledge(company_id, 'insights', insights)
        
        return insights
    
    async def _summarize_market(self, clusters: List[Dict]) -> Dict:
        """Create market-wide summary using prompt 8"""
        
        # Use 8_Summarize_Ads_Analysis_prompt.md
        response = await self.chat([{
            "role": "user",
            "content": f"Summarize market patterns:\n{json.dumps(clusters)}"
        }])
        
        return json.loads(response['content'])
```

**Task Checklist Week 7-8:**
- [ ] Implement market summarization (prompt 8)
- [ ] Build InsightAgent with prompt 7
- [ ] Create effective themes extraction
- [ ] Build theme selection UI
- [ ] Test insight quality with real data
- [ ] Add insight explanation features
- [ ] Implement insight versioning

---

## Phase 3: Creation (Weeks 9-12)
*Goal: Generate campaign briefs and ad creatives*

### Week 9-10: Brief Maker

**Brief Maker Agent:**
```python
# agents/brief_maker.py
class BriefMakerAgent(BaseAgent):
    def load_system_prompt(self) -> str:
        with open('prompts/14_Brief_Creator.md', 'r') as f:
            return f.read()
    
    async def generate_concepts(
        self, 
        company_id: str, 
        selected_theme_ids: List[str] = None,
        campaign_stage: str = "awareness"
    ) -> List[Dict]:
        """Generate 6 ad concepts (3 competitor-based + 3 contrarian)"""
        
        # Gather inputs
        company_info = await self._get_company_info(company_id)
        brand_guidelines = await self._get_brand_guidelines(company_id)
        icp_data = await self._get_icp_data(company_id)
        
        # Get insights if themes selected
        insights_data = None
        if selected_theme_ids:
            insights_data = await self._get_insights(company_id, selected_theme_ids)
        
        # Build context
        context = {
            "Company_Info": company_info,
            "Brand": brand_guidelines,
            "ICP_Data": icp_data,
            "Insights_Data": insights_data,
            "Campaign_Stage": campaign_stage
        }
        
        # Generate concepts
        response = await self.chat([{
            "role": "user",
            "content": f"Generate 6 distinct ad concepts:\n{json.dumps(context)}"
        }])
        
        concepts = json.loads(response['content'])['strategic_concepts']
        
        # Store concepts
        for concept in concepts:
            await self.db.execute(
                """
                INSERT INTO briefs 
                (company_id, concept_data, status)
                VALUES (%s, %s, 'draft')
                """,
                (company_id, concept)
            )
        
        return concepts
    
    async def generate_without_insights(self, company_id: str, campaign_stage: str) -> List[Dict]:
        """Generate concepts without competitor insights (prompt 18)"""
        
        # Use 18_Briefs_without_Insights_Prompt.md
        # Focus on 6 contrarian angles
        pass
```

**Hook Generation Tools:**
```python
# agents/tools/hook_generator.py
class HookGenerator:
    """Implements hook toolkit from hook-toolkit.md"""
    
    HOOK_SHAPES = [
        "contradiction",
        "unspoken_truth",
        "pattern_break",
        "reframe",
        "personal_stake",
        "odd_observation",
        "economic_shift",
        "false_consensus"
    ]
    
    async def generate_hook_variants(
        self, 
        theme: str, 
        persona: Dict, 
        company_info: Dict
    ) -> List[str]:
        """Generate 5 hook variants using different shapes"""
        
        hooks = []
        for shape in random.sample(self.HOOK_SHAPES, 5):
            hook = await self._generate_hook(shape, theme, persona, company_info)
            hooks.append(hook)
        
        return hooks
    
    async def _generate_hook(self, shape: str, theme: str, persona: Dict, company_info: Dict) -> str:
        """Generate specific hook using LLM"""
        # Use hook-toolkit.md examples and patterns
        pass
```

**Task Checklist Week 9-10:**
- [ ] Implement BriefMaker with prompt 14
- [ ] Create HookGenerator from hook-toolkit
- [ ] Build concept generation pipeline
- [ ] Implement both insight-based & contrarian modes
- [ ] Test concept quality with marketers
- [ ] Create concept preview UI
- [ ] Add concept editing capabilities

---

### Week 11-12: Creative Prompter

**Image Generation:**
```python
# agents/tools/image_generator.py
import anthropic

class ImageGenerator:
    def __init__(self):
        self.client = anthropic.Anthropic()
    
    async def generate_from_brief(self, brief: Dict, brand: Dict) -> str:
        """Generate ad image from brief using Claude + image gen"""
        
        # Use 17_Template_Generation_Prompt.md
        prompt = self._build_generation_prompt(brief, brand)
        
        # Generate with Claude's image generation
        response = await self.client.messages.create(
            model="claude-sonnet-4-20250514",
            max_tokens=1024,
            messages=[{
                "role": "user",
                "content": prompt
            }]
        )
        
        # Extract image URL from response
        image_url = self._extract_image_url(response)
        
        return image_url
    
    async def remix_competitor_ad(
        self, 
        competitor_ad_image: str,
        brand_logo: str,
        company_info: Dict,
        temperature: float = 0.6
    ) -> str:
        """Remix competitor ad using prompt 13"""
        
        # Use 13_remix_ad_prompt.md
        pass
```

**Creative Prompter Agent:**
```python
# agents/creative_prompter.py
class CreativePrompterAgent(BaseAgent):
    def __init__(self, db_connection, llm_client):
        self.image_gen = ImageGenerator()
        self.template_matcher = TemplateMatcher()
        super().__init__("creative_prompter", db_connection, llm_client)
    
    async def generate_visuals(self, brief_id: str, method: str = "template") -> List[str]:
        """Generate ad images from brief"""
        
        # Get brief data
        brief = await self.db.fetch_one(
            "SELECT * FROM briefs WHERE brief_id = %s",
            (brief_id,)
        )
        
        # Get brand guidelines
        brand = await self.db.fetch_one(
            "SELECT brand_data FROM companies WHERE company_id = %s",
            (brief['company_id'],)
        )
        
        if method == "template":
            # Match and apply template
            template = await self.template_matcher.find_best_template(
                brief['concept_data']['brief']['Compositional_elements']
            )
            image_url = await self.image_gen.generate_from_template(template, brief, brand)
        
        elif method == "from_scratch":
            # Generate from scratch
            image_url = await self.image_gen.generate_from_brief(brief, brand)
        
        elif method == "remix":
            # Remix competitor ad
            image_url = await self.image_gen.remix_competitor_ad(...)
        
        # Store image
        await self.db.execute(
            """
            INSERT INTO generated_images 
            (brief_id, image_url, generation_method, metadata)
            VALUES (%s, %s, %s, %s)
            """,
            (brief_id, image_url, method, {})
        )
        
        return image_url
```

**Task Checklist Week 11-12:**
- [ ] Integrate image generation APIs
- [ ] Implement template matching system
- [ ] Build CreativePrompter with prompts 13, 17
- [ ] Create template library (50+ templates)
- [ ] Test image quality across styles
- [ ] Implement brand consistency validation
- [ ] Build image variant generator
- [ ] Create image editing interface

---

## Phase 4: Optimization (Weeks 13-16)
*Goal: Add campaign planning, monitoring, and analysis*

### Week 13-14: Planner & Publisher

**Planner Agent:**
```python
# agents/planner_agent.py
class PlannerAgent(BaseAgent):
    async def create_campaign_plan(
        self, 
        company_id: str,
        objective: str,
        budget: float,
        timeline: Dict
    ) -> Dict:
        """Create strategic campaign plan"""
        
        # Get insights and personas
        insights = await self._get_insights(company_id)
        personas = await self._get_personas(company_id)
        
        # Generate testing strategy
        testing_strategy = await self._generate_testing_strategy(
            objective, budget, timeline
        )
        
        # Allocate budget
        budget_allocation = await self._allocate_budget(
            budget, testing_strategy, personas
        )
        
        # Create timeline
        campaign_timeline = await self._create_timeline(
            timeline, testing_strategy
        )
        
        plan = {
            "objective": objective,
            "testing_strategy": testing_strategy,
            "budget_allocation": budget_allocation,
            "timeline": campaign_timeline,
            "recommended_concepts": await self._recommend_concepts(company_id, objective)
        }
        
        # Store plan
        await self.db.execute(
            """
            INSERT INTO campaigns 
            (company_id, campaign_plan, status)
            VALUES (%s, %s, 'planning')
            """,
            (company_id, plan)
        )
        
        return plan
```

**Publisher Agent:**
```python
# agents/publisher_agent.py
class PublisherAgent(BaseAgent):
    async def create_draft(self, brief_id: str, image_id: str) -> str:
        """Create publishable draft"""
        
        # Get all components
        brief = await self._get_brief(brief_id)
        image = await self._get_image(image_id)
        brand = await self._get_brand(brief['company_id'])
        
        # Validate brand consistency
        validation = await self._validate_brand_consistency(
            brief, image, brand
        )
        
        if not validation['passed']:
            return {
                "error": "Brand consistency check failed",
                "issues": validation['issues']
            }
        
        # Create draft
        draft_id = await self.db.execute(
            """
            INSERT INTO drafts 
            (brief_id, image_id, status, validation_result)
            VALUES (%s, %s, 'draft', %s)
            RETURNING draft_id
            """,
            (brief_id, image_id, validation)
        )
        
        return draft_id
    
    async def publish_to_linkedin(self, draft_id: str, campaign_id: str) -> Dict:
        """Publish draft to LinkedIn Campaign Manager"""
        
        draft = await self._get_draft(draft_id)
        
        # LinkedIn API integration
        ad_data = {
            "creative": {
                "text": draft['ad_copy']['primary_text'],
                "title": draft['ad_copy']['headline_text'],
                "callToAction": draft['ad_copy']['cta_button_text'],
                "images": [draft['image_url']]
            },
            "targeting": draft['targeting_criteria']
        }
        
        response = await self.linkedin_api.create_ad(campaign_id, ad_data)
        
        # Update draft status
        await self.db.execute(
            """
            UPDATE drafts 
            SET status = 'published', published_at = NOW(), platform_ad_id = %s
            WHERE draft_id = %s
            """,
            (response['ad_id'], draft_id)
        )
        
        return response
```

**Task Checklist Week 13-14:**
- [ ] Implement PlannerAgent
- [ ] Create campaign planning UI
- [ ] Build testing strategy generator
- [ ] Implement PublisherAgent
- [ ] Integrate LinkedIn Campaign Manager API
- [ ] Create draft management system
- [ ] Build publishing workflow
- [ ] Add scheduling capabilities

---

### Week 15-16: Monitor & Analyst

**Monitor Agent:**
```python
# agents/monitor_agent.py
class MonitorAgent(BaseAgent):
    async def start_monitoring(self, published_ad_id: str):
        """Start real-time monitoring"""
        
        # Schedule periodic checks
        await self.scheduler.add_job(
            self._check_performance,
            'interval',
            hours=1,
            args=[published_ad_id]
        )
    
    async def _check_performance(self, published_ad_id: str):
        """Check ad performance and detect anomalies"""
        
        # Fetch latest metrics from LinkedIn
        ad = await self.db.fetch_one(
            "SELECT * FROM published_ads WHERE published_ad_id = %s",
            (published_ad_id,)
        )
        
        metrics = await self.linkedin_api.get_ad_metrics(ad['platform_ad_id'])
        
        # Store metrics
        await self.db.execute(
            """
            INSERT INTO performance_metrics 
            (published_ad_id, metrics, timestamp)
            VALUES (%s, %s, NOW())
            """,
            (published_ad_id, metrics)
        )
        
        # Detect anomalies
        anomalies = await self._detect_anomalies(published_ad_id, metrics)
        
        if anomalies:
            await self._create_alert(published_ad_id, anomalies)
    
    async def _detect_anomalies(self, published_ad_id: str, current_metrics: Dict) -> List[Dict]:
        """Detect performance anomalies"""
        
        # Get historical performance
        history = await self.db.fetch_all(
            """
            SELECT metrics FROM performance_metrics 
            WHERE published_ad_id = %s 
            ORDER BY timestamp DESC LIMIT 24
            """,
            (published_ad_id,)
        )
        
        anomalies = []
        
        # Check CTR anomaly
        historical_ctr = np.mean([m['metrics']['ctr'] for m in history])
        if current_metrics['ctr'] < historical_ctr * 0.5:  # 50% drop
            anomalies.append({
                "type": "ctr_drop",
                "severity": "high",
                "message": f"CTR dropped 50%: {historical_ctr:.2%} → {current_metrics['ctr']:.2%}"
            })
        
        # Check cost anomaly
        historical_cpl = np.mean([m['metrics']['cpl'] for m in history])
        if current_metrics['cpl'] > historical_cpl * 1.5:  # 50% increase
            anomalies.append({
                "type": "cpl_increase",
                "severity": "medium",
                "message": f"CPL increased 50%: ${historical_cpl:.2f} → ${current_metrics['cpl']:.2f}"
            })
        
        return anomalies
```

**Analyst Agent:**
```python
# agents/analyst_agent.py
class AnalystAgent(BaseAgent):
    async def analyze_campaign(self, campaign_id: str, time_period: Dict) -> Dict:
        """Deep analysis of campaign performance"""
        
        # Get all published ads in campaign
        ads = await self.db.fetch_all(
            "SELECT * FROM published_ads WHERE campaign_id = %s",
            (campaign_id,)
        )
        
        # Get performance data
        performance_data = []
        for ad in ads:
            metrics = await self._get_ad_metrics(ad['published_ad_id'], time_period)
            performance_data.append({
                "ad": ad,
                "metrics": metrics
            })
        
        # Analyze patterns
        winning_patterns = await self._identify_winning_patterns(performance_data)
        losing_patterns = await self._identify_losing_patterns(performance_data)
        
        # Statistical analysis
        ab_test_results = await self._analyze_ab_tests(performance_data)
        
        # Generate recommendations
        recommendations = await self._generate_recommendations(
            winning_patterns,
            losing_patterns,
            ab_test_results
        )
        
        analysis = {
            "key_findings": winning_patterns + losing_patterns,
            "ab_test_results": ab_test_results,
            "recommendations": recommendations,
            "performance_summary": await self._summarize_performance(performance_data)
        }
        
        # Store analysis
        await self.db.execute(
            """
            INSERT INTO analyses 
            (campaign_id, analysis_data, time_period)
            VALUES (%s, %s, %s)
            """,
            (campaign_id, analysis, time_period)
        )
        
        # Send learnings to other agents
        await self._propagate_learnings(analysis)
        
        return analysis
    
    async def _propagate_learnings(self, analysis: Dict):
        """Send learnings back to other agents"""
        
        # Update ICP Agent with persona performance
        await self.trigger_agent(
            'icp',
            'update_persona_performance',
            {'analysis': analysis}
        )
        
        # Update Insight Agent with new patterns
        await self.trigger_agent(
            'insight',
            'update_market_patterns',
            {'analysis': analysis}
        )
        
        # Update Brief Maker with winning concepts
        await self.trigger_agent(
            'brief_maker',
            'update_concept_patterns',
            {'analysis': analysis}
        )
```

**Task Checklist Week 15-16:**
- [ ] Implement MonitorAgent with real-time checks
- [ ] Build anomaly detection algorithms
- [ ] Create alerting system
- [ ] Implement AnalystAgent
- [ ] Build statistical analysis tools
- [ ] Create performance dashboard
- [ ] Implement learning propagation
- [ ] Test full feedback loop

---

## Phase 5: Refinement (Weeks 17-20)
*Goal: Polish UX, optimize performance, enhance AI*

### Key Activities

**Week 17: Agent Communication**
- [ ] Optimize agent-to-agent messaging
- [ ] Implement event-driven architecture
- [ ] Add async processing for heavy tasks
- [ ] Build agent coordination dashboard

**Week 18: Conversation UX**
- [ ] Refine chat interface for each agent
- [ ] Implement smart routing between agents
- [ ] Add context preservation across agents
- [ ] Create agent collaboration UI

**Week 19: Performance Optimization**
- [ ] Optimize database queries
- [ ] Add caching layers
- [ ] Implement rate limiting
- [ ] Scale infrastructure

**Week 20: AI Enhancement**
- [ ] Fine-tune agent responses
- [ ] Improve prompt engineering
- [ ] Add multi-modal capabilities
- [ ] Enhance learning algorithms

---

## Technical Stack Recommendations

### Backend
- **Language**: Python 3.11+
- **Framework**: FastAPI (async support)
- **Database**: PostgreSQL 15+ with JSONB
- **Cache**: Redis
- **Queue**: Celery with Redis broker
- **LLM**: Anthropic Claude API (Sonnet 4)
- **Embeddings**: AWS Bedrock Titan

### Frontend
- **Framework**: React 18+ with TypeScript
- **State**: Zustand or Jotai
- **UI**: Tailwind CSS + Radix UI
- **Real-time**: WebSockets (Socket.io)

### Infrastructure
- **Hosting**: AWS (ECS/EKS)
- **Storage**: S3 for images
- **CDN**: CloudFront
- **Monitoring**: DataDog or New Relic
- **Logging**: ELK Stack

### DevOps
- **CI/CD**: GitHub Actions
- **Containers**: Docker
- **Orchestration**: Kubernetes (optional, or ECS)
- **IaC**: Terraform

---

## Success Metrics per Phase

### Phase 1 (Foundation)
- [ ] 90%+ successful company profile extraction
- [ ] 8+ high-quality personas generated
- [ ] < 5 min average onboarding time
- [ ] 80%+ user satisfaction with initial setup

### Phase 2 (Intelligence)
- [ ] 500+ competitor ads scraped per competitor
- [ ] 85%+ clustering accuracy
- [ ] 5+ actionable insights per company
- [ ] 70%+ users select effective themes

### Phase 3 (Creation)
- [ ] 6 distinct concepts generated per request
- [ ] 80%+ concepts rated "good" or "excellent"
- [ ] < 2 min image generation time
- [ ] 75%+ brand consistency score

### Phase 4 (Optimization)
- [ ] 95%+ successful ad publishing
- [ ] < 5 min alerting latency
- [ ] 10+ actionable recommendations per campaign
- [ ] 60%+ recommendations implemented by users

---

## Risk Mitigation

### Technical Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| LLM API rate limits | High | Implement queuing, caching, fallbacks |
| Ad scraping blocked | High | Multiple scraping methods, proxies, legal review |
| Poor clustering quality | Medium | Iterate on algorithms, manual validation |
| Slow image generation | Medium | Optimize prompts, pre-generate templates |

### Product Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| Agent responses too generic | High | Extensive prompt engineering, testing |
| Users confused by multiple agents | Medium | Smart routing, clear agent roles |
| Poor concept quality | High | Human review loop, quality scoring |
| Low ad performance | High | Continuous learning from performance data |

---

## Next Immediate Steps

1. **Set up development environment** (Day 1-2)
   - Initialize repo with agent framework
   - Set up database with core schema
   - Configure LLM API access

2. **Build BaseAgent class** (Day 3-5)
   - Implement core agent functionality
   - Create tool execution framework
   - Set up knowledge storage/retrieval

3. **Implement Discovery Agent** (Week 1)
   - Web scraping tools
   - Company profile generation
   - Test with 20+ companies

4. **User testing checkpoint** (End of Week 2)
   - Test onboarding flow with 5-10 beta users
   - Gather feedback on Discovery Agent quality
   - Iterate on prompts and UX

---

*This roadmap provides a structured path from concept to production-ready agent system.*
