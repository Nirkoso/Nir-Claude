# 2. Campaign Structure & Budget Allocation

## Core Principle: Simplicity Wins in 2025

**The #1 mistake advertisers make:** Over-complicating campaign structure.

Meta's AI (GEM + Andromeda) learns fastest with simple, consolidated structures. Every additional campaign, ad set, or targeting layer slows learning and reduces performance.

**Golden Rule:** Start with 1-2 campaigns maximum. Only add complexity when spending $10k+/week AND you have proven winners.

---

## Campaign Structure Framework (By Budget)

### Budget Tier 1: $1,000-$3,000/month

**Recommended Structure:**

```
Campaign 1: Prospecting (TOFU)
├── Budget: $35-70/day (70% of total)
├── Objective: Leads or Conversions
├── Optimization: Leads or Purchases
├── Advantage+ Audience: ON
├── Advantage+ Placements: ON
├── Advantage+ Creative: ON
├── CBO (Campaign Budget Optimization): ON
└── Ad Set 1: Broad Prospecting
    ├── Audience: 1% Lookalike (customers) + Advantage+ expansion
    ├── Age: 25-65
    ├── Location: Your target countries
    ├── Optional light layering: Job titles or company size
    └── 10-20 different ads (genuinely different concepts)

Campaign 2: Retargeting (BOFU)  
├── Budget: $15-30/day (30% of total)
├── Objective: Leads or Conversions
├── Optimization: Same as Campaign 1
├── CBO: ON
└── Ad Set 1: Website Warm Audiences
    ├── Audience: 180-day website visitors, 50%+ video viewers, form abandons
    ├── Exclude: Customers, current leads in pipeline
    └── 5-10 ads (stronger offer, urgency, social proof)
```

**Why this works:**
- Gives algorithm enough budget to exit learning phase quickly
- Simple structure = clear signals for AI
- Retargeting capitalizes on existing awareness
- Can manage easily even without team

### Budget Tier 2: $3,000-$6,000/month

**Recommended Structure:**

```
Campaign 1: Cold Prospecting
├── Budget: $70-140/day (70%)
├── Ad Set 1: LAL 1% (Customers) - Advantage+ ON
├── Ad Set 2: LAL 1% (High-Value Actions) - Advantage+ ON
└── 20-30 different ads

Campaign 2: Warm Retargeting
├── Budget: $30-60/day (25%)
└── Ad Set 1: 180-day engagers + visitors
    └── 10-15 ads (conversion-focused)

Campaign 3: Advantage+ Sales/Leads (Test)
├── Budget: $10-15/day (5%) - Testing allocation
├── Fully automated (all Advantage+ features ON)
└── 30-50 different ads
```

**Why add third campaign:**
- Budget sufficient to test Advantage+ fully automated approach
- Can compare performance vs. manual campaigns
- More creative diversity without overloading single campaign

### Budget Tier 3: $6,000-$10,000/month

**Recommended Structure:**

```
Campaign 1: Advantage+ Sales/Leads (Primary)
├── Budget: $120-200/day (60%)
├── All automation ON
├── 50-100 different ads
└── Multiple ad sets for segmentation (optional)

Campaign 2: Manual Prospecting (Control)
├── Budget: $50-100/day (25%)
└── Test specific audiences or offers AI might miss

Campaign 3: Retargeting
├── Budget: $30-60/day (15%)
└── High-intent audiences with strong offers
```

**Why shift to Advantage+:**
- At this budget, algorithm has enough data to fully optimize
- Advantage+ handles complexity better than manual at scale
- Frees time to focus on creative production

### Budget Tier 4: $10,000+/month

**Recommended Structure:**

```
Campaign 1: Advantage+ Primary (50-60%)
Campaign 2: Testing & Innovation (20-30%)  
Campaign 3: Retargeting & Upsell (15-20%)
Campaign 4: Seasonal/Promotional (As needed)
```

**At this level:**
- Work with agency or dedicated team
- Creative production becomes full-time operation
- Can test aggressive budget scaling rules
- Consider separate campaigns per product/service if catalog is diverse

---

## Campaign Objectives (What to Choose)

### For Lead Generation (B2B SaaS, Services, Local Business)

**Primary Objective: Leads**

**Optimization Event:**
- Start: `Lead` (form submission)
- After 50+ leads/week: `QualifiedLead` (from offline conversions)
- Advanced: Optimize for `SQL` or `Opportunity` if data volume sufficient

**Ad Destinations:**
- **Instant Forms (Recommended):** 20-40% lower CPL than website forms
- **Messenger:** Good for high-touch services
- **Website:** Use if form experience is superior or need custom qualification

**Best Practices:**
- Use "Higher Intent" form type once you have volume
- Add 1-2 qualifying questions maximum
- Enable lead verification (SMS or work email)
- Sync instantly to CRM
- Upload offline conversions weekly

### For eCommerce

**Primary Objective: Sales** (formerly Shopping)

**Optimization Event:**
- If <50 purchases/week: Start with `AddToCart` or `InitiateCheckout`
- Once stable volume: Switch to `Purchase`
- Advanced: Use Value optimization (maximize order value)

**Campaign Type:**
- **Advantage+ Sales Campaigns (ASC):** Should be 60-80% of budget
- **Manual campaigns:** For testing, specific products, or geographic tests

**Best Practices:**
- Provide product catalog feed
- Use dynamic ads for retargeting
- Test Value optimization vs. Conversions
- Upload Purchase events with correct revenue values

### For SaaS (Free Trial / Freemium)

**Primary Objective: Conversions**

**Optimization Event:**
- Trial signups: `StartTrial` or `CompleteRegistration`
- After conversion data matures: Optimize for activation events
- Upload: Qualified users, paid conversions, expansion

**Creative Strategy:**
- Focus on problem/solution in product context
- Use product demos, testimonials, ROI calculators
- Test free trial vs. free forever messaging

### For B2B (Demo/Sales Focused)

**Primary Objective: Leads**

**Optimization Event:**
- Start: `Lead` (demo request form)
- Advanced: `Schedule` (confirmed booking) or `DemoCompleted`

**Qualification Strategy:**
- Ask company size in form
- Ask current tool/situation
- Ask budget range (optional but helps quality)
- Use work email verification

---

## Budget Allocation Rules

### Daily Budget Minimums

**Per Ad Set:**
- Minimum: $50/day
- Ideal: $100+/day for B2B
- Never go below $40/day or algorithm gets confused

**Why these minimums?**
- Algorithm needs ~50 conversions/week per ad set to optimize
- At $50 CPL (B2B average), need $350/week = $50/day minimum
- Below this threshold, you'll stay in "Learning Limited" forever

### Budget Split: Prospecting vs. Retargeting

**Standard Split:**
- Prospecting (Cold): 65-75%
- Retargeting (Warm): 25-35%

**Why?**
- Prospecting feeds the retargeting funnel
- Can't scale retargeting without prospecting volume
- Retargeting more efficient but limited audience size

**Exception:** Very early stage (first 2-4 weeks)
- Can shift to 50/50 to build initial retargeting pool faster
- Once pool reaches 5,000+, shift back to 70/30

### Budget Pacing

**Use Campaign Budget Optimization (CBO):**
- Meta automatically distributes budget to best-performing ad sets
- Responds to real-time performance shifts
- Prevents manual budget adjustments that reset learning

**Avoid:**
- ❌ Daily manual budget changes
- ❌ Changing budget after 7 PM (algorithm paces for full day)
- ❌ 50%+ budget increases in single day
- ❌ Moving budget between campaigns frequently

---

## Campaign Settings Checklist

### Required Settings for Optimal Performance

**Campaign Level:**
- ✅ Objective: Leads, Conversions, or Sales
- ✅ Campaign Budget Optimization: ON
- ✅ Advantage+ campaign budget: ON (if available)
- ✅ Campaign Spending Limit: Set if needed for safety
- ❌ Split testing at campaign level: OFF (do manual testing instead)

**Ad Set Level:**
- ✅ Optimization Event: Lead, Purchase, or custom conversion
- ✅ Bid Strategy: Highest Volume (most common) or Cost Cap (if target CPL known)
- ✅ Advantage+ Audience: ON
- ✅ Advantage+ Placements: ON
- ✅ Age: Broad (25-65) unless specific reason to narrow
- ✅ Gender: All unless specific reason to narrow
- ✅ Locations: Your target markets
- ✅ Languages: Leave blank (Meta auto-optimizes)
- ❌ Detailed Targeting: Minimal (just lookalikes + suggestions)
- ❌ Manual placement selection: OFF

**Ad Level:**
- ✅ Advantage+ Creative: ON (test with and without)
- ✅ Multiple formats: Video, Carousel, Static (provide variety)
- ✅ Different concepts: 10-20+ meaningfully different ads
- ✅ Primary text variations: 2-3 per ad
- ✅ Headlines: 2-3 variations per ad
- ❌ Minor tweaks only: This doesn't work; need real variation

---

## Learning Phase Strategy

### Understanding Learning Phase

**What it is:** Period when Meta's algorithm gathers data to optimize delivery.

**Duration:**
- Minimum: 50 conversion events
- Timeline: Typically 3-7 days with proper budget
- Can extend to 2-3 weeks with small budgets

**Status indicators:**
- "Learning" = Currently gathering data (normal)
- "Learning Limited" = Not enough conversion volume (bad)
- "Active" = Learning complete, stable delivery

### Exiting Learning Phase Faster

**Method 1: Consolidate**
- Fewer ad sets = more events per ad set = faster learning
- Example: Instead of 5 ad sets with 10 conversions each, use 1 ad set with 50 conversions

**Method 2: Optimize for Easier Event**
- If optimizing for "Purchase" but only 3 purchases/week, temporarily switch to "AddToCart"
- Once volume stable, switch to Purchase
- Warning: This can impact final quality

**Method 3: Increase Budget**
- More spend = more events = faster learning
- But don't increase >25% in single day

**Method 4: Broaden Audience**
- Narrow audiences exhaust quickly
- Broad audiences have more inventory for algorithm to explore

### Actions That Reset Learning

**Avoid these during learning phase:**
- Changing optimization event
- Changing audience definition significantly
- Adding/removing placements
- Changing bid strategy
- Budget changes >20%
- Pausing campaign for >3 days

**Safe actions during learning:**
- Adding new ads (doesn't reset)
- Pausing individual underperforming ads
- Minor budget increases (10-15%)
- Changing ad creative content

---

## Bid Strategies Explained

### Highest Volume (Recommended Default)

**What it does:** Gets maximum results at any cost.

**When to use:**
- Default for most advertisers
- When cost per result is acceptable
- When scaling and volume is priority
- During testing phase

**Pros:**
- Simplest strategy
- Usually delivers most conversions
- Good for learning phase

**Cons:**
- Costs can spike if conversion rate drops
- Less predictable CPL/CPA

### Cost Cap

**What it does:** Aims to keep average cost per result at or below your cap.

**When to use:**
- You know your target CPL/CPA precisely
- You need predictable costs
- Scaling campaigns with proven unit economics

**How to set:**
- Start at 120% of current CPL/CPA
- Gradually lower by 10-15% every 5-7 days
- Stop when volume drops significantly

**Pros:**
- Protects against cost spikes
- More predictable budget utilization
- Good for scaling

**Cons:**
- Can limit delivery volume
- May miss peak performance opportunities
- Requires monitoring

### Bid Cap (Advanced - Rarely Recommended)

**What it does:** Never bids above your specified amount per impression/action.

**When to use:**
- Advanced users only
- Very specific efficiency targets
- Tight profit margins

**Pros:**
- Maximum cost control
- Predictable CPMs

**Cons:**
- Very limited delivery
- High expertise required
- Easy to set too low and get zero delivery

### Cost Per Result Goal (Budget Restricted)

**What it does:** Like Cost Cap but considers overall budget pacing.

**When to use:**
- Need predictable cost per result
- Want to spend full daily budget
- Similar to Cost Cap with extra safety

---

## Advanced Campaign Structures

### When to Use Multiple Campaigns

**Scenario 1: Different Products/Services**
- If products have very different audiences or economics
- Example: Budget tool ($10/mo) vs. Enterprise software ($50k/year)
- Separate campaigns allow different optimization goals and creative

**Scenario 2: Different Geos**
- If economics vastly different by country
- Example: US (high LTV) vs. India (low LTV)
- Can bid differently and optimize separately

**Scenario 3: Testing Innovation**
- Always allocate 10-20% budget to testing new approaches
- Keep winners separate from testing campaigns
- Example: 80% Advantage+ proven, 20% testing manual with new angles

**Scenario 4: Seasonal/Promotional**
- Time-limited offers
- Keep separate so can shut off without disrupting evergreen campaigns

### Campaign Naming Convention

**Use clear, consistent names:**

**Format:** `[Type]-[Audience]-[Objective]-[Date/Version]`

**Examples:**
- `PROS-LAL1%-Leads-Dec2025`
- `RETARG-180dVisitors-Demos-v2`
- `ADV+-Cold-Purchase-Dec2025`
- `TEST-JobTitle-Leads-Week1`

**Benefits:**
- Easy to understand at a glance
- Can sort alphabetically
- Simplifies reporting
- Helps team collaboration

---

## Scaling Rules (Critical - Don't Break These)

### When to Scale

**Requirements (ALL must be true):**
- ✅ 7+ days of stable performance
- ✅ CPL/CPA within target range
- ✅ Lead quality acceptable (SQL rate ≥15%)
- ✅ "Learning Limited" status cleared
- ✅ No major changes planned

**Don't scale if:**
- ❌ Performance fluctuating day-to-day
- ❌ Just made major change (wait 7 days)
- ❌ Frequency >3.0
- ❌ CTR declining
- ❌ Quality declining (even if quantity good)

### How to Scale (Safe Methods)

**Method 1: Gradual Budget Increases (Safest)**

| Current Budget | Increase By | Wait Period |
|----------------|-------------|-------------|
| $50-100/day | +15-20% | 4-5 days |
| $100-300/day | +20-25% | 4-5 days |
| $300-500/day | +25-30% | 3-4 days |
| $500+/day | +30-40% | 3-4 days |

**Example:**
- Day 1-5: $100/day, $50 CPL, stable
- Day 6: Increase to $120/day (+20%)
- Day 6-10: Monitor, stay at $120/day
- Day 11: Increase to $145/day (+20%)
- Continue pattern

**Method 2: Duplicate Campaign (Safer for Large Jumps)**

If need to scale quickly (50%+ increase):
1. Duplicate entire working campaign
2. Keep original running at current budget
3. New campaign starts at desired additional budget
4. Both campaigns compete; best one gets delivery
5. After 7 days, consolidate to winner

**Method 3: Add New Ad Sets (When Hitting Ceiling)**

If campaign can't scale further with budget increases:
1. Add new ad set with different audience segment
2. Give it proportional budget allocation
3. Same campaign objective and settings
4. Different creative variations

**Method 4: Expand Geographies**

If maxing out in current markets:
1. Add new country/region
2. Create separate ad set for new geo
3. Adjust budget proportionally to market size
4. May need geo-specific creative

### Scaling Red Flags (Stop Immediately)

**If you see these after scaling, revert budget:**
- CPL/CPA increases >30%
- CTR drops >25%
- Frequency jumps >3.0
- Quality score drops
- High volume but zero quality (SQL rate <5%)

### What NOT to Do When Scaling

**Common Scaling Mistakes:**
- ❌ Doubling budget overnight (50%+ increase)
- ❌ Scaling when frequency already high
- ❌ Adding budget to learning limited campaigns
- ❌ Scaling based on 1-2 good days
- ❌ Changing creative at same time as budget increase
- ❌ Scaling without monitoring quality
- ❌ Setting budget too high and not spending it all (confuses algorithm)

---

## Special Campaign Types

### Advantage+ Sales Campaigns (ASC) - Formerly Advantage+ Shopping

**What it is:** Fully automated campaign type where Meta controls targeting, placements, and creative optimization.

**Best for:**
- eCommerce with product catalog
- B2B SaaS with 30+ ads
- Budgets $3,000+/month
- Advertisers comfortable giving up control

**Setup:**
```
1. Create campaign → Choose "Sales" objective
2. Turn ON all Advantage+ toggles:
   - Advantage+ audience
   - Advantage+ placements  
   - Advantage+ creative
   - Advantage+ campaign budget
3. Provide 50-100 diverse ads
4. Set budget
5. Launch and don't touch for 7-14 days
```

**Performance Expectations:**
- 10-30% better ROAS vs. manual (if done right)
- Requires high creative volume
- Takes 7-10 days to optimize
- Don't try to control; trust the AI

**Common ASC Mistakes:**
- Only providing 5-10 ads (need 50+)
- Trying to restrict placements/audiences
- Checking daily and panicking
- Not providing enough budget ($100+/day minimum)

### Advantage+ Leads Campaigns

**What it is:** Automated lead generation campaigns using instant forms.

**Best for:**
- B2B lead generation
- Service businesses
- Events/webinar promotion
- Budget $50+/day

**Setup:**
```
1. Create campaign → "Leads" objective
2. Enable Advantage+ audience
3. Use Instant Forms (not website forms)
4. Add 1-2 qualifying questions
5. Connect to CRM for instant sync
6. Enable lead verification
```

**Performance:**
- 10% lower cost per qualified lead vs. manual (Meta data)
- 20-40% lower CPL vs. website forms
- Better mobile experience
- Faster lead delivery

---

## Budget Planning by Business Type

### B2B SaaS ($8k+ ACV)

**Recommended Budget:** $3,000-10,000/month minimum

**Expected Performance:**
- CPL: $18-75
- SQL Rate: 15-30%
- CAC Payback: 4-8 months
- Campaigns: 2 (Prospecting + Retargeting)

**Budget Split:**
- 70% Prospecting
- 30% Retargeting

### B2B Services (Professional Services, Agencies)

**Recommended Budget:** $2,000-5,000/month

**Expected Performance:**
- CPL: $25-100
- SQL Rate: 10-25%
- CAC Payback: 3-6 months

**Strategy:**
- Heavy focus on social proof
- Case studies in creative
- Instant forms with qualification

### eCommerce (AOV $50-200)

**Recommended Budget:** $3,000-15,000/month

**Expected Performance:**
- ROAS: 3:1-8:1
- CPM: $8-15
- CTR: 1.5-3.0%

**Strategy:**
- 60% Advantage+ Sales Campaigns
- 25% Manual prospecting
- 15% Retargeting/upsell

### Local Services (Home Services, Medical, Legal)

**Recommended Budget:** $1,500-5,000/month

**Expected Performance:**
- CPL: $20-60
- Qualified Rate: 20-40%
- Geographic concentration critical

**Strategy:**
- Tight geographic targeting (10-30 mile radius)
- Mobile-first creative
- Click-to-call ads
- Local testimonials

---

## Common Campaign Structure Mistakes

**Mistake 1: Too Many Campaigns**
- ❌ 10+ campaigns for small budget
- ✅ Start with 1-2, add only when scaling >$10k/month

**Mistake 2: Too Many Ad Sets per Campaign**
- ❌ 8-10 ad sets each with $10/day
- ✅ 1-3 ad sets with $50-100+/day each

**Mistake 3: Micro-Budgets**
- ❌ $20/day per ad set
- ✅ Minimum $50/day, ideally $100+

**Mistake 4: Complex Targeting Layers**
- ❌ 15 interests + behaviors + demographics stacked
- ✅ Lookalike + Advantage+ audience expansion

**Mistake 5: Mixing Objectives**
- ❌ One campaign for Awareness, then Conversions, then Traffic
- ✅ Stick to conversion-focused objectives (Leads/Sales)

**Mistake 6: Constant Changes**
- ❌ Changing settings every day
- ✅ Make change, wait 7 days, evaluate, repeat

**Mistake 7: Not Using CBO**
- ❌ Manual ad set budgets you adjust daily
- ✅ Campaign Budget Optimization handles it automatically

---

## Next Steps

Once your campaign structure is defined:
→ Proceed to **3-audience-targeting.md** for audience strategy
→ Reference **4-creative-strategy.md** for ad creation
→ Use **5-optimization-scaling.md** for ongoing management

**Remember:** Start simple. Add complexity only when proven necessary. The algorithm performs best with clear, consistent signals - not with clever manual overrides.
