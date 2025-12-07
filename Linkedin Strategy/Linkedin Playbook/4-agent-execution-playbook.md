# Agent Execution Playbook
**LinkedIn B2B Advertising - AI Agent Templates & Workflows**

Version 1.0 | December 2025

---

## When to Use This File

**Purpose:** Standardized templates and workflows for AI agents creating LinkedIn strategies
**Use cases:**
- Gathering user requirements
- Structuring strategy deliverables
- Quality assurance before delivery
- Avoiding common agent mistakes

---

## 1. Standard Input Template

### Copy and send to user for completion:

```markdown
=== LINKEDIN CAMPAIGN STRATEGY REQUEST ===

COMPANY CONTEXT:
- Company Name: [fill]
- Industry/Vertical: [fill]
- Target Audience (who they sell to): [fill]
- Company Stage: [Startup / Growth / Enterprise]
- Unique Value Proposition: [fill]
- Key Differentiators: [fill]

CAMPAIGN PARAMETERS:
- Primary Objective: [Awareness / Consideration / Conversion]
- Total Budget: $[amount]
- Monthly Budget: $[amount]
- Campaign Duration: [weeks/months]
- Current Assets:
  □ Website, blog content
  □ Case studies, testimonials
  □ Product demos, videos
  □ Lead magnets (guides, templates)
  □ Email lists, CRM contacts
  □ LinkedIn Company Page (followers: ___)

GOALS & CONSTRAINTS:
- Target CPL: $[amount] (or "no target")
- Desired leads/month: [number]
- Average deal size: $[amount]
- Sales cycle: [days/weeks]
- Geographic focus: [countries/regions]
- Must-have requirements: [list]
- Known limitations: [list]

ADDITIONAL CONTEXT:
- Previous LinkedIn experience: [Yes/No + details]
- What's worked in other channels: [fill]
- What hasn't worked: [fill]
```

### Pre-delivery quality check:

Before proceeding, verify:
- [ ] Objective is singular (not "awareness AND conversion")
- [ ] Budget ≥ $1K for test campaigns
- [ ] Target audience is specific (not just "businesses")
- [ ] At least one existing asset available
- [ ] Success metrics defined (even if approximate)

---

## 2. Standard Output Template

### Use this structure for all strategy deliverables:

```markdown
=== LINKEDIN CAMPAIGN STRATEGY ===
Generated: [Date]
For: [Company Name]

---

## EXECUTIVE SUMMARY

[2-3 sentence overview]

Expected Results:
- Timeline to first results: [X weeks]
- Estimated monthly leads: [range]
- Estimated CPL: $[range]
- Campaign structure: [X campaigns, Y ads]

---

## CAMPAIGN STRATEGY

### Campaign 1: [Name]

**Objective:** [Awareness / Consideration / Conversion]
**Budget:** $[amount]/month ([%] of total)
**Duration:** [weeks]

**Targeting:**
- Primary: [Job Function / Titles]
  - Criteria: [specific list]
- Secondary: [Company Size / Industry]
  - Criteria: [specific list]
- Audience Size: [50K-500K range]
- Expansion: [10% / 15% / 20%] enabled

**Ad Format:** [Single Image / Carousel / Video / Lead Gen Form]
**Why:** [1-2 sentence rationale based on objective]

**Bidding:**
- Strategy: [Automated / Manual CPC / Manual CPM]
- Suggested Range: $[X]-$[Y] (if manual)

**Expected Benchmarks:**
- CTR Target: [%]
- CPL Target: $[amount]
- Conversion Rate: [%]

[Repeat for additional campaigns]

---

## CREATIVE SPECIFICATIONS

### Campaign 1: [Name]

**Headlines** (3 variants for testing):
1. [Headline 1 - benefit-focused]
2. [Headline 2 - problem-focused]
3. [Headline 3 - curiosity-driven]

**Primary Copy:**
[150-200 characters for single image, 250-300 for other formats]

**Visual Direction:**
- Format: [dimensions + file specs]
- Key Elements: [what to show]
- Example: [reference if available]

**CTA:** "[Button text]" → [destination]

[Repeat for each campaign]

---

## OPTIMIZATION PLAN

### Week 1: Warm-Up & Monitoring
**Daily (15 min):**
- Budget pacing (80-100% spend?)
- CPL monitoring (expect $200-500 Week 1)
- "Low Delivery" warnings
- Pause CTR <0.10% after 1K impressions

**Week 1 Goal:** 5-10 leads for baseline

### Week 2: First Optimization
**Mid-Week Review (60 min):**
- Compare headline variants (>30% CTR diff? Pause loser)
- Check lead quality (CRM feedback)
- Adjust bids if underspending or CPL >$250

**Iteration Triggers:**
- CTR <0.20%: Test new headlines
- CTR good, CPL high: Check landing page
- Both good, leads unqualified: Tighten targeting

### Week 3-4: Scale or Pivot
**Decision Point (Day 21):**
- IF CPL <$150 AND quality >50%
  → SCALE: +30% budget, test lookalike
- IF CPL $150-250 AND quality >40%
  → OPTIMIZE: Refine creative, test CTAs
- IF CPL >$250 OR quality <30%
  → PIVOT: Revisit targeting/offer

### Success Criteria (30 Days)
Campaign successful if:
- [ ] CPL ≤ $[target]
- [ ] Lead quality ≥ 40%
- [ ] Volume ≥ [minimum]
- [ ] CTR ≥ 0.30%

---

## NEXT STEPS & REQUIREMENTS

**Before Launch:**
1. [ ] Install Insight Tag
2. [ ] Set up conversion tracking
3. [ ] Create landing page / Lead Gen Form
4. [ ] Prepare creative assets
5. [ ] Define qualification criteria with sales

**Timeline:**
- Setup: [X] days
- Creative: [Y] days
- Launch: [Date]
- First review: [Date] (Day 7)
- Scale/pivot decision: [Date] (Day 21)

**Resources Needed:**
[List tools, approvals, budget confirmations]

---

## FRAMEWORK REFERENCES

Grounded in:
- Budget: Section 4 [70/20/10 model / scaling framework]
- Targeting: Section 5 [2-3 criteria rule / 50K-500K sweet spot]
- Creative: Section 6 [format selection matrix]
- Optimization: Section 8 [pause/adjust/scale triggers]
- Benchmarks: Section 9 [industry-specific KPIs]

---
```

### After delivering strategy, offer to create:
1. Detailed ad copy (all 3 headline variants + full text)
2. Landing page outline
3. Email nurture sequence (if applicable)
4. Weekly optimization checklist (campaign-specific)

---

## 3. Quality Assurance Checklist

### Before delivering ANY strategy, verify:

**Completeness:**
- [ ] All output sections filled (no "TBD" placeholders)
- [ ] Budget allocations sum to 100%
- [ ] Audience sizes within 50K-500K range
- [ ] Creative specs match recommended format
- [ ] Optimization triggers are specific (numbers, not vague)
- [ ] Success criteria measurable and time-bound

**Framework Alignment:**
- [ ] Budget references Core Strategy (70/20/10 or variant)
- [ ] Targeting follows 2-3 criteria rule
- [ ] Ad format aligns with objective matrix
- [ ] Bidding matches decision tree
- [ ] Benchmarks from Benchmarks file

**Actionability:**
- [ ] User can implement without additional strategy decisions
- [ ] Next steps concrete (not "create ads" but specific dimensions/elements)
- [ ] Timeline realistic (accounts for creative production)
- [ ] Contingencies address user constraints

**No Contradictions:**
- [ ] Creative doesn't contradict targeting (enterprise messaging for SMB)
- [ ] Budget fits user's stated budget
- [ ] Timeline accounts for warm-up (Week 1 expectations managed)
- [ ] Benchmarks appropriate for industry

**Clarity:**
- [ ] Technical terms defined in context
- [ ] Acronyms spelled out first use
- [ ] Minimal jargon (write for marketer, not specialist)
- [ ] Formatting makes strategy scannable

---

## 4. Common Agent Mistakes to Avoid

### ❌ Mistake 1: Generic Recommendations
**Bad:** "Create engaging content and target your audience"

**Good:** "Create 3 single image ads (1200x627px) with benefit-focused headlines. Target Marketing function, Director+ seniority, 51-500 employees (est. 180K audience size)."

---

### ❌ Mistake 2: Ignoring User Constraints
**Bad:** User says "$2K budget" → Agent recommends 4 campaigns at $1K each = $4K

**Good:** User says "$2K budget" → Agent recommends 2 campaigns: $1,400 core offer, $400 remarketing, $200 reserve

---

### ❌ Mistake 3: Omitting the "Why"
**Bad:** "Use Lead Gen Forms"

**Good:** "Use Lead Gen Forms because your offer requires 5 form fields, and Lead Gen Forms auto-fill from LinkedIn profiles, reducing friction and improving conversion 2-3x vs. landing pages."

---

### ❌ Mistake 4: Unrealistic Timelines
**Bad:** "Launch tomorrow"

**Good:** "Timeline: 2 days (Insight Tag + creative brief) → 3 days (designer creates variants) → 1 day (approval) → Launch Day 7 → First review Day 14"

---

### ❌ Mistake 5: Forgetting Warm-Up Expectations
**Bad:** "You should see $80 CPL from Day 1"

**Good:** "Week 1: Expect $200-400 CPL (algorithm learning). Week 2: CPL drops to $120-180. Week 3-4: Target $80-120 blended. This is normal LinkedIn optimization."

---

### ❌ Mistake 6: Not Referencing Frameworks
**Bad:** Just providing recommendations without grounding

**Good:** "This budget allocation follows the 70/20/10 model (Core Strategy Framework, Section 4), proven effective by focusing 70% on direct conversion."

---

### ❌ Mistake 7: Analysis Paralysis
**Bad:** Recommending 10 different audiences to test simultaneously

**Good:** "Start with this single audience. After 2 weeks, if CPL <$120, test this expansion. If CPL >$180, pivot to this alternative."

---

## 5. Strategy Creation Workflow

### Step 1: Gather Requirements (10 min)
1. Send input template to user
2. Set 24-48 hour deadline for completion
3. While waiting, review their industry in Benchmarks file

### Step 2: Validate Inputs (5 min)
1. Check completeness (all fields filled?)
2. Verify clarity (can you explain their audience to someone else?)
3. Confirm realism (budget adequate for objective?)
4. Ask clarifying questions if needed (don't assume)

### Step 3: Map to Strategic Framework (15 min)
1. Identify primary objective → determines campaign type
2. Calculate budget allocation (70/20/10 or variant)
3. Select targeting approach (2-3 criteria, 50K-500K)
4. Choose ad formats (objective matrix from Core Strategy)
5. Set expected benchmarks (industry-specific from Benchmarks file)

### Step 4: Structure Campaign(s) (20 min)
1. Define campaign hierarchy (1-3 campaigns typically)
2. For each campaign:
   - Objective (singular)
   - Budget allocation
   - Targeting (specific criteria)
   - Ad format + rationale
   - Bidding approach
   - Expected benchmarks
3. Verify total allocation = 100% of budget

### Step 5: Draft Creative Direction (15 min)
1. Write 3 headline variants (benefit, problem, curiosity)
2. Draft primary copy (format-specific length)
3. Describe visual direction (what to show/avoid)
4. Specify CTA (specific, not generic)
5. Reference format specs from Benchmarks file

### Step 6: Build Optimization Plan (10 min)
1. Week-by-week milestones (Weeks 1, 2, 3-4)
2. Daily/weekly monitoring tasks
3. Specific triggers for pause/adjust/scale
4. Success criteria (measurable, time-bound)
5. Reference Decision Trees file for triggers

### Step 7: Quality Assurance (10 min)
1. Run through QA checklist (Section 3 above)
2. Verify all frameworks referenced correctly
3. Check for contradictions or unrealistic expectations
4. Ensure actionability (user can implement)

### Step 8: Deliver + Follow-Up (5 min)
1. Send strategy in standard output format
2. Offer optional deliverables (ad copy, landing page outline)
3. Set expectation for when they should expect first review
4. Document key decisions in internal log

**Total time: ~90 minutes for standard strategy**

---

## 6. Ad Copy Generation Template

When user requests detailed ad copy:

```markdown
### CAMPAIGN: [Name]
### FORMAT: [Single Image / Carousel / Video]

---

## VARIANT 1: Benefit-Focused

**Headline:** [Specific outcome, 25-50 chars]
Example: "3.2x Pipeline Growth in 90 Days"

**Description:** [How you achieve it, 70-100 chars]
Example: "B2B service providers: Get the 8-phase system that books 20-40 qualified calls/month."

**Primary Text (if applicable):**
[Expand on benefit, include social proof, 150-200 chars]

**Visual Direction:**
[What image should show]

**CTA Button:** "[Specific action]"

---

## VARIANT 2: Problem-Focused

**Headline:** [Call out pain point, 25-50 chars]
Example: "Struggling with Inconsistent Client Flow?"

**Description:** [Tease solution, 70-100 chars]
Example: "This proven system helped [Client] triple their pipeline in 90 days. Download the framework."

**Primary Text:**
[Agitate problem, introduce solution]

**Visual Direction:**
[What to show - before/after, problem illustration]

**CTA Button:** "[Action that solves]"

---

## VARIANT 3: Curiosity-Driven

**Headline:** [Intrigue without revealing, 25-50 chars]
Example: "The System Top B2B Firms Use to Book 40 Calls/Month"

**Description:** [What they'll discover, 70-100 chars]
Example: "See the exact 3-phase framework that generated $2.4M in pipeline for [Industry] companies."

**Primary Text:**
[Build curiosity, hint at inside knowledge]

**Visual Direction:**
[What to show - partial reveal, framework preview]

**CTA Button:** "[Discovery action]"

---

## TESTING APPROACH

**Launch all 3 variants simultaneously**
Let LinkedIn auto-rotate (best performers get more impressions)

**After 7 days / 1,000 impressions per variant:**
- Compare CTR (should have clear winner by 20%+ difference)
- Check CPL (sometimes lower CTR variant has better CPL)
- Declare winner, pause bottom performer

**Scale winner:**
- Increase budget allocation to winning variant
- Create 2 new variants based on winning approach
- Continue testing cycle
```

---

## 7. Landing Page Outline Template

When user requests landing page structure:

```markdown
### LANDING PAGE OUTLINE
### PURPOSE: [Lead magnet opt-in / Demo request / Trial signup]

---

## ABOVE THE FOLD

**Headline (H1):**
"Access the [Lead Magnet Name] (Free)"

**Subheadline (H2):**
[Reinforce value + urgency, 1 sentence]
Example: "The exact system we use to generate 300+ qualified leads per quarter—yours free in 2 minutes."

**Hero Visual:**
[Preview of resource - PDF cover, video thumbnail, tool screenshot]

**CTA Button (Primary):**
"[Access Now / Get Instant Access / Download Free Guide]"

---

## VALUE PROPOSITION SECTION

**What You'll Learn:**

✓ [Specific takeaway 1 - actionable]
Example: "Discover the 3V Rule that boosts lead magnet opt-ins to 50%+"

✓ [Specific takeaway 2 - framework/template]
Example: "Copy the exact 10-email pre-call sequence"

✓ [Specific takeaway 3 - tools/resources]
Example: "Access 5 plug-and-play LinkedIn post templates"

✓ [Specific takeaway 4-5]

---

## SOCIAL PROOF

**Testimonial:**
"[Quote about results]"
— [Name, Title, Company]

**OR Usage Stat:**
"Trusted by 1,200+ B2B marketers"

**OR Client Logos:**
[3-5 recognizable company logos]

---

## FORM SECTION

**Form Fields (Minimum Friction):**
- First Name
- Email Address
- [Company Name if needed for qualification]

**Privacy Note:**
"We respect your inbox. Unsubscribe anytime."

**CTA Button (Repeat):**
"[Same as above]"

---

## OPTIONAL: BELOW THE FOLD

**About the Author/Company:**
[1-2 sentences establishing authority]

**FAQ (if applicable):**
- Q: [Common objection]
  A: [Address directly]

---

## TECHNICAL REQUIREMENTS

- Mobile-responsive (70% traffic from mobile)
- Load time <3 seconds
- Form auto-focus on page load
- Thank-you redirect to: [Offer page with VSL]

---

## CONVERSION OPTIMIZATION NOTES

**Target opt-in rate:** 35-60%

**If below 30%:**
- Simplify headline (clearer benefit)
- Reduce form fields (each = 10% drop)
- Add social proof (testimonial or logos)
- Test Lead Gen Form vs. landing page

**If above 60%:**
- Excellent! Scale traffic to this page.
```

---

## 8. Weekly Optimization Checklist Template

Customize for each campaign:

```markdown
### WEEKLY OPTIMIZATION CHECKLIST
### CAMPAIGN: [Name]
### WEEK: [Number]

---

## MONDAY: Performance Review (30 min)

**Compare to Targets:**
- [ ] CPL: $[actual] vs. $[target] ([% variance])
- [ ] CTR: [%] vs. 0.35% minimum
- [ ] Lead volume: [#] vs. [target #]
- [ ] Lead quality: [%] vs. 40% minimum

**Campaign Health:**
- [ ] Budget utilization: [%] (target 80-95%)
- [ ] Frequency: [number] (target <3.5)
- [ ] Delivery status: [Normal / Low / Limited]

**Action Items:**
- [ ] [Specific action based on data]
- [ ] [Specific action based on data]

---

## TUESDAY: Creative Analysis (20 min)

**Ad Performance:**

Ad 1 - [Name]:
- CTR: [%]
- CPL: $[amount]
- Status: [Keep / Test / Pause]

Ad 2 - [Name]:
- CTR: [%]
- CPL: $[amount]
- Status: [Keep / Test / Pause]

Ad 3 - [Name]:
- CTR: [%]
- CPL: $[amount]
- Status: [Keep / Test / Pause]

**Decisions:**
- [ ] Pause ads with CTR <[0.20%]
- [ ] Scale ads with CTR >[campaign avg × 1.3]
- [ ] Refresh if top performer CTR declined >[20%]

---

## WEDNESDAY: Budget Reallocation (15 min)

**Current Allocation:**
- Campaign A: $[amount]/day
- Campaign B: $[amount]/day
- Campaign C: $[amount]/day

**Proposed Changes:**
- [ ] [Increase/Decrease] Campaign [X] by $[amount]
  Reason: [CPL/Quality/Volume]

**Total Reallocation:** $[amount]

---

## THURSDAY: Audience Insights (20 min)

**Demographics Check:**
- [ ] Top-performing job title: [title]
- [ ] Top-performing company size: [range]
- [ ] Top-performing geography: [location]

**Unexpected Patterns:**
- [ ] [Note any surprising demographics]
- [ ] [Note any off-ICP segments clicking]

**Actions:**
- [ ] Exclude: [specific demographics]
- [ ] Test new campaign targeting: [specific criteria]

---

## FRIDAY: Testing & Planning (30 min)

**Active A/B Tests:**

Test 1: [Variable being tested]
- Control: [metric]
- Variant: [metric]
- Status: [Ongoing / Winner declared]
- Action: [Continue / Scale winner / Launch new test]

**Next Week Plan:**
- [ ] [New creative to test]
- [ ] [Audience expansion to try]
- [ ] [Budget adjustment planned]

---

## NOTES / OBSERVATIONS

[Free-form space for insights, questions, concerns]

---
```

---

## 9. Agent Self-Improvement Protocol

After delivering strategies, log learnings:

### In `/Linkedin Strategy/progress-log.md`:

```markdown
Date: [YYYY-MM-DD]
Agent: [your name]
Company/Industry: [if known]
Task: [Brief description]

Frameworks Used:
- Core Strategy: [specific sections]
- Benchmarks: [which tables]
- Decision Trees: [which trees]

Novel Scenarios:
[Any situations not covered by existing frameworks]

Deviations:
[Times you couldn't follow standard frameworks and why]

Questions Encountered:
[Ambiguities or gaps in documentation]

User Feedback (if available):
[What user said about strategy quality]
```

### Monthly Review (First Monday):
1. Review all progress-log.md entries
2. Identify patterns (3+ agents mention same issue)
3. Propose documentation updates

---

## 10. Quick Reference Decision Trees

### "Which file should I reference?"

```
User asks about...

├─ Budget allocation or strategic approach
│  └─ Core Strategy Framework
│
├─ "What's a good CPL for my industry?"
│  └─ Benchmarks & Specifications
│
├─ "Should I pause this campaign?"
│  └─ Decision Trees & Optimization Rules
│
├─ How to format my strategy output
│  └─ Agent Execution Playbook (this file)
│
└─ Technical setup (Insight Tag, CRM)
   └─ Technical Setup & Tools
```

### "How much detail should I provide?"

```
User sophistication level:

├─ Novice (first LinkedIn campaign)
│  └─ High detail: Explain every term, include examples
│
├─ Intermediate (ran campaigns before)
│  └─ Moderate detail: Focus on strategy, less on basics
│
└─ Expert (LinkedIn Ads specialist)
   └─ Low detail: Just recommendations, skip explanations
```

### "Should I create full ad copy or just guidelines?"

```
User request includes...

├─ "Create the ads for me"
│  └─ Full copy (3 variants, all fields, CTAs)
│
├─ "Give me ad direction"
│  └─ Guidelines (headline themes, visual direction, CTA approach)
│
└─ Unclear
   └─ Ask: "Would you like full ad copy, or just creative direction?"
```

---

## Usage Notes

**This playbook is for agents, not end users:**
- Use technical language (agents understand frameworks)
- Prioritize consistency over creativity
- Reference source files by name
- Document deviations for future improvement

**When uncertain:**
- Default to Core Strategy Framework for strategic questions
- Default to Benchmarks for metrics questions
- Default to Decision Trees for if-then scenarios
- Ask clarifying questions rather than assume

**Quality over speed:**
- Better to take 90 minutes and deliver excellent strategy
- Than to rush and deliver generic/incomplete strategy
- User will trust future recommendations more if first is high-quality

---

**End of Agent Execution Playbook**

For strategic frameworks → See Core Strategy Framework
For benchmarks → See Benchmarks & Specifications
For optimization logic → See Decision Trees & Optimization Rules
For technical implementation → See Technical Setup & Tools
