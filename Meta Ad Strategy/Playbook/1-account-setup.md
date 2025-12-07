# 1. Account Setup & Technical Foundation

## Overview

Proper tracking and account setup is the #1 determinant of Meta ads success in 2025. With Meta's AI (GEM + Andromeda) relying heavily on accurate conversion data, incomplete or incorrect tracking setup will waste your entire budget.

**Critical Truth:** You cannot optimize what you cannot measure. Meta's algorithm is only as good as the data you feed it.

---

## Step 1: Meta Business Manager Setup

### Create Business Manager Account

**Purpose:** Centralizes all assets, permissions, billing, and data in one place.

**Required Components:**
1. **Business Manager** - Your master control panel
2. **Ad Account** - Where campaigns run and billing happens
3. **Facebook Business Page** - Required for all ads
4. **Instagram Business Profile** - Essential for Instagram placement ads

**Setup Process:**
```
1. Go to business.facebook.com
2. Click "Create Account"
3. Enter business name, your name, business email
4. Add your Facebook Page (or create one)
5. Create new Ad Account or request access to existing
6. Connect Instagram Business Profile to Facebook Page
```

**Best Practices:**
- Use business email (not personal Gmail)
- Enable two-factor authentication immediately
- Add team members with appropriate roles (Admin, Advertiser, Analyst)
- Create separate ad accounts for different brands/clients (don't mix)

---

## Step 2: Meta Pixel Installation (Required)

### What is the Meta Pixel?

A piece of JavaScript code that tracks user actions on your website. It's the foundation of all conversion tracking, remarketing, and optimization.

**In 2025, Pixel alone is insufficient** - you MUST also implement Conversions API (CAPI), but Pixel is still required.

### Standard Events to Track

**Priority 1 - Essential (Track These First):**
- `ViewContent` - User views product/service page
- `Lead` - Form submission (email signup, contact form, etc.)
- `AddToCart` - User adds item to cart (eCommerce)
- `InitiateCheckout` - User begins checkout process
- `Purchase` - Completed transaction
- `CompleteRegistration` - User completes signup/account creation

**Priority 2 - Valuable (Add After Basics Work):**
- `Schedule` - User books demo/appointment/call
- `StartTrial` - User begins free trial
- `SubmitApplication` - Application form submitted
- `Search` - User searches on your site

**Priority 3 - Advanced (For Optimization):**
- Custom events like `QualifiedLead`, `DemoCompleted`, `HighValueAction`

### Installation Methods

**Option 1: Direct Installation (Simplest)**
```html
<!-- Place this code in your <head> tag, right after opening -->
<script>
  !function(f,b,e,v,n,t,s)
  {if(f.fbq)return;n=f.fbq=function(){n.callMethod?
  n.callMethod.apply(n,arguments):n.queue.push(arguments)};
  if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
  n.queue=[];t=b.createElement(e);t.async=!0;
  t.src=v;s=b.getElementsByTagName(e)[0];
  s.parentNode.insertBefore(t,s)}(window, document,'script',
  'https://connect.facebook.net/en_US/fbevents.js');
  fbq('init', 'YOUR_PIXEL_ID');
  fbq('track', 'PageView');
</script>
<!-- Place this immediately after </head> -->
<noscript><img height="1" width="1" style="display:none"
  src="https://www.facebook.com/tr?id=YOUR_PIXEL_ID&ev=PageView&noscript=1"
/></noscript>
```

Then add event tracking on relevant pages:
```javascript
// On lead form submission
fbq('track', 'Lead');

// On purchase completion
fbq('track', 'Purchase', {
  value: 99.99,
  currency: 'USD'
});

// On demo booking
fbq('track', 'Schedule');
```

**Option 2: Google Tag Manager (Recommended for Non-Technical)**
1. Install GTM container on your site
2. Add Meta Pixel as a Custom HTML tag
3. Create triggers for each event
4. Test using Meta Pixel Helper browser extension

**Option 3: Platform-Specific Integrations**
- **Shopify:** Use native Meta channel app (automatically tracks Purchase, AddToCart, etc.)
- **WordPress:** Use PixelYourSite or similar plugin
- **Webflow:** Add code to custom code section
- **Squarespace:** Add code injection in site settings

### Verify Pixel Installation

1. Install **Meta Pixel Helper** Chrome extension
2. Visit your website
3. Extension icon should show green checkmark with Pixel ID
4. Perform test actions (form submission, etc.) and verify events fire

**Common Issues:**
- ❌ Pixel fires multiple times → Check for duplicate code
- ❌ Events not firing → Check JavaScript console for errors
- ❌ Pixel shows but events missing → Event code not added properly

---

## Step 3: Conversions API (CAPI) Setup (Mandatory 2025)

### Why CAPI is Non-Negotiable

**The Problem:** Browser tracking (Pixel) is increasingly blocked by:
- iOS 14.5+ ATT framework (~50% opt-out rate)
- Ad blockers
- Privacy browsers (Brave, Firefox)
- Cookie restrictions

**The Solution:** Server-side tracking via Conversions API sends event data directly from your server to Meta, bypassing browser restrictions.

**Performance Impact (Real Data):**
- 14% lower CPL when Pixel + CAPI vs Pixel alone
- 10-20% better lead quality
- 40-60% improvement in attribution accuracy

### CAPI Implementation Options

**Option 1: Native Platform Integrations (Easiest)**

**If you use these platforms, use native integration:**
- HubSpot → Native Meta integration (Settings → Marketing → Ads → Meta)
- Salesforce → MuleSoft connector or native integration
- Shopify → Meta Sales Channel (auto-enables CAPI)
- WooCommerce → Meta for WooCommerce plugin
- Zapier → Meta Conversions trigger
- Segment → Meta Destinations integration

**Setup example (HubSpot):**
```
1. HubSpot → Settings → Marketing → Ads
2. Connect Facebook Ad Account
3. Enable Conversions API
4. Map HubSpot properties to Meta parameters
5. Test using Events Manager
```

**Option 2: LeadsBridge (Best for Lead Gen)**
- Connects 380+ marketing tools to Meta
- Real-time lead sync (<5 min delay)
- Automatic CAPI event sending
- Supports offline conversions

**Cost:** $29-$149/month depending on volume

**Setup:**
```
1. Sign up at leadsbridge.com
2. Connect Meta Ad Account
3. Connect your CRM/form tool
4. Create bridge: Form → Meta Lead Ad → CRM
5. Enable CAPI sync
6. Map fields (email, phone, name, custom data)
```

**Option 3: Manual Server Implementation (Developers)**

**Requirements:**
- Server-side code capability (PHP, Python, Node.js, etc.)
- Access to Meta Conversions API
- Event queue system for reliability

**Basic flow:**
```
1. User completes action on website
2. Your server logs event
3. Server sends event to Meta Conversions API
4. Include event_id to deduplicate with Pixel
```

**Example (Node.js):**
```javascript
const bizSdk = require('facebook-nodejs-business-sdk');
const ServerEvent = bizSdk.ServerEvent;
const EventRequest = bizSdk.EventRequest;
const UserData = bizSdk.UserData;

const access_token = 'YOUR_ACCESS_TOKEN';
const pixel_id = 'YOUR_PIXEL_ID';

const user_data = (new UserData())
  .setEmail('user@example.com')
  .setPhone('1234567890')
  .setClientUserAgent(req.headers['user-agent'])
  .setFbc('fb.1.1234567890123.abcdefg')
  .setFbp('fb.1.1234567890123.1234567890');

const server_event = (new ServerEvent())
  .setEventName('Lead')
  .setEventTime(Math.floor(Date.now() / 1000))
  .setUserData(user_data)
  .setEventSourceUrl('https://yoursite.com/thank-you')
  .setActionSource('website')
  .setEventId('event_id_12345'); // Matches Pixel event_id

const events_data = [server_event];
const event_request = (new EventRequest(access_token, pixel_id))
  .setEvents(events_data);

event_request.execute().then(
  response => console.log('Event sent successfully')
);
```

### CAPI Event Parameters (What to Send)

**Required:**
- `event_name` - Lead, Purchase, etc.
- `event_time` - Unix timestamp
- `action_source` - Usually "website"
- `user_data` - At least one identifier

**Strongly Recommended (for better matching):**
- `email` - Hashed with SHA256
- `phone` - E.164 format, hashed with SHA256
- `first_name` - Lowercase, hashed
- `last_name` - Lowercase, hashed
- `client_ip_address` - User's IP
- `client_user_agent` - Browser user agent
- `fbc` - Facebook click ID from URL parameter
- `fbp` - Facebook browser ID from Pixel cookie
- `event_source_url` - The page URL
- `event_id` - Unique ID to deduplicate with Pixel

**Event-Specific Parameters:**
- `value` - Purchase amount (Purchase events)
- `currency` - USD, EUR, etc.
- `content_ids` - Product IDs (eCommerce)
- `contents` - Array of purchased items

### Verify CAPI Setup

**Events Manager Check:**
```
1. Meta Ads Manager → Events Manager
2. Select your Pixel
3. Go to "Test Events" tab
4. Perform test conversion on your site
5. Should see event appear with both "Browser" and "Server" icons
6. Check "Event Match Quality" score (aim for 8.0+)
```

**Match Quality Score:**
- 8.0+ = Excellent (aim for this)
- 6.0-7.9 = Good
- 4.0-5.9 = Okay
- <4.0 = Poor (fix immediately)

**Common CAPI Issues:**
- ❌ Duplicate events (not using same event_id) → Add unique event_id in both Pixel and CAPI
- ❌ Low match quality → Add more user parameters (email, phone, etc.)
- ❌ Events delayed → Check server logs for API errors
- ❌ Wrong event names → Must match standard event names exactly

---

## Step 4: Custom Conversions & Event Setup

### When to Use Custom Conversions

**Use Case 1: URL-Based Tracking**
If you can't edit website code, create custom conversions based on URL visits.

**Example:**
- Event: `ViewContent`
- Custom Conversion Name: "Demo Request"
- Rule: URL contains `/thank-you-demo`

**Use Case 2: Grouping Multiple Actions**
Create custom conversion for "Engaged User" that fires when someone does any of:
- Watches video 50%+
- Visits 3+ pages
- Spends 2+ minutes on site

**Use Case 3: Value Optimization**
Create high-value conversion for users who:
- Purchase >$100
- Sign up for enterprise plan
- Come from target company size

### Setting Up Custom Conversions

```
1. Events Manager → Custom Conversions
2. Click "Create Custom Conversion"
3. Name: Descriptive (e.g., "Qualified Demo Request")
4. Select Data Source (your Pixel)
5. Set Rules:
   - URL contains /thank-you
   AND
   - Value is greater than 100
6. Set Event Type (Lead, Purchase, etc.)
7. Save
```

---

## Step 5: Offline Conversion Tracking (Advanced - Critical for Lead Quality)

### Why Offline Conversions Matter

**The Problem:** Meta sees a "Lead" event when someone fills a form, but doesn't know if they became a qualified lead, demo, or customer.

**The Solution:** Upload data about what happened after the lead (SQL, demo completed, customer) so Meta can optimize for quality, not just volume.

**Impact:**
- 40-60% better lead quality
- 20-35% lower cost per qualified lead
- Algorithm learns which ad/audience drives real customers

### What to Upload

**Upload these events weekly (or daily for high volume):**
- Qualified leads (passed sales criteria)
- Demos completed
- Opportunities created
- Closed deals
- Deal value

**Required Data for Each Upload:**
1. Match key (email, phone, Facebook ID - at least one)
2. Event name (e.g., "QualifiedLead", "Purchase")
3. Event time (when it happened)
4. Value (deal size, if applicable)

### How to Upload Offline Conversions

**Method 1: Direct Upload (Manual - for testing)**
```
1. Events Manager → Data Sources → Your Pixel
2. Click "Upload Offline Events"
3. Download CSV template
4. Fill in data:
   - email, event_name, event_time, value, currency
5. Upload file
6. Wait 30-60 min for processing
```

**CSV Example:**
```csv
email,event_name,event_time,value,currency
user1@example.com,QualifiedLead,1701892800,500,USD
user2@example.com,Purchase,1701896400,5000,USD
```

**Method 2: API Upload (Automated - recommended)**

Most CRMs can auto-sync:
- **HubSpot:** Use native integration or Zapier
- **Salesforce:** MuleSoft or Zapier
- **Pipedrive:** Native integration
- **LeadsBridge:** Supports 380+ CRMs

**Method 3: CRM Native Integration**

**HubSpot Example:**
```
1. HubSpot → Settings → Marketing → Ads → Meta
2. Enable "Send CRM events to Meta"
3. Map lifecycle stages:
   - Marketing Qualified Lead → QualifiedLead event
   - Sales Qualified Lead → SQL event
   - Customer → Purchase event
4. Set values (deal amount or fixed value)
```

### Offline Conversion Best Practices

**Frequency:**
- Upload at least weekly (daily is better)
- More data = faster learning

**Event Naming:**
- Use standard events when possible (Lead, Purchase)
- Custom events should be clear ("DemoCompleted" not "Event1")

**Value Assignment:**
- If actual deal value not known, use estimated LTV
- Consistent values help algorithm optimize

**Time Windows:**
- Upload events within 7 days of original click/impression
- Events older than 7 days won't attribute properly

---

## Step 6: Advanced Tracking Setup

### Enhanced Conversion Tracking (New in 2025)

Meta now supports additional conversion tracking methods for better attribution:

**1. SMS Verification for Leads**
- Sends verification code to lead's phone
- Confirms phone number is real and owned by submitter
- Reduces spam leads by ~40%

**Setup:**
```
1. Lead Form Settings → Lead Verification
2. Enable "SMS by phone number"
3. Select countries to enable
4. Test with your own phone
```

**2. Work Email Verification**
- Validates that email is not generic (gmail, yahoo, etc.)
- Requires corporate domain email
- Best for B2B campaigns

**Setup:**
```
1. Lead Form Settings → Lead Verification  
2. Enable "Work email"
3. Optionally block specific domains
```

**3. Address Verification (Beta)**
- Tests in select regions
- Verifies physical address provided
- Useful for local service businesses

### UTM Parameter Tracking

**Always use UTM parameters** for external traffic analysis:

**Standard structure:**
```
https://yoursite.com/landing-page?
  utm_source=facebook
  &utm_medium=cpc
  &utm_campaign=lead-gen-q4
  &utm_content=video-testimonial-1
  &utm_term=small-business-software
```

**Best Practices:**
- Use consistent naming conventions
- Campaign = campaign name in Meta
- Content = ad creative variant
- Term = audience or placement
- Track in your analytics platform (GA4, Heap, etc.)

### Cross-Domain Tracking

If your funnel spans multiple domains (example.com → checkout.example.io), configure cross-domain tracking:

**Pixel Setup:**
```javascript
fbq('init', 'PIXEL_ID', {
  external_id: 'user_unique_id'
});

// Set same external_id on both domains
```

---

## Step 7: Account Security & Compliance

### Security Checklist

**Required Actions:**
- ✅ Enable two-factor authentication on all accounts
- ✅ Use business email (not personal)
- ✅ Review Business Manager permissions quarterly
- ✅ Remove inactive team members immediately
- ✅ Set spending limits if using shared accounts
- ✅ Review payment methods regularly

### Compliance & Policy

**Ad Account Restrictions:**
Common reasons accounts get restricted:
- Payment issues (expired card, declined payment)
- Policy violations (misleading claims, prohibited content)
- Sudden unusual spend increases
- Too many ad rejections
- Landing page issues (broken links, mismatched content)

**Prevention:**
- Keep payment methods current
- Read Meta's Advertising Policies: facebook.com/policies/ads
- Match ad content to landing page exactly
- Avoid making absolute claims ("#1", "best", "guaranteed")
- Get medical/financial claims reviewed if applicable
- Don't suddenly 10x your spend (scale gradually)

### Backup & Recovery

**Prevent Account Loss:**
1. Add backup Admin to Business Manager
2. Keep documentation of all setup (Pixel IDs, CAPI configs, etc.)
3. Export audience lists monthly (Custom Audiences)
4. Screenshot critical campaign settings
5. Download performance reports quarterly

**If Account Gets Restricted:**
1. Check notification for specific issue
2. Fix the issue immediately
3. Request review in Account Quality section
4. Response time: 24-72 hours typically
5. Be polite and specific in appeal

---

## Step 8: Validation Checklist

Before launching any campaigns, verify:

### Technical Validation
- ✅ Meta Pixel installed and firing PageView events
- ✅ Conversion events (Lead/Purchase) tested and working
- ✅ CAPI set up and showing in Events Manager
- ✅ Event Match Quality score 8.0+ (if using CAPI)
- ✅ Custom conversions created (if needed)
- ✅ Domains verified in Business Manager
- ✅ Privacy policy URL added to Business Manager

### Account Validation
- ✅ Business Manager created with business email
- ✅ Two-factor authentication enabled
- ✅ Payment method added and verified
- ✅ Spending limit set (if desired)
- ✅ Ad Account permissions correct
- ✅ Facebook Page and Instagram connected

### Integration Validation
- ✅ CRM connected (if using native integration)
- ✅ Lead sync tested (if applicable)
- ✅ Offline conversion upload scheduled (weekly minimum)
- ✅ UTM parameters working in analytics platform
- ✅ Landing pages load fast (<3 seconds)

### Compliance Validation
- ✅ Landing page matches ad claims exactly
- ✅ Privacy policy accessible
- ✅ Terms of service available
- ✅ No prohibited content in ads or landing pages
- ✅ No misleading claims ("free" when not free, etc.)

---

## Common Setup Mistakes to Avoid

**Mistake 1: Pixel Only, No CAPI**
- ❌ Impact: Missing 30-50% of conversions due to tracking restrictions
- ✅ Fix: Set up CAPI immediately (use LeadsBridge if unsure how)

**Mistake 2: Generic Event Tracking**
- ❌ Impact: Can't optimize for specific goals (all leads treated equally)
- ✅ Fix: Track specific events (QualifiedLead, DemoCompleted, etc.) and upload offline conversions

**Mistake 3: Poor Event Match Quality**
- ❌ Impact: CAPI events can't match to users, wasted server calls
- ✅ Fix: Send more parameters (email, phone, IP, user agent, fbc, fbp)

**Mistake 4: Not Verifying Setup**
- ❌ Impact: Running campaigns with broken tracking, can't optimize
- ✅ Fix: Always test with Meta Pixel Helper and Events Manager before launch

**Mistake 5: Forgetting About Offline Conversions**
- ❌ Impact: Algorithm optimizes for form fills, not qualified leads
- ✅ Fix: Schedule weekly uploads from CRM to Meta

**Mistake 6: Inconsistent Event Naming**
- ❌ Impact: Data fragmentation, can't aggregate learning
- ✅ Fix: Use standard event names, document custom events clearly

**Mistake 7: Multiple Pixels on Same Site**
- ❌ Impact: Duplicate events, incorrect attribution
- ✅ Fix: One Pixel per website (can share across multiple ad accounts if needed)

---

## Tools & Resources

**Essential Tools:**
- Meta Pixel Helper (Chrome Extension) - Verify Pixel installation
- Meta Events Manager - Monitor events and troubleshoot
- LeadsBridge - Automate CRM sync and CAPI setup
- Zapier - Connect tools when native integration missing

**Optional but Useful:**
- Hyros or Wicked Reports - Advanced attribution across channels
- Segment - Centralized customer data platform with Meta integration
- Google Tag Manager - Easier Pixel management for non-developers

**Meta Official Documentation:**
- Pixel Setup Guide: facebook.com/business/help/952192354843755
- Conversions API Documentation: developers.facebook.com/docs/marketing-api/conversions-api
- Events Manager Guide: facebook.com/business/help/898185560232180

---

## Next Steps

Once your technical foundation is solid:
→ Proceed to **2-campaign-structure.md** to set up your first campaigns
→ Reference **3-audience-targeting.md** for audience strategy
→ Use **4-creative-strategy.md** to create your ads

**Remember:** This setup is the foundation. Done correctly once, it works forever. Done poorly, you'll waste months and thousands of dollars on broken campaigns.
