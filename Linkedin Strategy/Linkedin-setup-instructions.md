# LinkedIn Ads: First Campaign Setup Guide

**Quick-Start Guide for Beginners**

Last Updated: December 2025

---

## Pre-Launch Checklist (Do This First)

### 1. Create Campaign Manager Account
**Time: 10 minutes**

- Go to [linkedin.com/campaignmanager](https://linkedin.com/campaignmanager)
- Link your LinkedIn Company Page (required)
- Add billing information
- Add team members if needed

---

### 2. Install LinkedIn Insight Tag
**Time: 15 minutes | Critical for tracking**

**Why:** Tracks conversions and enables remarketing

**How:**
1. Campaign Manager → Account Assets → Insight Tag
2. Copy the tracking code
3. Paste in `<head>` section of every website page
   - **OR** use Google Tag Manager (Custom HTML tag)
   - **OR** install via WordPress/Shopify plugin

**Verify:**
- Install [LinkedIn Insight Tag Helper](https://chrome.google.com/webstore) extension
- Visit your website - extension shows green checkmark if working

---

### 3. Set Up Conversion Tracking
**Time: 10 minutes**

1. Campaign Manager → Account Assets → Conversions
2. Click "Create Conversion"
3. Configure:
   - **Name:** "Demo Request" (or relevant action)
   - **Type:** Lead/Purchase/Download
   - **Tracking Method:**
     - **URL-based:** Fire on thank-you page (e.g., `/thank-you`)
     - **Event-based:** Fire on button click (needs developer)

**Test:** Complete a conversion yourself and verify it appears in Campaign Manager (24-48 hours)

---

### 4. Create Matched Audiences
**Time: 5 minutes**

**Essential audiences:**
- Website visitors (all pages, 180 days)
- High-intent pages (pricing/demo pages, 30 days)

**Exclusion audiences (prevent wasted spend):**
- Existing customers
- Employees
- Recent converters (last 30 days)

**How:** Campaign Manager → Account Assets → Matched Audiences → Create

---

## Campaign Setup (Step-by-Step)

### Step 1: Choose Campaign Objective
**Time: 2 minutes**

**Beginners start with:**
- **Lead Generation** (if using LinkedIn Lead Gen Forms)
- **Website Conversions** (if using external landing page)

---

### Step 2: Define Target Audience
**Time: 10 minutes**

**Key targeting options:**
- **Job Titles:** Exact roles (e.g., "VP of Marketing", "IT Director")
- **Seniority:** Director, VP, C-level
- **Company Size:** 50-200 employees, 500-1000, etc.
- **Industries:** Select 3-5 relevant industries
- **Location:** Target specific countries/regions

**Decision Rules:**
- Start narrow (more specific = higher quality)
- Minimum audience size: 50,000
- Maximum audience size: 300,000 (for beginners)

---

### Step 3: Select Ad Format
**Time: 5 minutes**

**Best formats for beginners:**

| Format | Best For | Specs |
|--------|----------|-------|
| **Sponsored Content (Single Image)** | Most versatile | 1200x627px |
| **Lead Gen Form** | Easiest lead capture | Form auto-fills from profile |
| **Video Ad** | Storytelling/demos | Square (1:1) or landscape (16:9) |

**Start with:** Single Image Sponsored Content + Lead Gen Form

---

### Step 4: Create Ad Creative
**Time: 30 minutes**

**Image specs:**
- Size: 1200x627px
- No text overlays >20% of image
- High quality, professional

**Ad copy structure:**
- **Headline:** 70 characters max (clear value)
- **Description:** 150 characters (expand on benefit)
- **CTA Button:** "Learn More" or "Download" or "Register"

**Example:**
```
Headline: Get 50 Qualified B2B Leads in 30 Days
Description: Proven LinkedIn ad framework used by 200+ SaaS companies. Free guide shows you how.
CTA: Download Now
```

---

### Step 5: Configure Budget & Bidding
**Time: 5 minutes**

**Recommended starting budget:**
- **Minimum:** $30/day ($900/month)
- **Comfortable:** $50-100/day
- **Test budget:** Run for 2 weeks minimum

**Bidding strategy:**
- **Beginners:** Use "Maximum Delivery" (auto-bidding)
- **Experienced:** Set manual bid at suggested range midpoint

**Expected costs (2025 benchmarks):**
- CPC: $8-15
- CPM: $30-80
- CPL (Lead Gen Form): $40-100

---

### Step 6: Set Up Lead Gen Form (Optional)
**Time: 10 minutes**

**Why use Lead Gen Forms:**
- Higher conversion rate (form pre-fills from LinkedIn profile)
- No landing page needed
- Lower cost per lead

**Setup:**
1. Create Campaign → Select "Lead Generation" objective
2. Build form with 3-5 fields max:
   - Name, Email, Company (auto-fill)
   - Custom question (optional): "Company size?"
3. Add privacy policy link
4. Write confirmation message

**Form best practices:**
- Fewer fields = higher conversion
- Add qualifying question to filter leads
- Sync to CRM automatically

---

### Step 7: Launch Campaign
**Time: 2 minutes**

**Pre-flight checklist:**
- [ ] Insight Tag installed and verified
- [ ] Conversion tracking configured
- [ ] Audience size: 50K-300K
- [ ] Budget set ($30+ per day)
- [ ] Ad creative meets specs
- [ ] Lead Gen Form synced to CRM (if using)

**Click "Launch"**

---

## First Week Actions

### Daily (5 minutes):
- Check campaign status in Campaign Manager
- Monitor spend and impressions
- Verify leads are coming through

### Day 3:
- Check CTR (Click-Through Rate)
  - **Good:** 0.5%+
  - **Excellent:** 1%+
- If CTR <0.3%: Revise ad creative

### Day 7:
- Review cost per lead/conversion
- Compare against benchmarks
- Decide: Continue, adjust, or pause

---

## Essential Integrations

### 1. CRM Integration (Highly Recommended)
**Time: 15 minutes**

**Why:** Automatically sync leads, track ROI

**Supported CRMs:**
- HubSpot (15 min setup, free tier available)
- Salesforce (30 min setup)
- Pipedrive, Zoho (via Zapier)

**Setup:**
1. Your CRM → Integrations → LinkedIn Ads
2. Authenticate Campaign Manager account
3. Map form fields to CRM properties
4. Test with dummy lead

---

### 2. Landing Page Tool (If Not Using Lead Gen Forms)
**Time: 30-60 minutes**

**Recommended tools:**
- **Carrd:** $19/year (simplest)
- **ConvertKit (KIT):** $29/month (includes email)
- **Framer:** $20/month (design-focused)

**Landing page must have:**
- Clear headline matching ad promise
- 3-5 form fields max
- Privacy policy link
- Thank-you page for conversion tracking

**Target conversion rate:** 35-60%

---

### 3. Calendar Tool (For Call Bookings)
**Time: 10 minutes**

**Recommended:**
- **Calendly:** Free tier or $10/month
- **TidyCal:** $29 one-time payment

**Setup:**
1. Connect to Google Calendar/Outlook
2. Set availability hours
3. Add confirmation email with:
   - Zoom/Google Meet link
   - What to prepare
   - Priming video (optional but recommended)

---

## Optimization Quick Wins

### Week 2-4: Monitor These Metrics

| Metric | Benchmark | If Underperforming |
|--------|-----------|-------------------|
| **CTR** | 0.5-1%+ | Test new ad creative |
| **Conversion Rate** | 35-60% (Lead Gen Form) | Reduce form fields |
| **Cost Per Lead** | $40-100 | Tighten targeting or improve creative |
| **Relevance Score** | 6+ | Align ad copy with audience |

---

### Quick Fixes by Problem

**Problem: High impressions, low clicks**
- Ad creative not compelling
- **Fix:** Test different images, rewrite headline

**Problem: High clicks, low conversions**
- Landing page/form issues
- **Fix:** Reduce form fields, improve offer clarity

**Problem: High cost per lead**
- Audience too broad or creative weak
- **Fix:** Narrow targeting, test new ad variations

**Problem: Low delivery (few impressions)**
- Budget too low or bid too low
- **Fix:** Increase daily budget or bid amount

---

## Common Beginner Mistakes

### 1. Starting Too Broad
- **Mistake:** Targeting "All Marketing Professionals" (10M+ audience)
- **Fix:** Target specific job titles + seniority + company size

### 2. Not Installing Insight Tag
- **Mistake:** Skip tracking setup
- **Fix:** You can't optimize or remarket without it

### 3. Giving Up Too Early
- **Mistake:** Pausing after 3 days because no results
- **Fix:** LinkedIn needs 7-14 days to optimize delivery

### 4. Too Many Form Fields
- **Mistake:** Asking for phone, company, title, budget, timeline
- **Fix:** Name + email + 1 qualifying question max

### 5. No Exclusion Audiences
- **Mistake:** Showing ads to existing customers
- **Fix:** Always exclude customers and employees

### 6. Setting Daily Budget Too Low
- **Mistake:** $10/day budget
- **Fix:** Minimum $30/day or campaign won't deliver

---

## Minimum Viable Setup (Startup Budget)

**Total cost: ~$2-50/month + ad spend**

- Campaign Manager (free)
- Insight Tag (free)
- HubSpot CRM free tier
- Carrd landing page ($19/year) OR Lead Gen Forms (free)
- Calendly free tier

**Ad spend:** Start with $900-1500/month ($30-50/day)

---

## Next Steps After First Campaign

### Once Running Smoothly (Week 4+):
1. Create remarketing campaign (target website visitors)
2. Add second ad variation (A/B test)
3. Set up email nurture sequence in CRM
4. Build lookalike audience (need 300+ conversions first)
5. Add video ad creative

### Advanced Optimization (Month 2+):
- Test different targeting segments
- Launch thought leadership campaign (boost organic content)
- Add priming video after calendar booking
- Implement multi-touch attribution

---

## Support Resources

**LinkedIn Help:**
- Campaign Manager: [linkedin.com/campaignmanager](https://linkedin.com/campaignmanager)
- Help Center: [business.linkedin.com/marketing-solutions/help](https://business.linkedin.com/marketing-solutions/help)

**Tag Helper Extension:**
- [LinkedIn Insight Tag Helper](https://chrome.google.com/webstore) (Chrome)

**Recommended Learning:**
- Test small, iterate fast
- Monitor metrics daily for first 2 weeks
- Don't change too many variables at once

---

**Remember:** Your first campaign won't be perfect. Focus on getting it live, collecting data, and optimizing based on performance. LinkedIn's algorithm needs 7-14 days to optimize delivery.

---

**Related Playbook Files:**
- Core Strategy Framework (overall strategy)
- Benchmarks & Specifications (performance targets)
- Decision Trees & Optimization (troubleshooting guide)
