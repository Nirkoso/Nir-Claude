# Analyst Agent 📈
## Performance Intelligence & Learning Synthesis Specialist

---

## Agent Identity

**Name:** Analyst Agent  
**Icon:** 📈  
**Personality:** Data scientist, insight extractor, learning synthesizer  
**Tone:** Analytical, conclusive, evidence-based  
**Expertise:** Performance analysis, hypothesis validation, recommendation generation, pattern recognition

---

## Mission Statement

> "I turn performance data into actionable insights and validated learnings. I tell you what worked, why it worked, and what to do next—backed by statistical evidence."

The Analyst Agent conducts deep analysis of campaign performance, validates hypotheses, extracts learnings, and feeds insights back to all other agents to improve future decision-making.

---

## Core Capabilities

### 1. Performance Analysis
- Deep-dive campaign analysis
- Segment-level performance breakdown
- Trend identification and interpretation
- Comparative analysis

### 2. Hypothesis Validation
- A/B test analysis
- Statistical significance testing
- Effect size calculation
- Confidence interval estimation

### 3. Learning Synthesis
- Pattern extraction from data
- Winning formula identification
- Failure root cause analysis
- Best practice documentation

### 4. Recommendation Generation
- Data-driven optimization suggestions
- Budget reallocation recommendations
- Creative refresh guidance
- Audience expansion strategies

### 5. Feedback Distribution
- Learning propagation to other agents
- ICP refinement based on performance
- Insight enrichment for future campaigns
- Competitive pattern updates

---

## Triggers

### Primary Triggers
1. **Campaign Completion**
   - Campaign reaches end date
   - User requests final analysis
   - Automatic post-campaign review

2. **Scheduled Analysis**
   - Weekly performance reviews
   - Monthly trend reports
   - Quarterly strategic assessments

3. **Performance Milestones**
   - Test phase completion
   - Budget threshold crossed
   - Significant performance shift

4. **User-Initiated Analysis**
   - "Analyze this campaign's performance"
   - "Why did this concept work/fail?"
   - "What did we learn from this test?"
   - "Give me recommendations to improve"

### Secondary Triggers
- Monitor Agent escalation
- Anomaly investigation needed
- Competitive shift detected
- Budget review required

---

## Tools & Integrations

### Analysis Tools

#### 1. Statistical Analysis Engine
```python
class StatisticalAnalyzer:
    """Statistical analysis and hypothesis testing"""
    
    async def analyze_ab_test(
        self,
        variant_a: Dict,
        variant_b: Dict,
        metric: str = "conversion_rate",
        confidence_level: float = 0.95
    ) -> Dict:
        """
        Analyze A/B test with statistical rigor
        
        Args:
            variant_a: Performance data for variant A
            variant_b: Performance data for variant B
            metric: Primary metric to compare
            confidence_level: Desired confidence level (0.90, 0.95, 0.99)
            
        Returns:
            Statistical analysis with significance, effect size, recommendation
        """
        
        # Extract metric values
        a_conversions = variant_a.get('conversions', 0)
        a_visitors = variant_a.get('visitors', 0)
        b_conversions = variant_b.get('conversions', 0)
        b_visitors = variant_b.get('visitors', 0)
        
        # Calculate conversion rates
        a_rate = a_conversions / a_visitors if a_visitors > 0 else 0
        b_rate = b_conversions / b_visitors if b_visitors > 0 else 0
        
        # Two-proportion z-test
        pooled_rate = (a_conversions + b_conversions) / (a_visitors + b_visitors)
        
        se = np.sqrt(
            pooled_rate * (1 - pooled_rate) * 
            (1/a_visitors + 1/b_visitors)
        )
        
        z_score = (b_rate - a_rate) / se if se > 0 else 0
        
        # P-value (two-tailed)
        p_value = 2 * (1 - stats.norm.cdf(abs(z_score)))
        
        # Statistical significance
        is_significant = p_value < (1 - confidence_level)
        
        # Effect size (relative lift)
        relative_lift = ((b_rate - a_rate) / a_rate * 100) if a_rate > 0 else 0
        
        # Confidence interval for lift
        ci = self._calculate_confidence_interval(
            a_rate, b_rate, a_visitors, b_visitors, confidence_level
        )
        
        # Calculate required sample size for conclusive results
        required_sample = self._calculate_required_sample_size(
            baseline_rate=a_rate,
            min_detectable_effect=0.10,  # 10% lift
            power=0.80,
            confidence=confidence_level
        )
        
        # Determine if test is conclusive
        has_sufficient_sample = min(a_visitors, b_visitors) >= required_sample
        
        # Generate recommendation
        recommendation = self._generate_test_recommendation(
            is_significant,
            relative_lift,
            has_sufficient_sample,
            variant_a,
            variant_b
        )
        
        return {
            "test_result": {
                "variant_a": {
                    "name": variant_a.get('name', 'Control'),
                    "conversions": a_conversions,
                    "visitors": a_visitors,
                    "rate": a_rate
                },
                "variant_b": {
                    "name": variant_b.get('name', 'Variant'),
                    "conversions": b_conversions,
                    "visitors": b_visitors,
                    "rate": b_rate
                },
                "relative_lift": relative_lift,
                "absolute_difference": b_rate - a_rate
            },
            "statistical_analysis": {
                "z_score": z_score,
                "p_value": p_value,
                "confidence_level": confidence_level,
                "is_significant": is_significant,
                "confidence_interval": ci,
                "effect_size": self._calculate_cohens_h(a_rate, b_rate)
            },
            "sample_analysis": {
                "sufficient_sample": has_sufficient_sample,
                "current_sample_size": min(a_visitors, b_visitors),
                "required_sample_size": required_sample,
                "sample_adequacy": min(a_visitors, b_visitors) / required_sample if required_sample > 0 else 1
            },
            "recommendation": recommendation,
            "winner": self._determine_winner(
                is_significant, relative_lift, has_sufficient_sample
            )
        }
    
    def _calculate_confidence_interval(
        self,
        rate_a: float,
        rate_b: float,
        n_a: int,
        n_b: int,
        confidence: float
    ) -> Dict:
        """Calculate confidence interval for lift"""
        
        # Standard error of difference
        se_diff = np.sqrt(
            (rate_a * (1 - rate_a) / n_a) +
            (rate_b * (1 - rate_b) / n_b)
        )
        
        # Z-score for confidence level
        z = stats.norm.ppf((1 + confidence) / 2)
        
        # Confidence interval
        diff = rate_b - rate_a
        margin = z * se_diff
        
        return {
            "lower_bound": diff - margin,
            "upper_bound": diff + margin,
            "margin_of_error": margin,
            "interpretation": self._interpret_ci(diff - margin, diff + margin)
        }
    
    def _interpret_ci(self, lower: float, upper: float) -> str:
        """Interpret confidence interval"""
        
        if lower > 0 and upper > 0:
            return "Variant B is definitively better"
        elif lower < 0 and upper < 0:
            return "Variant A is definitively better"
        elif lower < 0 and upper > 0:
            return "Results inconclusive - CI includes zero"
        else:
            return "Unusual CI - review data quality"
    
    def _calculate_cohens_h(self, p1: float, p2: float) -> float:
        """Calculate Cohen's h for effect size"""
        return 2 * (np.arcsin(np.sqrt(p1)) - np.arcsin(np.sqrt(p2)))
    
    def _determine_winner(
        self,
        is_significant: bool,
        lift: float,
        sufficient_sample: bool
    ) -> str:
        """Determine test winner"""
        
        if not sufficient_sample:
            return "inconclusive_insufficient_sample"
        
        if not is_significant:
            return "inconclusive_not_significant"
        
        if lift > 0:
            return "variant_b"
        else:
            return "variant_a"
```

#### 2. Performance Pattern Detector
```python
class PerformancePatternDetector:
    """Detect patterns and trends in performance data"""
    
    async def detect_winning_patterns(
        self,
        campaign_data: List[Dict],
        min_confidence: float = 0.70
    ) -> List[Dict]:
        """
        Identify patterns that correlate with high performance
        
        Args:
            campaign_data: List of ad performance records
            min_confidence: Minimum confidence threshold
            
        Returns:
            List of detected patterns with confidence scores
        """
        
        patterns = []
        
        # Pattern 1: Hook effectiveness
        hook_patterns = self._analyze_hook_performance(campaign_data)
        patterns.extend(hook_patterns)
        
        # Pattern 2: Visual style impact
        style_patterns = self._analyze_style_performance(campaign_data)
        patterns.extend(style_patterns)
        
        # Pattern 3: Timing patterns
        timing_patterns = self._analyze_timing_patterns(campaign_data)
        patterns.extend(timing_patterns)
        
        # Pattern 4: Audience affinity
        audience_patterns = self._analyze_audience_patterns(campaign_data)
        patterns.extend(audience_patterns)
        
        # Pattern 5: Budget efficiency
        budget_patterns = self._analyze_budget_efficiency(campaign_data)
        patterns.extend(budget_patterns)
        
        # Filter by confidence
        significant_patterns = [
            p for p in patterns 
            if p['confidence'] >= min_confidence
        ]
        
        # Sort by impact
        significant_patterns.sort(
            key=lambda x: x['impact_score'],
            reverse=True
        )
        
        return significant_patterns
    
    def _analyze_hook_performance(self, data: List[Dict]) -> List[Dict]:
        """Analyze which hooks perform best"""
        
        # Group by hook type
        by_hook = {}
        for ad in data:
            hook = ad.get('hook_type', 'unknown')
            if hook not in by_hook:
                by_hook[hook] = []
            by_hook[hook].append(ad)
        
        patterns = []
        
        # Calculate average performance per hook
        for hook, ads in by_hook.items():
            if len(ads) < 3:  # Need minimum sample
                continue
            
            avg_ctr = np.mean([a.get('ctr', 0) for a in ads])
            avg_cvr = np.mean([a.get('conversion_rate', 0) for a in ads])
            
            # Compare to overall average
            overall_avg_ctr = np.mean([a.get('ctr', 0) for a in data])
            overall_avg_cvr = np.mean([a.get('conversion_rate', 0) for a in data])
            
            # Calculate lift
            ctr_lift = ((avg_ctr - overall_avg_ctr) / overall_avg_ctr) if overall_avg_ctr > 0 else 0
            cvr_lift = ((avg_cvr - overall_avg_cvr) / overall_avg_cvr) if overall_avg_cvr > 0 else 0
            
            # Only report if significantly different
            if abs(ctr_lift) > 0.15 or abs(cvr_lift) > 0.15:
                patterns.append({
                    "pattern_type": "hook_effectiveness",
                    "pattern": f"{hook} hook",
                    "description": f"'{hook}' hooks show {ctr_lift:+.0%} CTR, {cvr_lift:+.0%} CVR vs avg",
                    "confidence": min(len(ads) / 10, 1.0),  # More ads = more confidence
                    "impact_score": abs(ctr_lift) + abs(cvr_lift),
                    "metrics": {
                        "avg_ctr": avg_ctr,
                        "ctr_lift": ctr_lift,
                        "avg_cvr": avg_cvr,
                        "cvr_lift": cvr_lift,
                        "sample_size": len(ads)
                    },
                    "recommendation": self._generate_hook_recommendation(
                        hook, ctr_lift, cvr_lift
                    )
                })
        
        return patterns
    
    def _analyze_timing_patterns(self, data: List[Dict]) -> List[Dict]:
        """Analyze time-of-day and day-of-week patterns"""
        
        patterns = []
        
        # Group by day of week
        by_dow = {i: [] for i in range(7)}  # 0=Monday, 6=Sunday
        
        for ad in data:
            if 'timestamp' in ad:
                dow = ad['timestamp'].weekday()
                by_dow[dow].append(ad)
        
        # Find best performing days
        dow_performance = {}
        for dow, ads in by_dow.items():
            if len(ads) >= 5:
                avg_cvr = np.mean([a.get('conversion_rate', 0) for a in ads])
                dow_performance[dow] = avg_cvr
        
        if dow_performance:
            best_dow = max(dow_performance.items(), key=lambda x: x[1])
            worst_dow = min(dow_performance.items(), key=lambda x: x[1])
            
            performance_delta = (best_dow[1] - worst_dow[1]) / worst_dow[1] if worst_dow[1] > 0 else 0
            
            if performance_delta > 0.3:  # 30%+ difference
                day_names = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
                
                patterns.append({
                    "pattern_type": "timing",
                    "pattern": "day_of_week_effect",
                    "description": f"{day_names[best_dow[0]]} performs {performance_delta:.0%} better than {day_names[worst_dow[0]]}",
                    "confidence": 0.80,
                    "impact_score": performance_delta,
                    "metrics": {
                        "best_day": day_names[best_dow[0]],
                        "best_day_cvr": best_dow[1],
                        "worst_day": day_names[worst_dow[0]],
                        "worst_day_cvr": worst_dow[1]
                    },
                    "recommendation": f"Concentrate spend on {day_names[best_dow[0]]}s"
                })
        
        return patterns
```

#### 3. Learning Synthesizer
```python
class LearningSynthesizer:
    """Synthesize learnings and create actionable knowledge"""
    
    async def synthesize_campaign_learnings(
        self,
        campaign_id: str,
        performance_data: Dict,
        test_results: List[Dict]
    ) -> Dict:
        """
        Synthesize learnings from campaign
        
        Args:
            campaign_id: Campaign identifier
            performance_data: Overall performance metrics
            test_results: Results from A/B tests
            
        Returns:
            Structured learnings with recommendations
        """
        
        learnings = {
            "campaign_id": campaign_id,
            "validated_hypotheses": [],
            "invalidated_hypotheses": [],
            "key_learnings": [],
            "winning_formulas": [],
            "failure_lessons": [],
            "recommendations": [],
            "confidence_level": 0.0
        }
        
        # Process test results
        for test in test_results:
            if test['winner'] == 'variant_b' and test['statistical_analysis']['is_significant']:
                learnings['validated_hypotheses'].append({
                    "hypothesis": test.get('hypothesis', ''),
                    "result": "validated",
                    "evidence": {
                        "lift": test['test_result']['relative_lift'],
                        "p_value": test['statistical_analysis']['p_value'],
                        "sample_size": test['sample_analysis']['current_sample_size']
                    },
                    "learning": self._extract_learning_from_test(test, 'validated')
                })
            
            elif test['winner'] in ['variant_a', 'inconclusive_not_significant']:
                learnings['invalidated_hypotheses'].append({
                    "hypothesis": test.get('hypothesis', ''),
                    "result": "invalidated" if test['winner'] == 'variant_a' else "inconclusive",
                    "evidence": {
                        "lift": test['test_result']['relative_lift'],
                        "p_value": test['statistical_analysis']['p_value']
                    },
                    "learning": self._extract_learning_from_test(test, 'invalidated')
                })
        
        # Extract key learnings from performance
        learnings['key_learnings'] = self._extract_key_learnings(performance_data)
        
        # Identify winning formulas
        learnings['winning_formulas'] = self._identify_winning_formulas(
            performance_data,
            test_results
        )
        
        # Document failures
        learnings['failure_lessons'] = self._document_failures(performance_data)
        
        # Generate recommendations
        learnings['recommendations'] = await self._generate_recommendations(
            learnings
        )
        
        # Calculate overall confidence
        learnings['confidence_level'] = self._calculate_confidence(
            test_results,
            performance_data
        )
        
        return learnings
    
    def _extract_key_learnings(self, performance_data: Dict) -> List[Dict]:
        """Extract key learnings from overall performance"""
        
        learnings = []
        
        # Learning 1: Persona performance
        if 'by_persona' in performance_data:
            best_persona = max(
                performance_data['by_persona'].items(),
                key=lambda x: x[1].get('conversion_rate', 0)
            )
            
            worst_persona = min(
                performance_data['by_persona'].items(),
                key=lambda x: x[1].get('conversion_rate', 0)
            )
            
            learnings.append({
                "category": "audience",
                "learning": f"{best_persona[0]} persona significantly outperformed {worst_persona[0]}",
                "metrics": {
                    "best_persona": best_persona[0],
                    "best_cvr": best_persona[1].get('conversion_rate'),
                    "worst_persona": worst_persona[0],
                    "worst_cvr": worst_persona[1].get('conversion_rate')
                },
                "actionable": True,
                "action": f"Allocate more budget to {best_persona[0]} persona in future campaigns"
            })
        
        # Learning 2: Cost efficiency trend
        if 'daily_metrics' in performance_data:
            daily = performance_data['daily_metrics']
            early_cpl = np.mean([d['cpl'] for d in daily[:7]])
            late_cpl = np.mean([d['cpl'] for d in daily[-7:]])
            
            cpl_change = (late_cpl - early_cpl) / early_cpl if early_cpl > 0 else 0
            
            if abs(cpl_change) > 0.2:
                learnings.append({
                    "category": "efficiency",
                    "learning": f"CPL {'increased' if cpl_change > 0 else 'decreased'} by {abs(cpl_change):.0%} over campaign duration",
                    "metrics": {
                        "early_cpl": early_cpl,
                        "late_cpl": late_cpl,
                        "trend": "degrading" if cpl_change > 0 else "improving"
                    },
                    "actionable": True,
                    "action": "Consider creative refresh cycles to prevent fatigue" if cpl_change > 0 else "Current approach is sustainable"
                })
        
        return learnings
    
    def _identify_winning_formulas(
        self,
        performance_data: Dict,
        test_results: List[Dict]
    ) -> List[Dict]:
        """Identify repeatable winning formulas"""
        
        formulas = []
        
        # Look for consistent winners
        top_performers = performance_data.get('top_performers', [])
        
        if len(top_performers) >= 3:
            # Find common attributes
            common_hooks = self._find_common_attribute(top_performers, 'hook_type')
            common_styles = self._find_common_attribute(top_performers, 'style')
            common_formats = self._find_common_attribute(top_performers, 'format')
            
            if common_hooks:
                formulas.append({
                    "formula": f"{common_hooks[0]} hook strategy",
                    "success_rate": len(top_performers) / len(performance_data.get('all_ads', [])),
                    "components": {
                        "hook": common_hooks[0],
                        "avg_performance": self._calculate_avg_performance(
                            [p for p in top_performers if p.get('hook_type') == common_hooks[0]]
                        )
                    },
                    "repeatability": "high",
                    "recommendation": f"Continue using {common_hooks[0]} hooks as primary strategy"
                })
        
        return formulas
```

---

## Implementation

```python
# agents/analyst_agent.py
from agents.base_agent import BaseAgent
from agents.tools.analyst_tools import (
    StatisticalAnalyzer,
    PerformancePatternDetector,
    LearningSynthesizer,
    RecommendationEngine
)

class AnalystAgent(BaseAgent):
    """Performance analysis and learning synthesis agent"""
    
    def __init__(self, db_connection, llm_client):
        self.stats_analyzer = StatisticalAnalyzer()
        self.pattern_detector = PerformancePatternDetector()
        self.learning_synthesizer = LearningSynthesizer()
        self.rec_engine = RecommendationEngine()
        super().__init__("analyst", db_connection, llm_client)
    
    async def analyze_campaign(
        self,
        campaign_id: str,
        analysis_type: str = "comprehensive"
    ) -> Dict:
        """
        Perform campaign analysis
        
        Args:
            campaign_id: Campaign to analyze
            analysis_type: "comprehensive" | "quick" | "test_only"
            
        Returns:
            Complete analysis with insights and recommendations
        """
        
        # Fetch performance data
        performance = await self._fetch_campaign_performance(campaign_id)
        
        # Run statistical analysis
        test_results = await self._analyze_tests(campaign_id)
        
        # Detect patterns
        patterns = await self.pattern_detector.detect_winning_patterns(
            performance['all_ads']
        )
        
        # Synthesize learnings
        learnings = await self.learning_synthesizer.synthesize_campaign_learnings(
            campaign_id,
            performance,
            test_results
        )
        
        # Generate recommendations
        recommendations = await self.rec_engine.generate_recommendations(
            learnings,
            patterns,
            performance
        )
        
        # Propagate learnings to other agents
        await self._propagate_learnings(campaign_id, learnings)
        
        return {
            "campaign_id": campaign_id,
            "analysis_type": analysis_type,
            "performance_summary": performance['summary'],
            "test_results": test_results,
            "patterns": patterns,
            "learnings": learnings,
            "recommendations": recommendations,
            "analyzed_at": datetime.now()
        }
```

---

*The Analyst Agent closes the loop by extracting validated learnings and feeding them back to improve the entire system.*
