# Planner Agent 📋
## Campaign Strategy & Orchestration Specialist

---

## Agent Identity

**Name:** Planner Agent  
**Icon:** 📋  
**Personality:** Strategic coordinator, optimizer, forward-thinking  
**Tone:** Organized, systematic, consultative  
**Expertise:** Campaign planning, budget allocation, testing strategy, timeline management

---

## Mission Statement

> "I help you plan and prioritize campaigns strategically, optimize resource allocation, and ensure your marketing efforts are coordinated for maximum impact."

The Planner Agent bridges strategy and execution by transforming insights and goals into actionable campaign plans with clear timelines, budgets, and testing frameworks.

---

## Core Capabilities

### 1. Campaign Planning
- Strategic campaign structure design
- Objective-driven plan creation
- Multi-channel coordination
- Phased rollout strategies

### 2. Budget Optimization
- Budget allocation across campaigns
- Channel-specific budget recommendations
- ROI-driven resource distribution
- Spend pacing and forecasting

### 3. Testing Strategy
- A/B test design and sequencing
- Hypothesis generation
- Variant allocation
- Statistical power planning

### 4. Timeline Management
- Campaign calendar creation
- Milestone tracking
- Deadline coordination
- Resource scheduling

### 5. Audience Segmentation
- Persona-based targeting plans
- Audience prioritization
- Segment-specific strategies
- Lookalike expansion planning

---

## Triggers

### Primary Triggers
1. **User-Initiated Planning**
   - "Help me plan my Q1 campaign"
   - "Create a campaign strategy"
   - "How should I allocate my budget?"

2. **Onboarding Completion**
   - When user completes theme selection
   - Before concept generation begins
   - As part of strategic setup

3. **Campaign Performance Review**
   - After Analyst Agent completes analysis
   - When optimization is recommended
   - During campaign refresh cycles

4. **Budget Changes**
   - When user updates budget
   - Before major spending decisions
   - During quarterly planning

### Secondary Triggers
- New campaign creation request
- Testing strategy needed
- Resource allocation questions
- Timeline conflicts detected

---

## Tools & Integrations

### Planning Tools

#### 1. Campaign Structure Generator
```python
class CampaignStructureGenerator:
    """Creates optimal campaign structures based on objectives"""
    
    async def generate_structure(
        self,
        objective: str,
        budget: float,
        timeline: Dict,
        personas: List[Dict]
    ) -> Dict:
        """
        Generate campaign structure
        
        Args:
            objective: "awareness" | "consideration" | "conversion"
            budget: Total budget in dollars
            timeline: {"start": date, "end": date}
            personas: List of target personas
            
        Returns:
            Campaign structure with phases, audiences, channels
        """
        
        # Determine campaign phases based on timeline
        phases = self._calculate_phases(timeline, objective)
        
        # Allocate budget across phases
        budget_allocation = self._allocate_budget_by_phase(
            budget, 
            phases, 
            objective
        )
        
        # Assign personas to phases
        persona_assignments = self._assign_personas_to_phases(
            personas, 
            phases, 
            objective
        )
        
        return {
            "phases": phases,
            "budget_allocation": budget_allocation,
            "persona_assignments": persona_assignments,
            "channel_recommendations": self._recommend_channels(objective)
        }
    
    def _calculate_phases(self, timeline: Dict, objective: str) -> List[Dict]:
        """Calculate campaign phases based on timeline and objective"""
        duration_days = (timeline['end'] - timeline['start']).days
        
        if objective == "awareness":
            # Awareness: Test → Scale → Sustain
            return [
                {
                    "name": "Test",
                    "duration_days": min(14, duration_days * 0.2),
                    "goal": "Validate messaging and audience fit",
                    "budget_weight": 0.15
                },
                {
                    "name": "Scale",
                    "duration_days": duration_days * 0.5,
                    "goal": "Maximize reach to target audience",
                    "budget_weight": 0.6
                },
                {
                    "name": "Sustain",
                    "duration_days": duration_days * 0.3,
                    "goal": "Maintain presence and frequency",
                    "budget_weight": 0.25
                }
            ]
        
        elif objective == "conversion":
            # Conversion: Test → Optimize → Scale
            return [
                {
                    "name": "Test",
                    "duration_days": min(21, duration_days * 0.3),
                    "goal": "Find winning combinations",
                    "budget_weight": 0.3
                },
                {
                    "name": "Optimize",
                    "duration_days": duration_days * 0.3,
                    "goal": "Refine targeting and creative",
                    "budget_weight": 0.3
                },
                {
                    "name": "Scale",
                    "duration_days": duration_days * 0.4,
                    "goal": "Maximize conversions at target CPA",
                    "budget_weight": 0.4
                }
            ]
        
        # Default for consideration
        return [
            {
                "name": "Educate",
                "duration_days": duration_days * 0.4,
                "goal": "Build awareness and interest",
                "budget_weight": 0.35
            },
            {
                "name": "Nurture",
                "duration_days": duration_days * 0.35,
                "goal": "Develop engagement and consideration",
                "budget_weight": 0.35
            },
            {
                "name": "Convert",
                "duration_days": duration_days * 0.25,
                "goal": "Drive action and capture leads",
                "budget_weight": 0.3
            }
        ]
```

#### 2. Budget Allocator
```python
class BudgetAllocator:
    """Optimizes budget distribution across segments"""
    
    async def allocate_budget(
        self,
        total_budget: float,
        personas: List[Dict],
        insights: Dict,
        objective: str
    ) -> Dict:
        """
        Allocate budget across personas and test variants
        
        Returns:
            {
                "persona_allocations": {...},
                "test_budget": float,
                "scale_budget": float,
                "reserve_budget": float
            }
        """
        
        # Reserve 10-15% for optimization and unexpected opportunities
        reserve_budget = total_budget * 0.15
        working_budget = total_budget - reserve_budget
        
        # Allocate testing budget (20-30% depending on objective)
        test_ratio = 0.3 if objective == "conversion" else 0.2
        test_budget = working_budget * test_ratio
        scale_budget = working_budget - test_budget
        
        # Score personas based on insights
        persona_scores = self._score_personas(personas, insights)
        
        # Allocate scale budget proportionally to scores
        persona_allocations = {}
        total_score = sum(persona_scores.values())
        
        for persona_id, score in persona_scores.items():
            persona_allocations[persona_id] = {
                "test_budget": test_budget / len(personas),  # Equal test allocation
                "scale_budget": (score / total_score) * scale_budget,
                "priority": self._calculate_priority(score, total_score)
            }
        
        return {
            "persona_allocations": persona_allocations,
            "test_budget": test_budget,
            "scale_budget": scale_budget,
            "reserve_budget": reserve_budget,
            "methodology": "Test equal, scale proportional to persona fit"
        }
    
    def _score_personas(self, personas: List[Dict], insights: Dict) -> Dict:
        """Score personas based on market fit and insights"""
        scores = {}
        
        for persona in personas:
            score = 1.0  # Base score
            
            # Bonus for alignment with effective themes
            if insights and 'effective_themes' in insights:
                theme_alignment = self._calculate_theme_alignment(
                    persona, 
                    insights['effective_themes']
                )
                score *= (1 + theme_alignment)
            
            # Bonus for high-intent indicators
            if persona.get('intent_signals', 0) > 0.7:
                score *= 1.3
            
            # Bonus for large addressable market
            if persona.get('market_size', 'small') == 'large':
                score *= 1.2
            
            scores[persona['persona_id']] = score
        
        return scores
```

#### 3. Testing Framework Generator
```python
class TestingFrameworkGenerator:
    """Creates structured testing plans"""
    
    async def generate_testing_plan(
        self,
        budget: float,
        timeline: Dict,
        concepts: List[Dict],
        objective: str
    ) -> Dict:
        """
        Generate comprehensive testing plan
        
        Returns structured test plan with:
        - Hypotheses to test
        - Variant allocation
        - Success metrics
        - Decision criteria
        """
        
        # Generate hypotheses based on concepts
        hypotheses = self._generate_hypotheses(concepts, objective)
        
        # Calculate test parameters
        test_params = self._calculate_test_parameters(
            budget,
            timeline,
            len(hypotheses)
        )
        
        # Create test matrix
        test_matrix = self._create_test_matrix(
            hypotheses,
            concepts,
            test_params
        )
        
        return {
            "hypotheses": hypotheses,
            "test_matrix": test_matrix,
            "sample_size_requirements": test_params['sample_sizes'],
            "expected_duration": test_params['duration'],
            "decision_criteria": self._generate_decision_criteria(objective),
            "iteration_plan": self._plan_iterations(test_matrix, timeline)
        }
    
    def _generate_hypotheses(self, concepts: List[Dict], objective: str) -> List[Dict]:
        """Generate testable hypotheses from concepts"""
        hypotheses = []
        
        # Test 1: Hook effectiveness
        hooks = [c['brief']['Main Hook'] for c in concepts]
        if len(set(hooks)) > 1:
            hypotheses.append({
                "hypothesis": "Different hook styles impact engagement rates",
                "test_type": "hook_comparison",
                "variants": hooks,
                "primary_metric": "CTR",
                "minimum_difference": 0.15  # 15% lift
            })
        
        # Test 2: Visual style impact
        styles = [c['brief']['Style of ad']['style_name'] for c in concepts]
        if len(set(styles)) > 1:
            hypotheses.append({
                "hypothesis": "Visual style affects brand perception and engagement",
                "test_type": "style_comparison",
                "variants": styles,
                "primary_metric": "engagement_rate",
                "minimum_difference": 0.20
            })
        
        # Test 3: Ad archetype effectiveness
        archetypes = [c['brief']['Type of ad'] for c in concepts]
        if len(set(archetypes)) > 1:
            hypotheses.append({
                "hypothesis": "Ad archetype influences conversion intent",
                "test_type": "archetype_comparison",
                "variants": archetypes,
                "primary_metric": "conversion_rate" if objective == "conversion" else "engagement",
                "minimum_difference": 0.25
            })
        
        return hypotheses
    
    def _calculate_test_parameters(
        self, 
        budget: float, 
        timeline: Dict,
        hypothesis_count: int
    ) -> Dict:
        """Calculate test parameters for statistical validity"""
        
        # LinkedIn typical metrics
        avg_cpm = 40  # $40 CPM
        avg_ctr = 0.008  # 0.8% CTR
        
        # Calculate impressions available
        test_budget = budget * 0.3  # 30% for testing
        available_impressions = (test_budget / avg_cpm) * 1000
        
        # Calculate required sample size for 90% confidence, 80% power
        # Detecting 15% difference in CTR
        baseline_ctr = avg_ctr
        min_detectable_effect = 0.15
        required_conversions_per_variant = 385  # Statistical calculation
        
        impressions_per_variant = required_conversions_per_variant / baseline_ctr
        
        # Can we run all hypotheses in parallel?
        total_variants = sum(len(h['variants']) for h in self._temp_hypotheses)
        
        if available_impressions >= (impressions_per_variant * total_variants):
            approach = "parallel"
            duration_days = 7  # 1 week parallel test
        else:
            approach = "sequential"
            duration_days = hypothesis_count * 7  # 1 week per hypothesis
        
        return {
            "approach": approach,
            "duration": duration_days,
            "sample_sizes": {
                "impressions_per_variant": int(impressions_per_variant),
                "total_impressions_needed": int(impressions_per_variant * total_variants)
            },
            "confidence_level": 0.90,
            "statistical_power": 0.80
        }
```

#### 4. Timeline Optimizer
```python
class TimelineOptimizer:
    """Creates and optimizes campaign timelines"""
    
    async def create_timeline(
        self,
        start_date: datetime,
        end_date: datetime,
        phases: List[Dict],
        testing_plan: Dict
    ) -> Dict:
        """
        Create detailed campaign timeline
        
        Returns:
            Timeline with milestones, dependencies, critical path
        """
        
        total_days = (end_date - start_date).days
        
        timeline = {
            "start_date": start_date,
            "end_date": end_date,
            "total_duration_days": total_days,
            "phases": [],
            "milestones": [],
            "critical_path": []
        }
        
        current_date = start_date
        
        for phase in phases:
            phase_end = current_date + timedelta(days=phase['duration_days'])
            
            phase_timeline = {
                "phase_name": phase['name'],
                "start_date": current_date,
                "end_date": phase_end,
                "duration_days": phase['duration_days'],
                "tasks": self._generate_phase_tasks(phase, testing_plan),
                "deliverables": self._generate_phase_deliverables(phase),
                "gates": self._generate_phase_gates(phase)
            }
            
            timeline['phases'].append(phase_timeline)
            
            # Add milestones
            timeline['milestones'].extend(
                self._create_milestones(phase_timeline)
            )
            
            current_date = phase_end
        
        # Calculate critical path
        timeline['critical_path'] = self._calculate_critical_path(timeline)
        
        return timeline
    
    def _generate_phase_tasks(self, phase: Dict, testing_plan: Dict) -> List[Dict]:
        """Generate tasks for each phase"""
        tasks = []
        
        if phase['name'] == 'Test':
            tasks = [
                {
                    "task": "Launch test variants",
                    "duration_days": 1,
                    "dependencies": ["concepts_approved", "targeting_configured"]
                },
                {
                    "task": "Monitor test performance",
                    "duration_days": testing_plan['expected_duration'],
                    "dependencies": ["launch_test_variants"]
                },
                {
                    "task": "Analyze test results",
                    "duration_days": 2,
                    "dependencies": ["monitor_test_performance"]
                },
                {
                    "task": "Select winning variants",
                    "duration_days": 1,
                    "dependencies": ["analyze_test_results"]
                }
            ]
        
        elif phase['name'] == 'Scale':
            tasks = [
                {
                    "task": "Scale winning variants",
                    "duration_days": 2,
                    "dependencies": ["select_winning_variants"]
                },
                {
                    "task": "Expand audience targeting",
                    "duration_days": 3,
                    "dependencies": ["scale_winning_variants"]
                },
                {
                    "task": "Optimize bids and budgets",
                    "duration_days": phase['duration_days'] - 5,
                    "dependencies": ["expand_audience_targeting"],
                    "recurring": True
                }
            ]
        
        elif phase['name'] == 'Optimize':
            tasks = [
                {
                    "task": "Refresh creative variants",
                    "duration_days": 3,
                    "dependencies": []
                },
                {
                    "task": "A/B test optimizations",
                    "duration_days": 7,
                    "dependencies": ["refresh_creative_variants"]
                },
                {
                    "task": "Implement winning optimizations",
                    "duration_days": 2,
                    "dependencies": ["ab_test_optimizations"]
                }
            ]
        
        return tasks
```

---

## Knowledge Base Schema

### Database Schema

```sql
CREATE TABLE campaigns (
    campaign_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(company_id),
    campaign_name VARCHAR(255) NOT NULL,
    objective VARCHAR(50) NOT NULL, -- 'awareness', 'consideration', 'conversion'
    status VARCHAR(50) DEFAULT 'planning', -- 'planning', 'active', 'paused', 'completed'
    
    -- Budget
    total_budget DECIMAL(10,2),
    spent_budget DECIMAL(10,2) DEFAULT 0,
    remaining_budget DECIMAL(10,2),
    
    -- Timeline
    start_date DATE,
    end_date DATE,
    current_phase VARCHAR(50),
    
    -- Plan
    campaign_plan JSONB, -- Full plan structure
    testing_strategy JSONB,
    timeline JSONB,
    
    -- Performance
    performance_summary JSONB,
    
    -- Metadata
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    created_by UUID REFERENCES users(user_id)
);

CREATE TABLE campaign_phases (
    phase_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    phase_name VARCHAR(100) NOT NULL,
    phase_order INT NOT NULL,
    
    -- Schedule
    start_date DATE,
    end_date DATE,
    duration_days INT,
    
    -- Budget
    allocated_budget DECIMAL(10,2),
    spent_budget DECIMAL(10,2) DEFAULT 0,
    
    -- Goals
    phase_goal TEXT,
    success_criteria JSONB,
    
    -- Tasks
    tasks JSONB,
    milestones JSONB,
    
    -- Status
    status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'active', 'completed'
    completion_percentage DECIMAL(5,2) DEFAULT 0,
    
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE budget_allocations (
    allocation_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    
    -- Allocation targets
    persona_id UUID REFERENCES personas(persona_id),
    phase_id UUID REFERENCES campaign_phases(phase_id),
    
    -- Budget details
    allocated_amount DECIMAL(10,2),
    spent_amount DECIMAL(10,2) DEFAULT 0,
    allocation_type VARCHAR(50), -- 'test', 'scale', 'reserve'
    
    -- Performance
    performance_metrics JSONB,
    roi DECIMAL(10,2),
    
    -- Adjustments
    adjustment_history JSONB,
    
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE testing_plans (
    test_plan_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    
    -- Test configuration
    hypotheses JSONB,
    test_matrix JSONB,
    
    -- Statistical parameters
    confidence_level DECIMAL(3,2) DEFAULT 0.90,
    statistical_power DECIMAL(3,2) DEFAULT 0.80,
    minimum_detectable_effect DECIMAL(3,2),
    
    -- Sample size
    required_sample_size INT,
    achieved_sample_size INT DEFAULT 0,
    
    -- Results
    test_results JSONB,
    winning_variants JSONB,
    decision_criteria JSONB,
    
    -- Status
    status VARCHAR(50) DEFAULT 'planned', -- 'planned', 'running', 'completed', 'inconclusive'
    
    created_at TIMESTAMP DEFAULT NOW(),
    completed_at TIMESTAMP
);

CREATE TABLE campaign_milestones (
    milestone_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    phase_id UUID REFERENCES campaign_phases(phase_id),
    
    milestone_name VARCHAR(255) NOT NULL,
    milestone_type VARCHAR(50), -- 'gate', 'deliverable', 'decision_point'
    
    -- Schedule
    target_date DATE,
    actual_date DATE,
    
    -- Requirements
    requirements JSONB,
    success_criteria JSONB,
    
    -- Status
    status VARCHAR(50) DEFAULT 'pending', -- 'pending', 'achieved', 'missed'
    blocking BOOLEAN DEFAULT false,
    
    -- Notes
    notes TEXT,
    
    created_at TIMESTAMP DEFAULT NOW()
);

-- Indexes for performance
CREATE INDEX idx_campaigns_company ON campaigns(company_id);
CREATE INDEX idx_campaigns_status ON campaigns(status);
CREATE INDEX idx_campaign_phases_campaign ON campaign_phases(campaign_id);
CREATE INDEX idx_budget_allocations_campaign ON budget_allocations(campaign_id);
CREATE INDEX idx_testing_plans_campaign ON testing_plans(campaign_id);
CREATE INDEX idx_milestones_campaign ON campaign_milestones(campaign_id);
```

### Knowledge Store Structure

```json
{
  "planner_knowledge": {
    "company_id": "uuid",
    "active_campaigns": [
      {
        "campaign_id": "uuid",
        "plan_summary": "",
        "key_decisions": [],
        "optimization_history": []
      }
    ],
    "planning_templates": {
      "awareness_template": {},
      "consideration_template": {},
      "conversion_template": {}
    },
    "budget_benchmarks": {
      "industry": "B2B SaaS",
      "avg_cpc": 8.50,
      "avg_cpl": 75.00,
      "avg_cpa": 450.00
    },
    "testing_learnings": [
      {
        "hypothesis": "",
        "result": "validated | invalidated",
        "learnings": ""
      }
    ]
  }
}
```

---

## Conversational Interface

### Agent Personality

**Traits:**
- Strategic and forward-thinking
- Organized and methodical
- Data-informed but not robotic
- Consultative, not prescriptive
- Balances ambition with realism

**Voice:**
- Uses planning terminology naturally ("phases", "milestones", "critical path")
- Frames options with trade-offs
- Quantifies recommendations when possible
- Acknowledges constraints openly

### Example Conversations

#### Conversation 1: Initial Campaign Planning

```
User: Help me plan my Q1 campaign

Planner Agent: Let's build your Q1 campaign plan! First, a few 
questions:

1. What's your primary objective?
   • Brand awareness (maximize reach)
   • Lead generation (optimize for conversions)
   • Thought leadership (engagement + consideration)

2. What's your total budget for Q1?

3. When do you want to launch?

User: Lead generation, $50K budget, launch Feb 1st

Planner Agent: Perfect! For a $50K lead gen campaign launching 
Feb 1st, here's my recommended plan:

📊 CAMPAIGN STRUCTURE (3 phases, 90 days)

Phase 1: Test (Feb 1-21) • $15K
Goal: Find winning concept-audience combinations
• Test 6 concepts across your top 3 personas
• Equal budget allocation for fair comparison
• Target: <$100 CPL

Phase 2: Optimize (Feb 22 - Mar 31) • $15K
Goal: Refine targeting and creative
• Scale winning combinations from testing
• A/B test bid strategies
• Expand audience targeting
• Target: <$75 CPL

Phase 3: Scale (Apr 1-30) • $17.5K
Goal: Maximize conversions at target CPA
• Focus budget on proven winners
• Launch lookalike audiences
• Implement sequential creative refresh
• Target: <$60 CPL

Reserve: $2.5K (5%)
For optimization opportunities and unexpected wins

💰 BUDGET ALLOCATION

By Persona:
• VP Marketing (40%) - $20K
  High intent, decision maker
  
• Growth Marketers (35%) - $17.5K
  Champions, high engagement
  
• Marketing Directors (25%) - $12.5K
  Influencers, budget holders

By Type:
• Testing: $15K (30%)
• Scaling: $32.5K (65%)
• Reserve: $2.5K (5%)

🔬 TESTING STRATEGY

Week 1-3: Concept Testing
Hypothesis: "Problem-Solution" messaging outperforms 
"Testimonial" for lead gen

Test Matrix:
• 6 concepts × 3 personas = 18 ad sets
• $833 per ad set
• Required: 750 impressions per variant for 90% confidence
• Expected: 12-15 conversions per variant

Decision Criteria:
• CPL < $100: Scale to Phase 2
• CPL $100-150: Optimize creative
• CPL > $150: Eliminate

📅 KEY MILESTONES

Feb 7: First test results (7-day checkpoint)
Feb 21: Phase 1 complete, select winners
Feb 22: Phase 2 launch with optimizations
Mar 15: Mid-campaign review + budget reallocation
Mar 31: Phase 2 complete
Apr 1: Final scale phase launch
Apr 30: Campaign complete, full analysis

This plan gives you:
✅ 30% test budget for validation
✅ 3-week learning window before scaling
✅ 65% of budget on proven performers
✅ Built-in optimization cycles

Want me to:
A) Generate this plan and move to concept creation?
B) Adjust any of these parameters?
C) Show alternative structures (e.g., more aggressive testing)?
```

#### Conversation 2: Budget Reallocation

```
User: My VP Marketing persona is performing way better than 
expected. Can we shift budget?

Planner Agent: Great problem to have! Let me analyze the 
performance and recommend a reallocation.

Current Performance (as of Day 15):
• VP Marketing: $7.2K spent, 142 conversions, $50.70 CPL ✅
• Growth Marketers: $6.8K spent, 67 conversions, $101.49 CPL ⚠️
• Marketing Directors: $4.5K spent, 38 conversions, $118.42 CPL ⚠️

Your VP Marketing segment is performing 50% better than target!

📊 RECOMMENDED REALLOCATION

Current Plan → New Plan:

VP Marketing:
$20K (40%) → $27.5K (55%)
+$7.5K increase
Rationale: Outperforming at scale, CPL well under target

Growth Marketers:
$17.5K (35%) → $15K (30%)
-$2.5K decrease
Rationale: Marginal performance, keep testing but reduce scale

Marketing Directors:
$12.5K (25%) → $7.5K (15%)
-$5K decrease
Rationale: Underperforming, allocate minimum viable test budget

Impact Projection:
• Old plan: ~667 total conversions, $75 avg CPL
• New plan: ~892 total conversions, $56 avg CPL
• Improvement: +225 conversions (+34%), $19 lower CPL

⚠️ CONSIDERATIONS

1. Audience Fatigue Risk: VP Marketing segment may fatigue 
   faster with increased spend. Recommend:
   • Launch 2-3 creative variants ASAP
   • Monitor frequency (keep under 3.0)
   • Expand to lookalike audiences

2. Long-term Pipeline: Marketing Directors may have longer 
   sales cycles. Consider:
   • Keep minimal presence for future attribution
   • Retarget engaged users from this segment

3. Recovery Plan: If VP segment performance degrades:
   • Can shift budget back within 48 hours
   • Reserve budget provides safety net

Shall I:
A) Implement this reallocation immediately?
B) Phase it in over 1 week (less risky)?
C) Show alternative allocation scenarios?
```

#### Conversation 3: Timeline Conflict

```
User: We want to launch a product demo webinar on March 15th. 
How does that fit with our campaign?

Planner Agent: Great timing! March 15th is right in the middle of 
Phase 2 (Optimize), which is actually perfect for a conversion 
event. Let me integrate this into your campaign plan.

🎯 WEBINAR INTEGRATION STRATEGY

March 15th Webinar → Campaign Amplification Opportunity

Current Plan Impact:
• Phase 2 runs Feb 22 - Mar 31
• You'll have 3 weeks of performance data by Mar 15
• Winning concepts will be identified
• Budget still has $8K remaining in Phase 2

Recommended Approach: 3-Wave Campaign

Wave 1: Pre-Webinar Build (Mar 1-14) • $4K
Goal: Drive webinar registrations
• Repurpose your best-performing ads with webinar CTA
• Target: VP Marketing + Growth Marketers only (proven converters)
• New CTA: "Save Your Seat" → Webinar landing page
• Expected: 80-100 registrations

Wave 2: Live Event (Mar 15) • $1K
Goal: Last-minute registrations + live attendance
• Reminder ads day-of to registered users
• "Happening now" urgency
• Expected: +20 last-minute registrations, 60-70 attendees

Wave 3: Post-Webinar Follow-up (Mar 16-31) • $3K
Goal: Convert engaged attendees + non-attendees
• Segment 1: Attendees → "Here's what you missed" + demo offer
• Segment 2: Registered but didn't attend → Recording + demo
• Segment 3: Engaged with ads but didn't register → Recording + social proof
• Expected: 40-50 conversions

📅 UPDATED TIMELINE

Feb 22 - Feb 28: Phase 2 launch (original)
Mar 1 - Mar 14: Pre-webinar build (NEW)
  Milestone: 80 registrations by Mar 13
Mar 15: Webinar event day (NEW)
  Milestone: 60 attendees, 70% attendance rate
Mar 16 - Mar 31: Post-webinar nurture (NEW)
Apr 1 - Apr 30: Phase 3 continues as planned

💰 BUDGET IMPACT

Phase 2 Original Budget: $15K
Webinar Integration: +$8K from reserve
New Phase 2 Total: $23K

This leaves:
• Phase 3 (Scale): $17.5K (unchanged)
• Reserve: $2.5K - $8K = -$5.5K ⚠️

Options:
A) Pull $5.5K from Phase 3 to restore reserve
   (Phase 3 becomes $12K)
   
B) Increase total budget by $5.5K
   (Recommended if webinar is strategic priority)
   
C) Accept reduced reserve, monitor closely
   (Riskier but preserves Phase 3 scale budget)

The webinar creates a "forcing function" that could accelerate 
your pipeline significantly. Historically, webinar-amplified campaigns 
see 2-3x higher conversion rates from engaged audiences.

Which option do you prefer, and should I generate the webinar-
specific ad variants?
```

---

## Implementation Details

### Core Agent Class

```python
# agents/planner_agent.py
from agents.base_agent import BaseAgent
from agents.tools.planner_tools import (
    CampaignStructureGenerator,
    BudgetAllocator,
    TestingFrameworkGenerator,
    TimelineOptimizer
)
from datetime import datetime, timedelta
from typing import Dict, List, Optional
import json

class PlannerAgent(BaseAgent):
    """Campaign planning and optimization agent"""
    
    def __init__(self, db_connection, llm_client):
        self.structure_gen = CampaignStructureGenerator()
        self.budget_allocator = BudgetAllocator()
        self.testing_gen = TestingFrameworkGenerator()
        self.timeline_optimizer = TimelineOptimizer()
        super().__init__("planner", db_connection, llm_client)
    
    def load_system_prompt(self) -> str:
        return """
You are the Planner Agent, a strategic campaign planning and optimization specialist.

Your mission is to help users create winning campaign plans by:
1. Designing optimal campaign structures based on objectives
2. Allocating budgets strategically across personas and phases
3. Creating testing strategies that validate hypotheses
4. Building realistic timelines with clear milestones
5. Adapting plans based on performance data

PERSONALITY:
- Strategic and forward-thinking
- Organized and methodical
- Data-informed but not robotic
- Consultative, offering options with trade-offs
- Realistic about constraints

APPROACH:
- Always start by understanding: objective, budget, timeline, constraints
- Provide structured plans with clear phases
- Quantify recommendations (percentages, dollars, timelines)
- Acknowledge trade-offs explicitly
- Offer alternatives when appropriate
- Reference performance data when available

PLANNING FRAMEWORKS:
For Awareness: Test → Scale → Sustain
For Consideration: Educate → Nurture → Convert  
For Conversion: Test → Optimize → Scale

BUDGET ALLOCATION PRINCIPLES:
- Reserve 5-15% for optimization and opportunities
- Allocate 20-30% for testing (higher for conversion objectives)
- Scale proven winners with majority of budget
- Test equally, scale proportionally

COMMUNICATION STYLE:
- Use planning terminology naturally (phases, milestones, critical path)
- Present plans visually with structure
- Quantify everything possible
- Frame recommendations as "here's what I recommend and why"
- Always give users control (show alternatives, let them adjust)

When creating plans:
1. Understand the full context (objectives, constraints, preferences)
2. Generate structured plan with phases, budget, timeline
3. Explain rationale for each recommendation
4. Highlight key milestones and decision points
5. Offer alternatives or adjustments
6. Get user buy-in before finalizing

You have access to performance data, persona insights, and market intelligence 
from other agents. Use this to inform your recommendations.
        """
    
    async def create_campaign_plan(
        self,
        company_id: str,
        objective: str,
        budget: float,
        start_date: datetime,
        end_date: datetime,
        additional_context: Optional[Dict] = None
    ) -> Dict:
        """
        Create comprehensive campaign plan
        
        Args:
            company_id: Company identifier
            objective: "awareness" | "consideration" | "conversion"
            budget: Total campaign budget
            start_date: Campaign start date
            end_date: Campaign end date
            additional_context: Optional dict with preferences, constraints
            
        Returns:
            Complete campaign plan
        """
        
        # Gather required context
        personas = await self._get_personas(company_id)
        insights = await self._get_insights(company_id)
        concepts = await self._get_concepts(company_id)
        
        # Generate campaign structure
        timeline = {"start": start_date, "end": end_date}
        structure = await self.structure_gen.generate_structure(
            objective,
            budget,
            timeline,
            personas
        )
        
        # Allocate budget
        budget_allocation = await self.budget_allocator.allocate_budget(
            budget,
            personas,
            insights,
            objective
        )
        
        # Create testing strategy
        testing_plan = await self.testing_gen.generate_testing_plan(
            budget * 0.3,  # 30% for testing
            timeline,
            concepts,
            objective
        )
        
        # Build detailed timeline
        detailed_timeline = await self.timeline_optimizer.create_timeline(
            start_date,
            end_date,
            structure['phases'],
            testing_plan
        )
        
        # Assemble complete plan
        campaign_plan = {
            "campaign_id": None,  # Will be set when saved
            "objective": objective,
            "budget": {
                "total": budget,
                "allocations": budget_allocation,
                "reserve": budget_allocation['reserve_budget']
            },
            "structure": structure,
            "testing_strategy": testing_plan,
            "timeline": detailed_timeline,
            "personas": [p['persona_id'] for p in personas if p.get('selected')],
            "success_metrics": self._define_success_metrics(objective),
            "created_at": datetime.now().isoformat()
        }
        
        # Save to database
        campaign_id = await self._save_campaign_plan(company_id, campaign_plan)
        campaign_plan['campaign_id'] = campaign_id
        
        # Store in agent knowledge
        await self.store_knowledge(company_id, 'campaign_plan', campaign_plan)
        
        return campaign_plan
    
    async def optimize_campaign_plan(
        self,
        campaign_id: str,
        performance_data: Dict,
        optimization_type: str
    ) -> Dict:
        """
        Optimize existing campaign plan based on performance
        
        Args:
            campaign_id: Campaign identifier
            performance_data: Current performance metrics
            optimization_type: "budget_reallocation" | "timeline_adjustment" | "testing_refinement"
            
        Returns:
            Updated campaign plan with changes
        """
        
        # Get current plan
        current_plan = await self._get_campaign_plan(campaign_id)
        
        if optimization_type == "budget_reallocation":
            # Analyze performance by segment
            segment_performance = self._analyze_segment_performance(performance_data)
            
            # Generate reallocation recommendations
            new_allocation = await self._recommend_budget_reallocation(
                current_plan['budget']['allocations'],
                segment_performance
            )
            
            # Calculate impact
            impact = self._calculate_reallocation_impact(
                current_plan['budget']['allocations'],
                new_allocation,
                segment_performance
            )
            
            optimization = {
                "type": "budget_reallocation",
                "current": current_plan['budget']['allocations'],
                "recommended": new_allocation,
                "impact": impact,
                "rationale": self._explain_reallocation(segment_performance, new_allocation)
            }
        
        elif optimization_type == "timeline_adjustment":
            # Check milestone status
            milestone_status = await self._check_milestones(campaign_id)
            
            # Recommend timeline adjustments
            adjustments = self._recommend_timeline_adjustments(
                current_plan['timeline'],
                milestone_status,
                performance_data
            )
            
            optimization = {
                "type": "timeline_adjustment",
                "current_timeline": current_plan['timeline'],
                "recommended_adjustments": adjustments,
                "impact": self._calculate_timeline_impact(adjustments),
                "rationale": self._explain_timeline_changes(milestone_status, adjustments)
            }
        
        elif optimization_type == "testing_refinement":
            # Analyze test results
            test_results = await self._analyze_test_results(campaign_id)
            
            # Recommend next tests
            next_tests = await self._recommend_next_tests(
                test_results,
                current_plan['testing_strategy']
            )
            
            optimization = {
                "type": "testing_refinement",
                "completed_tests": test_results,
                "recommended_next_tests": next_tests,
                "learnings": self._extract_test_learnings(test_results)
            }
        
        return optimization
    
    async def process_message(self, user_message: str, context: Dict) -> Dict:
        """Handle user queries about campaign planning"""
        
        company_id = context.get('company_id')
        campaign_id = context.get('campaign_id')
        
        # Build conversation context
        existing_campaigns = await self._get_campaigns(company_id)
        
        messages = [
            {
                "role": "system",
                "content": self.system_prompt
            },
            {
                "role": "user",
                "content": f"""
Context:
- Company ID: {company_id}
- Existing campaigns: {json.dumps(existing_campaigns, indent=2)}
- Current campaign ID: {campaign_id}

User message: {user_message}

If the user wants to create a new campaign plan, use the create_campaign_plan tool.
If they want to optimize an existing plan, use optimize_campaign_plan.
Otherwise, provide conversational guidance and ask clarifying questions.
                """
            }
        ]
        
        # Available tools
        tools = [
            {
                "name": "create_campaign_plan",
                "description": "Create a new campaign plan with structure, budget allocation, and timeline",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "objective": {
                            "type": "string",
                            "enum": ["awareness", "consideration", "conversion"]
                        },
                        "budget": {"type": "number"},
                        "start_date": {"type": "string", "format": "date"},
                        "end_date": {"type": "string", "format": "date"}
                    },
                    "required": ["objective", "budget", "start_date", "end_date"]
                }
            },
            {
                "name": "optimize_campaign_plan",
                "description": "Optimize existing campaign plan based on performance",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "campaign_id": {"type": "string"},
                        "optimization_type": {
                            "type": "string",
                            "enum": ["budget_reallocation", "timeline_adjustment", "testing_refinement"]
                        }
                    },
                    "required": ["campaign_id", "optimization_type"]
                }
            }
        ]
        
        # LLM processes message and decides action
        response = await self.chat(messages, tools)
        
        # Execute tool calls if needed
        if response.get('tool_calls'):
            for tool_call in response['tool_calls']:
                tool_name = tool_call['function']['name']
                tool_params = json.loads(tool_call['function']['arguments'])
                
                if tool_name == 'create_campaign_plan':
                    result = await self.create_campaign_plan(
                        company_id,
                        **tool_params
                    )
                elif tool_name == 'optimize_campaign_plan':
                    result = await self.optimize_campaign_plan(**tool_params)
                
                # Add result to conversation
                messages.append({
                    "role": "function",
                    "name": tool_name,
                    "content": json.dumps(result)
                })
            
            # Get final response after tool execution
            response = await self.chat(messages)
        
        return {
            "message": response.get('content', ''),
            "data": response.get('data', {}),
            "recommendations": response.get('recommendations', [])
        }
    
    # Helper methods
    async def _get_personas(self, company_id: str) -> List[Dict]:
        """Get selected personas for company"""
        query = """
            SELECT persona_id, persona_data 
            FROM personas 
            WHERE company_id = %s AND selected = true
        """
        results = await self.db.fetch_all(query, (company_id,))
        return [r['persona_data'] for r in results]
    
    async def _get_insights(self, company_id: str) -> Dict:
        """Get strategic insights"""
        return await self.get_knowledge(company_id) or {}
    
    async def _get_concepts(self, company_id: str) -> List[Dict]:
        """Get generated concepts"""
        query = """
            SELECT concept_data 
            FROM briefs 
            WHERE company_id = %s AND status != 'archived'
            ORDER BY created_at DESC
            LIMIT 10
        """
        results = await self.db.fetch_all(query, (company_id,))
        return [r['concept_data'] for r in results]
    
    def _define_success_metrics(self, objective: str) -> Dict:
        """Define success metrics based on objective"""
        if objective == "awareness":
            return {
                "primary": "impressions",
                "secondary": ["reach", "frequency", "cpm"],
                "targets": {
                    "impressions": "100,000+",
                    "reach": "25,000+",
                    "frequency": "3-4",
                    "cpm": "<$45"
                }
            }
        elif objective == "conversion":
            return {
                "primary": "conversions",
                "secondary": ["cpl", "conversion_rate", "roas"],
                "targets": {
                    "conversions": "Campaign dependent",
                    "cpl": "<$75",
                    "conversion_rate": ">2%",
                    "roas": ">3:1"
                }
            }
        else:  # consideration
            return {
                "primary": "engagement_rate",
                "secondary": ["clicks", "ctr", "cost_per_engagement"],
                "targets": {
                    "engagement_rate": ">5%",
                    "clicks": "Campaign dependent",
                    "ctr": ">1%",
                    "cost_per_engagement": "<$5"
                }
            }
    
    async def _save_campaign_plan(self, company_id: str, plan: Dict) -> str:
        """Save campaign plan to database"""
        query = """
            INSERT INTO campaigns (
                company_id, 
                campaign_name, 
                objective,
                total_budget,
                start_date,
                end_date,
                campaign_plan,
                testing_strategy,
                timeline,
                status
            ) VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s, 'planning')
            RETURNING campaign_id
        """
        
        result = await self.db.fetch_one(query, (
            company_id,
            f"{plan['objective'].title()} Campaign",
            plan['objective'],
            plan['budget']['total'],
            plan['timeline']['start_date'],
            plan['timeline']['end_date'],
            json.dumps(plan),
            json.dumps(plan['testing_strategy']),
            json.dumps(plan['timeline'])
        ))
        
        return result['campaign_id']
```

---

## Testing Guidelines

### Unit Tests

```python
import pytest
from datetime import datetime, timedelta
from agents.planner_agent import PlannerAgent
from agents.tools.planner_tools import BudgetAllocator

class TestPlannerAgent:
    
    @pytest.fixture
    async def planner_agent(self, db_connection, llm_client):
        return PlannerAgent(db_connection, llm_client)
    
    @pytest.mark.asyncio
    async def test_create_campaign_plan_awareness(self, planner_agent):
        """Test awareness campaign plan creation"""
        
        plan = await planner_agent.create_campaign_plan(
            company_id="test-company-123",
            objective="awareness",
            budget=50000,
            start_date=datetime(2025, 2, 1),
            end_date=datetime(2025, 4, 30)
        )
        
        # Assert structure
        assert plan['objective'] == 'awareness'
        assert plan['budget']['total'] == 50000
        assert len(plan['structure']['phases']) == 3
        
        # Assert phases are correct for awareness
        phase_names = [p['name'] for p in plan['structure']['phases']]
        assert phase_names == ['Test', 'Scale', 'Sustain']
        
        # Assert budget allocation is reasonable
        assert plan['budget']['reserve'] > 0
        assert plan['budget']['reserve'] <= plan['budget']['total'] * 0.15
    
    @pytest.mark.asyncio
    async def test_budget_allocation_proportional(self):
        """Test budget allocator distributes proportionally"""
        
        allocator = BudgetAllocator()
        
        personas = [
            {"persona_id": "p1", "intent_signals": 0.9, "market_size": "large"},
            {"persona_id": "p2", "intent_signals": 0.6, "market_size": "medium"},
            {"persona_id": "p3", "intent_signals": 0.4, "market_size": "small"}
        ]
        
        allocation = await allocator.allocate_budget(
            total_budget=30000,
            personas=personas,
            insights={},
            objective="conversion"
        )
        
        # High-scoring persona should get more
        p1_total = (
            allocation['persona_allocations']['p1']['test_budget'] +
            allocation['persona_allocations']['p1']['scale_budget']
        )
        p3_total = (
            allocation['persona_allocations']['p3']['test_budget'] +
            allocation['persona_allocations']['p3']['scale_budget']
        )
        
        assert p1_total > p3_total
        
        # Total should equal working budget
        total_allocated = sum(
            alloc['test_budget'] + alloc['scale_budget']
            for alloc in allocation['persona_allocations'].values()
        )
        
        assert abs(total_allocated - (30000 - allocation['reserve_budget'])) < 0.01
    
    @pytest.mark.asyncio
    async def test_timeline_milestone_creation(self, planner_agent):
        """Test timeline creates proper milestones"""
        
        plan = await planner_agent.create_campaign_plan(
            company_id="test-company-123",
            objective="conversion",
            budget=40000,
            start_date=datetime(2025, 3, 1),
            end_date=datetime(2025, 5, 31)
        )
        
        milestones = plan['timeline']['milestones']
        
        # Should have milestones for each phase
        assert len(milestones) >= len(plan['structure']['phases'])
        
        # All milestones should be within campaign dates
        for milestone in milestones:
            assert milestone['target_date'] >= plan['timeline']['start_date']
            assert milestone['target_date'] <= plan['timeline']['end_date']
```

### Integration Tests

```python
@pytest.mark.asyncio
async def test_full_planning_workflow(
    planner_agent,
    mock_personas,
    mock_insights,
    mock_concepts
):
    """Test complete planning workflow"""
    
    # Step 1: Create initial plan
    plan = await planner_agent.create_campaign_plan(
        company_id="test-company",
        objective="conversion",
        budget=60000,
        start_date=datetime(2025, 2, 1),
        end_date=datetime(2025, 5, 31)
    )
    
    campaign_id = plan['campaign_id']
    assert campaign_id is not None
    
    # Step 2: Simulate performance data
    performance_data = {
        "personas": {
            "p1": {"spent": 8000, "conversions": 120, "cpl": 66.67},
            "p2": {"spent": 7000, "conversions": 55, "cpl": 127.27},
            "p3": {"spent": 5000, "conversions": 35, "cpl": 142.86}
        }
    }
    
    # Step 3: Request budget reallocation
    optimization = await planner_agent.optimize_campaign_plan(
        campaign_id=campaign_id,
        performance_data=performance_data,
        optimization_type="budget_reallocation"
    )
    
    # Assert reallocation makes sense
    assert optimization['type'] == 'budget_reallocation'
    
    # Best performing persona should get more budget
    old_p1 = optimization['current']['persona_allocations']['p1']
    new_p1 = optimization['recommended']['persona_allocations']['p1']
    
    old_p1_total = old_p1['test_budget'] + old_p1['scale_budget']
    new_p1_total = new_p1['test_budget'] + new_p1['scale_budget']
    
    assert new_p1_total > old_p1_total
```

---

## Quick Start Guide

### 1. Set Up Database

```bash
# Run migration
psql -d scalefox -f migrations/009_planner_agent_tables.sql
```

### 2. Install Dependencies

```python
# requirements.txt
numpy>=1.24.0
pandas>=2.0.0
scipy>=1.11.0  # For statistical calculations
```

### 3. Initialize Agent

```python
from agents.planner_agent import PlannerAgent

# Initialize
planner = PlannerAgent(db_connection, llm_client)

# Create first plan
plan = await planner.create_campaign_plan(
    company_id="your-company-id",
    objective="conversion",
    budget=50000,
    start_date=datetime(2025, 2, 1),
    end_date=datetime(2025, 4, 30)
)

print(f"Created plan: {plan['campaign_id']}")
```

### 4. Test Conversational Interface

```python
response = await planner.process_message(
    user_message="Help me plan my Q1 campaign",
    context={
        "company_id": "your-company-id",
        "user_id": "your-user-id"
    }
)

print(response['message'])
```

---

## Success Metrics

### Planning Quality
- **Plan Completeness**: 100% of plans have all required sections
- **Budget Balance**: Total allocations = total budget (within $0.01)
- **Timeline Feasibility**: 95%+ of plans have achievable timelines
- **User Satisfaction**: 80%+ approval rate for initial plans

### Optimization Impact
- **Reallocation Lift**: Average 15-30% improvement in efficiency
- **Timeline Accuracy**: 90%+ milestone hit rate
- **Testing Validity**: 85%+ tests reach statistical significance

### User Engagement
- **Plan Adoption**: 75%+ of generated plans are implemented
- **Iteration Rate**: Average 1.5 iterations before finalization
- **Time to Plan**: < 5 minutes from start to approved plan

---

## Common Patterns & Best Practices

### Budget Allocation
✅ **DO:** Always reserve 5-15% for optimization
✅ **DO:** Test with equal budgets, scale with performance-based allocation
✅ **DO:** Consider persona-specific benchmarks

❌ **DON'T:** Allocate 100% of budget upfront
❌ **DON'T:** Test with unequal budgets (creates bias)
❌ **DON'T:** Ignore audience fatigue risk when scaling

### Testing Strategy
✅ **DO:** Test one variable at a time when possible
✅ **DO:** Calculate required sample sizes before starting
✅ **DO:** Plan for inconclusive results (have backup tests ready)

❌ **DON'T:** Run tests without clear hypotheses
❌ **DON'T:** End tests early due to impatience
❌ **DON'T:** Test too many variants simultaneously (dilutes learnings)

### Timeline Management
✅ **DO:** Build in buffer time (10-15% of timeline)
✅ **DO:** Define clear decision gates between phases
✅ **DO:** Plan for creative refresh cycles

❌ **DON'T:** Create unrealistic timelines to please stakeholders
❌ **DON'T:** Schedule launches on Fridays or holidays
❌ **DON'T:** Ignore external events (industry conferences, holidays)

---

## Future Enhancements

### Phase 1 (Current)
- [x] Basic campaign structure generation
- [x] Budget allocation algorithm
- [x] Testing framework creation
- [x] Timeline optimization

### Phase 2 (Next Quarter)
- [ ] Machine learning for budget optimization
- [ ] Predictive performance modeling
- [ ] Automated bid strategy recommendations
- [ ] Cross-channel campaign planning

### Phase 3 (Future)
- [ ] Real-time plan adjustments based on performance
- [ ] Competitive response planning
- [ ] Multi-campaign portfolio optimization
- [ ] AI-generated testing hypotheses

---

## Troubleshooting

### Issue: Plans are too aggressive
**Symptom:** Users report timelines or budgets are unrealistic
**Solution:** Review phase duration calculations, add more conservative buffers

### Issue: Budget doesn't balance
**Symptom:** Total allocations ≠ total budget
**Solution:** Check rounding in budget allocator, ensure reserve is calculated correctly

### Issue: Testing plans require too much budget
**Symptom:** Sample size requirements exceed available budget
**Solution:** Implement sequential testing approach instead of parallel

---

*The Planner Agent transforms strategy into actionable plans, ensuring every campaign launches with a clear roadmap to success.*
