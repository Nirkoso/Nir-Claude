# Scalefox 3.0: Complete Product Specification

**Version:** 1.0
**Date:** 2025-12-03
**Status:** Specification Complete - Ready for Development

---

## Executive Summary

Scalefox 3.0 is a hand-held LinkedIn advertising platform designed to enable first-time B2B advertisers (SMB founders and marketing heads) to create and publish professional LinkedIn campaigns in a single session. The product eliminates the need for agencies or deep platform expertise by automating complex tasks, providing expert guidance, and educating users throughout the journey.

**Core Value Proposition:**
"Create your first LinkedIn campaign in one session - no agency, no guesswork, no wasted budget"

**Target Market:**
- B2B companies with $1M+ ARR
- Average Contract Value (ACV) >$10K
- Never advertised on LinkedIn before
- Budget: $2K-10K/month for advertising

**Key Differentiators:**
1. Complete campaign setup in 45-60 minutes (not weeks with agencies)
2. Agency-level strategy based on $10M+ analyzed ad spend (automated)
3. Hand-held education throughout (explain like to a 6-year-old but warm/professional)
4. Budget-efficient warm-up approach (proven 70/20/10 allocation)
5. Real-time optimization guidance (not set-it-and-forget-it)

---

## Product Architecture

### 10-Step User Flow

**Stage 1: Discovery (Steps 1-2)**
- Step 1: Enter URL → AI-powered company analysis
- Step 2: Enter Competitors → Market intelligence and competitive insights

**Stage 2: Strategy (Steps 3-6)**
- Step 3: Select Persona → Auto-generated ICP personas with customization
- Step 4: Brand Profile → Visual identity, USP, tone, messaging, social proof
- Step 5: Campaign Planning → Budget setting and week-by-week campaign roadmap
- Step 6: GTM Playbook → 6 creative briefs (3 proven patterns + 3 creative angles)

**Stage 3: Execution (Steps 7-8)**
- Step 7: Create Ads → Media playground with dual workflow options
- Step 8: Publish → Review, connect LinkedIn, and launch campaigns

**Stage 4: Activation (Steps 9-10)**
- Step 9: Success → Confirmation, expectations, and next steps
- Step 10: Monitor Results → Dashboard with real-time metrics and optimization guidance

**Estimated Completion Time:** 45-60 minutes
**Session Completion Rate Target:** 60-75%
**Publish Within 48 Hours Target:** 80%

---

## Technical Requirements Summary

### Core Technology Stack Needs

**Frontend:**
- Responsive web application (desktop, tablet, mobile)
- Real-time preview rendering (ad mockups, campaign visualizations)
- Drag-and-drop ad creator
- Multi-step form with progress tracking and auto-save
- Data visualization (charts, graphs, dashboards)

**Backend:**
- RESTful API architecture
- Asynchronous job processing (website analysis, competitor research)
- Session management and draft persistence
- File upload and asset management
- Email notification system

**AI/ML Integrations:**
- Website analysis (industry classification, value prop extraction, brand color detection)
- Competitor analysis (campaign identification, messaging theme extraction)
- Persona generation (ICP modeling based on firmographics and competitor data)
- Creative brief generation (strategy synthesis from competitive intelligence)
- Image generation (DALL-E, Midjourney, or Stable Diffusion API)
- Copy assistance (GPT-4 for variations and refinements)
- Performance insights (automated analysis and recommendations)

**Third-Party Integrations:**
- LinkedIn Campaign Manager API (OAuth 2.0)
  - Create campaigns and ads
  - Upload creative assets
  - Set targeting, budgets, schedules
  - Pull performance metrics
  - Install Insight Tag
- Data enrichment APIs (Clearbit, ZoomInfo, or similar for company data)
- Email service (SendGrid, Postmark, or similar)
- Cloud storage (S3, GCS for asset storage)
- Analytics (Google Analytics, Mixpanel, or similar)
- CRM integrations (HubSpot, Salesforce via API or Zapier)

### Data Flows

**Onboarding Flow (Steps 1-6):**
1. User enters URL → Scrape/analyze website → Extract company data
2. User adds competitors → Query LinkedIn, scrape data → Analyze campaigns and messaging
3. System generates personas → LinkedIn audience size API → Validate and present
4. User defines brand → Parse website assets → Pre-fill brand profile
5. User sets budget → Calculate campaign allocation → Generate plan visualization
6. System creates briefs → Synthesize competitive intelligence → Output 6 creative concepts

**Ad Creation Flow (Step 7):**
1. User selects brief → Pre-fill copy based on brief
2. User chooses image source (AI, upload, template) → Process and optimize
3. User edits ad → Real-time preview updates
4. User saves ad → Store in database with status "draft"

**Publishing Flow (Step 8):**
1. User reviews campaigns → Display all configured campaigns
2. User connects LinkedIn → OAuth flow → Store access token
3. System creates campaigns in LinkedIn → API calls to Campaign Manager
4. System confirms success → Email user with instructions
5. User activates in LinkedIn Campaign Manager → Campaign goes live

**Monitoring Flow (Step 10):**
1. System polls LinkedIn API → Pull performance data every 2-5 minutes
2. System analyzes metrics → Compare to benchmarks, generate insights
3. Dashboard updates → Display real-time data to user
4. System sends daily emails → Summarize performance and provide guidance

### Security & Compliance

**Authentication & Authorization:**
- User authentication (email/password, social login)
- LinkedIn OAuth 2.0 (secure token storage, automatic refresh)
- Role-based access control (if team features added)

**Data Privacy:**
- GDPR compliant (data portability, right to deletion)
- SOC 2 certification pathway
- Encryption at rest and in transit
- No storage of LinkedIn passwords (OAuth only)
- Clear privacy policy and data usage terms

**API Security:**
- Rate limiting
- Input validation and sanitization
- SQL injection prevention
- XSS protection
- CSRF tokens

---

## User Experience Design Principles

### Design Philosophy

**1. Automate the Intimidating**
Users fear complexity and making mistakes. Automate everything that requires expertise:
- Website and competitor analysis
- Persona generation
- Campaign structure and budget allocation
- Targeting recommendations
- Creative brief development

**2. Educate Through Action**
Don't just tell users how LinkedIn ads work - teach them while they build:
- Inline tooltips for every concept
- Expandable sections for deeper learning
- Real-world analogies (warm-up = first date)
- Benchmarks for context (your CTR vs average)
- "Why this matters" explanations

**3. Celebrate Progress Frequently**
First-time advertisers need validation at every step:
- Progress indicator showing advancement
- Celebration messages after each step
- Milestone acknowledgments (first lead, Week 1 complete)
- Specific praise ("Your CTR is 52% above average!")

**4. Manage Expectations Proactively**
The biggest risk is user disappointment from unrealistic expectations:
- Set ranges, not exact numbers ("35-65 leads" not "50 leads")
- Explain learning phases ("Days 1-3 will be slow - that's normal")
- Provide timelines ("First leads typically appear Days 3-5")
- Compare to benchmarks ("Your Week 1 CPL is $42 - that's excellent")

**5. Safety Nets Everywhere**
Reduce fear of commitment and mistakes:
- "You can pause anytime"
- "Nothing is live until YOU approve"
- Auto-save drafts (no fear of losing work)
- Edit after publishing
- Clear instructions for reversal

**6. Make Data Actionable**
Don't just show metrics - tell users what to do:
- "Your best ad is X. Create 2 more like it."
- "Low CTR detected. Pause this ad and reallocate budget."
- One-click optimization actions
- "Apply All Recommendations" button

### Visual Design Language

**Colors:**
- Primary: Blue (trust, professionalism, LinkedIn brand association)
- Success: Green (validation, positive performance)
- Warning: Yellow (caution, attention needed)
- Error: Red (issues, critical actions)
- Neutral: Grays (UI structure, secondary content)

**Typography:**
- Headlines: Large, bold, clear hierarchy
- Body: Readable, 16px minimum for accessibility
- Microcopy: 14px, sufficient contrast
- Code/Data: Monospace where appropriate

**Iconography:**
- Simple, recognizable icons
- Consistent style throughout
- Tooltips on hover for clarification

**Spacing:**
- Generous whitespace to avoid overwhelm
- Clear section separation
- Card-based layouts for scanability

**Responsive Design:**
- Mobile-first approach
- Tablet-optimized layouts
- Desktop full-feature experience

---

## Campaign Strategy Framework (Built Into Product)

### Week 1: Warm-Up Campaign

**Budget:** $210 ($30/day for 7 days)
**Objective:** Website Visits (learning phase)
**Ads:** 6 initial ads testing different angles

**Purpose:**
- Teach LinkedIn algorithm who your best audience is
- Test messaging and creative approaches
- Establish baseline performance metrics
- Avoid wasting budget on cold, untested campaigns

**Expected Results:**
- 2,000-3,500 impressions
- 40-80 clicks
- 3-6 leads
- CPL: $35-70 (higher than ongoing, but acceptable for learning)

**User Education:**
"Think of this like a first date - we're not proposing marriage yet, just seeing what clicks."

### Week 2-4: Optimized Campaigns

**Campaign A: Core Offer (70% of remaining budget)**
- **Purpose:** Main revenue driver
- **Objective:** Lead Generation
- **Targeting:** Personas validated in Week 1
- **Ads:** 3 optimization ads (based on Week 1 winners) + 6 new targeting ads
- **Expected:** 60-75% of total leads

**Campaign B: Brand Awareness (20% of remaining budget)**
- **Purpose:** Build credibility, reach wider audience
- **Objective:** Engagement
- **Targeting:** Broader than Core Offer
- **Ads:** 2 awareness ads (thought leadership, case studies)
- **Expected:** Feed retargeting funnel, increase brand recall

**Campaign C: Retargeting (10% of remaining budget)**
- **Purpose:** Convert engaged users (highest ROI)
- **Objective:** Lead Generation
- **Targeting:** Website visitors, video viewers, ad clickers
- **Ads:** 4 retargeting ads (created in Week 2, run ongoing)
- **Expected:** 50% lower CPL than cold campaigns, 3-5x conversion rate

**Budget Allocation Rationale:**
"This 70/20/10 split is battle-tested from $10M+ in ad spend analysis. We tested other combinations - this one consistently wins."

---

## Content & Messaging Strategy

### Brand Voice

**Scalefox speaks as:** The Expert Friend
- Knowledgeable but never condescending
- Empowering ("You can do this, and here's how")
- Transparent (honest about challenges and realistic about outcomes)
- Confidence-building (celebrates wins, normalizes setbacks)

### Tone Spectrum

**Educational Content:** Warm, clear, slightly informal
- Use analogies and metaphors
- "Explain like I'm smart but new"
- Active voice, second person
- Short sentences for clarity

**Motivational Content:** Enthusiastic, validating, energizing
- Specific praise (not generic "good job")
- Forward momentum ("Next up:", "Now let's:")
- Celebration of milestones

**Reassurance Content:** Calm, normalizing, supportive
- Acknowledge concerns ("We know this feels...")
- Normalize ("This is completely normal")
- Provide proof ("85% of campaigns start this way")
- Offer concrete next step

**Technical Explanations:** Clear, jargon-free, practical
- Define terms inline ("CTR (click-through rate)")
- Use "what this means for you" framing
- Provide benchmarks for context
- Actionable takeaways

### Key Messages

**Pre-Signup:**
"Create your first LinkedIn campaign in one session - no agency, no guesswork, no wasted budget"

**During Onboarding:**
"We'll automate the complex parts. You focus on strategy. We'll teach you everything along the way."

**Campaign Planning:**
"This is the proven framework from analyzing 1,000+ successful campaigns. Trust the process."

**Publishing:**
"You built a professional LinkedIn campaign from scratch. That's a $5K-10K agency deliverable - and you did it yourself."

**Monitoring:**
"Week 1 will feel slow. That's by design. The algorithm is learning. Week 2 is where the magic happens."

---

## Success Metrics & KPIs

### Product Metrics

**Acquisition:**
- Website visitors from ads/content
- Demo requests
- Trial starts
- Free tier signups

**Activation:**
- Same-session completion rate: Target 60-75%
- Time to complete setup: Target <60 minutes
- Campaigns published within 48 hours: Target 80%

**Engagement:**
- Daily active users (DAU)
- Dashboard logins per week
- Average session duration
- Feature adoption rates

**Retention:**
- Week 1 campaign stays active: Target 85%
- Week 2 campaigns launched: Target 70%
- Month 1→Month 2 retention: Target 65%
- 6-month retention: Target 45%

**Revenue:**
- Monthly recurring revenue (MRR)
- Average revenue per user (ARPU)
- Customer lifetime value (LTV)
- Customer acquisition cost (CAC)
- LTV:CAC ratio: Target 3:1

**Advocacy:**
- Net Promoter Score (NPS): Target 50+
- Referral rate: Target 15-25%
- Case study participation: Target 10% of successful users
- Reviews and testimonials

### User Success Metrics (In-Product)

**Week 1:**
- Impressions: 2,000-3,500
- Clicks: 40-80
- Leads: 3-6
- CTR: 0.30-0.50%
- CPL: $35-70

**Month 1:**
- Impressions: 15,000-30,000
- Clicks: 300-600
- Leads: 35-65
- CTR: 0.35-0.50%
- CPL: $77-143

**Month 2+ (Optimized):**
- Impressions: 25,000-50,000
- Clicks: 500-1,000
- Leads: 60-100
- CTR: 0.40-0.60%
- CPL: $50-100 (improved)

---

## Development Roadmap Recommendations

### MVP (Minimum Viable Product)

**Scope:**
- Steps 1-10 (full user flow)
- Single image ad format only (no carousel, video)
- Basic dashboard (core metrics)
- Email notifications (daily summaries)
- LinkedIn Campaign Manager integration

**Timeline:** 12-16 weeks

**Priority Features:**
1. Automated website and competitor analysis
2. Persona generation and validation
3. Campaign plan calculator
4. Creative brief generator
5. Ad creator with AI image generation
6. LinkedIn OAuth and campaign creation
7. Performance dashboard with insights
8. Daily email updates

### V1.1 (Post-MVP Enhancements)

**Scope:**
- Additional ad formats (carousel, video)
- Advanced targeting options
- A/B testing framework
- CRM integrations
- Team collaboration features
- Mobile app (iOS/Android)

**Timeline:** +8-12 weeks after MVP

### V2.0 (Advanced Features)

**Scope:**
- Multi-campaign management
- Cross-platform advertising (LinkedIn + Google, Facebook)
- Advanced analytics and attribution
- White-label options
- API for integrations
- Marketplace for templates and playbooks

**Timeline:** +16-20 weeks after V1.1

---

## Risk Assessment & Mitigation

### Technical Risks

**Risk: LinkedIn API limitations or changes**
- Impact: High - core functionality depends on API
- Mitigation: Regular monitoring of API updates, fallback to manual processes, clear communication with users

**Risk: AI/ML model accuracy (persona generation, insights)**
- Impact: Medium - affects user confidence in recommendations
- Mitigation: Human review layer, allow user overrides, continuous model training

**Risk: Performance at scale (dashboard real-time updates)**
- Impact: Medium - affects user experience
- Mitigation: Caching strategies, background job processing, WebSocket optimization

### User Experience Risks

**Risk: User drop-off during setup (60-minute commitment)**
- Impact: High - directly affects activation rate
- Mitigation: Auto-save drafts, progress indicator, allow return later, simplify steps

**Risk: Unrealistic expectations leading to disappointment**
- Impact: High - affects retention and NPS
- Mitigation: Proactive education, range-based projections, daily emails managing expectations

**Risk: Users over-optimize too early (reset learning)**
- Impact: Medium - affects campaign performance
- Mitigation: "Don't change yet" warnings, locked editing during learning phase, explanation of why

### Business Risks

**Risk: Competitor copy or undercut pricing**
- Impact: Medium - affects differentiation
- Mitigation: Continuous product innovation, build network effects (community), focus on education/support

**Risk: LinkedIn increases ad costs or changes policies**
- Impact: High - affects user ROI
- Mitigation: Diversify to multi-platform (Google, Facebook), focus on optimization features, transparent communication

**Risk: Agencies view as threat and spread negative perception**
- Impact: Low-Medium - affects brand reputation
- Mitigation: Position as complementary (for smaller budgets agencies don't serve), offer white-label to agencies

---

## Go-To-Market Strategy

### Target Customer Segments

**Primary (Year 1):**
1. B2B SaaS companies ($1-10M ARR, 10-100 employees)
2. Professional services firms (consulting, agencies)
3. IT/Technology companies

**Secondary (Year 2):**
4. Financial services (B2B fintech, accounting)
5. Manufacturing/Industrial B2B
6. Healthcare B2B (med tech, health IT)

### Pricing Model Recommendation

**Tiered SaaS Model:**

**Starter: $199/month**
- Single user
- 1 active campaign at a time
- Up to $5K/month ad spend managed
- Basic dashboard and reporting
- Email support
- Core features only

**Professional: $399/month** (Most Popular)
- 3 users
- 3 active campaigns
- Up to $15K/month ad spend managed
- Advanced dashboard with insights
- Priority email + chat support
- A/B testing features
- CRM integration

**Business: $799/month**
- Unlimited users
- Unlimited campaigns
- Unlimited ad spend managed
- Full analytics and attribution
- Dedicated account manager
- Phone support
- Early access to new features
- API access

**Enterprise: Custom pricing**
- White-label options
- Custom integrations
- SLA guarantees
- Onboarding and training

**Alternative: Performance-Based Model**
- Free to use product
- 10-15% fee on ad spend managed
- Aligns incentives (we succeed when you succeed)
- Lower barrier to entry

### Launch Channels

**1. LinkedIn Advertising (Dogfooding)**
- Target: Marketing decision-makers at B2B companies
- Budget: $10-20K/month
- Message: "We used our own product to find you"

**2. Content Marketing**
- SEO-optimized guides: "LinkedIn Ads for B2B", "First LinkedIn Campaign Guide"
- Case studies from beta users
- Weekly LinkedIn posts (Grow/Educate/Capture strategy from research)
- Lead magnet: "LinkedIn Advertising Playbook for B2B SaaS"

**3. Partnerships**
- SaaS communities (SaaStr, Pavilion)
- Marketing tool integrations (HubSpot, Salesforce app marketplaces)
- Referral partnerships with complementary tools

**4. Direct Outreach**
- Warm introductions from beta users
- LinkedIn outreach to target personas
- Founder-led sales for first 100 customers

**5. Product-Led Growth**
- Free tier or trial (7-14 days)
- Viral loops (referral program with incentives)
- Template/playbook marketplace (community-generated)

---

## Appendices

### A. Reference Documents

This complete specification synthesizes insights from:

1. **LinkedIn Strategy Analysis** (`/research/linkedin-strategy-analysis.md`)
   - 7 key sections covering campaign planning, creative strategy, targeting, monitoring
   - Based on analyzing LinkedIn B2B guide, funnel concept, and warm leads system
   - 25+ actionable insights for first-time advertisers

2. **Screen-by-Screen Flows** (`/product-specs/screen-by-screen-flows.md`)
   - Detailed UI/UX for all 10 steps
   - User interactions, technical requirements, error states
   - Copy examples and design patterns
   - 60+ pages of comprehensive product flows

3. **User Journey Map** (`/product-specs/user-journey-map.md`)
   - Complete emotional journey from awareness to advocacy
   - Touchpoint matrix across all stages
   - Pain points and solutions mapping
   - Key insights for product design

4. **Messaging Framework** (`/product-specs/messaging-framework.md`)
   - Brand voice and tone guidelines
   - Copy patterns for all contexts
   - Educational content templates
   - CTA library and testing framework

### B. Success Stories (Template for Case Studies)

**Company:** [Name], [Industry]
**Size:** [Employees], [ARR]
**Challenge:** [What they struggled with before Scalefox]
**Solution:** [How they used Scalefox]
**Results:**
- Month 1: [X] leads at $[Y] CPL
- Month 3: [X] leads at $[Y] CPL
- ROI: [Z]x
- Key win: [Specific success moment]
**Quote:** "[Testimonial from user]" - [Name, Title]

### C. Competitive Landscape

**Agencies:**
- Positioning: Too expensive ($5-10K/month) for SMBs
- Scalefox advantage: Same strategy, 1/10th the cost, user retains control

**DIY LinkedIn Campaign Manager:**
- Positioning: Too complex, steep learning curve, high error risk
- Scalefox advantage: Hand-held guidance, automated strategy, reduced risk

**Other Ad Platforms (AdEspresso, Madgicx, etc.):**
- Positioning: Focus on Facebook/Instagram, not LinkedIn-specific
- Scalefox advantage: LinkedIn expertise, B2B-focused strategies

**Competitor Products (AdStage, Metadata.io, etc.):**
- Positioning: Enterprise-focused, complex interfaces, expensive
- Scalefox advantage: SMB-focused, simple interface, accessible pricing

### D. Technical Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        USER INTERFACE                        │
│  (React SPA - Responsive Web App)                           │
│  - Onboarding Flow (Steps 1-10)                             │
│  - Dashboard & Monitoring                                    │
│  - Ad Creator & Campaign Builder                             │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌─────────────────────────────────────────────────────────────┐
│                      API LAYER (Node.js)                     │
│  - Authentication & Authorization                            │
│  - RESTful Endpoints                                         │
│  - Business Logic                                            │
│  - Rate Limiting & Validation                                │
└─────────────────────────────────────────────────────────────┘
                            ↕
┌───────────────────┬──────────────────┬──────────────────────┐
│  BACKGROUND JOBS  │   DATABASE       │   EXTERNAL APIS      │
│  (Redis Queue)    │   (PostgreSQL)   │                      │
│                   │                  │                      │
│ - Website scrape  │ - Users          │ - LinkedIn Campaign  │
│ - Competitor      │ - Campaigns      │   Manager API        │
│   analysis        │ - Ads            │ - AI/ML APIs         │
│ - AI generation   │ - Performance    │   (GPT-4, DALL-E)    │
│ - Email sending   │   metrics        │ - Data enrichment    │
│ - Metric sync     │ - Drafts         │   (Clearbit)         │
│                   │                  │ - Email service      │
│                   │                  │ - Cloud storage      │
└───────────────────┴──────────────────┴──────────────────────┘
```

### E. User Personas Detail

**Persona 1: Sarah (VP Marketing)**
- Age: 32-45
- Experience: 5-10 years in marketing
- Company: 30-150 employees, $2-10M ARR
- Pain: Pressure to generate predictable pipeline, limited budget
- Goals: Prove marketing ROI, hit lead volume targets, look competent to CEO
- Tech comfort: High (uses marketing stack daily)
- LinkedIn ads experience: None
- Key motivation: Results and efficiency

**Persona 2: Mike (Founder/CEO)**
- Age: 35-50
- Experience: First-time entrepreneur or second company
- Company: 10-50 employees, $1-5M ARR
- Pain: Wearing too many hats, needs scalable lead gen
- Goals: Profitable growth, build marketing system, free up time
- Tech comfort: Medium-high (technical background)
- LinkedIn ads experience: None, intimidated by complexity
- Key motivation: Speed to results and clear ROI

**Persona 3: Jessica (Marketing Manager)**
- Age: 27-35
- Experience: 3-5 years in marketing
- Company: 50-200 employees, $3-15M ARR
- Pain: Executing VP's directive, proving value to secure promotion
- Goals: Successfully launch campaigns, learn new skills, advance career
- Tech comfort: High (digital native)
- LinkedIn ads experience: None, eager to learn
- Key motivation: Career advancement and skill building

---

## Conclusion

Scalefox 3.0 represents a comprehensive solution to a well-defined market problem: B2B SMBs want to advertise on LinkedIn but are blocked by complexity, cost, and lack of expertise. By automating strategy development, simplifying execution, and providing expert guidance throughout, Scalefox democratizes access to LinkedIn advertising.

**Key Success Factors:**
1. **Automation:** Remove expertise barriers through AI-powered analysis and generation
2. **Education:** Build user confidence through clear explanations and benchmarks
3. **Strategy:** Embed proven frameworks (70/20/10 allocation, warm-up campaigns) into the product
4. **Support:** Proactive communication via daily emails and dashboard insights
5. **Results:** Focus relentlessly on user outcomes (leads, CPL, ROI)

**Unique Positioning:**
Scalefox is not a campaign management tool - it's a LinkedIn advertising education platform that happens to also run your campaigns. Users don't just get results; they become competent advertisers in 30 days.

**Next Steps:**
1. Validate core assumptions with user testing (prototype Steps 1-6)
2. Build MVP (16-week sprint)
3. Beta launch with 20-50 pilot customers
4. Iterate based on feedback
5. Public launch with full marketing push

**Vision:**
Make LinkedIn advertising accessible to every B2B company, regardless of budget or expertise. Become the default first step for companies exploring paid B2B advertising.

---

**Document Status:** Complete and ready for stakeholder review
**Prepared by:** Orchestrator with specialist agents (deep-researcher, product-manager, ux-designer, copywriter, conversion-optimizer)
**Review Cycle:** Pending - awaiting feedback from product, engineering, design, and go-to-market teams
