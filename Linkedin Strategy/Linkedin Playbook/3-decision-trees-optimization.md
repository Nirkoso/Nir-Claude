# Decision Trees & Optimization Rules
**LinkedIn B2B Advertising - When-Then Logic for Scenarios**

Version 1.0 | December 2025

---

## When to Use This File

**Purpose:** Procedural decision-making for specific scenarios
**Use cases:**
- "Should I pause or adjust this campaign?"
- "When do I switch from automated to manual bidding?"
- "How do I know if I should scale?"
- Campaign troubleshooting and optimization triggers

---

## 1. Budget Allocation Decision Tree

```
START: What is the user's primary goal?

├─ Goal: "Generate leads / Book demos" (Conversion focus)
│  ├─ Budget ≥ $5,000/month
│  │  └─ RECOMMEND: 70% Conversion, 20% Awareness, 10% Remarketing
│  └─ Budget < $5,000/month
│     └─ RECOMMEND: 80% Conversion, 10% Remarketing, 10% Awareness
│
├─ Goal: "Build brand awareness" (Awareness focus)
│  ├─ Budget ≥ $10,000/month
│  │  └─ RECOMMEND: 50% Awareness, 30% Consideration, 20% Conversion
│  └─ Budget < $10,000/month
│     └─ RECOMMEND: 60% Awareness, 40% Consideration
│
├─ Goal: "Educate market / Nurture" (Consideration focus)
│  └─ RECOMMEND: 40% Consideration, 40% Conversion, 20% Remarketing
│
└─ Goal: "All of the above" (User unclear)
   └─ CLARIFY: "Which is most urgent for your business?"
   └─ DEFAULT if unclear: 70/20/10 model
```

---

## 2. Ad Format Selection Tree

```
START: What is the campaign objective?

├─ Objective: Awareness
│  ├─ Have video assets? → YES
│  │  └─ RECOMMEND: Video Ad (15-30 seconds)
│  └─ Have video assets? → NO
│     ├─ Have multiple images/stats? → YES
│     │  └─ RECOMMEND: Carousel Ad (3-5 cards)
│     └─ Have multiple images/stats? → NO
│        └─ RECOMMEND: Single Image Ad
│
├─ Objective: Consideration
│  ├─ Offering downloadable content? → YES
│  │  ├─ Long-form PDF? → YES
│  │  │  └─ RECOMMEND: Document Ad
│  │  └─ Guide/checklist? → YES
│  │     └─ RECOMMEND: Lead Gen Form OR Carousel
│  └─ Offering webinar/demo? → YES
│     └─ RECOMMEND: Video Ad OR Carousel
│
├─ Objective: Conversion
│  ├─ Have landing page with form? → YES
│  │  ├─ Form has ≤3 fields? → YES
│  │  │  └─ RECOMMEND: Single Image → Landing Page
│  │  └─ Form has >3 fields? → YES
│  │     └─ RECOMMEND: Lead Gen Form (lower friction)
│  └─ Have landing page? → NO
│     └─ RECOMMEND: Lead Gen Form OR create landing page first
│
└─ Objective: Remarketing
   ├─ Audience: Website visitors (warm)
   │  └─ RECOMMEND: Message Ad OR Lead Gen Form
   └─ Audience: Video viewers / Engagers
      └─ RECOMMEND: Lead Gen Form (high intent)
```

---

## 3. Bidding Strategy Decision Tree

```
START: Review campaign after 7 days

├─ CTR ≥ 0.40% (Good)
│  ├─ Budget utilization ≥ 90%
│  │  ├─ CPL ≤ target
│  │  │  └─ ACTION: Increase budget 30%, maintain bid
│  │  └─ CPL > target
│  │     └─ ACTION: Maintain budget, optimize creative
│  └─ Budget utilization < 80%
│     └─ ACTION: Increase bid 15-20%
│
├─ CTR 0.25-0.39% (Average)
│  ├─ Budget utilization ≥ 90%
│  │  └─ ACTION: Test new headlines, maintain bid
│  └─ Budget utilization < 80%
│     └─ ACTION: Increase bid 10-15%, test creative
│
└─ CTR < 0.25% (Below Average)
   ├─ Impressions < 2,000
   │  └─ ACTION: Wait until 5,000 impressions
   └─ Impressions ≥ 2,000
      ├─ Audience < 50K
      │  └─ ACTION: Broaden audience, enable Expansion 15%
      └─ Audience ≥ 50K
         └─ ACTION: Pause, create new creative
```

---

## 4. Targeting Expansion Decision Tree

```
START: Campaign performing well (CPL on target, quality >60%)

└─ Budget utilization ≥ 95% for 5+ days
   ├─ Frequency < 2.5
   │  └─ Can expand without losing focus
   │     ├─ Targeting specific job titles?
   │     │  └─ EXPAND: Add adjacent titles
   │     │     Example: VP → add Directors
   │     ├─ Targeting one seniority?
   │     │  └─ EXPAND: Add one level down
   │     │     Example: Directors → add Managers
   │     ├─ Targeting specific company size?
   │     │  └─ EXPAND: Add adjacent range
   │     │     Example: 51-200 → add 201-500
   │     └─ None applicable?
   │        └─ EXPAND: Enable/increase Audience Expansion
   │           10% → 20%
   └─ Frequency ≥ 2.5
      └─ EXPAND: Increase budget first (reaches more in existing audience)
      └─ THEN: If frequency climbs to 3.0+, broaden audience
```

---

## 5. Creative Refresh Decision Tree

```
START: Review CTR trend

├─ CTR declining >30% from peak over 4 weeks?
│  ├─ Frequency ≥ 4.0
│  │  └─ ACTION: Immediate refresh (new image + headline)
│  └─ Frequency < 4.0
│     └─ ACTION: Wait 1 week, check trends, then refresh
│
├─ CTR declining 15-29% over 4 weeks?
│  ├─ Frequency 3.0-4.0
│  │  └─ ACTION: Refresh in 1-2 weeks, start production now
│  └─ Frequency < 3.0
│     └─ ACTION: Monitor, not urgent
│
└─ CTR stable or improving?
   ├─ Campaign running ≥ 8 weeks (always-on)
   │  └─ ACTION: Proactive refresh (prevent decline)
   └─ Campaign running < 8 weeks
      └─ ACTION: Continue current creative
```

---

## 6. Pause/Adjust/Scale Matrix

### PAUSE Immediately If:

| Trigger | Threshold | Timeline | Reason |
|---------|-----------|----------|--------|
| CTR collapse | <0.15% for 5+ days, 5K+ impressions | Within 24 hours | Creative fundamentally broken |
| CPL explosion | >2x target for 7+ days | Within 48 hours | Economics don't work |
| Severe fatigue | Frequency >5.0 for 3+ days | Immediately | Audience saturated |
| Quality collapse | <30% qualified for 10+ leads | Within 24 hours | Wrong targeting |
| Zero conversions | $500+ spend, 100+ clicks | Immediately | Tracking or offer broken |
| Delivery failure | "Low Delivery" for 5+ days despite fixes | Pause & restructure | Audience too small |

**After pausing:** Diagnose root cause, fix, retest at 50% original budget.

### ADJUST (Bid/Budget/Creative) If:

| Trigger | Threshold | Adjustment | Expected Outcome |
|---------|-----------|------------|------------------|
| CTR declining | 20-30% decline, 2+ weeks | Refresh creative (2 variants) | CTR recovery in 5-7 days |
| CPL above target | 20-50% above target | Decrease bid 10% OR simplify LP | Within 10% target in 7-14 days |
| Underspending | <80% utilization, 5+ days | Increase bid 15-20% | 90%+ utilization in 3-5 days |
| Moderate fatigue | Frequency 3.0-5.0 | Add 2-3 variants OR expand 20-30% | Frequency <3.0 in 7 days |
| Quality declining | 40-60% qualified | Add qualify question OR tighten targeting | 60%+ quality in 10 leads |
| CTR plateauing | Stable 4+ weeks, no growth | Test new format/hook | New winner in 14 days |

### SCALE (Budget/Audience) If:

| Trigger | Threshold | Scaling Action | Velocity |
|---------|-----------|----------------|----------|
| High sustained CTR | >0.50% for 7+ days | Increase budget 30% + 2 variants | Weekly 30% until 0.40% |
| CPL under target | <target for 10+ days, 90%+ utilization | Increase budget 30%, bid 10% | Aggressive (50% weekly) |
| High quality | >60% qualified, 20+ leads | Expand audience 20-30%, budget 30% | Scale until 50% quality |
| Low frequency | <2.5, strong performance | Increase budget 30-50% | Weekly until frequency 3.0 |
| High utilization | >90% spent, good performance | Increase budget 30%, consider expansion | Scale until 80-85% |
| Strong funnel | CTR >0.50%, CVR >5%, quality >60% | Launch 2nd campaign (50% budget), adjacent audience | Gradual expansion |

**Scaling checkpoints:** After each 30% increase, pause 5-7 days and monitor. If CPL increases 20%+, revert.

---

## 7. Troubleshooting Guide

### Issue: High Impressions, Low CTR (<0.20%)

**Diagnosis Tree:**
```
Is audience relevant to offer?
├─ No → PROBLEM: Targeting mismatch
│  └─ FIX: Check Demographics tab, pause off-ICP segments
└─ Yes → Is creative compelling?
   ├─ No → PROBLEM: Weak value prop or visual
   │  └─ FIX: Test benefit headlines, add faces, social proof
   └─ Yes → Is ad message clear?
      └─ PROBLEM: Unclear CTA or value
         └─ FIX: Simplify headline, test specific CTAs
```

**Actions:**
1. Review Demographics tab (pause wrong seniority/industry)
2. Test 3 new headlines (benefit, problem, curiosity)
3. Update image (include faces +38% engagement)
4. Add social proof (logos, testimonial)

---

### Issue: High CTR, Low Conversions (<2%)

**Diagnosis Tree:**
```
Does ad match landing page?
├─ No → PROBLEM: Message disconnect
│  └─ FIX: Align ad headline with LP H1
└─ Yes → Is form too complex?
   ├─ Yes → PROBLEM: Friction
   │  └─ FIX: Reduce to 3-5 fields, test Lead Gen Form
   └─ No → Is page slow?
      └─ PROBLEM: Technical issue
         └─ FIX: Improve speed (<3 sec), check mobile
```

**Actions:**
1. Verify ad headline = landing page H1 exactly
2. Reduce form fields (3-5 max, each removal = 10% lift)
3. Test Lead Gen Form vs. landing page (forms 2-3x better)
4. Add trust signals (testimonials, logos, security badges)
5. Check page load speed (<3 seconds)

---

### Issue: Good Metrics, Poor Lead Quality (<40%)

**Diagnosis Tree:**
```
Is targeting too broad?
├─ Yes → PROBLEM: Wrong personas clicking
│  └─ FIX: Add seniority, narrow company size
└─ No → Is offer attracting wrong people?
   ├─ Yes → PROBLEM: Offer too generic
   │  └─ FIX: Update ad to call out specific ICP
   └─ No → Are we qualifying leads?
      └─ PROBLEM: No filter
         └─ FIX: Add qualifying questions to form
```

**Actions:**
1. Add seniority filter (VP/Director, exclude Entry-level)
2. Narrow company size to ICP (e.g., 10-500 only)
3. Add qualifying question: "What's your biggest challenge?"
4. Update ad: "Built for B2B SaaS CMOs at $5M+ companies"
5. Exclude job seekers (targeting option)

---

### Issue: "Low Delivery" Warning

**Diagnosis Tree:**
```
Is audience >50K?
├─ No → PROBLEM: Audience too small
│  └─ FIX: Remove 1 criterion, enable Expansion 15-20%
└─ Yes → Is bid competitive?
   ├─ No → PROBLEM: Bid too low
   │  └─ FIX: Increase 20%, check suggested range
   └─ Yes → Is budget adequate?
      └─ PROBLEM: Budget exhausted or too low
         └─ FIX: Raise daily budget 30-50%
```

**Actions:**
1. Check audience size (if <50K, remove targeting layer)
2. Enable Audience Expansion +10-20%
3. Increase bid to top of suggested range
4. Raise daily budget 30-50%
5. If persists, switch CPC → CPM bidding

---

### Issue: Creative Fatigue (CTR -30%+)

**Diagnosis Tree:**
```
Is frequency >3.5?
├─ Yes → PROBLEM: Audience saturation
│  └─ FIX: Immediate creative refresh + expand audience
└─ No → External factors?
   ├─ Possible → PROBLEM: Seasonality, competition
   │  └─ FIX: Research trends, test new angles
   └─ Unlikely → PROBLEM: Message stale
      └─ FIX: Rotate creative every 6-8 weeks
```

**Actions:**
1. Check frequency (if >3.5, immediate refresh)
2. Pause current creative 2 weeks (reset)
3. Create 2-3 variants (different visual + headline)
4. Test seasonal angles ("2025 trends," "Q2 update")
5. Expand audience 30-50% (reduce per-person impressions)

---

## 8. Weekly Optimization Workflow

### Day 1 (Monday) - Performance Review

**Tasks (30 min):**
1. Sort campaigns by CPL (low → high)
2. Identify top 20% performers (CPL <target, quality >50%)
3. Identify bottom 20% (CPL >target +50% OR quality <30%)
4. Flag anomalies (CPL swings >40% week-over-week)

**Decisions:**
- Top 20%: Plan to scale (increase budget 30% or expand audience)
- Bottom 20%: Diagnose issue (use troubleshooting guide above)
- Anomalies: Investigate (check for holidays, budget issues, audience saturation)

---

### Day 2 (Tuesday) - Creative Analysis

**Tasks (30 min):**
1. Review ads within each campaign
2. Calculate CTR variance: Best ad CTR ÷ Campaign average CTR
3. Identify fatigue: Any ad with -30% CTR from peak?

**Decisions:**
- Ads with CTR >1.3x campaign average: Scale (allocate more budget)
- Ads with CTR <0.5x campaign average: Pause (replace with new variant)
- Fatigued ads: Refresh immediately (new visual + headline combo)

---

### Day 3 (Wednesday) - Budget Reallocation

**Tasks (20 min):**
1. Calculate available budget: Reallocate from paused/reduced campaigns
2. Prioritize: Which campaigns get the new budget?

**Formula:**
```
Incremental Budget Priority Score = 
  (Target CPL - Actual CPL) × Lead Quality %

Example:
- Campaign A: ($100 - $75) × 60% = 15 points
- Campaign B: ($100 - $90) × 45% = 4.5 points
→ Prioritize Campaign A for budget increase
```

**Action:**
- Move budget from bottom 20% to top 20%
- Increase top performers 30% (don't exceed 50% increase in one week)

---

### Day 4 (Thursday) - Audience Insights

**Tasks (30 min):**
1. Check Demographics tab for top campaigns
2. Identify unexpected patterns:
   - Wrong seniority levels (Entry instead of VP)?
   - Geographic mismatch (Rural instead of Urban)?
   - Industry drift (Healthcare instead of SaaS)?

**Decisions:**
- Exclude underperforming demographics
- Create new campaign targeting high-performing demographics
- Adjust targeting criteria for next campaign iteration

---

### Day 5 (Friday) - A/B Test Review

**Tasks (20 min):**
1. Check tests launched 7-14+ days ago
2. Verify minimum data: 1,000+ impressions per variant, 10+ conversions
3. Declare winners if data sufficient

**Criteria:**
- Winner: >20% improvement in primary KPI (CTR, CVR, CPL)
- Marginal: 10-20% improvement → run another week
- Tie: <10% difference → use secondary metric as tiebreaker

**Actions:**
- Scale winning variant to 100% budget
- Pause losing variant
- Document in testing log

---

## 9. Monthly Deep Dive Workflow

### Week 1 - Funnel Analysis

**Calculate drop-offs:**
```
Impression → Click: CTR
Click → Landing Page: Load rate
Landing Page → Form Open: Engagement rate
Form Open → Submit: Completion rate
Submit → MQL: Qualification rate
MQL → Opportunity: Sales accept rate
Opportunity → Close: Win rate
```

**Identify weakest link:**
- If CTR is bottleneck: Creative issue (test new headlines)
- If Load rate is bottleneck: Technical issue (page speed, mobile)
- If Completion is bottleneck: Form friction (reduce fields)
- If Qualification is bottleneck: Targeting issue (wrong audience)

---

### Week 2 - Creative Fatigue Audit

**For each ad running 4+ weeks:**
1. Chart CTR week-over-week
2. Calculate decline: (Peak CTR - Current CTR) ÷ Peak CTR
3. Check frequency metric

**Actions:**
- Decline >20%: Plan refresh (start creative production)
- Decline >30%: Immediate refresh (pause within 3 days)
- Frequency >3.5: Expand audience OR refresh creative

---

### Week 3 - Competitive Benchmarking

**Compare to industry benchmarks:**
1. Your CTR vs. industry average (Benchmarks file, Section 1)
2. Your CPL vs. industry average
3. Your conversion rate vs. industry average

**Diagnosis:**
- All metrics below average: Fundamental issue (targeting, offer, creative)
- CTR below, CPL above average: Creative issue
- CTR above, conversion below: Landing page issue
- All metrics above average: Opportunity to scale aggressively

---

### Week 4 - Strategic Adjustments

**Review monthly performance:**
1. Calculate total leads, blended CPL, lead quality %
2. Compare to targets and prior month
3. Assess: On track to hit quarterly goals?

**Decisions:**
- Exceeding targets: Scale budget 50-100% next month
- Meeting targets: Maintain + 20-30% budget increase
- Missing targets: Diagnose (use troubleshooting guide), consider pivot
- Plan next month: Budget allocation, new campaigns, tests to run

---

## 10. Scaling Decision Framework

### When NOT to Scale

❌ **Don't scale if:**
- Campaign running <30 days (insufficient data)
- Lead quality declining (even if CPL looks good)
- Frequency >3.0 (audience saturation)
- CPL increasing week-over-week
- Budget utilization <90% (fix delivery first)

### How to Scale Safely

**Step 1: Validate Stability (Week 4)**
- CPL stable ±10% for 2+ weeks?
- Lead quality >50% for 20+ leads?
- CTR >0.40%?
→ If yes, proceed. If no, optimize first.

**Step 2: Choose Scaling Method**

**Option A: Budget Increase (Safest)**
- Week 5: +30% budget ($100 → $130/day)
- Week 6: +30% again ($130 → $170/day)
- Monitor CPL—if increases >15%, slow scaling

**Option B: Audience Expansion**
- Enable Audience Expansion 10% → 20%
- OR add adjacent targeting (Directors → Managers)
- OR create lookalike audience (source: converters)
- Run parallel for 2 weeks, compare CPL

**Option C: Duplicate Campaign**
- Clone top performer
- Target adjacent segment (different industry/company size)
- Allocate 50% of original budget
- Avoids disrupting proven campaign

**Step 3: Monitor Closely**
- Daily checks during scaling period
- If CPL increases >20%: Pause scaling, revert 50%
- If quality drops >10%: Tighten targeting
- If frequency >3.5: Expand audience further

---

## 11. Quarterly Planning Decision Tree

```
START: Review last 90 days

├─ Overall Performance
│  ├─ Exceeded targets (CPL <target, volume met)
│  │  └─ PLAN: Increase budget 50-100%, test new formats
│  ├─ Met targets (CPL on target, volume met)
│  │  └─ PLAN: Increase budget 20-30%, expand audience
│  ├─ Mixed results (Some campaigns good, some poor)
│  │  └─ PLAN: Reallocate (50% to proven, 30% optimize, 20% experiment)
│  └─ Missed targets (CPL high OR volume low)
│     └─ PLAN: Diagnose fundamentals, consider pivot
│
├─ Budget Allocation Next Quarter
│  ├─ If scaling (exceeded targets)
│  │  └─ 60% Proven, 25% Optimization, 15% Experimental
│  ├─ If maintaining (met targets)
│  │  └─ 50% Proven, 30% Optimization, 20% Experimental
│  └─ If rebuilding (missed targets)
│     └─ 30% Proven, 40% Optimization, 30% Experimental
│
└─ New Initiatives to Test
   ├─ New ad formats? (Document Ads, Thought Leader, Conversation)
   ├─ New audiences? (Adjacent industries, lookalikes)
   ├─ New offers? (Webinar vs. Guide vs. Trial)
   └─ New channels? (Coordinate LinkedIn with Google, email)
```

---

## Usage Notes

**When using these trees:**
1. Start at the top node
2. Answer each question honestly based on data
3. Follow the branch to recommendation
4. Execute recommendation
5. Monitor for expected outcome
6. Document results

**Common mistakes:**
- Skipping diagnostic steps (jumping to "fix")
- Not waiting for minimum data (1K impressions, 10 conversions)
- Changing multiple variables simultaneously (can't isolate cause)
- Ignoring frequency metric (key saturation indicator)

**Remember:**
- These are frameworks, not absolute rules
- Always validate with your specific data
- Document exceptions and learnings
- Update trees when new patterns emerge

---

**End of Decision Trees & Optimization Rules**

For strategic context → See Core Strategy Framework
For benchmarks → See Benchmarks & Specifications
For agent workflows → See Agent Execution Playbook
