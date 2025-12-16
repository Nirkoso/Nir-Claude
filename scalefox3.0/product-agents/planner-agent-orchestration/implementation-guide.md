# Planner Agent - Implementation Guide

## How It Works

### 1. Agent Receives Inputs
```json
{
  "company_info": {
    "company_name": "Acme Workflow",
    "primary_offering": "Proposal automation software",
    "problem_addressed": "Manual proposal process takes too long",
    "solution": "Automates entire quote-to-close workflow",
    "target_audience": "VP Marketing, Growth Marketers at mid-market B2B"
  },
  "icp_data": {
    "personas": [
      {
        "name": "Sarah - VP Marketing",
        "pains": ["Manual processes", "Long sales cycles"],
        "goals": ["Increase pipeline", "Improve efficiency"],
        "linkedin_targeting": {
          "job_titles": ["VP of Marketing", "CMO"],
          "seniorities": ["Director", "VP", "CXO"],
          "company_sizes": ["201-500", "501-1000"]
        }
      }
    ]
  },
  "budget": 2500
}
```

### 2. Agent Asks for Budget (if not provided)
```
User: Help me plan my LinkedIn campaign

Agent: I'll create a campaign plan for Acme Workflow. 
What's your monthly budget? ($1k-$5k range)

User: $2,500

Agent: [Generates plan...]
```

### 3. Agent References LinkedIn Playbook

**The agent internally reads:**
```
/linkedin-playbook/campaign-structure.md
/linkedin-playbook/budget-allocation.md
/linkedin-playbook/testing-strategy.md
/linkedin-playbook/best-practices.md
```

**It uses these to:**
- Determine if 2-week or monthly plan (based on budget)
- Calculate exact budget splits
- Structure test matrix
- Set realistic benchmarks

### 4. Agent Outputs Complete Plan

See `/linkedin-playbook/example-plan.md` for format.

---

## File Structure

```
/
├── planner-agent-prompt.md          # Main agent prompt
└── linkedin-playbook/
    ├── campaign-structure.md         # Phase frameworks
    ├── budget-allocation.md          # Budget formulas
    ├── testing-strategy.md           # Test setups
    ├── best-practices.md             # LinkedIn tips
    └── example-plan.md               # Reference output
```

---

## Agent Behavior

### What It Does Automatically
✅ Determines plan duration (2-week vs monthly) based on budget
✅ Applies budget allocation formulas
✅ Creates test matrix based on ICP
✅ Sets realistic CPL targets based on industry
✅ Structures phases with specific dates
✅ Includes all necessary details for execution

### What It Asks User
❓ Budget (if not provided)
❓ Preferred start date (defaults to "next Monday")
❓ Any specific constraints or preferences

### What It Doesn't Do
❌ Create the actual ads (that's Creative Prompter's job)
❌ Set up campaigns in LinkedIn (that's Publisher's job)
❌ Track performance (that's Monitor's job)
❌ Analyze results (that's Analyst's job)

---

## Integration with Other Agents

### Inputs From:
- **Discovery Agent** → Company info
- **ICP Agent** → Persona data with LinkedIn targeting
- **Insight Agent** → (Optional) Market insights for hypothesis generation

### Outputs To:
- **Brief Maker** → Test concepts needed (e.g., "Create 3 concepts: Problem-Solution, Testimonial, Data-Backed")
- **Publisher** → Campaign structure for setup
- **Monitor Agent** → Success metrics and milestones to track

---

## Conversation Examples

### Example 1: Simple Request
```
User: Create a campaign plan for us

Agent: [References company_info and icp_data]
What's your budget for this campaign? ($1k-$5k)

User: $3,000

Agent: [Generates complete monthly plan using playbook frameworks]

# LinkedIn Campaign Plan: LeadGen-VP_Marketing-Feb25
**Budget:** $3,000 | **Duration:** 1 month | **Dates:** Feb 1 - Feb 29

[Full structured plan...]
```

### Example 2: With Context
```
User: I have $1,500 to test LinkedIn ads for our VPs

Agent: [Recognizes $1,500 = 2-week sprint structure]

# LinkedIn Campaign Plan: LeadGen-VP_Marketing-Feb25
**Budget:** $1,500 | **Duration:** 2 weeks | **Dates:** Feb 1 - Feb 14

## Campaign Structure

### Phase 1: Test (Days 1-7) - $600
### Phase 2: Optimize (Days 8-14) - $825
Reserve: $75

[Continues with details...]
```

### Example 3: Constraint Handling
```
User: Plan a campaign but we can't launch until March

Agent: [Adjusts dates in plan]

**Dates:** March 1 - March 31, 2025

[Rest of plan with March dates...]
```

---

## Budget-Based Behavior

### $1,000-$1,999 → 2-Week Sprint
- 2 phases (Test → Optimize)
- 3 test concepts max
- Focused, lean approach

### $2,000-$5,000 → Monthly Plan
- 3 phases (Test → Optimize → Scale)
- 4-6 test concepts
- Full optimization cycle

### Edge Cases
- **<$1,000:** Agent warns this is below minimum for meaningful results
- **>$5,000:** Agent suggests breaking into multiple campaigns or extending timeline

---

## Customization Points

### Easy to Adjust:
1. **Budget thresholds** (2-week vs monthly cutoff)
2. **Phase ratios** (test/optimize/scale percentages)
3. **CPL benchmarks** (by industry)
4. **Test matrix size** (3-6 concepts)

### Files to Edit:
- **Thresholds:** `planner-agent-prompt.md` and `campaign-structure.md`
- **Formulas:** `budget-allocation.md`
- **Benchmarks:** `best-practices.md`

---

## Quality Checks

The agent should always:
- [ ] Budget allocations sum to total budget
- [ ] Include specific LinkedIn targeting from ICP
- [ ] Set realistic CPL targets for industry
- [ ] Structure clear phase transitions
- [ ] Define specific success criteria
- [ ] Provide actionable next steps
- [ ] Reference playbook frameworks

---

## Testing the Agent

### Test Inputs:

**Minimal:**
```json
{
  "company_info": { "company_name": "Test Co", "primary_offering": "B2B SaaS" },
  "icp_data": { "personas": [{"linkedin_targeting": {...}}] },
  "budget": 2000
}
```

**Expected Output:**
- Complete plan in specified format
- Budget math adds up
- Specific dates provided
- LinkedIn targeting included

---

## Troubleshooting

### Issue: Agent asks for more info
**Cause:** Missing required fields in inputs
**Fix:** Ensure company_info has: name, offering, problem, solution

### Issue: Budget doesn't add up
**Cause:** Rounding errors in allocation
**Fix:** Agent should round to nearest $5 and adjust reserve

### Issue: Unrealistic CPL targets
**Cause:** Not referencing industry benchmarks
**Fix:** Check `best-practices.md` CPL ranges are loaded

### Issue: Plan too generic
**Cause:** Not using ICP data effectively
**Fix:** Ensure agent pulls specific job titles and criteria from ICP

---

## Future Enhancements

1. **Dynamic Phase Ratios** - Adjust based on confidence level from Insight Agent
2. **Seasonal Adjustments** - Account for holidays, quarters, industry events
3. **Multi-Persona Weighting** - More sophisticated persona priority scoring
4. **Historical Learning** - Reference past campaign performance for targets
5. **Platform Expansion** - Add Meta/Google playbooks

---

## Quick Start

1. **Load the prompt:** Use `planner-agent-prompt.md` as system prompt
2. **Make playbook accessible:** Ensure agent can read `/linkedin-playbook/*.md` files
3. **Provide inputs:** Company info + ICP data + budget
4. **Get plan:** Agent outputs complete structured plan
5. **Execute:** Hand off to Brief Maker → Creative Prompter → Publisher

**That's it!** The planner is designed to be autonomous and require minimal user input.
