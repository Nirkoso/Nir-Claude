# Lovable Prompt: GTM Playbook Page for ScaleFox.ai

## Project Context

I'm building a **GTM Playbook Display Page** for ScaleFox.ai, an AI-powered marketing automation platform that generates LinkedIn ad campaign playbooks for B2B startups. This page displays a comprehensive, actionable playbook that busy founders and marketing directors can use to launch campaigns in under 5 minutes.

**Target Users:** Busy founders and marketing directors at B2B startups who need to launch LinkedIn campaigns quickly and confidently.

**Core User Journey:** User lands on page → scans Quick Start section → copies top campaign brief → launches in LinkedIn Campaign Manager within 5 minutes.

## Design Aesthetic

Create a **modern, minimal, professional B2B SaaS aesthetic** with:
- **Style:** Clean, scannable, action-oriented (like Notion, Linear, or Stripe documentation)
- **Color Palette:**
  - Primary: Blues (#0066CC) for trust and credibility
  - Success/Growth: Greens (#00AA66) for metrics and positive results
  - Priority indicators: Red/orange for high priority, yellow for medium, blue for test
  - Backgrounds: White (#FFFFFF) with subtle grays (#F5F7FA) for cards
- **Typography:** Clean, professional sans-serif (system fonts or Inter-like). Hierarchy is critical.
- **Spacing:** Generous white space, lots of breathing room. This should feel organized, not cluttered.
- **Visual Style:** Card-based layout with subtle shadows, rounded corners (8px), clean borders

**Overall Vibe:** Premium, trustworthy, efficient. Think "executive dashboard" not "consumer app." Users should feel confident and in control.

## Page Structure & Layout

Create a single-page layout with these sections (in order):

### 1. Header Section (Sticky)
- **Company Name:** "TechFlow Analytics" (large, bold)
- **Metadata Row:** Display inline with subtle separators
  - Industry: "B2B SaaS - Marketing Analytics"
  - Budget: "$5K/month"
  - ICP: "Marketing Directors at $5-50M ARR companies"
- **Visual Style:** Clean white background, subtle bottom border, sticky on scroll
- **Content should be at the top of the page, no excessive padding**

### 2. Executive Summary (Prominent Card)
- **Layout:** Full-width card with subtle background color (#F5F7FA)
- **Content Structure:**
  - Competitive insight (2-3 sentences with key metrics highlighted)
  - Your competitive edge (2-3 bullet points)
  - Quick Start summary (expected results)
- **Visual Treatment:** Use bold text for key numbers (CTR percentages, costs). Make this scannable with short paragraphs.

### 3. Quick Start Section (Hero CTA Section)
- **Header:** "🚀 Quick Start: Launch This Week (15 Minutes)"
- **Layout:** Two-column grid on desktop, stacked on mobile
- **Each Campaign Card Shows:**
  - Campaign name (bold headline)
  - Budget per day (prominent)
  - "Why" statement (1-2 sentences explaining rationale)
  - Format, funnel stage, estimated CTR (inline badges or pills)
  - **Primary CTA Button:** "View Full Brief" (scrolls to that brief)
  - **Secondary CTA Button:** "Copy Campaign Settings" (copies targeting/setup)
- **Week 1 Summary Box Below Cards:**
  - Total budget, expected clicks, expected leads, cost per lead
  - Visual: Simple metrics display with icons

### 4. Campaign Briefs Section (6 Briefs Total)

**Each Brief is a Card Component with:**

#### Brief Header
- **Campaign Title** (large, bold)
- **Priority Badge:** Visual indicator
  - 🔥 High Priority (red/orange badge)
  - ⚡ Medium Priority (yellow badge)
  - 🧪 Test (blue badge)
- **Meta Tags (Inline Pills):**
  - Format: "Single Image" / "Carousel" / "Video"
  - Funnel Stage: "Top of Funnel" / "Middle" / "Bottom"
  - Expected CTR: "0.40-0.50%"

#### Brief Body (Progressive Disclosure)

**Default View (Always Visible):**
- One-sentence objective
- Target audience (1-2 lines)
- Value proposition (bold)
- Main hook (headline style)
- **CTA Buttons Row:**
  - "Copy Ad Copy" (copies Primary text + Headline + CTA)
  - "Copy Targeting" (copies targeting criteria)
  - "Expand Full Brief" (toggles accordion)

**Expandable Sections (Accordion/Collapsible):**

1. **JSON Brief (Collapsible)**
   - **Toggle:** "View Full JSON Brief" (collapsed by default)
   - Display the complete JSON in a code block with syntax highlighting
   - Add a "Copy JSON" button in the top-right corner

2. **Hook Variations (Collapsible)**
   - **Toggle:** "View 4 Hook Alternatives"
   - List all hook variations (Hook_var_1, Hook_var_2, etc.)
   - Each with a small "Copy" button

3. **Visual Brief for Designer (Collapsible)**
   - **Toggle:** "View Creative Brief for Designer"
   - Display visual requirements:
     - Image/video description
     - Dimensions
     - Color palette
     - Style notes
     - Composition guidelines
   - If carousel: Show slide-by-slide structure

4. **LinkedIn Campaign Setup (Collapsible)**
   - **Toggle:** "View LinkedIn Setup Instructions"
   - Display step-by-step setup:
     - Objective
     - Targeting criteria (formatted as copy-paste ready list)
     - Budget
     - Landing page
   - **"Copy All Settings" button** at bottom

5. **Ad Copy (Always Visible or Slightly Highlighted)**
   - Primary Text (with "Copy" button)
   - Headline (with "Copy" button)
   - CTA Button Text (with "Copy" button)
   - Make these easily accessible since they're used most

**Visual Card Design:**
- Each brief card has subtle shadow, rounded corners, white background
- Use horizontal dividers between sections
- Priority badge should be color-coded and prominent
- Collapsible sections should have smooth expand/collapse animations

### 5. Week 1 Plan (Checklist Section)

**Layout:** Timeline or step-by-step layout

**Day 1 Setup (Expandable)**
- Task list with checkboxes (non-functional, visual only for now)
- Time estimate for each task
- Links or references to which briefs to use

**Days 2-7: Monitor (Expandable)**
- Daily checklist items
- What to look for (delivery warnings, CTR tracking)
- Note: "Do NOT optimize yet—collect data only"

**End of Week 1: Success Check**
- Target metrics as checklist items
- Visual: Green checkmarks or badges
- "Next Steps" section below

### 6. Expected Results (Data Table)

**Table Layout:**
- Columns: Metric, Week 1, Week 2, Week 3, Week 4, Total
- Rows: Daily Budget, Total Clicks, Total Leads, Avg CTR, Cost/Lead
- **Visual Treatment:**
  - Zebra striping for readability
  - Bold the "Total" column
  - Use color coding for good/warning metrics (greens for good CTR, etc.)
- **Mobile:** Make table horizontally scrollable with sticky first column

### 7. Campaign Monitoring Checklist (Expandable Sections)

**Three sections (Daily, Weekly, Monthly):**
- Each is an expandable accordion
- Show time commitment in header (e.g., "Daily (5 minutes)")
- Checklist items (non-functional checkboxes for visual reference)

### 8. Quick Reference Table (All Briefs at a Glance)

**Table Layout:**
- Columns: Brief, Format, Priority, Week, Budget, CTR, Use Case
- **Interactive:** Clicking a row scrolls to that brief's card above
- **Visual Treatment:**
  - Priority column uses color-coded badges
  - CTR column uses subtle green highlighting
  - Compact, scannable design
- **Mobile:** Horizontally scrollable with sticky first column

### 9. Footer Section

**Competitive Insights Box (Subtle Card):**
- "Key Insights from Competitive Analysis"
- Three subsections:
  - What's working in your market
  - Your competitive advantages
  - Gaps in competitor approach
- Keep this concise (3-4 bullet points each)

**Final CTA:**
- "Next Step: Copy Brief #1 and Brief #2 into LinkedIn Campaign Manager and launch today."
- Buttons: "Jump to Brief #1" and "Jump to Brief #2"

**Powered By Footer:**
- "GTM Playbook powered by ScaleFox.ai | Based on analysis of 47 competitor LinkedIn ads"
- Small, subtle text at very bottom

## Technical Requirements

### Technologies & Components
- **Framework:** React + TypeScript + Vite
- **Styling:** Tailwind CSS
- **UI Components:** Use shadcn/ui components throughout:
  - `Accordion` for collapsible sections
  - `Card` for brief cards and sections
  - `Table` for data tables
  - `Button` for CTAs (primary and secondary variants)
  - `Badge` for priority indicators and meta tags
  - `Tabs` (optional, if you think it improves navigation)

### Key Functionality

1. **Copy-to-Clipboard:**
   - Implement copy-to-clipboard for:
     - Ad copy (Primary text, Headline, CTA)
     - JSON briefs
     - Targeting criteria
     - Campaign setup instructions
     - Hook variations
   - Show a brief "Copied!" toast notification after each copy

2. **Smooth Scrolling & Jump Links:**
   - Quick Start campaign buttons scroll smoothly to respective briefs
   - Quick Reference table rows scroll to briefs
   - Footer CTA buttons scroll to top briefs
   - Optional: Floating "Back to Top" button

3. **Collapsible/Expandable Sections:**
   - Use shadcn/ui Accordion component
   - Smooth animations (300ms ease)
   - Icons to indicate expand/collapse state (chevron down/up)

4. **Responsive Design:**
   - **Mobile-first approach**
   - **Breakpoints:**
     - Mobile (<768px): Single column, stacked cards, horizontal scroll tables
     - Tablet (768px-1024px): Two-column grid where appropriate
     - Desktop (>1024px): Full layout with optimal spacing
   - **Sticky header** on all breakpoints
   - **Touch-friendly** buttons and interactive elements on mobile (48px min height)

5. **Print-Friendly CSS:**
   - Add print stylesheet that:
     - Expands all accordion sections
     - Removes sticky positioning
     - Ensures proper page breaks
     - Uses print-friendly colors (no dark backgrounds)

### Content to Use

Use the content from **Brief #1: The ROI Proof Machine** as the example for the first campaign brief card. Here's the data:

**Brief #1 Content:**
- **Priority:** 🔥 Launch Week 1
- **Format:** Single Image
- **Funnel:** Top of Funnel
- **Est. CTR:** 0.40-0.50%
- **Objective:** "Drive demo bookings by showcasing concrete ROI results"
- **Audience:** "Marketing Directors at B2B SaaS ($10M-50M ARR), using 3+ tools, frustrated with unclear attribution"
- **Value Prop:** "See your full-funnel marketing attribution in one dashboard—no spreadsheets, no guessing"
- **Main Hook:** "Marketing teams using TechFlow see 3.2x pipeline growth in their first quarter"
- **Hook Variations:**
  - "Prove marketing ROI in 24 hours, not 6 months"
  - "How B2B marketers are finally showing the C-suite where revenue comes from"
  - "Stop guessing which campaigns work—see your attribution in real-time"
  - "The dashboard that turns marketing from cost center to revenue driver"
- **Ad Copy:**
  - Primary Text: "TechFlow connects your entire marketing stack and shows exactly which campaigns drive revenue. No more spreadsheet gymnastics or guessing. See your full-funnel attribution in one dashboard."
  - Headline: "See your marketing ROI"
  - CTA: "Learn More"
- **Visual Brief:** Clean dashboard screenshot, upward-trending graph, 1200x627px, blues/greens, minimal text
- **LinkedIn Setup:**
  - Objective: Website visits
  - Targeting: Job Titles: Marketing Director, VP Marketing, Head of Marketing | Company Size: 51-500 employees | Industries: Computer Software, IT Services, Marketing
  - Budget: $15/day
  - Landing Page: ROI calculator

For the other 5 briefs, you can use placeholder content or simplified versions. The key is to establish the **component structure and UX patterns** so I can easily populate the rest.

## Design & UX Priorities

1. **Scannable First:** Use visual hierarchy (size, weight, color) to guide users to high-priority content
2. **Progressive Disclosure:** Don't overwhelm—show essentials, hide details until needed
3. **Action-Oriented:** Every section should have clear CTAs (copy, expand, jump to)
4. **Fast Navigation:** Users should be able to jump to any section quickly
5. **Mobile-Optimized:** This will be checked on the go—make it work perfectly on mobile
6. **Copy-Paste Ready:** Reduce friction—users should be able to copy and launch in minutes

## Questions for Clarification

Ask me any questions you need to fully understand:
1. The visual hierarchy and emphasis (what should stand out most?)
2. The navigation pattern (tabs vs. scrolling, sticky nav?)
3. Any interactive features I haven't specified (filtering, sorting, favoriting briefs?)
4. Color palette refinements or brand guidelines
5. Any specific shadcn/ui components you think would work well that I haven't mentioned

## Success Criteria

When complete, the page should:
- ✅ Display all 6 campaign briefs in scannable, card-based layout
- ✅ Implement copy-to-clipboard for all key content
- ✅ Use progressive disclosure (accordions) to avoid overwhelming users
- ✅ Work flawlessly on mobile, tablet, and desktop
- ✅ Have clear visual priority indicators (badges, colors)
- ✅ Enable a founder to copy Brief #1 and launch a campaign in under 5 minutes
- ✅ Be print-friendly for offline reference
- ✅ Use shadcn/ui and Tailwind for a polished, modern B2B SaaS aesthetic

## Next Steps

Please:
1. Review this prompt and ask any clarifying questions
2. Outline your implementation plan (components, layout approach, state management)
3. Once I approve the plan, implement the page starting with the header, executive summary, and Quick Start section
4. Then we'll iterate on the campaign brief cards and remaining sections

---

**Note:** Focus on creating a **reusable BriefCard component** that can handle all 6 briefs with different data. This will make it easy to scale and maintain.