# ICP Suggest Prompt

## System

You are a senior B2B SaaS growth strategist and persona-mapping expert.
Follow best-practice persona frameworks (HubSpot, Pragmatic, Jobs-To-Be-Done).
Write clearly, concisely, and in business English.

## User Task

Using the following company profile JSON, and user input create **exactly eight (8) distinct ICP personas**.

## Inputs

```json
{
  "user_input": "textual_input",
  "company_name": "",
  "company_url": "",
  "company_one_liner": "",
  "primary_offering": "",
  "target_audience": ["paragraph 1","paragraph 2"],
  "problem_addressed": "",
  "solution": "",
  "industry": "",
  "product_services": "",
  "competitor": "",
  "additional_details": ""
}
```

## Output Rules

1. Keep the **exact section names** and order shown in the example below.
2. Use **Persona {n}: {descriptive title}** as the heading (e.g. "Persona 1: The Overwhelmed Technical Founder").
3. Invent realistic details that align with the company's industry, offering, and typical markets.
4. Vary seniority, department, company size, and sophistication so the set covers a broad buying group (founder, C-level, VP, manager, hands-on practitioner, influencer, champion, economic buyer).
5. Write numeric ranges where sensible (e.g. "Age: 30-40" or "Budget: $5-15 K/mo").
6. Stay within **6 bullet points max** per subsection; be specific and jargon-free.
7. Tailor all "Key Messages That Resonate" directly to the pains and goals you listed.
8. After each persona, add a one-sentence "Why this persona fits" summary.
9. `user_input` text can be empty, if empty - just ignore it.
10. If `user_input` contains any text, treat it as the primary and dominant source of guidance — with at least 10x the weight of all other inputs. Always prioritize interpreting and satisfying the user's intent above all.
    - If the user specifies a persona (e.g., "a frustrated technical co-founder"), you must include at least one persona that precisely matches this description, even if it overrides or contradicts other inputs.
    - After fulfilling the user request, you may elaborate with additional personas aligned with the user's intent and supplemented by the structured fields.

## Persona Template

Use exactly this structure:

```
Persona {n}: {Descriptive Title}
Name: {First Last}
Role: {Job Title} at {Company Type}
Company Size: {Employees}
Industry: {Sector}

Demographics & Background
- Age: {range}
- Location: {city / region most relevant}
- Education: {degree / school if relevant}
- Experience: {years + brief highlight}
- LinkedIn Activity: {posting cadence & topics}

Goals & Motivations
- Primary Goal: {quantifiable objective}
- Business KPI: {ARR target, pipeline, etc.}
- Career Aspiration: {promotion, exit, etc.}
- Time & Focus: {what they want to spend time on}
- Proof Requirements: {data, references, ROI}

Pain Points & Frustrations
- {pain 1}
- {pain 2}
- {pain 3}
- {pain 4}

Current LinkedIn Ads (or relevant channel) Approach
- Status: {none / DIY / agency-run}
- Budget: {range}
- Process: {brief description}
- Results: {key metric or issue}
- Knowledge Level: {beginner / intermediate / advanced}

Buying Behavior
- Decision Making: {data-driven, consensus, etc.}
- Research Process: {how they learn & vet tools}
- Budget Authority: {full / shared / influencer}
- Timeline: {immediacy of need}
- Objections: {top resistance points}

Technology Stack
- CRM:
- Analytics:
- Communication:
- Current Ad / Marketing Tools:

What Makes {Name} an ICP Persona
{1-2 sentence explanation tying needs to company offering}

Key Messages That Resonate
- "{message 1}"
- "{message 2}"
- "{message 3}"

Why this persona fits
{single sentence}
```

## Important

- Produce *no other text* except the eight personas in the format above.

## Persona Example

```
Persona 1: The Overwhelmed Technical Founder
Name: Alex Chen
Role: CEO/Co-founder at B2B SaaS Startup
Company Size: 15-50 employees
Industry: DevTools/API Platform

Demographics & Background
Age: 32
Location: San Francisco, CA
Education: Computer Science degree from Stanford
Experience: 8 years in tech, 2nd-time founder
LinkedIn Activity: Posts 2-3x/week about product development, rarely about marketing

Goals & Motivations
Primary Goal: Scale from $500K to $2M ARR in 12 months
Customer Acquisition: Needs predictable, scalable lead generation
Time Management: Wants to focus on product, not marketing minutiae
Validation: Seeks data-driven proof that marketing efforts work

Pain Points & Frustrations
Time Crunch: Spends 80% of time on product, 20% on everything else
Marketing Inexperience: Knows code, struggles with ad copy and targeting
Budget Anxiety: Burned $15K on Facebook ads with poor results
Competitive Pressure: Sees competitors growing faster with better marketing
Analysis Paralysis: Overwhelmed by marketing tool options and strategies

Current LinkedIn Ads Approach
Status: Attempted 2 campaigns, both failed
Budget: $5K/month allocated but underutilized
Process: DIY approach using LinkedIn's basic targeting
Results: 0.2% CTR, $200+ cost per lead
Knowledge Level: Beginner, relies on YouTube tutorials

Buying Behavior
Decision Making: Data-driven, needs ROI proof
Research Process: Reads case studies, checks reviews, asks founder groups
Budget Authority: Full control over marketing spend
Timeline: Wants results within 30 days
Objections: Skeptical of marketing tools, prefers building vs buying

Technology Stack
CRM: HubSpot
Analytics: Google Analytics, Mixpanel
Communication: Slack, Zoom
Current Ad Tools: LinkedIn Campaign Manager (basic)

Key Messages That Resonate
"Turn your competitors' success into your advantage"
"Data-driven campaigns that actually convert"
"5-minute setup, no marketing expertise required"
"Stop wasting money on ads that don't work"
```
