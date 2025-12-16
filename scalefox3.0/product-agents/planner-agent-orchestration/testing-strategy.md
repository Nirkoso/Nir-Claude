# LinkedIn Testing Strategy Framework

## Core Testing Principles

1. **Test One Variable at a Time** (when possible)
2. **Equal Budget Split** across variants
3. **Minimum 7 Days** for significance
4. **Statistical Validation** before scaling

---

## Standard Test Matrix

### Concept Testing (Phase 1)
Test 3-6 distinct concepts based on:

**Test Variables:**
- Hook style (Problem-Solution, Testimonial, Data-Backed, etc.)
- Visual approach (Minimalist, Bold, UGC-style, etc.)
- Value proposition angle

**Example Matrix:**
```
Concept A: Problem-Solution Hook + Bold Colors + Efficiency Value
Concept B: Testimonial + Minimalist + Trust Value
Concept C: Data-Backed + Infographic + ROI Value
```

### Creative Testing (Phase 2)
Test optimizations on winning concepts:

**Test Variables:**
- Headline variations (3 versions)
- Visual styles (2-3 variants)
- CTA wording (2-3 options)

---

## Testing by Budget

### Small Budget ($1k-$1.5k)
- **Test:** 3 concepts max
- **Per variant:** $133-$166
- **Approach:** Simple A/B/C test

### Medium Budget ($1.5k-$3k)
- **Test:** 4-5 concepts
- **Per variant:** $180-$240
- **Approach:** Concept test + optimization test

### Large Budget ($3k-$5k)
- **Test:** 6 concepts
- **Per variant:** $250-$300
- **Approach:** Full matrix + refinement tests

---

## Sample Size Requirements

### For Statistical Significance (95% confidence)

**Minimum per variant:**
- 100 clicks OR
- 5 conversions OR
- $300 spend

**Recommended per variant:**
- 250 clicks AND
- 10 conversions AND
- $500 spend

**Reality:** Most tests need 7-10 days to reach these thresholds at typical LinkedIn volumes.

---

## Decision Criteria

### After Test Phase

**SCALE** if:
- CPL < Target CPL
- CTR > 0.8%
- Conversion Rate > 2%
- Trend is stable or improving

**OPTIMIZE** if:
- CPL is 100-150% of target
- CTR is 0.5-0.8%
- High clicks but low conversions

**PAUSE** if:
- CPL > 200% of target
- CTR < 0.5%
- Zero conversions after $300 spend

---

## Common Test Hypotheses

### Hook Effectiveness
**Hypothesis:** "Problem-Solution hooks will outperform testimonials for our ICP"

**Test Setup:**
- Variant A: Problem-Solution hook
- Variant B: Testimonial hook
- Same visual style, same CTA

**Measure:** CTR and CPL

---

### Visual Style Impact
**Hypothesis:** "Bold, colorful designs will drive higher engagement than minimalist"

**Test Setup:**
- Variant A: Bold colors, high contrast
- Variant B: Minimalist, clean design
- Same messaging, same hook

**Measure:** CTR and engagement rate

---

### Value Proposition Angle
**Hypothesis:** "ROI-focused messaging will convert better than efficiency-focused"

**Test Setup:**
- Variant A: "Save $50k annually"
- Variant B: "Save 20 hours per week"
- Same creative style

**Measure:** Conversion rate and CPL

---

## Test Analysis Framework

### Calculate Lift
```
Lift = (Variant B Metric - Variant A Metric) / Variant A Metric × 100%
```

**Example:**
- Variant A: 1.0% CTR
- Variant B: 1.3% CTR
- Lift: (1.3 - 1.0) / 1.0 = 30% improvement

### Determine Significance

**Quick Check:**
- Lift > 20% AND
- Min 7 days data AND
- Min 100 clicks per variant
→ Likely significant

**Statistical Test:**
Use two-proportion z-test (available in most analytics tools)
- p-value < 0.05 = significant

---

## Testing Mistakes to Avoid

❌ **Ending tests too early**
- Need minimum 7 days for day-of-week effects
- Need sufficient sample size

❌ **Testing too many variables**
- Can't determine what caused difference
- Dilutes budget across too many variants

❌ **Unequal budget allocation**
- Creates bias in results
- Can't fairly compare

❌ **Ignoring external factors**
- Holidays, industry events
- Platform changes
- Competitive activity

❌ **Not documenting learnings**
- Can't build on past tests
- Repeat same tests

---

## Sequential Testing Strategy

If budget is tight, test sequentially:

**Week 1-2:** Test 3 concepts
**Week 3-4:** Take winner, test 3 variations
**Week 5-6:** Scale final winner

**Trade-off:** Takes longer but more budget-efficient

---

## Test Documentation Template

```markdown
## Test #[Number]: [Test Name]

**Hypothesis:** [What we're testing and why]

**Setup:**
- Variant A: [Description]
- Variant B: [Description]
- Budget per variant: $XXX
- Duration: [dates]

**Results:**
| Variant | Impressions | Clicks | CTR | Conversions | CPL |
|---------|-------------|--------|-----|-------------|-----|
| A | | | | | |
| B | | | | | |

**Winner:** Variant [A/B]
**Lift:** [X]%
**Significant:** Yes/No

**Learning:** [Key takeaway in 1-2 sentences]

**Next Action:** [What to do with this learning]
```

---

## Quick Reference: Test Sizes

| Budget | Max Variants | Per Variant | Expected Conversions |
|--------|--------------|-------------|---------------------|
| $1,000 | 3 | $333 | 4-5 each |
| $1,500 | 3-4 | $375 | 5 each |
| $2,000 | 4 | $500 | 6-7 each |
| $3,000 | 5 | $600 | 8 each |
| $5,000 | 6 | $833 | 11 each |

*Based on $75 average LinkedIn B2B CPL
