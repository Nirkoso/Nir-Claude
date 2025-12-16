# ScaleFox.ai Agent Architecture Plan
## Autonomous Agent System Design

---

## Core Philosophy

**Agent Principles:**
- Each agent is an autonomous expert in its domain
- Agents maintain persistent knowledge in database
- Users can chat with any agent at any time
- Agents collaborate through structured data exchange
- Context is continuously managed and optimized
- Agents learn and improve recommendations over time

---

## Agent Roster & Architecture

### 1. **Discovery Agent** (Company & Industry Intelligence)
*"I understand your business and industry landscape"*

**Mission:**
Research and continuously update company profile, industry benchmarks, and market positioning.

**Triggers:**
- User provides company URL + name
- Scheduled refresh (weekly/monthly)
- User requests company info update
- Major product/positioning changes detected

**Tools:**
- Web scraping (company website, about pages, product pages)
- Web search (company mentions, news, funding)
- Industry database APIs
- Competitor identification algorithms

**Knowledge Base (DB Schema):**
```json
{
  "company_profile": {
    "company_name": "",
    "company_url": "",
    "overview": "",
    "company_description": "",
    "primary_offering": "",
    "problem_addressed": "",
    "solution": "",
    "industry": "",
    "product_services": [],
    "lifecycle_stage": "",
    "evidence_sources": []
  },
  "industry_intelligence": {
    "industry_benchmarks": {},
    "market_size": "",
    "growth_rate": "",
    "key_players": [],
    "trends": []
  },
  "refresh_history": [],
  "confidence_scores": {}
}
```

**Conversational Capabilities:**
- "Tell me about my company positioning"
- "What are the key industry trends right now?"
- "How does my offering compare to market standards?"
- "Update my company information"
- "What's missing from my profile?"

**Outputs to Other Agents:**
→ Brand Agent (company identity, tone indicators)
→ ICP Agent (target audience hints, industry context)
→ Competitor Agent (industry, market position for finding competitors)
→ Brief Maker (company info, positioning, USPs)

**Base Prompt:** 
`1_company_info_prompt.md` + `9_mini_company_info_prompt.md` (combined/enhanced)

---

### 2. **Brand Agent** (Visual & Verbal Identity)
*"I define and maintain your brand essence"*

**Mission:**
Analyze and codify brand identity (visual, verbal, messaging) and ensure consistency across all outputs.

**Triggers:**
- Discovery Agent completes initial research
- User uploads brand assets
- Brand refresh requested
- Inconsistencies detected in outputs

**Tools:**
- Image analysis (logo, color extraction)
- Website scraping (design patterns, typography)
- Social media analysis (tone of voice, content style)
- Competitive brand analysis

**Knowledge Base (DB Schema):**
```json
{
  "visual_identity": {
    "logo_url": "",
    "primary_colors": ["#hex"],
    "secondary_colors": ["#hex"],
    "typography": {
      "headlines": "",
      "body": ""
    },
    "design_style": [],
    "mood_board": {
      "adjectives": [],
      "image_keywords": []
    }
  },
  "verbal_identity": {
    "tone_of_voice": "",
    "brand_voice_attributes": [],
    "messaging_pillars": [],
    "banned_phrases": [],
    "preferred_language_patterns": []
  },
  "brand_guidelines": {
    "dos": [],
    "donts": [],
    "examples": []
  },
  "consistency_rules": {}
}
```

**Conversational Capabilities:**
- "Show me my brand identity"
- "How should my ads sound?"
- "Is this copy on-brand?" [paste copy]
- "What colors should I use?"
- "Update my brand voice to be more [adjective]"

**Outputs to Other Agents:**
→ Brief Maker (tone, visual style, brand constraints)
→ Creative Prompter (visual guidelines, color palettes)
→ Publisher (brand consistency checks)

**Base Prompt:**
New (synthesize from brand analysis sections in existing prompts)

---

### 3. **ICP Agent** (Ideal Customer Profile)
*"I know exactly who you're trying to reach"*

**Mission:**
Research, define, and continuously refine target audience personas with deep behavioral and psychographic insights.

**Triggers:**
- Discovery Agent completes company research
- User requests persona suggestions
- Campaign performance data indicates persona mismatch
- Quarterly persona refresh

**Tools:**
- LinkedIn Sales Navigator data
- Industry research
- Persona suggestion algorithms
- Behavioral analysis

**Knowledge Base (DB Schema):**
```json
{
  "active_personas": [
    {
      "persona_id": "",
      "name": "",
      "role": "",
      "demographics": {},
      "firmographics": {},
      "pains": [],
      "goals": [],
      "success_metrics": [],
      "modal_behavior": [],
      "modal_motivation": [],
      "modal_communities": [],
      "modal_tools": [],
      "why_us": "",
      "selected_by_user": true
    }
  ],
  "suggested_personas": [],
  "persona_performance_data": {},
  "targeting_criteria": {
    "linkedin_targeting": {},
    "watering_holes": {},
    "triggering_events": []
  }
}
```

**Conversational Capabilities:**
- "Who should I target?"
- "Suggest personas for my product"
- "Tell me more about [persona name]"
- "What motivates this persona?"
- "Where does this persona hang out online?"
- "Which personas are performing best?"

**Outputs to Other Agents:**
→ Competitor Agent (persona context for relevant competitor identification)
→ Insight Agent (persona context for theme analysis)
→ Brief Maker (audience definition, pains, goals)
→ Monitor Agent (persona performance tracking)

**Base Prompt:**
`2_Target_audience_prompt.md` + `2a_ICP_suggest_prompt.md`

---

### 4. **Competitor Agent** (Competitive Intelligence)
*"I track what's working in your market"*

**Mission:**
Continuously discover, scrape, analyze, and cluster competitor ads to identify winning patterns.

**Triggers:**
- User provides competitor URLs
- Automated competitor discovery (weekly)
- New campaign planning initiated
- User requests competitive analysis

**Tools:**
- Ad scraping (LinkedIn, Meta, etc.)
- Embedding models (AWS Bedrock Titan)
- Clustering algorithms (HDBSCAN)
- Performance estimation

**Knowledge Base (DB Schema):**
```json
{
  "competitors": [
    {
      "competitor_id": "",
      "name": "",
      "url": "",
      "last_scraped": "",
      "ad_count": 0,
      "status": "active"
    }
  ],
  "competitor_ads": [
    {
      "ad_id": "",
      "competitor_id": "",
      "ad_data": {},
      "scrape_date": "",
      "cluster_id": "",
      "performance_estimate": {}
    }
  ],
  "clusters": [
    {
      "cluster_id": "",
      "cluster_rank": 0,
      "cluster_score": 0,
      "best_ad_id": "",
      "ad_count": 0,
      "theme": "",
      "analysis": {}
    }
  ],
  "refresh_schedule": {}
}
```

**Conversational Capabilities:**
- "Show me my competitors' top ads"
- "What's working in my market right now?"
- "Find new competitors for me"
- "Analyze [competitor name]'s ads"
- "What ad styles are trending?"
- "How often are competitors posting?"

**Outputs to Other Agents:**
→ Insight Agent (clustered ads, performance data)
→ Brief Maker (winning patterns, themes)
→ Monitor Agent (competitive benchmarks)

**Base Prompt:**
`4_Analyze_ad_prompt.md` + `8_Summarize_Ads_Analysis_prompt.md`

---

### 5. **Insight Agent** (Strategic Intelligence)
*"I synthesize market patterns into strategy"*

**Mission:**
Combine ICP data, competitor analysis, and market trends to generate actionable strategic insights and effective themes.

**Triggers:**
- Competitor Agent completes clustering analysis
- User requests insights
- Campaign performance review
- Monthly strategic refresh

**Tools:**
- Pattern recognition algorithms
- Theme extraction
- Success scoring
- Strategic synthesis

**Knowledge Base (DB Schema):**
```json
{
  "effective_themes": [
    {
      "theme_id": "",
      "theme_name": "",
      "description": "",
      "supporting_ad_uuids": [],
      "relevance_to_icp": "",
      "strength_score": 0,
      "selected_by_user": false
    }
  ],
  "common_pitfalls": [
    {
      "pitfall": "",
      "issue": "",
      "ad_examples": []
    }
  ],
  "success_patterns": {
    "ad_archetypes": [],
    "successful_styles": [],
    "best_formats": [],
    "common_hooks": [],
    "cta_patterns": []
  },
  "message_evolution": [],
  "strategic_recommendations": {}
}
```

**Conversational Capabilities:**
- "What themes are working right now?"
- "Show me effective themes for my ICP"
- "What should I avoid?"
- "How is messaging evolving in my market?"
- "What's the best ad archetype for [goal]?"
- "Why is this theme effective?"

**Outputs to Other Agents:**
→ Brief Maker (effective themes, success patterns)
→ Planner (strategic direction, campaign priorities)
→ Monitor Agent (success benchmarks)

**Base Prompt:**
`5_Ads_Insight_Prompt.md` + `6_Overall_Market_summary_prompt.md` + `7_Analyze_Insight_prompt.md`

---

### 6. **Brief Maker** (Campaign Strategist)
*"I create winning ad concepts tailored to your strategy"*

**Mission:**
Generate 6 distinct ad concepts (3 competitor-validated + 3 contrarian) with full creative briefs and platform copy.

**Triggers:**
- User completes theme selection (or requests briefs without insights)
- User requests "generate new concepts"
- Campaign refresh needed
- A/B test variant creation

**Tools:**
- Hook generation (8 hook shapes)
- Framework selection (10+ copywriting frameworks)
- Style matching algorithms
- Compositional element tagging

**Knowledge Base (DB Schema):**
```json
{
  "generated_concepts": [
    {
      "concept_id": "",
      "concept_name": "",
      "concept_type": "competitor_success | rare_angle",
      "creation_date": "",
      "status": "draft | selected | published",
      "ad_copy": {
        "primary_text": "",
        "headline_text": "",
        "cta_button_text": ""
      },
      "brief": {
        "objective": "",
        "audience": "",
        "value_prop": "",
        "hooks": [],
        "tone": "",
        "rationale": "",
        "style": {},
        "type_of_ad": "",
        "compositional_elements": []
      },
      "performance_prediction": {},
      "user_feedback": ""
    }
  ],
  "concept_history": [],
  "winning_patterns": {}
}
```

**Conversational Capabilities:**
- "Generate ad concepts for [campaign goal]"
- "Create briefs without competitor insights"
- "Explain this concept's strategy"
- "Generate variations of concept #3"
- "Why did you choose this hook?"
- "Make this concept more [adjective]"

**Outputs to Other Agents:**
→ Creative Prompter (briefs for image generation)
→ Publisher (ad copy for drafting)
→ Monitor Agent (concept tracking)

**Base Prompt:**
`14_Brief_Creator.md` + `18_Briefs_without_Insights_Prompt.md`

---

### 7. **Creative Prompter** (Visual Generator)
*"I bring your ads to visual life"*

**Mission:**
Generate production-ready ad images from briefs using AI image generation and template systems.

**Triggers:**
- Brief Maker outputs approved concepts
- User selects "generate visuals"
- Template remix requested
- Visual iteration requested

**Tools:**
- AI image generation (Stable Diffusion, DALL-E, etc.)
- Template matching algorithm
- Competitor ad remixing
- Brand consistency validator

**Knowledge Base (DB Schema):**
```json
{
  "generated_images": [
    {
      "image_id": "",
      "concept_id": "",
      "generation_method": "template | remix | from_scratch",
      "prompt_used": "",
      "template_id": "",
      "source_ad_id": "",
      "temperature": 0.6,
      "image_url": "",
      "brand_consistency_score": 0,
      "user_rating": 0,
      "selected": false
    }
  ],
  "templates": [],
  "generation_history": {}
}
```

**Conversational Capabilities:**
- "Generate images for concept #2"
- "Remix [competitor ad] for my brand"
- "Make this more [brand attribute]"
- "Try different templates"
- "Show me variations with higher/lower temperature"
- "Why did you choose this style?"

**Outputs to Other Agents:**
→ Publisher (images for draft ads)
→ Monitor Agent (visual performance tracking)

**Base Prompt:**
`13_remix_ad_prompt.md` + `17_Template_Generation_Prompt.md`

---

### 8. **Publisher** (Content Manager)
*"I organize your drafts and manage publishing"*

**Mission:**
Maintain draft library, validate brand consistency, manage approval workflows, and publish to platforms.

**Triggers:**
- Creative Prompter generates new ads
- User requests "show drafts"
- Publishing schedule triggers
- User initiates publishing workflow

**Tools:**
- Draft management system
- Brand validation engine
- Platform APIs (LinkedIn Campaign Manager)
- Scheduling system

**Knowledge Base (DB Schema):**
```json
{
  "drafts": [
    {
      "draft_id": "",
      "concept_id": "",
      "image_id": "",
      "status": "draft | approved | scheduled | published | archived",
      "brand_validation": {
        "passed": true,
        "issues": []
      },
      "platform": "linkedin | meta | etc",
      "schedule_date": "",
      "published_date": "",
      "campaign_id": ""
    }
  ],
  "publishing_queue": [],
  "templates_library": {},
  "validation_rules": {}
}
```

**Conversational Capabilities:**
- "Show me all drafts"
- "What needs approval?"
- "Validate this ad against brand guidelines"
- "Schedule this for next week"
- "Publish draft #4 to LinkedIn"
- "Archive old drafts"

**Outputs to Other Agents:**
→ Monitor Agent (published ad tracking)
→ Analyst Agent (performance data collection)

**Base Prompt:**
New (draft management + validation logic)

---

### 9. **Planner** (Campaign Orchestrator)
*"I help you plan and prioritize campaigns"*

**Mission:**
Strategic campaign planning, budget allocation, testing strategy, and timeline management.

**Triggers:**
- User initiates campaign planning
- Quarterly planning cycle
- Budget allocation needed
- Testing strategy requested

**Tools:**
- Campaign planning templates
- Budget optimization algorithms
- Testing framework generator
- Timeline management

**Knowledge Base (DB Schema):**
```json
{
  "campaigns": [
    {
      "campaign_id": "",
      "campaign_name": "",
      "objective": "",
      "budget": 0,
      "timeline": {},
      "target_personas": [],
      "concepts_used": [],
      "testing_strategy": {},
      "status": "planning | active | completed",
      "kpis": {}
    }
  ],
  "testing_hypotheses": [],
  "resource_allocation": {},
  "campaign_calendar": {}
}
```

**Conversational Capabilities:**
- "Help me plan my Q1 campaign"
- "What should I test first?"
- "Allocate budget across campaigns"
- "Create a testing roadmap"
- "What's my campaign timeline?"
- "Which concepts should I prioritize?"

**Outputs to Other Agents:**
→ Brief Maker (campaign requirements)
→ Publisher (campaign structure)
→ Monitor Agent (KPI tracking setup)

**Base Prompt:**
New (campaign planning logic + testing frameworks)

---

### 10. **Monitor Agent** (Real-Time Performance Tracker)
*"I track what's working right now"*

**Mission:**
Continuously monitor ad performance, detect anomalies, alert on issues, and feed data back to other agents.

**Triggers:**
- Ads published
- Scheduled performance checks (hourly/daily)
- Performance thresholds crossed
- User requests "show performance"

**Tools:**
- Platform APIs (LinkedIn Ads, Meta Ads)
- Performance analytics
- Anomaly detection algorithms
- Real-time alerting

**Knowledge Base (DB Schema):**
```json
{
  "performance_data": [
    {
      "ad_id": "",
      "timestamp": "",
      "metrics": {
        "impressions": 0,
        "clicks": 0,
        "ctr": 0,
        "conversions": 0,
        "cost": 0,
        "cpl": 0
      }
    }
  ],
  "alerts": [
    {
      "alert_id": "",
      "type": "anomaly | threshold | opportunity",
      "severity": "low | medium | high",
      "message": "",
      "recommended_action": ""
    }
  ],
  "benchmarks": {},
  "performance_trends": {}
}
```

**Conversational Capabilities:**
- "How are my ads performing?"
- "Show me today's metrics"
- "What's my best performing ad?"
- "Alert me if CPL exceeds $X"
- "Compare performance to last week"
- "Why did this ad underperform?"

**Outputs to Other Agents:**
→ Analyst Agent (performance data for analysis)
→ ICP Agent (persona performance feedback)
→ Insight Agent (market performance trends)

**Base Prompt:**
New (performance monitoring + alerting logic)

---

### 11. **Analyst Agent** (Performance Intelligence)
*"I turn performance data into actionable insights"*

**Mission:**
Deep analysis of campaign performance, hypothesis validation, recommendation generation, and learning synthesis.

**Triggers:**
- Weekly/monthly analysis cycles
- Campaign completion
- User requests analysis
- Performance review requested

**Tools:**
- Statistical analysis
- A/B test analysis
- Attribution modeling
- Recommendation engine

**Knowledge Base (DB Schema):**
```json
{
  "analyses": [
    {
      "analysis_id": "",
      "analysis_date": "",
      "time_period": {},
      "key_findings": [],
      "recommendations": [],
      "hypothesis_validations": [],
      "winning_patterns": [],
      "losing_patterns": []
    }
  ],
  "learnings_library": [],
  "optimization_playbook": {}
}
```

**Conversational Capabilities:**
- "Analyze this campaign's performance"
- "What did we learn from this test?"
- "Give me recommendations to improve"
- "Why did this concept work/fail?"
- "What should I do next?"
- "Show me patterns across campaigns"

**Outputs to Other Agents:**
→ Insight Agent (performance-based insights)
→ ICP Agent (persona refinement)
→ Brief Maker (winning concept patterns)
→ Planner (optimization recommendations)

**Base Prompt:**
New (performance analysis + recommendation logic)

---

### 12. **Onboarding Agent** (Orchestrator & Guide)
*"I guide you through setup and keep everything flowing"*

**Mission:**
Orchestrate user onboarding, manage agent workflows, provide guidance, and ensure smooth progression.

**Triggers:**
- New user signup
- Major workflow steps completed
- User requests help
- Workflow stuck/blocked

**Tools:**
- Workflow orchestration
- Progress tracking
- Help system
- Agent coordination

**Knowledge Base (DB Schema):**
```json
{
  "onboarding_state": {
    "current_step": "",
    "completed_steps": [],
    "pending_actions": [],
    "blockers": []
  },
  "user_preferences": {},
  "help_history": [],
  "agent_coordination": {}
}
```

**Conversational Capabilities:**
- "What should I do next?"
- "Show my progress"
- "I'm stuck, help me"
- "Skip this step"
- "What are other agents working on?"
- "Customize my workflow"

**Outputs to Other Agents:**
→ All Agents (orchestration signals, user context)
← All Agents (status updates, completion signals)

**Base Prompt:**
New (orchestration logic based on `Orchestration_Flow.md`)

---

## Agent Communication Protocols

### Data Exchange Format
```json
{
  "from_agent": "agent_name",
  "to_agent": "agent_name",
  "message_type": "data_update | request | notification",
  "timestamp": "",
  "payload": {},
  "priority": "low | medium | high",
  "requires_response": false
}
```

### Agent Dependencies (Workflow Order)

```
1. Discovery Agent
   ↓
2. Brand Agent (parallel with #3)
3. ICP Agent (parallel with #2)
   ↓
4. Competitor Agent
   ↓
5. Insight Agent
   ↓
6. Brief Maker
   ↓
7. Creative Prompter
   ↓
8. Publisher
   ↓
9. Monitor Agent → Analyst Agent → (feedback loop to all agents)

Planner Agent: Can be invoked at any time after Discovery completes
Onboarding Agent: Always active, coordinates all
```

---

## User Interaction Model

### Context Management Strategy

**Persistent Context (Stored in DB):**
- User profile & preferences
- Company & brand identity
- Selected personas & competitors
- Campaign history & performance
- Conversation history per agent

**Session Context (In-Memory):**
- Current conversation with specific agent
- Last N interactions
- Active workflow state
- Pending actions

**Context Passing:**
When user switches agents, relevant context is summarized and passed:
```json
{
  "previous_agent": "",
  "conversation_summary": "",
  "relevant_entities": [],
  "user_intent": "",
  "pending_questions": []
}
```

### Multi-Agent Chat Interface

**Option 1: Explicit Agent Selection**
- User selects agent from dropdown/menu
- Chat interface switches to that agent's context
- Agent avatar/name clearly shown
- User can see what each agent "knows"

**Option 2: Smart Routing**
- User asks question in unified chat
- System routes to appropriate agent
- Agent responds and identifies itself
- User can override routing

**Option 3: Hybrid (Recommended)**
- Default: Smart routing for efficiency
- Option to "Talk to [Agent Name]" directly
- Agent can say "Let me bring in [Other Agent]" for collaboration

---

## Database Schema (High-Level)

```sql
-- Core Tables
users
companies
agents
conversations
messages
agent_knowledge (JSONB storage per agent)
workflows
tasks

-- Domain Tables
personas
competitors
competitor_ads
ad_clusters
insights
briefs
generated_images
drafts
campaigns
performance_metrics
```

---

## Implementation Phases

### Phase 1: Foundation (Weeks 1-4)
- Discovery Agent
- Brand Agent
- ICP Agent
- Onboarding Agent (basic)
- Database setup
- Basic chat interface

### Phase 2: Intelligence (Weeks 5-8)
- Competitor Agent
- Insight Agent
- Agent communication protocols
- Enhanced onboarding flows

### Phase 3: Creation (Weeks 9-12)
- Brief Maker
- Creative Prompter
- Publisher
- Template system

### Phase 4: Optimization (Weeks 13-16)
- Planner Agent
- Monitor Agent
- Analyst Agent
- Learning loops

### Phase 5: Refinement (Weeks 17-20)
- Performance optimization
- Advanced AI features
- User experience polish
- Agent collaboration improvements

---

## Key Technical Considerations

### Agent Architecture Pattern
```
Agent = {
  Core Logic (Mission execution)
  + Tools (APIs, algorithms)
  + Knowledge Base (DB access)
  + Conversation Interface (LLM-powered)
  + Context Manager (State handling)
}
```

### LLM Integration
- Each agent has specialized system prompt
- Context window management per agent
- Function calling for tool use
- RAG for knowledge retrieval

### Scalability
- Agent workloads can be distributed
- Async processing for heavy tasks
- Caching for frequently accessed data
- Event-driven architecture

### Monitoring & Debugging
- Agent action logging
- Performance metrics per agent
- Error tracking & recovery
- User feedback collection

---

## Success Metrics

**Agent Performance:**
- Task completion rate
- Response accuracy
- User satisfaction scores
- Time to resolution

**System Performance:**
- End-to-end workflow time
- Agent collaboration efficiency
- Data quality scores
- User engagement metrics

**Business Metrics:**
- Time to first campaign (reduction)
- Campaign performance (vs. manual)
- User retention
- Feature adoption rates

---

## Next Steps

1. **Prioritize agent development order** based on user value
2. **Define detailed API contracts** between agents
3. **Design database schema** with scalability in mind
4. **Build agent framework** (reusable architecture)
5. **Start with Discovery Agent** as proof of concept
6. **Iterate based on real user feedback**

---

*This architecture enables true autonomous agent collaboration while maintaining human oversight and conversational accessibility.*
