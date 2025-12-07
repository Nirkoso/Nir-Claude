# Technical Setup & Tools
**LinkedIn B2B Advertising - Implementation Guide**

Version 1.0 | December 2025

---

## When to Use This File

**Purpose:** Technical implementation requirements and tool integrations
**Use cases:**
- Setting up new LinkedIn Ads account
- Installing tracking pixels
- Configuring CRM integrations
- Selecting supporting tools
- Troubleshooting technical issues

---

## 1. LinkedIn Ads Required Setup

### A. Campaign Manager Account

**Setup Steps:**
1. Visit [linkedin.com/campaignmanager](https://linkedin.com/campaignmanager)
2. Create account (requires LinkedIn Company Page)
3. Add billing information
4. Add team members with appropriate permissions:
   - **Account Manager:** Full access
   - **Campaign Manager:** Create/edit campaigns, no billing
   - **Viewer:** Read-only

**Best Practice:** Separate accounts for different business units or clients.

---

### B. LinkedIn Insight Tag Installation

**What It Does:**
- Tracks website visitors for remarketing
- Measures conversions (form fills, demos, purchases)
- Enables attribution and demographics reporting

**Installation Code:**
```html
<!-- Place in <head> section of every page -->
<script type="text/javascript">
_linkedin_partner_id = "YOUR_PARTNER_ID";
window._linkedin_data_partner_ids = window._linkedin_data_partner_ids || [];
window._linkedin_data_partner_ids.push(_linkedin_partner_id);
</script>
<script type="text/javascript">
(function(l) {
if (!l){window.lintrk = function(a,b){window.lintrk.q.push([a,b])};
window.lintrk.q=[]}
var s = document.getElementsByTagName("script")[0];
var b = document.createElement("script");
b.type = "text/javascript";b.async = true;
b.src = "https://snap.licdn.com/li.lms-analytics/insight.min.js";
s.parentNode.insertBefore(b, s);})(window.lintrk);
</script>
<noscript>
<img height="1" width="1" style="display:none;" alt="" 
src="https://px.ads.linkedin.com/collect/?pid=YOUR_PARTNER_ID&fmt=gif" />
</noscript>
```

**Installation Methods:**
- **Manual:** Add to website <head>
- **Google Tag Manager:** Custom HTML tag
- **Platform-specific:** Shopify app, Wix integration, WordPress plugin

**Verification:**
1. Install [LinkedIn Insight Tag Helper](https://chrome.google.com/webstore) (Chrome extension)
2. Visit your website
3. Extension shows green checkmark if tag firing correctly

**Common Issues:**
- Tag not firing: Check if placed in `<head>` (not `<body>`)
- Multiple tags: Remove duplicates (causes double-counting)
- Ad blockers: ~85% of B2B visitors don't use them

---

### C. Conversion Tracking Setup

**What to Track:**

| Campaign Type | Conversion Events |
|---------------|------------------|
| Awareness | Page views, time on site, scroll depth |
| Consideration | Content downloads, video views, webinar registrations |
| Conversion | Form submissions, demo requests, trial signups, purchases |

**Setup in Campaign Manager:**
1. Account Assets → Insight Tag → Conversions
2. Click "Create Conversion"
3. Configure:
   - **Name:** Descriptive (e.g., "Demo Request Submission")
   - **Type:** Lead, Purchase, Download, Custom
   - **Value:** If applicable ($500 demo value)
   - **Tracking Method:**
     - **URL-based:** Fire when thank-you page loads (e.g., `/thank-you`)
     - **Event-based:** Fire on button click (requires developer)

**Example: Event-Based Tracking**
```javascript
// Fire on form submission
document.getElementById('demo-form').addEventListener('submit', function() {
  window.lintrk('track', { conversion_id: 123456 });
});
```

---

### D. Matched Audiences Setup

**Create Immediately:**
- **Website Visitors (All):** Last 180 days, any page
- **High-Intent Pages:** Pricing, demo, product pages (last 30 days)
- **Lead Form Openers:** Opened form but didn't submit
- **Video Viewers:** 50%+ completion

**Create After Launch:**
- **Email Lists:** Upload CRM contacts, refresh monthly
- **Account Lists:** Target accounts from Salesforce (300+ companies)
- **Lookalikes:** Based on converters (need 300+ source)

**Exclusion Audiences (Critical):**
- **Existing Customers:** Don't show acquisition ads to buyers
- **Employees:** Waste of budget (auto-suggested)
- **Recent Converters:** Last 30 days (prevent oversaturation)

---

## 2. CRM Integration

### Why Integrate:
- Auto-sync leads (no manual CSV exports)
- Track through sales funnel
- Calculate true ROI (LinkedIn spend → closed deals)
- Alert sales when target accounts engage

### Supported CRMs:

| CRM | Integration Type | Setup Time |
|-----|-----------------|-----------|
| **Salesforce** | Native | 30 minutes |
| **HubSpot** | Native | 15 minutes |
| **Marketo** | LinkedIn LaunchPoint | 45 minutes |
| **Microsoft Dynamics** | Native connector | 30 minutes |
| **Pipedrive, Zoho, Copper** | Via Zapier | 20 minutes |

### HubSpot Setup (Example):
1. HubSpot → Marketing → Ads → Connect Account → LinkedIn
2. Authenticate with Campaign Manager
3. Select campaigns to sync
4. Map form fields → HubSpot properties
5. Set up workflows:
   - Form submission → Create contact → Assign to rep → Send email
6. Create reports:
   - LinkedIn Ads → Leads → Opportunities → Deals

**Without CRM:**
- Download leads CSV daily from Campaign Manager
- Upload to CRM manually
- Update campaign tags for attribution

---

## 3. Supporting Tools

### A. Prospecting & Data Tools

**Sales Navigator** ($99-149/month)
- **Use:** Find prospects, build account lists, monitor job changes
- **Key Features:** Advanced filters, InMail credits, lead lists sync
- **When:** Building ABM target account lists, researching ICP

**Email Finders** (Free-$99/month)
- **Tools:** Apollo.io, ZoomInfo, Lusha, Hunter.io
- **Use:** Find email addresses for LinkedIn connections
- **When:** Cold outreach campaigns (Warm Leads System Phase 2)

---

### B. Automation Tools

**Email Automation** ($37-297/month)
- **Tools:** Instantly, Lemlist, Woodpecker, Reply.io
- **Use:** Cold/warm email campaigns, sequences
- **When:** Phase 2 (Prospecting), Phase 3 (Follow-up)
- **Context:** 3-email sequence (initial + 2 follow-ups)

**LinkedIn Automation** ($49-99/month)
- **Tools:** Drify, Expandi, Phantombuster, WeConnect
- **Use:** Auto connection requests, messages, comment-to-DM
- **When:** Prospecting playbook, lead magnet promotion
- **Warning:** LinkedIn limits (100 connections/week, 150 messages/day). Violations risk account restrictions.

---

### C. Landing Page Builders

| Tool | Price | Use Case | Best For |
|------|-------|----------|----------|
| **KIT** (ConvertKit) | $29-59/month | Lead magnets, email marketing | Simple funnels, easy setup |
| **Framer** | Free-$20/month | Design-forward pages | Brand presentation matters |
| **Carrd** | $19/year | Ultra-simple one-pagers | MVP testing, low budget |
| **Webflow** | $23-49/month | Complex pages, CMS | Custom functionality needed |
| **Unbounce** | $90+/month | A/B testing focus | Optimization-heavy campaigns |

**Target conversion rate:** 35-60% opt-in (first name + email only)

---

### D. Calendar & Scheduling

**Calendly** ($10-16/month per seat)
- **Use:** Automated booking for sales calls
- **Features:** Availability sync, confirmations, Zoom integration, redirects
- **When:** Standard for most B2B (offer page → calendar)

**Alternatives:**
- **TidyCal:** $29 one-time (budget option)
- **Chili Piper:** Enterprise (instant booking, routing)

**Integration with Warm Leads System:**
- Redirect to priming video (VSSL or Loom) after booking
- Increases show-up rate to 80%+

---

### E. Video Tools

**Loom** (Free-$15/month)
- **Use:** Post-call summaries, priming videos, async communication
- **Features:** Screen + camera, instant shareable links, CRM integration
- **When:** Follow-up flow (send recap within 2 hours of call)

**Wistia / Vidyard** ($300+/month)
- **Use:** Host videos on landing pages, VSLs on offer pages
- **Features:** Player customization, engagement analytics, CTAs in video
- **When:** Offer page VSL (2-5 minute explainer)

---

## 4. Tool Stack by Company Stage

### Startup (Budget: <$2K/month ads, <$500/month tools)

**Required:**
- LinkedIn Campaign Manager (free)
- Insight Tag (free)
- HubSpot free tier (CRM)

**Landing Pages:** Carrd ($19/year) or KIT free tier

**Calendar:** Calendly free tier

**Email:** Gmail or HubSpot free

**Total:** ~$30-50/month + ad spend

---

### Growth-Stage (Budget: $3K-10K/month ads, $500-1K/month tools)

**Required:**
- Campaign Manager + Insight Tag
- HubSpot Starter or Salesforce

**Landing Pages:** KIT ($29/month) or Framer ($20/month)

**Calendar:** Calendly ($10/month)

**Email:** Instantly ($37/month) or KIT

**Video:** Loom ($15/month)

**LinkedIn:** Sales Navigator ($99/month)

**Data:** Apollo free tier

**Total:** ~$200-400/month + ad spend

---

### Enterprise (Budget: $10K+/month ads, $1K+/month tools)

**Required:**
- Campaign Manager + Insight Tag
- Salesforce or HubSpot Pro

**Landing Pages:** Webflow ($49/month) or custom dev

**Calendar:** Calendly ($16/month)

**Email:** Instantly ($297/month for scale)

**Video:** Wistia or Vidyard ($300/month)

**LinkedIn:** Sales Navigator Team ($149/seat)

**Data:** ZoomInfo ($15K+/year)

**Automation:** Zapier ($299/month)

**Total:** ~$1,500-3,000/month + ad spend

---

## 5. Integration Workflow

### Standard B2B LinkedIn Tech Stack Flow:

```
1. Prospect sees LinkedIn Ad
   ↓
2. Clicks ad (LinkedIn tracks, costs CPC)
   ↓
3. Lands on page (Insight Tag fires, tracked for remarketing)
   ↓
4. Submits form (Conversion tracking fires)
   ↓
5. Lead syncs to CRM (HubSpot/Salesforce integration)
   ↓
6. Email sequence starts (HubSpot/Instantly workflow)
   ↓
7. Books call (Calendly link in email)
   ↓
8. CRM updated (Zapier or native integration)
   ↓
9. Receives priming video (VSSL/Loom in confirmation)
   ↓
10. Sales rep alerted (Slack via Zapier)
   ↓
11. Call happens (Zoom/Google Meet)
   ↓
12. Rep sends Loom recap (within 2 hours)
   ↓
13. CRM updated with outcome (Won/Lost)
   ↓
14. Attribution tracked (LinkedIn → Lead → Deal → Revenue)
```

**Every tool serves a specific purpose. Removing one creates friction or tracking gaps.**

---

## 6. Setup Priority Order

### Week 1 (Before Any Ads):
1. ✅ Campaign Manager account + billing
2. ✅ Insight Tag installed on all pages (verify with Tag Helper)
3. ✅ Conversion tracking configured
4. ✅ CRM account created (even free tier)

### Week 2 (Before Launch):
5. ✅ Landing page or Lead Gen Form created
6. ✅ Calendar tool set up (Calendly)
7. ✅ Matched Audiences created (visitors, exclusions)
8. ✅ Lead Gen Forms synced to CRM

### Week 3 (After Launch):
9. ✅ Email automation (nurture sequences)
10. ✅ Sales Navigator (if ABM or prospecting)
11. ✅ Lookalike audiences (after 300+ conversions)

### Month 2+ (Optimization):
12. ✅ Priming video tool (VSSL/Loom)
13. ✅ Cold email tool (Instantly) if multi-channel
14. ✅ LinkedIn automation (Drify) for DMs
15. ✅ Advanced tools (Wistia, Typeform, Zapier) as needed

**Don't set up everything at once. Master core flow first (ads → landing page → CRM → call).**

---

## 7. Common Integration Issues & Fixes

### Issue 1: Lead Gen Forms Not Syncing to CRM
**Cause:** Integration not configured or credentials expired

**Fix:**
1. Reconnect in CRM settings
2. Re-authenticate LinkedIn account
3. Check field mapping (LinkedIn "Company Name" → CRM "Company")
4. Test with dummy form submission

---

### Issue 2: Insight Tag Not Firing
**Cause:** Tag in `<body>` instead of `<head>`, or JavaScript error

**Fix:**
1. Move tag to `<head>` section
2. Check browser console for errors
3. Verify Partner ID is correct
4. Clear cache, test in incognito mode

---

### Issue 3: Conversion Tracking Not Recording
**Cause:** Conversion rule misconfigured (wrong URL or event)

**Fix:**
1. Test by manually completing conversion
2. Check thank-you page URL matches rule (exact vs. contains)
3. Verify event syntax if using JavaScript
4. Wait 24-48 hours for data to populate

---

### Issue 4: Matched Audience Too Small (<300)
**Cause:** Low traffic or email list doesn't match LinkedIn members

**Fix:**
1. Expand time window (30 days → 90 days)
2. Combine multiple pages into one audience
3. Upload larger email list
4. Wait for traffic to increase before remarketing

---

### Issue 5: Lookalike Audience Not Generating
**Cause:** Source audience <300 members or insufficient data

**Fix:**
1. Grow source audience first (wait for more conversions)
2. Upload larger customer list
3. Combine multiple source audiences
4. Use website visitors (larger pool) as temporary source

---

### Issue 6: Calendar Double-Booking
**Cause:** Calendar sync issues or timezone mismatch

**Fix:**
1. Check Calendly availability settings
2. Ensure Google Calendar/Outlook sync is active
3. Set timezone explicitly in Calendly
4. Test booking yourself to verify

---

### Issue 7: High-Volume Leads, Low Quality
**Cause:** Targeting too broad, no qualification filter

**Fix:**
1. Add qualifying question to form ("Annual revenue?")
2. Insert qualification form before Calendly (Typeform)
3. Tighten audience targeting (Section 5 of Core Strategy)
4. Update ad messaging to explicitly call out ICP

---

## 8. Tool Alternatives by Category

### CRM:
- **Free:** HubSpot, Zoho, Freshsales
- **Paid:** Salesforce, Pipedrive, Copper, Dynamics

### Landing Pages:
- **Simple:** Carrd, KIT, Mailchimp
- **Mid:** Framer, Webflow, Leadpages
- **Advanced:** Unbounce, Instapage, Custom dev

### Email:
- **Free:** HubSpot, Mailchimp, Sender
- **General:** KIT, ActiveCampaign, Klaviyo
- **Outreach:** Instantly, Lemlist, Reply.io

### Calendar:
- **Free:** Calendly, YouCanBook.me
- **Paid:** Calendly, TidyCal, Chili Piper

### Video:
- **Recording:** Loom, Vimeo Record, Vidyard
- **Hosting:** Wistia, Vidyard, Vimeo
- **Editing:** Descript, Camtasia

### Automation:
- **Zapier:** 5,000+ apps (easiest)
- **Make:** More powerful (formerly Integromat)
- **n8n:** Open-source (self-hosted)

**The best tool is the one you'll actually use. Start simple.**

---

## 9. Required vs. Optional Tools

### ✅ Required (Cannot run campaigns without):
1. LinkedIn Campaign Manager account
2. LinkedIn Insight Tag (for remarketing + tracking)
3. CRM (even free tier) (for lead management)
4. Landing page tool OR Lead Gen Forms
5. Calendar tool (for booking calls)

### ⚠️ Highly Recommended (Significantly improves results):
6. Email automation (for nurture sequences)
7. Conversion tracking (for ROI measurement)
8. Video tool for priming (Loom/VSSL)

### 💡 Optional (Nice-to-have for specific use cases):
9. Sales Navigator (for ABM or prospecting)
10. Cold email tool (for multi-channel outreach)
11. LinkedIn automation (for comment-to-DM at scale)
12. Advanced video hosting (Wistia for detailed analytics)
13. Form builder (Typeform for qualification)
14. Zapier (for complex integrations)

---

## 10. Technical Checklist

### Pre-Launch (Complete Before First Campaign):

**LinkedIn Setup:**
- [ ] Campaign Manager account created
- [ ] Billing information added
- [ ] Company Page linked
- [ ] Team members added with correct permissions

**Tracking Setup:**
- [ ] Insight Tag installed on all website pages
- [ ] Tag verified with LinkedIn Tag Helper extension
- [ ] Conversion events defined (demo, trial, download, etc.)
- [ ] Test conversion completed and tracked

**Audience Setup:**
- [ ] Website visitors audience created (all pages, 180 days)
- [ ] High-intent pages audience created (pricing, demo, 30 days)
- [ ] Customer exclusion list uploaded (if applicable)
- [ ] Employee exclusion enabled

**Integration Setup:**
- [ ] CRM account created
- [ ] Lead Gen Forms synced to CRM (if using)
- [ ] Test lead submitted and verified in CRM
- [ ] Attribution tracking configured

**Creative Assets:**
- [ ] Landing page created and tested (mobile + desktop)
- [ ] Lead Gen Forms drafted (3-5 fields max)
- [ ] Calendar tool configured (Calendly, etc.)
- [ ] Email sequences drafted (nurture + priming)

**Testing:**
- [ ] Submit test lead through full funnel
- [ ] Verify lead appears in CRM
- [ ] Verify conversion tracking fires
- [ ] Test calendar booking process
- [ ] Confirm email automation triggers

---

## 11. Maintenance Schedule

### Daily (Automated):
- CRM lead sync (automatic if integrated)
- Conversion tracking (automatic once configured)
- Email nurture sequences (automatic once set up)

### Weekly (Manual):
- Check CRM for lead quality feedback
- Review calendar show-up rates
- Audit email deliverability (bounce rates, spam)

### Monthly (Manual):
- Refresh customer exclusion list (upload new customers)
- Update remarketing audiences (check sizes, refresh time windows)
- Review CRM integration (any sync errors?)
- Update calendar availability (vacations, capacity changes)

### Quarterly (Manual):
- Audit all tool subscriptions (still using? Can downgrade?)
- Review tech stack efficiency (any redundant tools?)
- Update lookalike audiences (refresh source with latest converters)
- Check for new LinkedIn features or integrations

---

## 12. Cost Summary Table

### Minimum Stack (Startup):

| Tool | Cost | Purpose |
|------|------|---------|
| Campaign Manager | Free | Run ads |
| Insight Tag | Free | Tracking |
| HubSpot CRM | Free | Lead management |
| Carrd | $19/year | Landing pages |
| Calendly | Free | Booking |
| **Total** | **~$2/month** | Plus ad spend |

---

### Standard Stack (Growth):

| Tool | Cost | Purpose |
|------|------|---------|
| Campaign Manager | Free | Run ads |
| Insight Tag | Free | Tracking |
| HubSpot Starter | $50/month | CRM + email |
| Framer | $20/month | Landing pages |
| Calendly | $10/month | Booking |
| Loom | $15/month | Video |
| Sales Navigator | $99/month | Prospecting |
| Instantly | $37/month | Email automation |
| **Total** | **~$231/month** | Plus ad spend |

---

### Enterprise Stack:

| Tool | Cost | Purpose |
|------|------|---------|
| Campaign Manager | Free | Run ads |
| Insight Tag | Free | Tracking |
| Salesforce | $150/month | CRM |
| Webflow | $49/month | Landing pages |
| Calendly Pro | $16/month | Booking |
| Vidyard | $300/month | Video hosting |
| Sales Navigator Team | $149/month | Prospecting |
| Instantly Pro | $297/month | Email scale |
| Zapier | $299/month | Automation |
| **Total** | **~$1,260/month** | Plus ad spend |

---

## Quick Reference Links

### LinkedIn Resources:
- Campaign Manager: [linkedin.com/campaignmanager](https://linkedin.com/campaignmanager)
- Insight Tag: Campaign Manager → Account Assets → Insight Tag
- Help Center: [business.linkedin.com/marketing-solutions/help](https://business.linkedin.com/marketing-solutions/help)

### Tool Websites:
- **CRM:** [hubspot.com](https://hubspot.com), [salesforce.com](https://salesforce.com)
- **Landing Pages:** [kit.com](https://kit.com), [framer.com](https://framer.com), [carrd.co](https://carrd.co)
- **Calendar:** [calendly.com](https://calendly.com), [tidycal.com](https://tidycal.com)
- **Email:** [instantly.ai](https://instantly.ai), [lemlist.com](https://lemlist.com)
- **Video:** [loom.com](https://loom.com), [vidyard.com](https://vidyard.com)

---

**End of Technical Setup & Tools**

For strategic frameworks → See Core Strategy Framework
For benchmarks → See Benchmarks & Specifications
For optimization → See Decision Trees & Optimization Rules
For agent workflows → See Agent Execution Playbook
