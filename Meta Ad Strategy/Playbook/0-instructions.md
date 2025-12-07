# Meta Ads Playbook - Instructions for LLM Agents

## Overview

This playbook is a comprehensive guide for running Meta (Facebook & Instagram) advertising campaigns in December 2025. It is specifically designed for LLM agents to reference when helping users plan, launch, optimize, or troubleshoot Meta advertising campaigns.

## How to Use This Playbook

### Structure

The playbook is organized into 8 interconnected documents:

1. **1-account-setup.md** - Technical foundation (Pixel, CAPI, Business Manager)
2. **2-campaign-structure.md** - Campaign architecture and budget allocation
3. **3-audience-targeting.md** - Audience strategy and Advantage+ features
4. **4-creative-strategy.md** - Creative formats, production, and testing
5. **5-optimization-scaling.md** - Performance monitoring and scaling protocols
6. **6-benchmarks-metrics.md** - Industry benchmarks and KPIs
7. **7-troubleshooting.md** - Common problems and solutions
8. **8-technical-context.md** - Understanding Meta's AI (GEM & Andromeda)

### When to Reference Each Document

**For new advertisers or account setup:**
- Start with **1-account-setup.md** → then **2-campaign-structure.md**
- Reference **3-audience-targeting.md** and **4-creative-strategy.md** in parallel

**For existing campaigns needing optimization:**
- Start with **6-benchmarks-metrics.md** to establish baseline performance
- Use **5-optimization-scaling.md** for improvement strategies
- Reference **7-troubleshooting.md** if specific issues arise

**For strategic planning or budget allocation:**
- Begin with **2-campaign-structure.md** 
- Cross-reference **6-benchmarks-metrics.md** for realistic expectations
- Use **3-audience-targeting.md** and **4-creative-strategy.md** for execution

**For understanding "why" behind recommendations:**
- Read **8-technical-context.md** to understand GEM and Andromeda
- This provides the foundation for all strategic decisions

### Key Principles (Read This First)

**As of December 2025, Meta advertising is fundamentally different from 2024 and earlier:**

1. **AI is the Media Buyer** - Meta's GEM (ranking) + Andromeda (retrieval) systems are more sophisticated than manual optimization. Your job is to feed the AI quality inputs, not to outsmart it.

2. **Creative is the New Targeting** - With Advantage+ and broad audiences, the creative itself signals to the algorithm who should see the ad. Minor headline tweaks don't work; you need meaningfully different concepts.

3. **Simplicity Wins** - Complex campaign structures, excessive ad sets, and narrow targeting confuse the algorithm. 1-3 campaigns with broad targeting outperform 10+ campaigns with detailed targeting.

4. **Data Volume Matters** - The algorithm needs 50+ conversions/week per ad set to optimize effectively. Splitting budget across too many ad sets creates "Learning Limited" status.

5. **Refresh Cadence is Critical** - Even winning ads fatigue. Plan for creative refresh every 10-14 days. The algorithm rewards fresh, diverse creative.

### Critical Context: What Changed in 2025

**Andromeda Update (October 2025)**
- New retrieval engine processes millions of ads per impression
- 10,000× larger models enable nuanced intent understanding
- Creative variety became the #1 performance driver
- Accounts using 50-100+ diverse creatives saw 15-40% better performance

**GEM Model (Launched early 2025, detailed November 2025)**
- LLM-like architecture for ad recommendations
- Processes thousands of user events across months
- Cross-platform learning (Instagram ↔ Facebook)
- Delivered +5% Instagram conversions, +3% Facebook Feed conversions in Q2 2025

**Advantage+ Expansion (February 2025)**
- Now covers Sales, Leads, and App campaigns (not just Shopping)
- Automatic application of AI optimizations
- Early tests show 10% lower cost per qualified lead

**Key Policy Changes**
- Conversions API (CAPI) is now effectively mandatory for optimal performance
- AI chat interactions (Meta AI) will personalize ads starting December 16, 2025
- Opportunity Score feature expanded to all advertisers

### How to Provide Recommendations

**When helping users, always:**

1. **Start with their current state:**
   - Budget size
   - Business type (B2B SaaS, eCommerce, Lead Gen, etc.)
   - Current performance (if applicable)
   - Technical setup status

2. **Set realistic expectations using benchmarks:**
   - Reference **6-benchmarks-metrics.md** for their industry/vertical
   - Explain that results vary significantly by offer quality, creative, and market

3. **Prioritize high-impact actions:**
   - Proper tracking setup (if new)
   - Simplified campaign structure (if complex)
   - Creative volume and diversity (if stagnant)
   - Budget allocation and scaling rules (if growing)

4. **Provide specific, actionable steps:**
   - Don't say "optimize your creative" - give specific format recommendations
   - Don't say "improve tracking" - list exact events to track and tools to use
   - Don't say "test audiences" - provide specific audience configurations

5. **Explain the "why" briefly:**
   - Users want to understand, but keep technical explanations concise
   - Reference the playbook sections for deeper details
   - Focus on practical outcomes over technical architecture

### Common User Questions and Which Documents to Reference

| User Question | Primary Document | Supporting Documents |
|--------------|------------------|---------------------|
| "How much should I spend?" | 2-campaign-structure.md | 6-benchmarks-metrics.md |
| "What CPL should I expect?" | 6-benchmarks-metrics.md | 2-campaign-structure.md |
| "My ads stopped working" | 7-troubleshooting.md | 5-optimization-scaling.md |
| "How do I scale without increasing costs?" | 5-optimization-scaling.md | 2-campaign-structure.md |
| "What creative should I make?" | 4-creative-strategy.md | 8-technical-context.md |
| "Do I need Advantage+?" | 2-campaign-structure.md, 3-audience-targeting.md | 8-technical-context.md |
| "How do I set up tracking?" | 1-account-setup.md | - |
| "Should I use interest targeting?" | 3-audience-targeting.md | 8-technical-context.md |
| "Why are my leads low quality?" | 7-troubleshooting.md | 3-audience-targeting.md |
| "What's changed in 2025?" | 8-technical-context.md | All documents |

### Red Flags - What NOT to Recommend

**These strategies are outdated and will harm performance in 2025:**

❌ **Manual targeting with 10+ interests** - The algorithm performs better with broad targeting + Advantage+ audience
❌ **5-20 campaigns with complex structures** - Simplicity (1-3 campaigns) enables faster learning
❌ **Minor creative variations (headline swaps)** - Need meaningfully different concepts, formats, hooks
❌ **Detailed demographic targeting layers** - Restricts algorithm learning; use broad + suggestions
❌ **Pixel-only tracking** - CAPI is now essential for optimal performance
❌ **"Set and forget" creative strategy** - Must refresh every 10-14 days minimum
❌ **Optimizing for clicks or impressions** - Lead/Purchase events are far more effective
❌ **ABO (Ad Set Budget Optimization) for scaling** - CBO or Advantage+ campaign budget is superior
❌ **Excluding placements manually** - Advantage+ placements optimize across all surfaces
❌ **Traffic campaigns for conversions** - Use Conversion or Lead objectives directly

### Important Disclaimers

1. **This playbook reflects December 2025 best practices** - Meta's platform evolves rapidly. Strategies here are based on Q3-Q4 2025 data and official Meta updates through December 7, 2025.

2. **Results vary significantly by:**
   - Industry/vertical
   - Offer quality and pricing
   - Creative quality
   - Market maturity
   - Landing page experience
   - CRM integration quality

3. **Benchmarks are guidelines, not guarantees** - Use them to set expectations and identify underperformance, but don't expect every campaign to hit median benchmarks immediately.

4. **Budget minimums matter** - Most strategies in this playbook assume at least $1,000-$3,000/month budget. Below $1,000/month, recommendations must be adjusted for limited learning data.

5. **Technical accuracy** - All information is sourced from:
   - Official Meta engineering blogs and documentation
   - Verified agency reports (TripleDart, Azarian, IMM, LeadSavvy, etc.)
   - Aggregated benchmark data (Varos, WordStream, LocaliQ)
   - Current as of December 7, 2025

### Getting Started

**For a new advertiser:**
1. Read this instructions document in full
2. Review **8-technical-context.md** to understand the AI foundation
3. Work through **1-account-setup.md** to establish proper tracking
4. Follow **2-campaign-structure.md** for campaign architecture
5. Implement recommendations from **3-audience-targeting.md** and **4-creative-strategy.md**
6. Monitor using **5-optimization-scaling.md** and **6-benchmarks-metrics.md**

**For an existing advertiser seeking improvement:**
1. Assess current performance against **6-benchmarks-metrics.md**
2. Audit campaign structure against **2-campaign-structure.md** recommendations
3. Check tracking setup in **1-account-setup.md**
4. Evaluate creative volume/diversity using **4-creative-strategy.md**
5. Apply optimization protocols from **5-optimization-scaling.md**
6. Use **7-troubleshooting.md** for specific issues

### Meta's 2026 Roadmap (What's Coming)

**Early indicators suggest these developments for 2026:**
- Autoregressive candidate generation (real-time creative remixing per user)
- Full GEM + Andromeda integration (15-25% additional ROAS in early tests)
- Inference-time compute scaling (dynamic resource allocation per impression)
- Expanded multimodal learning across organic + ads content
- More agentic automation (AI builds and manages entire campaigns)

**Strategic implication:** The gap between top performers and average advertisers will widen. High-velocity creative production will become the only sustainable competitive advantage.

---

## Quick Reference: Most Common Recommendations by Scenario

### Scenario 1: B2B SaaS, $3k/month budget, new to Meta

**Priority Actions:**
1. Set up Pixel + CAPI properly (1-account-setup.md)
2. Create 2 campaigns: Prospecting (70%) + Retargeting (30%)
3. Use Advantage+ Leads with Instant Forms
4. Upload customer list for 1% lookalike
5. Produce 20-30 video/carousel ads testing different pain points
6. Target: $18-$75 CPL, 12-28% SQL rate

### Scenario 2: eCommerce, $10k/month budget, performance declining

**Priority Actions:**
1. Consolidate to 1-2 campaigns (Advantage+ Sales + Retargeting)
2. Audit tracking - ensure CAPI is working and events match
3. Increase creative volume to 50+ unique ads monthly
4. Enable all Advantage+ toggles (audience, placements, creative, budget)
5. Remove manual targeting restrictions
6. Upload offline conversion data weekly
7. Target: 4:1-7:1 ROAS for eCommerce

### Scenario 3: Lead Gen (Services), $5k/month budget, low lead quality

**Priority Actions:**
1. Add qualifying questions to lead forms (2-3 questions max)
2. Switch to "Higher Intent" form type
3. Upload customer email list and exclude bad-fit domains
4. Implement "SMS by phone number" or "Work email" verification
5. Tighten creative messaging to pre-qualify prospects
6. Sync CRM for offline conversion tracking
7. Upload "qualified lead" events weekly

### Scenario 4: Any vertical, stuck in "Learning Limited"

**Priority Actions:**
1. Consolidate ad sets (need 50+ conversions/week per ad set)
2. Increase daily budget to minimum $50-$100/day
3. Reduce number of active ads per ad set to 5-10
4. Switch to CBO if using ABO
5. Broaden audience (remove restrictive layers)
6. Consider optimizing for easier event temporarily (Lead vs QualifiedLead)

---

## Document Update Log

**Version:** 1.0  
**Last Updated:** December 7, 2025  
**Based on Meta Platform Status:** December 2025 (Post-Andromeda, Post-GEM public announcement)

**Major Sources:**
- Meta Engineering Blog (GEM - Nov 10, 2025; Andromeda - Dec 2024)
- Meta Business Help Center (Advantage+ updates - Feb-Nov 2025)
- Industry benchmarks (Varos, WordStream, LocaliQ Q3-Q4 2025)
- Agency reports (TripleDart, Azarian, IMM, LeadSavvy, Cropink - 2025)

**Next Recommended Update:** January 2026 (to capture any Q4 2025 year-end changes)

---

## Support & Additional Resources

**If user needs help beyond this playbook:**
- Meta Business Help Center: https://www.facebook.com/business/help
- Meta Blueprint (free training): https://www.facebook.com/business/learn
- Meta Developer Documentation: https://developers.facebook.com/docs/marketing-apis/

**For reporting bugs or outdated information in this playbook:**
- Note the specific section and date
- Cross-reference with Meta's official documentation
- Verify against current benchmarks from Varos or similar platforms

---

## Final Note for LLM Agents

This playbook represents best practices as of December 2025. Meta's platform evolves continuously. When providing recommendations:

1. **Trust the fundamentals** - The core principles (simplicity, creative diversity, data volume, AI trust) are stable
2. **Verify if uncertain** - If unsure about a specific feature status, acknowledge uncertainty and suggest user verify in Meta Ads Manager
3. **Context matters** - A $50k/month eCommerce brand needs different advice than a $2k/month local service business
4. **Be realistic** - Better to set conservative expectations and overdeliver than promise unrealistic results
5. **Prioritize ruthlessly** - Users are overwhelmed. Give them the 1-3 highest-impact actions first.

Now proceed to the relevant playbook section based on the user's needs.
