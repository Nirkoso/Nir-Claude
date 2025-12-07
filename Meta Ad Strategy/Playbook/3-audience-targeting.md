# 3. Audience Targeting Strategy (2025 Edition)

## Core Truth: Creative is the New Targeting

**The paradigm shift of 2025:**

In 2024 and earlier, success came from finding the perfect audience with detailed targeting.

In 2025, Meta's AI (Andromeda + GEM) finds the right people based on **who responds to your creative**, not based on demographics you specify.

**What this means:**
- Broad targeting + strong creative > Narrow targeting + okay creative
- The algorithm learns from creative-audience fit, not manual inputs
- Your job: Make diverse creative that appeals to different personas
- Algorithm's job: Match each creative to the right person

---

## Advantage+ Audience (The Default Setting)

### What It Is

Advantage+ Audience is Meta's AI-powered audience expansion that:
- Starts with your suggestions (lookalikes, interests, demographics)
- Expands 30-80% beyond your inputs
- Continuously tests new audience segments
- Automatically optimizes toward best performers

**Critical: This is now the DEFAULT and RECOMMENDED setting for all campaigns.**

### How It Works

**Traditional (Pre-2025):**
```
You: "Show ads to women, 35-50, interested in yoga and wellness"
Meta: "Okay, only showing to that exact group"
Result: Limited reach, misses good prospects outside definition
```

**Advantage+ Audience (2025):**
```
You: "Here are suggestions: women, 35-50, yoga/wellness interested"
Meta: "Got it, starting there but also testing: 
  - Men with similar behaviors
  - Age 25-34 who engage with wellness content
  - Users who visited similar websites
  - Users whose friends fit your description"
Result: Finds hidden high-intent users you wouldn't have targeted
```

### Setup

**In Ad Set Settings:**
```
1. Audience Controls → Advantage+ Audience → ON (default)
2. Add "Suggestions" (not requirements):
   - 1-3% Lookalike audiences
   - Broad interest categories (max 3-5)
   - Optional: Job titles, company sizes
3. Set exclusions:
   - Current customers
   - Bad-fit industries/demographics
4. Geographic location: Required (only hard restriction)
```

**What to include as "suggestions":**
- ✅ Lookalike audiences (your best customers)
- ✅ Broad interests (3-5 max)
- ✅ Life events (if relevant)
- ✅ Company size ranges (B2B)
- ❌ Don't stack 15+ detailed interests
- ❌ Don't create very narrow combinations

---

## Lookalike Audiences (Still Critical)

### What They Are

Lookalikes (LALs) find people similar to your best customers based on thousands of data points Meta tracks.

**Power:** A 1% LAL of 1,000 customers can reach 2-3 million similar people in the US.

### How to Create High-Performance Lookalikes

**Step 1: Upload Source Audience**

**Best sources (in order of quality):**
1. **Customers** (paid, closed-won deals) - Best
2. **High-value actions** (demos completed, trials activated)
3. **Qualified leads** (SQLs, opportunities)
4. **Website visitors** (180-day, visited key pages)
5. **Engaged users** (video 75%+ viewers, post engagers)

**Source size requirements:**
- Minimum: 100 people (Meta allows)
- Good: 1,000+ people
- Ideal: 5,000-10,000+ people
- Diminishing returns: >50,000 people

**How to upload:**
```
1. Audiences → Create Audience → Custom Audience
2. Choose source:
   - Customer list (upload CSV with email/phone)
   - Website traffic (requires Pixel)
   - App activity
   - Engagement (Meta assets)
3. Upload data:
   - Email (best)
   - Phone (good)
   - Both (ideal)
4. Name clearly: "Customers-Paid-2024-2025"
5. Save
```

**CSV format for customer list:**
```csv
email,phone,fn,ln,ct,st,zip,country
john@example.com,15555551234,john,doe,austin,tx,78701,us
jane@example.com,15555555678,jane,smith,boston,ma,02101,us
```

**Step 2: Create Lookalike**

```
1. Audiences → Create Audience → Lookalike Audience
2. Select source (your custom audience)
3. Choose location(s):
   - US: Can create for entire US
   - Multiple countries: Create separate LAL per country
4. Select audience size:
   - 1%: Most similar (best performance 90% of time)
   - 2%: Slightly broader
   - 3-5%: Much broader (test after 1% works)
   - 6-10%: Usually performs worse
5. Create 1%, 2%, 3% simultaneously
6. Test all three, but 1% usually wins
```

### Lookalike Strategy by Business Type

**B2B SaaS:**
- Source: Closed customers + MQLs/SQLs
- Size: 1% (start), 2% (scale)
- Update: Monthly with new customers
- Layer: Job titles (optional), company size

**eCommerce:**
- Source: Purchasers (last 180 days)
- Advanced: Create value-based LAL (highest spending customers)
- Size: 1% for cold, 2-3% for scaling
- Update: Every 2-4 weeks

**Local Services:**
- Source: Converted customers (booked/paid)
- Location: 30-50 mile radius from business
- Size: 1% only (local audience)
- Layer: Geographic + radius

**Lead Gen:**
- Source: Qualified leads (not all form fills)
- Size: 1-2%
- Critical: Upload offline conversion data (quality signal)

---

## Audience Layering (Light Touch Only)

**2025 Rule:** Add 1-2 layers maximum. More than that restricts learning.

### Acceptable Layers

**Geographic (Always set):**
- Country targeting (required)
- State/province (if multi-state business)
- Radius targeting (local businesses only)
- DMA targeting (regional services)

**Age (Sometimes useful):**
- Default: 25-65 (broad)
- Narrow only if product truly age-specific
- Example: Medicare plans (65+), College app (18-24)

**Gender (Rarely useful):**
- Default: All genders
- Narrow only if product is gender-exclusive
- Warning: Misses household purchaser patterns

**Job Titles (B2B only, light touch):**
- Maximum 30-50 titles
- Focus on decision-makers + influencers
- Don't be too narrow ("CMO" also catches "VP Marketing")
- Use "job title" interest category, not detailed targeting

**Company Size (B2B only):**
- Use if economics vary significantly by company size
- Typical segments:
  - Small: 11-50 employees
  - Mid: 51-200 employees
  - Large: 201-500 employees
- Test separately, don't combine

**Behaviors (Use sparingly):**
- B2B tech: "Uses Salesforce", "Uses HubSpot"
- eCommerce: "Engaged shoppers", "Online purchasers"
- Travel: "Frequent travelers"
- Warning: Many behaviors deprecated in 2025

### What NOT to Layer

**Avoid these targeting methods:**
- ❌ Stacking 10+ detailed interests
- ❌ Ultra-narrow demographic combinations
- ❌ Excluding broad categories (wastes potential)
- ❌ Psychographic layering (removed by Meta)
- ❌ Trying to recreate LinkedIn-style targeting

---

## Custom Audiences (Retargeting)

### Website Visitors

**Standard segments:**

**All Website Visitors (180 days)**
- Use for: Broad retargeting
- Minimum audience: 1,000+ people
- Creative: Brand recall + offer

**Specific page visitors:**
- Pricing page viewers (high intent)
- Product/feature page visitors
- Blog readers (educational content for TOFU)
- Form starters (didn't complete)

**High-intent visitors:**
- Multiple page visits (3+ pages)
- Time on site (2+ minutes)
- Visited key pages (pricing + product + demo request)

**Setup example:**
```
1. Audiences → Custom Audience → Website Traffic
2. Choose event: ViewContent, PageView, etc.
3. Set timeframe: 30, 60, 90, 180 days
4. Retention: Balance freshness vs. size
   - 30 days: Very high intent, small audience
   - 180 days: Broader, includes older traffic
5. Add URL filters (optional):
   - URL contains "/pricing"
   - URL contains "/product"
6. Save with clear name
```

### Engagement Audiences

**Video viewers:**
- 25% (aware)
- 50% (interested)
- 75% (highly engaged) - Best for retargeting
- 95% (completed)

**Instagram/Facebook engagers:**
- Profile visitors
- Post engagers (likes, comments, shares)
- CTA clickers
- DM senders

**Lead form openers:**
- Opened form but didn't submit
- High-intent, warm audience

**Setup:**
```
1. Audiences → Custom Audience → Engagement
2. Choose source:
   - Video
   - Lead form
   - Instagram/Facebook Page
3. Set engagement type and timeframe
4. Video: Choose 50% or 75% watched
5. Timeframe: 90-180 days (smaller than website audiences)
```

### Customer Lists

**Why use:**
- Exclude from prospecting (prevent waste)
- Create lookalikes (find similar people)
- Upload value data (high LTV vs. low LTV)

**What to upload:**
- Emails (hash automatically)
- Phone numbers (hash automatically)
- Names + location (lower match rate)

**Upload frequency:**
- Weekly: For active businesses
- Monthly: For smaller volume
- After major milestones: New product launch, seasonal campaign

**Advanced: Value-based audiences**
- Segment customers by LTV
- Create LAL from high-LTV customers
- Exclude low-LTV patterns

---

## Exclusions Strategy

### Who to Exclude

**Always exclude:**
- ✅ Current customers (paying/active)
- ✅ Current pipeline (open opportunities)
- ✅ Recent leads (last 7-30 days)
- ✅ Employees (your company domain)

**Sometimes exclude:**
- ✅ Unqualified leads (if volume warrants)
- ✅ Specific industries (B2B)
- ✅ Wrong company sizes
- ✅ Countries with bad ROI

**Don't exclude:**
- ❌ Broad demographic categories
- ❌ Past website visitors (can revisit later)
- ❌ Competitive interest categories

### How to Set Up Exclusions

```
1. Ad Set → Audience → Exclusions
2. Add Custom Audience(s):
   - Current customers list
   - CRM sync audience
3. Add demographics (if critical):
   - Exclude age <21 for alcohol
   - Exclude certain locations
4. Don't over-exclude:
   - Each exclusion reduces audience size
   - Smaller audience = higher CPMs
```

---

## Audience Size Guidelines

### Optimal Audience Sizes

**Minimum viable:**
- Cold prospecting: 500,000+ (US)
- Retargeting: 1,000+ (can be smaller)
- Lookalikes: 1-5 million+ (ideal)

**Meta's "Audience Size" indicator:**
- 🔴 Red (Too specific): <100,000 - Increase
- 🟡 Yellow (Fairly Specific): 100K-1M - Okay for retargeting
- 🟢 Green (Broad): 1M-50M+ - Ideal for prospecting

**By campaign type:**
- **Prospecting:** 2-10 million (US) - Broad is good
- **Retargeting:** 1,000-100,000 - Size depends on traffic volume
- **Advantage+:** 10+ million - Algorithm needs room to explore

### If Audience Too Small

**Solutions:**
1. **Remove layers:**
   - Drop from 5 interests to 1-2
   - Widen age range
   - Remove demographic restrictions

2. **Expand geographically:**
   - Add adjacent states
   - Add similar countries (US + Canada + UK)

3. **Use broader lookalikes:**
   - 2-3% instead of 1%
   - Multiple source combinations

4. **Let Advantage+ expand:**
   - Turn ON Advantage+ Audience
   - Algorithm will find users beyond your definition

---

## Testing Framework

### What to Test

**Priority 1: Lookalike sources**
- Test 1% LAL of customers vs. 1% LAL of high-value actions
- Create 2 ad sets, identical except source
- Run for 7-14 days
- Winner becomes primary, loser is paused

**Priority 2: Lookalike percentages**
- Test 1% vs. 2% vs. 3%
- Usually 1% wins, but not always
- Separate ad sets for each

**Priority 3: Interest suggestions**
- Broad interests vs. very broad (no interests)
- Example: Ad Set A with "Marketing" interest, Ad Set B with Advantage+ only
- See if algorithm finds better audience without suggestions

**Priority 4: Geographic splits**
- Different countries may have vastly different CPLs
- Create separate ad sets if performance warrants

### How to Test

**Use ABO (Ad Set Budget Optimization) for testing:**
```
1. Create campaign
2. Turn OFF CBO temporarily
3. Create 2-3 ad sets (testing variants)
4. Give each equal budget ($50/day each)
5. Same ads in all ad sets (isolate audience variable)
6. Run 7-14 days
7. Evaluate winner
8. Scale winner, pause losers
```

**After finding winner:**
- Switch back to CBO
- Let algorithm optimize budget across ad sets
- Or consolidate to single winner ad set

---

## Advantage+ Audience Best Practices

### What to Provide as "Suggestions"

**Ideal combination:**
```
Ad Set Setup:
├── Advantage+ Audience: ON
├── Suggestions:
│   ├── Lookalike 1%: Customers (Primary)
│   ├── Broad interest: Industry category (1-2 max)
│   └── Optional: Job title or company size
├── Age: 25-65 (broad)
├── Gender: All
├── Location: US (or target markets)
└── Exclusions: Current customers only
```

**This setup allows algorithm to:**
- Start with high-quality seed (LAL)
- Have broad room to explore (Advantage+ expansion)
- Not waste budget on existing customers (exclusion)

### Common Mistakes

**Mistake 1: Restricting too much**
- ❌ 10 interests + age 35-44 + income $100k+ + job titles
- ✅ 1% LAL + Advantage+ expansion + age 25-65

**Mistake 2: No seed data**
- ❌ Just Advantage+ with no suggestions
- ✅ At minimum provide 1% LAL or broad interest

**Mistake 3: Too many exclusions**
- ❌ Excluding 15 competitor interests, multiple demographics
- ✅ Exclude customers, maybe 1-2 truly bad fits

**Mistake 4: Not trusting expansion**
- ❌ Checking daily: "Why are men seeing this? I targeted women!"
- ✅ Let run 7+ days, judge by performance not assumptions

---

## Special Audience Strategies

### Cold Start (New Account, No Data)

**Week 1-2:**
- Use broad interest targeting (1-2 relevant categories)
- Age 25-65, all genders
- Focus on building pixel data
- 20-30 diverse creatives

**Week 3-4:**
- Create lookalike from website visitors (if 100+ visitors)
- Or continue broad with Advantage+ expansion

**Week 5+:**
- Create LAL from leads/customers once 100+ events
- This becomes your primary audience

### Scaling Past Audience Limits

**If audience exhausted (frequency >3.0):**

**Option 1: Expand geographically**
- Add new countries with similar demographics
- US → Canada, UK, Australia
- Create separate ad sets for localization

**Option 2: Broaden lookalike**
- Move from 1% to 2-3%
- Accepts lower quality for more volume

**Option 3: Add new seed audiences**
- Create LAL from different source
- Example: Added LAL from blog readers + LAL from demo requests

**Option 4: Test completely new audiences**
- Different interest categories
- Different creative angles that appeal to new personas

### Multi-Product Strategy

**If selling very different products:**

**Don't:** Single campaign with all products mixed
**Do:** Separate campaigns per product line (if economics differ)

**Example - SaaS company:**
```
Campaign 1: Budget Tool (SMB, $50/mo)
├── Audience: Small business owners, 1-50 employees
└── Creative: Price-focused, simple onboarding

Campaign 2: Enterprise Platform ($50k/year)
├── Audience: Director+ titles, 500+ employees
└── Creative: ROI, integration, security
```

---

## B2B Targeting Strategies

### The B2B Challenge

Meta doesn't have LinkedIn's professional targeting granularity. But B2B still works by:
1. Using broad targeting + creative-based qualification
2. Leveraging lookalikes from customers
3. Form-based qualification
4. Offline conversion signals for quality

### B2B Targeting Layers (Use Sparingly)

**Job Title Targeting:**
- Use "Job Title" interest category (not detailed targeting)
- Max 30-50 titles
- Focus on decision-makers + influencers
- Example target list for Marketing SaaS:
  - CMO, VP Marketing, Director Marketing
  - Marketing Manager, Digital Marketing Manager
  - CEO (small companies), Founder
  - Growth Lead, Demand Gen Manager

**Company Size:**
- Small: 11-50
- Medium: 51-200
- Large: 201-500
- Enterprise: 500+
- Test separately; economics often vary significantly

**Industry Interests:**
- Broader than you think
- "B2B", "Small Business", "Entrepreneurship"
- Industry specific: "SaaS", "Technology", "Healthcare"
- Don't stack 5+ industries

**Behaviors:**
- "Uses Salesforce"
- "Uses HubSpot"
- "Small business owners"
- Limited options remain in 2025

### B2B Best Practice

**Primary strategy:**
1. Upload customer list → Create 1% LAL
2. Add Advantage+ Audience expansion
3. Light layer: Job titles OR company size (not both)
4. Let creative qualify (problem/solution messaging)
5. Form qualification (company size, current tool, budget)
6. Upload offline conversions (qualified leads)

**This approach:**
- Reaches decision-makers in buying mode
- Lets algorithm find patterns beyond job titles
- Qualifies via form, not targeting
- Teaches algorithm what "quality" means

---

## Seasonal & Event-Based Audiences

### Retargeting for Events/Webinars

**Strategy:**
```
Week -4: TOFU awareness (broad targeting)
Week -2: MOFU (retarget engaged users)
Week -1: BOFU (retarget + urgency)
Day of: Last-minute reminders (high-intent retargeting only)
```

**Audience sequence:**
1. Broad prospecting → Build awareness
2. Video 50%+ viewers → Education/value proposition
3. Landing page visitors → Registration push
4. Registered users → Reminder campaign

### Holiday/Seasonal Audiences

**Preparation (4-6 weeks before):**
- Build retargeting pools early
- Broader targeting to capture volume

**Peak period:**
- Heavy retargeting focus
- Tighter ad sets (recent visitors only)
- Urgency messaging

**Post-period:**
- Retarget non-converters with discount
- Exclude recent purchasers
- Shift back to evergreen

---

## Audience Troubleshooting

**Problem: Audience too small (<100K)**
→ Remove layers, broaden age range, add countries, use 2-3% LAL

**Problem: High CPMs (>$30)**
→ Audience too narrow or competitive, broaden targeting

**Problem: Low-quality leads**
→ Add form qualification, tighten creative messaging, upload offline conversions

**Problem: Audience exhausted (frequency >3.0)**
→ Expand geographically, add new LAL sources, refresh creative, increase budget

**Problem: Learning Limited**
→ Consolidate ad sets, increase budget to $50+/day, broaden audience

**Problem: Algorithm serving to wrong people**
→ Check creative messaging (it's targeting), add exclusions if truly wrong fit, upload quality signals via offline conversions

---

## Next Steps

Once your audience strategy is defined:
→ Proceed to **4-creative-strategy.md** for ad creation
→ Reference **5-optimization-scaling.md** for ongoing optimization
→ Use **7-troubleshooting.md** if issues arise

**Remember:** In 2025, your creative does more targeting than your audience settings. Focus on making diverse, high-quality creative that appeals to different personas. The algorithm will find the right people for each ad.
