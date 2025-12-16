# ScaleFox Agent Conversational Interface Design
## User Experience & Agent Interaction Patterns

---

## Overview

This document defines how users interact with ScaleFox's autonomous agents through natural conversation, including routing patterns, context management, and user experience principles.

---

## Core UX Principles

### 1. **Agents as Experts, Not Assistants**
Each agent is a domain expert that users consult, not a generic chatbot. They have:
- Specialized knowledge and capabilities
- Persistent memory of their domain
- Opinions and recommendations
- Ability to say "Let me bring in [Other Agent]" when needed

### 2. **Transparent Agency**
Users always know:
- Which agent they're talking to
- What that agent is working on
- When agents collaborate
- What data agents have access to

### 3. **Context Flows Seamlessly**
- Users shouldn't repeat themselves
- Agents share relevant context automatically
- Conversation history travels with the user
- Each agent summarizes what they learned for others

---

## User Interface Models

### Option A: Unified Chat with Smart Routing (Recommended)

**Layout:**
```
┌─────────────────────────────────────────┐
│  ScaleFox                    [Settings] │
├─────────────────────────────────────────┤
│                                         │
│  [Active Agent: Discovery Agent 🔍]     │
│  Currently researching: Acme Corp       │
│                                         │
│  ┌───────────────────────────────────┐ │
│  │ User: Analyze my company         │ │
│  └───────────────────────────────────┘ │
│                                         │
│  ┌───────────────────────────────────┐ │
│  │ Discovery Agent:                 │ │
│  │ I'm analyzing acme.com now.      │ │
│  │ Found: B2B SaaS platform for     │ │
│  │ automated workflows...           │ │
│  │                                  │ │
│  │ [Show full analysis]             │ │
│  └───────────────────────────────────┘ │
│                                         │
│  ┌───────────────────────────────────┐ │
│  │ User: What about my brand?       │ │
│  └───────────────────────────────────┘ │
│                                         │
│  ┌───────────────────────────────────┐ │
│  │ System: Routing to Brand Agent   │ │
│  └───────────────────────────────────┘ │
│                                         │
│  ┌───────────────────────────────────┐ │
│  │ Brand Agent:                     │ │
│  │ Based on Discovery Agent's       │ │
│  │ research, I've analyzed your     │ │
│  │ visual identity...               │ │
│  │                                  │ │
│  │ [View brand guidelines]          │ │
│  └───────────────────────────────────┘ │
│                                         │
└─────────────────────────────────────────┘
│ Type your message...          [Send]  │
│ Quick actions: [Add competitor]       │
│              [Generate personas]      │
└─────────────────────────────────────────┘
```

**How Routing Works:**
1. User types message
2. System analyzes intent
3. Routes to appropriate agent
4. Agent responds and identifies itself
5. System suggests related actions

**Routing Logic Example:**
```python
async def route_message(user_message: str, context: Dict) -> str:
    """Determine which agent should handle message"""
    
    # Intent classification
    intent = await classify_intent(user_message, context)
    
    intent_to_agent = {
        "company_research": "discovery",
        "brand_analysis": "brand",
        "persona_generation": "icp",
        "competitor_analysis": "competitor",
        "strategy_insights": "insight",
        "campaign_concepts": "brief_maker",
        "ad_creation": "creative_prompter",
        "performance_tracking": "monitor",
        "campaign_analysis": "analyst",
        "planning": "planner",
        "publishing": "publisher"
    }
    
    return intent_to_agent.get(intent, "onboarding")
```

---

### Option B: Multi-Agent Sidebar

**Layout:**
```
┌─────────────┬───────────────────────────┐
│ Agents      │  Chat                     │
│             │                           │
│ 🔍 Discovery│  Discovery Agent:         │
│   (Active)  │  Analyzing acme.com...    │
│             │                           │
│ 🎨 Brand    │  [Show full analysis]     │
│   (Ready)   │                           │
│             │  User: What about my      │
│ 👥 ICP      │  competitors?             │
│   (Ready)   │                           │
│             │  Discovery Agent:         │
│ 🔬 Competitor│ Let me bring in the      │
│   (Idle)    │  Competitor Agent...      │
│             │                           │
│ 💡 Insights │  Competitor Agent:        │
│   (Idle)    │  I can help! Give me 3   │
│             │  competitor URLs...       │
│ 📝 Briefs   │                           │
│   (Idle)    │  [Type message...]        │
│             │                           │
│ 🎨 Creative │                           │
│   (Idle)    │                           │
│             │                           │
│ 📊 Monitor  │                           │
│   (Idle)    │                           │
│             │                           │
│ 📈 Analyst  │                           │
│   (Idle)    │                           │
└─────────────┴───────────────────────────┘
```

**Benefits:**
- Explicit agent selection
- See all agents at a glance
- Clear agent status (Active/Ready/Idle)
- Direct agent switching

**Trade-offs:**
- More UI chrome
- Users need to learn which agent does what
- Less fluid conversation flow

---

### Option C: Hybrid Approach (Best of Both)

**Default**: Smart routing in unified chat
**Override**: Quick action to "Talk to [Agent]"
**Collaboration**: Agents can bring others into conversation

**Example Conversation:**
```
User: Help me set up my campaign

Onboarding Agent: I'll guide you through it! First, 
let me start the Discovery Agent to research your company.

[Discovery Agent is researching acme.com... ●●●]

Discovery Agent: Found it! Acme Corp - B2B SaaS for 
automated workflows. Here's what I learned:
[View full profile]

Onboarding Agent: Great! While Brand Agent analyzes 
your visual identity, you can review these personas 
from ICP Agent:
[8 suggested personas]

User: These personas are too generic

ICP Agent: I can help refine them! Tell me more about 
your ideal customers. What roles do they have? What 
problems keep them up at night?

[User provides details]

ICP Agent: Perfect! I've updated the personas. Here 
are 3 more specific profiles:
[Show personas]

User: Much better! What's next?

Onboarding Agent: Now let's add competitors. Give me 
3 competitor URLs and Competitor Agent will analyze 
their ads.

[User adds competitors]

Competitor Agent: Analyzing 450 ads from your 3 
competitors... This will take about 5 minutes.

[Progress bar]

Competitor Agent: Done! I found 87 distinct ad 
clusters. Insight Agent is now extracting strategic 
themes...

Insight Agent: Found 12 effective themes! Here are 
the top 5:
[Show themes with examples]

User: Can I just skip to creating ads?

Brief Maker: I can generate concepts without competitor 
insights, but they'll be less data-driven. Want to 
wait 2 more minutes for Insight Agent to finish?

User: No, generate now

Brief Maker: On it! Creating 6 contrarian concepts 
based on your ICP and industry patterns...
[Show 6 concepts]
```

---

## Agent Personality & Voice

### Discovery Agent 🔍
**Personality**: Thorough researcher, fact-focused
**Tone**: Professional, detailed, confident
**Example phrases**:
- "I found 3 key differentiators..."
- "Your industry data shows..."
- "Let me dig deeper into..."
- "Here's what I learned about your company..."

### Brand Agent 🎨
**Personality**: Creative but analytical, detail-oriented
**Tone**: Appreciative of design, precise
**Example phrases**:
- "Your visual identity suggests..."
- "I extracted these brand colors..."
- "Your tone of voice is [adjective]..."
- "This aligns with your brand positioning"

### ICP Agent 👥
**Personality**: Empathetic, customer-focused
**Tone**: Insightful, questioning
**Example phrases**:
- "Your ideal customer likely struggles with..."
- "This persona values..."
- "Let me understand your audience better..."
- "I've identified 8 distinct buyer types..."

### Competitor Agent 🔬
**Personality**: Strategic analyst, pattern-finder
**Tone**: Observant, comparative
**Example phrases**:
- "I scraped 450 ads from your competitors..."
- "The market is trending toward..."
- "Your competitors are using this pattern..."
- "I clustered similar ads into 87 groups..."

### Insight Agent 💡
**Personality**: Strategic synthesizer, big-picture thinker
**Tone**: Confident, prescriptive
**Example phrases**:
- "The data reveals 3 winning themes..."
- "Market patterns suggest..."
- "This theme performs because..."
- "Your best opportunity is..."

### Brief Maker 📝
**Personality**: Creative strategist, concept generator
**Tone**: Inspired, explanatory
**Example phrases**:
- "I've crafted 6 distinct concepts..."
- "This concept works because..."
- "Here's a contrarian angle..."
- "Let me generate variations on this theme..."

### Creative Prompter 🎨
**Personality**: Visual artist, quality-focused
**Tone**: Aesthetic, technical
**Example phrases**:
- "I'm generating images that capture..."
- "This visual approach will..."
- "Let me try a different style..."
- "I can remix this competitor ad for your brand..."

### Publisher 📤
**Personality**: Organized executor, quality gatekeeper
**Tone**: Systematic, reliable
**Example phrases**:
- "I've validated this against your brand guidelines..."
- "This draft is ready to publish..."
- "I noticed a brand consistency issue..."
- "Your campaign is scheduled for..."

### Planner 📋
**Personality**: Strategic coordinator, optimizer
**Tone**: Organized, forward-thinking
**Example phrases**:
- "Your campaign strategy should..."
- "I recommend testing these 3 concepts first..."
- "Based on your budget, here's the plan..."
- "Let's prioritize these audiences..."

### Monitor Agent 📊
**Personality**: Vigilant tracker, alert system
**Tone**: Urgent when needed, factual
**Example phrases**:
- "Your CTR just dropped 40%..."
- "This ad is outperforming by 3x..."
- "I noticed an anomaly in..."
- "Real-time metrics show..."

### Analyst Agent 📈
**Personality**: Data scientist, insight extractor
**Tone**: Analytical, conclusive
**Example phrases**:
- "The data shows a clear pattern..."
- "This concept performed best because..."
- "My recommendation is to..."
- "I identified 5 key learnings..."

### Onboarding Agent 🧭
**Personality**: Friendly guide, coordinator
**Tone**: Helpful, encouraging
**Example phrases**:
- "Let's get you set up..."
- "While that's processing, you can..."
- "You're 60% done with onboarding..."
- "Let me bring in the right expert for this..."

---

## Context Management

### Context Types

**1. Persistent Context (Stored in DB)**
```json
{
  "user_context": {
    "user_id": "uuid",
    "company_id": "uuid",
    "preferences": {},
    "onboarding_state": {}
  },
  "entity_context": {
    "companies": [],
    "competitors": [],
    "personas": [],
    "campaigns": []
  },
  "conversation_history": [
    {
      "agent": "discovery",
      "messages": [],
      "summary": ""
    }
  ]
}
```

**2. Session Context (In-Memory)**
```json
{
  "current_agent": "brief_maker",
  "active_task": "generating_concepts",
  "recent_interactions": [],
  "pending_questions": [],
  "user_intent": "create_campaign"
}
```

**3. Agent-Specific Context**
```json
{
  "agent_name": "brief_maker",
  "working_memory": {
    "current_concepts": [],
    "selected_themes": [],
    "generation_params": {}
  },
  "dependencies": {
    "needs_from_discovery": true,
    "needs_from_insights": false
  }
}
```

### Context Passing Between Agents

**Pattern 1: Explicit Handoff**
```
Discovery Agent → Brand Agent

Discovery Agent: "I've finished researching Acme Corp. 
Brand Agent, can you analyze their visual identity?"

[System passes context]
{
  "from_agent": "discovery",
  "to_agent": "brand",
  "context": {
    "company_id": "uuid",
    "company_url": "acme.com",
    "summary": "B2B SaaS company...",
    "key_findings": []
  }
}

Brand Agent: "Got it! Based on Discovery Agent's 
research, I'm analyzing acme.com's design..."
```

**Pattern 2: User-Initiated Switch**
```
User: "What's my brand identity?"

[System routes to Brand Agent]
[System loads relevant context from Discovery]

Brand Agent: "Based on your company profile, here's 
your brand identity:
- Primary colors: #2C3E50, #3498DB
- Tone: Professional, innovative
- Visual style: Minimalist, modern
[Full guidelines]"
```

**Pattern 3: Agent Collaboration**
```
Brief Maker: "I need more details about your ICP 
personas before generating concepts. Let me bring 
in ICP Agent..."

[Brief Maker requests ICP Agent's knowledge]

ICP Agent: "I have 5 active personas for this company. 
The primary persona is Sarah, VP Marketing at 
mid-market B2B companies..."

Brief Maker: "Perfect! Using Sarah's pain points, 
I'm generating concepts that address..."
```

### Context Summarization

When switching agents, context is summarized:

**Full Context (for DB storage):**
```json
{
  "conversation_length": 47,
  "messages": [ /* all 47 messages */ ],
  "entities_discussed": ["company_profile", "persona_3", "competitor_2"],
  "actions_taken": ["scraped_website", "generated_personas"],
  "open_questions": []
}
```

**Summarized Context (for agent handoff):**
```json
{
  "summary": "User is setting up campaign for Acme Corp. 
             Company profile complete. 5 personas selected. 
             3 competitors added. Currently waiting for 
             insights.",
  "relevant_entities": ["company_123", "persona_1", "persona_3"],
  "user_intent": "create_campaign",
  "next_step": "theme_selection"
}
```

---

## Conversation Patterns

### Pattern 1: Linear Workflow (Onboarding)
```
User enters → Onboarding Agent greets
             ↓
          Discovery Agent researches
             ↓
     Brand Agent + ICP Agent (parallel)
             ↓
     User adds competitors
             ↓
     Competitor Agent scrapes
             ↓
     Insight Agent synthesizes
             ↓
     User selects themes
             ↓
     Brief Maker generates concepts
             ↓
     Creative Prompter creates visuals
             ↓
     User approves and publishes
```

**Onboarding Agent orchestrates, updates progress**

### Pattern 2: Exploratory Conversation
```
User: "Tell me about my competitors' ads"
  → Competitor Agent

User: "Why is this ad performing well?"
  → Analyst Agent (with context from Competitor)

User: "Can I use this strategy for my campaign?"
  → Brief Maker (with context from Analyst)

User: "Show me what that would look like"
  → Creative Prompter (with context from Brief Maker)
```

**Smart routing with context chaining**

### Pattern 3: Agent-Initiated Conversation
```
Monitor Agent: "⚠️ Alert! Your 'Product Demo' ad 
just dropped 50% in CTR. This could indicate:
1. Audience fatigue (running 30+ days)
2. Competitor launched similar campaign
3. Creative refresh needed

Would you like me to:
A) Ask Analyst Agent for deeper analysis?
B) Have Brief Maker generate new variations?
C) Pause the ad and reallocate budget?"
```

**Proactive agents suggest actions**

### Pattern 4: Multi-Agent Collaboration
```
User: "Why isn't my campaign performing?"

Onboarding Agent: "Let me gather the experts..."

[Brings in Monitor, Analyst, Competitor]

Monitor Agent: "Your ads have been running 45 days. 
Current CTR: 0.8% (down from 1.4%)"

Analyst Agent: "I see 3 issues:
1. Audience fatigue (same creative)
2. CPL increased 60% 
3. Competitor launched aggressive campaign"

Competitor Agent: "I just scraped your main competitor. 
They launched 12 new ads last week with different 
messaging angles."

Analyst Agent: "Recommendations:
1. Refresh creative (Creative Prompter can help)
2. Test new audiences (ICP Agent can suggest)
3. Adjust bids (Planner can optimize)"

User: "Let's refresh creative"

Brief Maker: "I'm on it! Based on Competitor Agent's 
findings and Analyst's insights, I'm generating 6 
new concepts with fresh angles..."
```

**Multiple agents contribute expertise**

---

## UI Components

### Agent Avatar & Status
```
┌─────────────────────────┐
│ 🔍 Discovery Agent      │
│ Status: Researching     │
│ ●●●○○                   │
│                         │
│ Current task:           │
│ Analyzing competitors   │
│                         │
│ Time remaining: 3 min   │
└─────────────────────────┘
```

### Agent Response Cards
```
┌─────────────────────────────────────┐
│ 💡 Insight Agent                    │
│                                     │
│ I found 5 effective themes:         │
│                                     │
│ ┌─────────────────────────────────┐│
│ │ 1. Problem → Solution           ││
│ │    Performance: 8.7/10          ││
│ │    12 competitor ads use this   ││
│ │    [View examples]              ││
│ └─────────────────────────────────┘│
│                                     │
│ ┌─────────────────────────────────┐│
│ │ 2. Testimonial-driven           ││
│ │    Performance: 8.2/10          ││
│ │    8 competitor ads use this    ││
│ │    [View examples]              ││
│ └─────────────────────────────────┘│
│                                     │
│ [Select themes] [See all 5]        │
└─────────────────────────────────────┘
```

### Action Buttons
```
┌─────────────────────────────────────┐
│ Quick Actions:                      │
│                                     │
│ [🔍 Research my company]            │
│ [👥 Generate personas]              │
│ [🔬 Analyze competitors]            │
│ [📝 Create ad concepts]             │
│ [📊 Check performance]              │
└─────────────────────────────────────┘
```

### Progress Indicators
```
┌─────────────────────────────────────┐
│ Onboarding Progress                 │
│                                     │
│ ✅ Company research                 │
│ ✅ Brand analysis                   │
│ ✅ Persona generation               │
│ ⏳ Competitor analysis (60%)        │
│ ○ Strategic insights                │
│ ○ Concept generation                │
└─────────────────────────────────────┘
```

---

## Error Handling & Failures

### Agent Unavailable
```
User: "Analyze my competitors"

Competitor Agent: "I'm currently processing 3 other 
requests. You're #2 in queue (est. 3 min wait).

Would you like to:
- Wait for me
- Continue with other setup tasks
- Get notified when I'm ready"
```

### Task Failure
```
Discovery Agent: "I couldn't access acme.com (timeout). 
Let me try a different approach:

Option 1: You can provide a brief description
Option 2: I can search for public info about Acme Corp
Option 3: Try accessing the website again

What would you prefer?"
```

### Missing Dependencies
```
Brief Maker: "I need information from Insight Agent 
before generating concepts. 

Current status:
- Competitor Agent: Still analyzing (2 min remaining)
- Insight Agent: Waiting for Competitor Agent

You can:
- Wait for insights (recommended)
- Generate concepts without insights
- Work on other tasks in the meantime"
```

---

## Best Practices

### DO:
✅ **Make agents feel human but capable**
   - "Let me analyze that..." not "Processing..."
   - "I found 3 patterns" not "Analysis complete"

✅ **Show, don't just tell**
   - Include preview cards, thumbnails, summaries
   - Let users drill down into details

✅ **Acknowledge handoffs explicitly**
   - "Let me bring in Brand Agent for this..."
   - "Based on what Discovery Agent found..."

✅ **Provide escape hatches**
   - "Skip this step"
   - "I'll do this later"
   - "Use default settings"

✅ **Be transparent about limitations**
   - "I can't access that website"
   - "I need more information about..."
   - "This will take about 5 minutes"

### DON'T:
❌ **Don't make users repeat information**
   - Agents should share context automatically

❌ **Don't use robotic language**
   - Avoid: "Task completed successfully"
   - Use: "Done! Here's what I found..."

❌ **Don't hide agent collaboration**
   - Show when agents are working together
   - Explain why another agent was brought in

❌ **Don't overwhelm with options**
   - Suggest next best action
   - Allow customization if needed

❌ **Don't lose context on errors**
   - Preserve conversation state
   - Allow users to retry or take alternative paths

---

## Implementation Example

**Chat Interface React Component:**
```typescript
interface AgentMessage {
  agent: string;
  message: string;
  data?: any;
  actions?: Action[];
  timestamp: Date;
}

const ChatInterface = () => {
  const [messages, setMessages] = useState<AgentMessage[]>([]);
  const [currentAgent, setCurrentAgent] = useState<string>("onboarding");
  const [inputValue, setInputValue] = useState("");
  
  const sendMessage = async () => {
    // Add user message
    const userMessage = { role: "user", content: inputValue };
    setMessages([...messages, userMessage]);
    
    // Route to appropriate agent
    const response = await fetch("/api/chat", {
      method: "POST",
      body: JSON.stringify({
        message: inputValue,
        context: {
          company_id: user.company_id,
          current_agent: currentAgent,
          conversation_history: messages
        }
      })
    });
    
    const { agent, message, data, actions } = await response.json();
    
    // Update current agent if changed
    if (agent !== currentAgent) {
      setCurrentAgent(agent);
    }
    
    // Add agent response
    setMessages([...messages, {
      agent,
      message,
      data,
      actions,
      timestamp: new Date()
    }]);
  };
  
  return (
    <div className="chat-interface">
      <AgentHeader agent={currentAgent} />
      
      <MessageList messages={messages} />
      
      <QuickActions actions={suggestedActions} />
      
      <ChatInput 
        value={inputValue}
        onChange={setInputValue}
        onSend={sendMessage}
      />
    </div>
  );
};
```

---

*This conversational interface design ensures users have natural, productive conversations with specialized AI agents while maintaining clarity and control.*
