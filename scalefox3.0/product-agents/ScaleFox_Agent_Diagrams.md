# ScaleFox Agent System Diagram

## System Architecture Visualization

```mermaid
graph TB
    subgraph "User Interface Layer"
        USER[User Chat Interface]
        DASHBOARD[Dashboard]
    end

    subgraph "Orchestration Layer"
        ONBOARD[Onboarding Agent<br/>Workflow Coordinator]
    end

    subgraph "Research & Intelligence Layer"
        DISCOVERY[Discovery Agent<br/>Company & Industry]
        BRAND[Brand Agent<br/>Visual & Verbal Identity]
        ICP[ICP Agent<br/>Target Personas]
        COMPETITOR[Competitor Agent<br/>Ad Intelligence]
    end

    subgraph "Strategic Layer"
        INSIGHT[Insight Agent<br/>Pattern Synthesis]
        PLANNER[Planner Agent<br/>Campaign Strategy]
    end

    subgraph "Creative Layer"
        BRIEF[Brief Maker<br/>Concept Generation]
        CREATIVE[Creative Prompter<br/>Visual Generation]
    end

    subgraph "Execution Layer"
        PUBLISHER[Publisher Agent<br/>Draft Management]
        MONITOR[Monitor Agent<br/>Real-Time Tracking]
        ANALYST[Analyst Agent<br/>Performance Intelligence]
    end

    subgraph "Data Layer"
        DB[(Database<br/>Agent Knowledge<br/>Performance Data)]
    end

    USER --> ONBOARD
    USER -.-> DISCOVERY
    USER -.-> BRAND
    USER -.-> ICP
    USER -.-> COMPETITOR
    USER -.-> INSIGHT
    USER -.-> BRIEF
    USER -.-> CREATIVE
    USER -.-> PUBLISHER
    USER -.-> PLANNER
    USER -.-> MONITOR
    USER -.-> ANALYST
    
    ONBOARD --> DISCOVERY
    ONBOARD --> BRAND
    ONBOARD --> ICP
    
    DISCOVERY --> BRAND
    DISCOVERY --> ICP
    DISCOVERY --> COMPETITOR
    DISCOVERY --> DB
    
    BRAND --> BRIEF
    BRAND --> CREATIVE
    BRAND --> PUBLISHER
    BRAND --> DB
    
    ICP --> COMPETITOR
    ICP --> INSIGHT
    ICP --> BRIEF
    ICP --> DB
    
    COMPETITOR --> INSIGHT
    COMPETITOR --> DB
    
    INSIGHT --> BRIEF
    INSIGHT --> PLANNER
    INSIGHT --> DB
    
    BRIEF --> CREATIVE
    BRIEF --> PUBLISHER
    BRIEF --> DB
    
    CREATIVE --> PUBLISHER
    CREATIVE --> DB
    
    PUBLISHER --> MONITOR
    PUBLISHER --> DB
    
    MONITOR --> ANALYST
    MONITOR --> DB
    
    ANALYST --> INSIGHT
    ANALYST --> ICP
    ANALYST --> BRIEF
    ANALYST --> PLANNER
    ANALYST --> DB
    
    PLANNER --> BRIEF
    PLANNER --> PUBLISHER
    PLANNER --> DB
    
    DASHBOARD --> DB
```

## Agent Communication Flow

```mermaid
sequenceDiagram
    participant User
    participant Onboarding
    participant Discovery
    participant Brand
    participant ICP
    participant Competitor
    participant Insight
    participant Brief
    participant Creative
    participant Publisher
    participant Monitor

    User->>Onboarding: Provide company URL
    Onboarding->>Discovery: Initialize company research
    
    par Parallel Research
        Discovery->>Discovery: Scrape website
        Discovery->>Discovery: Web search
        Discovery->>Discovery: Industry analysis
    end
    
    Discovery->>Brand: Company data
    Discovery->>ICP: Industry context
    
    par Brand & ICP Development
        Brand->>Brand: Analyze visual identity
        Brand->>Brand: Extract tone of voice
        ICP->>ICP: Generate personas
        ICP->>ICP: Research behaviors
    end
    
    User->>Onboarding: Add competitors
    Onboarding->>Competitor: Scrape competitor ads
    
    Competitor->>Competitor: Cluster ads
    Competitor->>Competitor: Rank clusters
    Competitor->>Insight: Clustered data
    
    Insight->>Insight: Identify themes
    Insight->>Insight: Extract patterns
    
    User->>Insight: Select themes
    Insight->>Brief: Selected themes + ICP + Brand
    
    Brief->>Brief: Generate 6 concepts
    Brief->>Creative: Concepts + Briefs
    
    Creative->>Creative: Generate images
    Creative->>Publisher: Images + Copy
    
    User->>Publisher: Approve & publish
    Publisher->>Monitor: Published ads
    
    Monitor->>Monitor: Track performance
    Monitor->>User: Real-time alerts
```

## Data Flow Architecture

```mermaid
flowchart LR
    subgraph "Input Sources"
        URL[Company URL]
        COMP[Competitor URLs]
        USER_INPUT[User Inputs]
    end

    subgraph "Agent Processing"
        A1[Discovery]
        A2[Brand]
        A3[ICP]
        A4[Competitor]
        A5[Insight]
        A6[Brief]
        A7[Creative]
    end

    subgraph "Knowledge Accumulation"
        K1[(Company<br/>Knowledge)]
        K2[(Brand<br/>Identity)]
        K3[(Persona<br/>Profiles)]
        K4[(Market<br/>Intelligence)]
        K5[(Strategic<br/>Insights)]
        K6[(Concepts<br/>& Briefs)]
        K7[(Creative<br/>Assets)]
    end

    subgraph "Outputs"
        OUT1[Campaign Briefs]
        OUT2[Ad Creatives]
        OUT3[Performance Reports]
    end

    URL --> A1
    COMP --> A4
    USER_INPUT --> A1
    USER_INPUT --> A3
    USER_INPUT --> A5
    USER_INPUT --> A6
    
    A1 --> K1
    K1 --> A2
    K1 --> A3
    
    A2 --> K2
    A3 --> K3
    A4 --> K4
    
    K2 --> A5
    K3 --> A5
    K4 --> A5
    
    A5 --> K5
    
    K1 --> A6
    K2 --> A6
    K3 --> A6
    K5 --> A6
    
    A6 --> K6
    
    K2 --> A7
    K6 --> A7
    
    A7 --> K7
    
    K6 --> OUT1
    K7 --> OUT2
    K4 --> OUT3
```

## Agent State Machine (Example: Brief Maker)

```mermaid
stateDiagram-v2
    [*] --> Idle
    
    Idle --> Analyzing: User requests concepts
    Analyzing --> GatheringInputs: Validate prerequisites
    
    GatheringInputs --> CheckInsights: Fetch insights
    CheckInsights --> WithInsights: Insights available
    CheckInsights --> WithoutInsights: No insights
    
    WithInsights --> GeneratingCompetitorBased: Generate 3 competitor concepts
    WithoutInsights --> GeneratingContrarian: Generate 6 contrarian concepts
    
    GeneratingCompetitorBased --> GeneratingContrarian
    GeneratingContrarian --> ValidatingConcepts
    
    ValidatingConcepts --> ConceptsReady: All pass QA
    ValidatingConcepts --> RefiningConcepts: Issues found
    
    RefiningConcepts --> ValidatingConcepts
    
    ConceptsReady --> StoringToDB
    StoringToDB --> NotifyingUser
    NotifyingUser --> Idle
    
    Idle --> [*]
```

## Agent Collaboration Pattern

```mermaid
graph LR
    subgraph "Agent Collaboration Example: Creating Campaign"
        A[Discovery Agent] -->|Company Data| B[Brief Maker]
        C[Brand Agent] -->|Brand Guidelines| B
        D[ICP Agent] -->|Personas| B
        E[Insight Agent] -->|Themes| B
        
        B -->|Concepts| F[Creative Prompter]
        C -->|Visual Identity| F
        
        F -->|Images + Copy| G[Publisher]
        C -->|Brand Validation Rules| G
        
        G -->|Published Ads| H[Monitor]
        H -->|Performance Data| I[Analyst]
        
        I -.->|Learning Feedback| A
        I -.->|Learning Feedback| D
        I -.->|Learning Feedback| E
        I -.->|Learning Feedback| B
    end
```

## Database Schema Overview

```mermaid
erDiagram
    USERS ||--o{ COMPANIES : owns
    COMPANIES ||--o{ COMPETITORS : tracks
    COMPANIES ||--o{ PERSONAS : targets
    COMPANIES ||--o{ CAMPAIGNS : runs
    
    COMPETITORS ||--o{ COMPETITOR_ADS : has
    COMPETITOR_ADS ||--o{ AD_CLUSTERS : belongs_to
    
    AD_CLUSTERS ||--o{ INSIGHTS : generates
    INSIGHTS ||--o{ EFFECTIVE_THEMES : contains
    
    PERSONAS ||--o{ BRIEFS : targets
    EFFECTIVE_THEMES ||--o{ BRIEFS : informs
    COMPANIES ||--o{ BRIEFS : creates
    
    BRIEFS ||--o{ GENERATED_IMAGES : produces
    GENERATED_IMAGES ||--o{ DRAFTS : becomes
    
    DRAFTS ||--o{ PUBLISHED_ADS : publishes_as
    CAMPAIGNS ||--o{ PUBLISHED_ADS : contains
    
    PUBLISHED_ADS ||--o{ PERFORMANCE_METRICS : tracks
    
    USERS {
        uuid user_id PK
        string email
        jsonb preferences
        timestamp created_at
    }
    
    COMPANIES {
        uuid company_id PK
        uuid user_id FK
        jsonb company_profile
        jsonb brand_identity
        timestamp last_updated
    }
    
    PERSONAS {
        uuid persona_id PK
        uuid company_id FK
        string name
        jsonb demographics
        jsonb psychographics
        boolean selected
    }
    
    COMPETITORS {
        uuid competitor_id PK
        uuid company_id FK
        string name
        string url
        timestamp last_scraped
    }
    
    COMPETITOR_ADS {
        uuid ad_id PK
        uuid competitor_id FK
        jsonb ad_data
        uuid cluster_id FK
    }
    
    AD_CLUSTERS {
        uuid cluster_id PK
        int cluster_rank
        float cluster_score
        uuid best_ad_id FK
    }
    
    INSIGHTS {
        uuid insight_id PK
        uuid company_id FK
        jsonb effective_themes
        jsonb success_patterns
        timestamp generated_at
    }
    
    BRIEFS {
        uuid brief_id PK
        uuid company_id FK
        string concept_name
        jsonb ad_copy
        jsonb brief_data
        string status
    }
    
    GENERATED_IMAGES {
        uuid image_id PK
        uuid brief_id FK
        string image_url
        jsonb generation_params
    }
    
    DRAFTS {
        uuid draft_id PK
        uuid brief_id FK
        uuid image_id FK
        string status
        jsonb validation_result
    }
    
    CAMPAIGNS {
        uuid campaign_id PK
        uuid company_id FK
        string campaign_name
        jsonb campaign_config
    }
    
    PUBLISHED_ADS {
        uuid published_ad_id PK
        uuid draft_id FK
        uuid campaign_id FK
        string platform
        timestamp published_at
    }
    
    PERFORMANCE_METRICS {
        uuid metric_id PK
        uuid published_ad_id FK
        jsonb metrics
        timestamp recorded_at
    }
```

## Agent Interaction Matrix

| Agent | Sends Data To | Receives Data From | Collaboration Type |
|-------|---------------|-------------------|-------------------|
| **Discovery** | Brand, ICP, Competitor, Brief | Analyst | Sequential (Foundation) |
| **Brand** | Brief, Creative, Publisher | Discovery | Sequential + Validation |
| **ICP** | Competitor, Insight, Brief | Discovery, Analyst | Sequential + Feedback |
| **Competitor** | Insight | Discovery, ICP | Sequential |
| **Insight** | Brief, Planner | Competitor, ICP, Analyst | Synthesis |
| **Brief** | Creative, Publisher | Discovery, Brand, ICP, Insight, Analyst | Creation |
| **Creative** | Publisher | Brief, Brand | Creation |
| **Publisher** | Monitor | Creative, Brand | Execution |
| **Monitor** | Analyst | Publisher | Real-time |
| **Analyst** | All Agents | Monitor | Feedback Loop |
| **Planner** | Brief, Publisher | Insight, Analyst | Coordination |
| **Onboarding** | All Agents | All Agents | Orchestration |

---

*These diagrams provide a visual overview of how the ScaleFox agent system operates.*
