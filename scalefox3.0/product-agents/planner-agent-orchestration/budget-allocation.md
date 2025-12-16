# LinkedIn Budget Allocation Framework

## Core Allocation Formula

### 2-Week Sprint ($1k-$2k)
```
Testing:    40% ($400-$800)
Scaling:    55% ($550-$1,100)
Reserve:    5%  ($50-$100)
```

### Monthly Campaign ($2k-$5k)
```
Testing:    30% ($600-$1,500)
Optimizing: 35% ($700-$1,750)
Scaling:    30% ($600-$1,500)
Reserve:    5%  ($100-$250)
```

---

## Persona-Level Allocation

When targeting multiple personas, allocate by priority:

### Priority Scoring
Score each persona (1-5) based on:
- **Intent Signals** (1-5): High intent = 5
- **Market Size** (1-5): Large addressable market = 5
- **Strategic Fit** (1-5): Core ICP = 5

**Total Score:** Sum of above (max 15)

### Budget Distribution Formula
```
Persona Budget = (Persona Score / Total Scores) × Phase Budget
```

**Example:**
- Persona A (Score: 13) = (13/35) × $1,000 = $371
- Persona B (Score: 12) = (12/35) × $1,000 = $343
- Persona C (Score: 10) = (10/35) × $1,000 = $286

---

## Test Phase Allocation

**Rule:** Equal budget per test variant

**Formula:**
```
Budget per Ad Set = Test Budget / Number of Test Variants
```

**Example:**
- Test Budget: $800
- Testing 4 concepts
- Per Ad Set: $800 / 4 = $200

**Minimum per ad set:** $150 (to reach statistical significance)

---

## Scale Phase Allocation

**Rule:** Weight by performance

**Formula:**
```
Ad Set Budget = (Ad Set Performance Score / Total Scores) × Scale Budget
```

**Performance Score Calculation:**
```
Score = (Conversions × 10) + (CTR × 100) - (CPL / Target CPL × 50)
```

Higher score = more budget

---

## Daily Pacing

### Even Pacing (Default)
```
Daily Budget = Total Phase Budget / Phase Days
```

### Front-Loaded (For Testing)
```
Week 1: 60% of phase budget
Week 2+: 40% of phase budget
```

### Back-Loaded (For Scaling)
```
First Half: 40% of phase budget
Second Half: 60% of phase budget
```

---

## Minimum Budget Requirements

**Per Ad Set:**
- Absolute minimum: $150
- Recommended: $200-300
- Optimal: $500+

**Why:** Need ~100 conversions for statistical significance
- Typical LinkedIn CPL: $75
- $150 budget ÷ $75 CPL = 2 conversions (not enough)
- $500 budget ÷ $75 CPL = 6-7 conversions (marginal)

**Reality Check:**
If total budget / number of variants < $150, reduce variants.

---

## Budget Reallocation Triggers

**Increase Budget When:**
- CPL 30%+ below target
- Conversion rate >3%
- Daily budget spent by 2 PM

**Decrease Budget When:**
- CPL 50%+ above target
- CTR <0.5%
- Frequency >5

**Pause When:**
- CPL 100%+ above target
- Zero conversions after $300 spend
- Creative fatigue detected

---

## Reserve Budget Usage

Use reserve for:

1. **Winning Concept Boost** (60%)
   - Add to clearly winning variants
   - Only after 7+ days data

2. **Emergency Optimizations** (30%)
   - Quick creative refresh
   - Audience expansion
   - Bid adjustments

3. **True Reserve** (10%)
   - Hold until campaign end
   - Use only if clear opportunity

---

## Budget Efficiency Benchmarks

**Good Performance:**
- 80%+ of budget spent
- CPL within 20% of target
- Even daily pacing

**Poor Performance:**
- <60% budget spent (delivery issues)
- Erratic daily spend
- Budget exhausted early in day

---

## Quick Reference: Budget Splits by Total

| Total | Test | Optimize | Scale | Reserve |
|-------|------|----------|-------|---------|
| $1,000 | $400 | - | $550 | $50 |
| $1,500 | $450 | - | $975 | $75 |
| $2,000 | $600 | $700 | $600 | $100 |
| $3,000 | $900 | $1,050 | $900 | $150 |
| $5,000 | $1,500 | $1,750 | $1,500 | $250 |
