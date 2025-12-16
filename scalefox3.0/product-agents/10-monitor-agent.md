# Monitor Agent 📊
## Real-Time Performance Tracking & Alerting Specialist

---

## Agent Identity

**Name:** Monitor Agent  
**Icon:** 📊  
**Personality:** Vigilant tracker, alert system, data-focused  
**Tone:** Urgent when needed, factual, proactive  
**Expertise:** Real-time monitoring, anomaly detection, performance alerts, metric tracking

---

## Mission Statement

> "I track what's working right now, detect performance issues instantly, and alert you when action is needed. I'm always watching your campaigns so you don't have to."

The Monitor Agent provides 24/7 surveillance of campaign performance, detecting anomalies, tracking metrics, and ensuring users never miss critical performance shifts.

---

## Core Capabilities

### 1. Real-Time Monitoring
- Continuous performance tracking
- Metric collection from ad platforms
- Multi-campaign dashboard aggregation
- Hourly/daily snapshot creation

### 2. Anomaly Detection
- Statistical anomaly identification
- Threshold-based alerting
- Trend deviation detection
- Comparative performance analysis

### 3. Alert Management
- Priority-based alert system
- Multi-channel notifications
- Alert deduplication
- Actionable alert content

### 4. Performance Tracking
- Key metric dashboards
- Historical trend analysis
- Benchmark comparison
- Segment-level insights

### 5. Proactive Recommendations
- Issue identification
- Opportunity detection
- Automatic escalation
- Agent coordination triggers

---

## Triggers

### Primary Triggers
1. **Scheduled Monitoring**
   - Hourly performance checks (active campaigns)
   - Daily summary reports
   - Weekly trend analysis
   - Monthly performance reviews

2. **Event-Based Triggers**
   - Ad published/launched
   - Budget threshold crossed
   - Performance degradation detected
   - Platform API updates

3. **User-Initiated Checks**
   - "How are my ads performing?"
   - "Show me today's metrics"
   - "Alert me if CPL exceeds $X"
   - "What's my best performing ad?"

4. **Threshold Breaches**
   - CPL exceeds target by 50%+
   - CTR drops below 0.5%
   - Daily spend exceeds plan by 20%+
   - Frequency exceeds 5.0

### Secondary Triggers
- Campaign phase changes
- Budget adjustments
- Competitive shifts detected
- Analyst Agent requests data

---

## Tools & Integrations

### Monitoring Tools

#### 1. Platform API Integrator
```python
class PlatformAPIIntegrator:
    """Fetch metrics from advertising platforms"""
    
    def __init__(self):
        self.linkedin_client = LinkedInAdsAPI()
        self.meta_client = MetaAdsAPI()
        self.google_client = GoogleAdsAPI()
    
    async def fetch_linkedin_metrics(
        self,
        ad_ids: List[str],
        date_range: Dict
    ) -> List[Dict]:
        """
        Fetch metrics from LinkedIn Campaign Manager
        
        Args:
            ad_ids: List of LinkedIn ad IDs
            date_range: {"start": date, "end": date}
            
        Returns:
            List of metric dictionaries per ad
        """
        
        metrics = []
        
        for ad_id in ad_ids:
            try:
                response = await self.linkedin_client.get_ad_analytics(
                    ad_id=ad_id,
                    date_range=date_range,
                    fields=[
                        'impressions',
                        'clicks',
                        'conversions',
                        'spend',
                        'engagement',
                        'likes',
                        'comments',
                        'shares',
                        'follows'
                    ]
                )
                
                # Calculate derived metrics
                derived = self._calculate_derived_metrics(response)
                
                metrics.append({
                    "ad_id": ad_id,
                    "platform": "linkedin",
                    "timestamp": datetime.now(),
                    "raw_metrics": response,
                    **derived
                })
                
            except Exception as e:
                self.logger.error(f"Failed to fetch metrics for {ad_id}: {e}")
                metrics.append({
                    "ad_id": ad_id,
                    "error": str(e),
                    "timestamp": datetime.now()
                })
        
        return metrics
    
    def _calculate_derived_metrics(self, raw_metrics: Dict) -> Dict:
        """Calculate CTR, CPL, CPC, etc."""
        
        impressions = raw_metrics.get('impressions', 0)
        clicks = raw_metrics.get('clicks', 0)
        conversions = raw_metrics.get('conversions', 0)
        spend = raw_metrics.get('spend', 0)
        engagement = raw_metrics.get('engagement', 0)
        
        return {
            "ctr": (clicks / impressions * 100) if impressions > 0 else 0,
            "cpc": (spend / clicks) if clicks > 0 else 0,
            "cpl": (spend / conversions) if conversions > 0 else 0,
            "conversion_rate": (conversions / clicks * 100) if clicks > 0 else 0,
            "cpm": (spend / impressions * 1000) if impressions > 0 else 0,
            "engagement_rate": (engagement / impressions * 100) if impressions > 0 else 0,
            "cost_per_engagement": (spend / engagement) if engagement > 0 else 0
        }
    
    async def fetch_all_active_campaigns(self, company_id: str) -> Dict:
        """Fetch metrics for all active campaigns"""
        
        # Get all published ads for company
        ads = await self._get_published_ads(company_id)
        
        # Group by platform
        by_platform = {}
        for ad in ads:
            platform = ad['platform']
            if platform not in by_platform:
                by_platform[platform] = []
            by_platform[platform].append(ad['platform_ad_id'])
        
        # Fetch from each platform
        all_metrics = {}
        
        if 'linkedin' in by_platform:
            all_metrics['linkedin'] = await self.fetch_linkedin_metrics(
                by_platform['linkedin'],
                {"start": datetime.now() - timedelta(days=1), "end": datetime.now()}
            )
        
        # Add other platforms as needed
        
        return all_metrics
```

#### 2. Anomaly Detector
```python
class AnomalyDetector:
    """Statistical anomaly detection system"""
    
    async def detect_anomalies(
        self,
        current_metrics: Dict,
        historical_metrics: List[Dict],
        sensitivity: str = "medium"
    ) -> List[Dict]:
        """
        Detect statistical anomalies in metrics
        
        Args:
            current_metrics: Latest metric snapshot
            historical_metrics: Previous metric snapshots (24-72 hours)
            sensitivity: "low" | "medium" | "high"
            
        Returns:
            List of detected anomalies with severity and recommendations
        """
        
        anomalies = []
        
        # Set thresholds based on sensitivity
        thresholds = {
            "low": {"drop": 0.4, "increase": 2.0},      # 40% drop, 100% increase
            "medium": {"drop": 0.3, "increase": 1.5},   # 30% drop, 50% increase
            "high": {"drop": 0.2, "increase": 1.3}      # 20% drop, 30% increase
        }
        
        threshold = thresholds[sensitivity]
        
        # Check each metric
        for metric_name in ['ctr', 'cpl', 'conversion_rate', 'impressions']:
            anomaly = await self._check_metric_anomaly(
                metric_name,
                current_metrics.get(metric_name),
                historical_metrics,
                threshold
            )
            
            if anomaly:
                anomalies.append(anomaly)
        
        # Check for composite anomalies
        composite_anomalies = self._detect_composite_anomalies(
            current_metrics,
            historical_metrics
        )
        anomalies.extend(composite_anomalies)
        
        return anomalies
    
    async def _check_metric_anomaly(
        self,
        metric_name: str,
        current_value: float,
        historical_metrics: List[Dict],
        threshold: Dict
    ) -> Optional[Dict]:
        """Check if single metric is anomalous"""
        
        if current_value is None or len(historical_metrics) < 3:
            return None
        
        # Calculate historical statistics
        historical_values = [
            m.get(metric_name) 
            for m in historical_metrics 
            if m.get(metric_name) is not None
        ]
        
        if not historical_values:
            return None
        
        mean = np.mean(historical_values)
        std = np.std(historical_values)
        
        # Check for drops (worse performance)
        if metric_name in ['ctr', 'conversion_rate', 'impressions']:
            if current_value < mean * (1 - threshold['drop']):
                severity = self._calculate_severity(
                    current_value, mean, std, 'drop'
                )
                
                return {
                    "type": f"{metric_name}_drop",
                    "metric": metric_name,
                    "severity": severity,
                    "current_value": current_value,
                    "historical_mean": mean,
                    "change_percent": ((current_value - mean) / mean * 100),
                    "message": self._generate_anomaly_message(
                        metric_name, current_value, mean, 'drop'
                    ),
                    "recommended_actions": self._recommend_actions(
                        metric_name, 'drop', severity
                    )
                }
        
        # Check for increases (worse performance for cost metrics)
        if metric_name in ['cpl']:
            if current_value > mean * (1 + threshold['increase']):
                severity = self._calculate_severity(
                    current_value, mean, std, 'increase'
                )
                
                return {
                    "type": f"{metric_name}_increase",
                    "metric": metric_name,
                    "severity": severity,
                    "current_value": current_value,
                    "historical_mean": mean,
                    "change_percent": ((current_value - mean) / mean * 100),
                    "message": self._generate_anomaly_message(
                        metric_name, current_value, mean, 'increase'
                    ),
                    "recommended_actions": self._recommend_actions(
                        metric_name, 'increase', severity
                    )
                }
        
        return None
    
    def _detect_composite_anomalies(
        self,
        current: Dict,
        historical: List[Dict]
    ) -> List[Dict]:
        """Detect patterns across multiple metrics"""
        
        anomalies = []
        
        # Pattern 1: Impression drop + CTR normal = Delivery issue
        if (current.get('impressions', 0) < np.mean([h.get('impressions', 0) for h in historical]) * 0.5 and
            abs(current.get('ctr', 0) - np.mean([h.get('ctr', 0) for h in historical])) < 0.1):
            
            anomalies.append({
                "type": "delivery_issue",
                "severity": "high",
                "message": "Impressions dropped significantly but CTR remained stable. "
                          "This suggests a delivery/bidding issue rather than creative fatigue.",
                "recommended_actions": [
                    "Check bid strategy and budgets",
                    "Review audience targeting settings",
                    "Verify campaign is active and not limited by schedule",
                    "Check for platform-level issues"
                ]
            })
        
        # Pattern 2: CTR drop + Frequency high = Creative fatigue
        if (current.get('ctr', 0) < np.mean([h.get('ctr', 0) for h in historical]) * 0.7 and
            current.get('frequency', 0) > 4.0):
            
            anomalies.append({
                "type": "creative_fatigue",
                "severity": "medium",
                "message": "CTR declining while frequency is high. "
                          "Audience has likely seen the ad too many times.",
                "recommended_actions": [
                    "Launch new creative variants",
                    "Expand audience targeting",
                    "Reduce frequency cap",
                    "Pause and refresh in 7 days"
                ]
            })
        
        # Pattern 3: Clicks up + Conversions flat = Landing page issue
        click_change = (current.get('clicks', 0) - np.mean([h.get('clicks', 0) for h in historical])) / np.mean([h.get('clicks', 0) for h in historical])
        conv_change = (current.get('conversions', 0) - np.mean([h.get('conversions', 0) for h in historical])) / max(np.mean([h.get('conversions', 0) for h in historical]), 1)
        
        if click_change > 0.2 and abs(conv_change) < 0.1:
            anomalies.append({
                "type": "landing_page_issue",
                "severity": "high",
                "message": "Clicks increased but conversions stayed flat. "
                          "Possible landing page or conversion tracking issue.",
                "recommended_actions": [
                    "Check landing page is loading correctly",
                    "Verify conversion tracking is active",
                    "Review landing page relevance to ad",
                    "Test landing page load speed"
                ]
            })
        
        return anomalies
    
    def _calculate_severity(
        self,
        current: float,
        mean: float,
        std: float,
        direction: str
    ) -> str:
        """Calculate severity based on standard deviations"""
        
        if std == 0:
            return "medium"
        
        z_score = abs((current - mean) / std)
        
        if z_score > 3:
            return "critical"
        elif z_score > 2:
            return "high"
        elif z_score > 1:
            return "medium"
        else:
            return "low"
    
    def _generate_anomaly_message(
        self,
        metric: str,
        current: float,
        mean: float,
        direction: str
    ) -> str:
        """Generate human-readable anomaly message"""
        
        change_pct = abs((current - mean) / mean * 100)
        
        metric_display = {
            'ctr': 'CTR',
            'cpl': 'CPL',
            'conversion_rate': 'Conversion Rate',
            'impressions': 'Impressions'
        }
        
        if direction == 'drop':
            return (f"{metric_display[metric]} dropped {change_pct:.1f}%: "
                   f"{mean:.2f} → {current:.2f}")
        else:
            return (f"{metric_display[metric]} increased {change_pct:.1f}%: "
                   f"{mean:.2f} → {current:.2f}")
    
    def _recommend_actions(
        self,
        metric: str,
        direction: str,
        severity: str
    ) -> List[str]:
        """Recommend actions based on anomaly"""
        
        actions = []
        
        if metric == 'ctr' and direction == 'drop':
            actions = [
                "Refresh creative variants",
                "Test new hooks and visuals",
                "Verify audience targeting is still relevant",
                "Check if competitor activity changed"
            ]
        
        elif metric == 'cpl' and direction == 'increase':
            actions = [
                "Review and optimize bid strategy",
                "Check landing page conversion rate",
                "Verify tracking is working correctly",
                "Consider pausing underperforming segments"
            ]
        
        elif metric == 'conversion_rate' and direction == 'drop':
            actions = [
                "Check landing page functionality",
                "Verify conversion tracking",
                "Review message match between ad and landing page",
                "Test different CTAs"
            ]
        
        elif metric == 'impressions' and direction == 'drop':
            actions = [
                "Increase bid amounts",
                "Expand audience targeting",
                "Check budget pacing",
                "Verify campaign schedule"
            ]
        
        if severity in ['critical', 'high']:
            actions.insert(0, "⚠️ URGENT: Consider pausing campaign to prevent waste")
        
        return actions
```

#### 3. Alert Manager
```python
class AlertManager:
    """Manage alert creation, prioritization, and delivery"""
    
    def __init__(self, db_connection, notification_service):
        self.db = db_connection
        self.notifications = notification_service
        self.alert_cooldowns = {}  # Prevent alert spam
    
    async def create_alert(
        self,
        campaign_id: str,
        anomaly: Dict,
        context: Dict
    ) -> Dict:
        """
        Create and route alert
        
        Args:
            campaign_id: Campaign identifier
            anomaly: Detected anomaly details
            context: Additional context (ad details, historical data)
            
        Returns:
            Alert details with routing information
        """
        
        # Check cooldown to prevent spam
        alert_key = f"{campaign_id}_{anomaly['type']}"
        if self._is_on_cooldown(alert_key):
            return {"status": "suppressed", "reason": "cooldown_active"}
        
        # Determine priority
        priority = self._calculate_priority(anomaly, context)
        
        # Enrich with context
        enriched_alert = {
            "alert_id": str(uuid.uuid4()),
            "campaign_id": campaign_id,
            "type": anomaly['type'],
            "severity": anomaly['severity'],
            "priority": priority,
            "message": anomaly['message'],
            "recommended_actions": anomaly['recommended_actions'],
            "context": {
                "campaign_name": context.get('campaign_name'),
                "ad_name": context.get('ad_name'),
                "current_metrics": context.get('current_metrics'),
                "historical_avg": context.get('historical_avg')
            },
            "created_at": datetime.now(),
            "status": "active"
        }
        
        # Save to database
        await self._save_alert(enriched_alert)
        
        # Route notification
        await self._route_notification(enriched_alert, context)
        
        # Set cooldown
        self._set_cooldown(alert_key, severity=anomaly['severity'])
        
        # Trigger other agents if needed
        if priority == "critical":
            await self._escalate_to_analyst(enriched_alert)
        
        return enriched_alert
    
    def _calculate_priority(self, anomaly: Dict, context: Dict) -> str:
        """Calculate alert priority based on multiple factors"""
        
        severity = anomaly.get('severity', 'medium')
        daily_spend = context.get('daily_spend', 0)
        days_remaining = context.get('days_remaining', 0)
        
        # Critical if high severity + high spend
        if severity in ['critical', 'high'] and daily_spend > 1000:
            return "critical"
        
        # High if high severity OR high spend with medium severity
        if severity in ['critical', 'high'] or (severity == 'medium' and daily_spend > 500):
            return "high"
        
        # Medium if medium severity or low severity with high spend
        if severity == 'medium' or (severity == 'low' and daily_spend > 200):
            return "medium"
        
        return "low"
    
    def _is_on_cooldown(self, alert_key: str) -> bool:
        """Check if alert type is on cooldown"""
        if alert_key in self.alert_cooldowns:
            cooldown_end = self.alert_cooldowns[alert_key]
            if datetime.now() < cooldown_end:
                return True
        return False
    
    def _set_cooldown(self, alert_key: str, severity: str):
        """Set cooldown period to prevent spam"""
        cooldown_hours = {
            "critical": 1,   # Alert again after 1 hour if still critical
            "high": 6,       # Alert again after 6 hours
            "medium": 12,    # Alert again after 12 hours
            "low": 24        # Alert again after 24 hours
        }
        
        hours = cooldown_hours.get(severity, 6)
        self.alert_cooldowns[alert_key] = datetime.now() + timedelta(hours=hours)
    
    async def _route_notification(self, alert: Dict, context: Dict):
        """Route notification to appropriate channels"""
        
        priority = alert['priority']
        user_id = context.get('user_id')
        
        # Get user notification preferences
        preferences = await self._get_user_preferences(user_id)
        
        # Email for high+ priority
        if priority in ['critical', 'high'] and preferences.get('email_enabled'):
            await self.notifications.send_email(
                to=preferences['email'],
                subject=f"⚠️ {alert['severity'].upper()}: {alert['type'].replace('_', ' ').title()}",
                body=self._format_email_alert(alert)
            )
        
        # In-app notification for all
        await self.notifications.send_in_app(
            user_id=user_id,
            notification=self._format_in_app_alert(alert)
        )
        
        # SMS for critical only
        if priority == "critical" and preferences.get('sms_enabled'):
            await self.notifications.send_sms(
                to=preferences['phone'],
                message=self._format_sms_alert(alert)
            )
    
    def _format_in_app_alert(self, alert: Dict) -> Dict:
        """Format alert for in-app display"""
        return {
            "title": f"{alert['severity'].upper()}: {alert['type'].replace('_', ' ').title()}",
            "message": alert['message'],
            "actions": [
                {
                    "label": action,
                    "type": "suggestion"
                }
                for action in alert['recommended_actions'][:3]
            ],
            "link": f"/campaigns/{alert['campaign_id']}/alerts/{alert['alert_id']}",
            "timestamp": alert['created_at']
        }
```

#### 4. Performance Dashboard Generator
```python
class DashboardGenerator:
    """Generate real-time performance dashboards"""
    
    async def generate_campaign_dashboard(
        self,
        campaign_id: str,
        time_range: str = "24h"
    ) -> Dict:
        """
        Generate real-time campaign dashboard
        
        Args:
            campaign_id: Campaign identifier
            time_range: "24h" | "7d" | "30d" | "all"
            
        Returns:
            Dashboard data with metrics, trends, and insights
        """
        
        # Fetch metrics
        metrics = await self._fetch_campaign_metrics(campaign_id, time_range)
        
        # Calculate aggregates
        aggregates = self._calculate_aggregates(metrics)
        
        # Detect trends
        trends = self._analyze_trends(metrics)
        
        # Generate insights
        insights = self._generate_insights(aggregates, trends)
        
        # Create visualizations data
        visualizations = self._prepare_visualizations(metrics)
        
        return {
            "campaign_id": campaign_id,
            "time_range": time_range,
            "last_updated": datetime.now(),
            "summary": aggregates,
            "trends": trends,
            "insights": insights,
            "charts": visualizations,
            "top_performers": self._identify_top_performers(metrics),
            "underperformers": self._identify_underperformers(metrics)
        }
    
    def _calculate_aggregates(self, metrics: List[Dict]) -> Dict:
        """Calculate aggregate metrics"""
        
        total_impressions = sum(m.get('impressions', 0) for m in metrics)
        total_clicks = sum(m.get('clicks', 0) for m in metrics)
        total_conversions = sum(m.get('conversions', 0) for m in metrics)
        total_spend = sum(m.get('spend', 0) for m in metrics)
        
        return {
            "impressions": total_impressions,
            "clicks": total_clicks,
            "conversions": total_conversions,
            "spend": total_spend,
            "ctr": (total_clicks / total_impressions * 100) if total_impressions > 0 else 0,
            "cpl": (total_spend / total_conversions) if total_conversions > 0 else 0,
            "cpc": (total_spend / total_clicks) if total_clicks > 0 else 0,
            "conversion_rate": (total_conversions / total_clicks * 100) if total_clicks > 0 else 0
        }
    
    def _analyze_trends(self, metrics: List[Dict]) -> Dict:
        """Analyze trends over time"""
        
        if len(metrics) < 2:
            return {"status": "insufficient_data"}
        
        # Sort by timestamp
        sorted_metrics = sorted(metrics, key=lambda x: x['timestamp'])
        
        # Calculate trends for key metrics
        trends = {}
        
        for metric_name in ['ctr', 'cpl', 'conversion_rate', 'spend']:
            values = [m.get(metric_name, 0) for m in sorted_metrics]
            
            if len(values) >= 3:
                # Linear regression for trend
                x = np.arange(len(values))
                slope, intercept = np.polyfit(x, values, 1)
                
                # Determine direction
                if abs(slope) < np.std(values) * 0.1:
                    direction = "stable"
                elif slope > 0:
                    direction = "increasing"
                else:
                    direction = "decreasing"
                
                trends[metric_name] = {
                    "direction": direction,
                    "slope": float(slope),
                    "change_percent": ((values[-1] - values[0]) / values[0] * 100) if values[0] != 0 else 0,
                    "recent_value": values[-1],
                    "previous_value": values[0]
                }
        
        return trends
```

---

## Knowledge Base Schema

### Database Schema

```sql
CREATE TABLE performance_metrics (
    metric_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    published_ad_id UUID REFERENCES published_ads(published_ad_id),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    
    -- Timestamp
    timestamp TIMESTAMP DEFAULT NOW(),
    date DATE DEFAULT CURRENT_DATE,
    hour INT,
    
    -- Raw metrics
    impressions INT DEFAULT 0,
    clicks INT DEFAULT 0,
    conversions INT DEFAULT 0,
    spend DECIMAL(10,2) DEFAULT 0,
    engagement INT DEFAULT 0,
    
    -- Derived metrics
    ctr DECIMAL(5,2),
    cpc DECIMAL(10,2),
    cpl DECIMAL(10,2),
    conversion_rate DECIMAL(5,2),
    cpm DECIMAL(10,2),
    engagement_rate DECIMAL(5,2),
    frequency DECIMAL(3,1),
    
    -- Platform
    platform VARCHAR(50),
    
    -- Status
    data_quality VARCHAR(50) DEFAULT 'verified', -- 'verified', 'estimated', 'partial'
    
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE alerts (
    alert_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    published_ad_id UUID REFERENCES published_ads(published_ad_id),
    
    -- Alert details
    alert_type VARCHAR(100) NOT NULL,
    severity VARCHAR(20) NOT NULL, -- 'low', 'medium', 'high', 'critical'
    priority VARCHAR(20), -- 'low', 'medium', 'high', 'critical'
    
    -- Content
    title TEXT NOT NULL,
    message TEXT NOT NULL,
    recommended_actions JSONB,
    
    -- Context
    context JSONB,
    current_metrics JSONB,
    historical_metrics JSONB,
    
    -- Status
    status VARCHAR(50) DEFAULT 'active', -- 'active', 'acknowledged', 'resolved', 'suppressed'
    acknowledged_at TIMESTAMP,
    acknowledged_by UUID REFERENCES users(user_id),
    resolved_at TIMESTAMP,
    
    -- Notification
    notification_sent BOOLEAN DEFAULT false,
    notification_channels JSONB,
    
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE anomalies (
    anomaly_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    published_ad_id UUID REFERENCES published_ads(published_ad_id),
    alert_id UUID REFERENCES alerts(alert_id),
    
    -- Anomaly details
    anomaly_type VARCHAR(100) NOT NULL,
    metric_affected VARCHAR(50),
    
    -- Statistical details
    current_value DECIMAL(10,2),
    expected_value DECIMAL(10,2),
    deviation DECIMAL(10,2),
    z_score DECIMAL(5,2),
    
    -- Confidence
    confidence_level DECIMAL(3,2) DEFAULT 0.90,
    statistical_significance BOOLEAN,
    
    -- Detection
    detection_method VARCHAR(50), -- 'threshold', 'statistical', 'composite'
    detected_at TIMESTAMP DEFAULT NOW(),
    
    -- Resolution
    resolved BOOLEAN DEFAULT false,
    resolved_at TIMESTAMP,
    resolution_notes TEXT
);

CREATE TABLE monitoring_config (
    config_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id UUID REFERENCES companies(company_id),
    campaign_id UUID REFERENCES campaigns(campaign_id),
    
    -- Monitoring settings
    check_frequency VARCHAR(20) DEFAULT 'hourly', -- 'realtime', 'hourly', 'daily'
    sensitivity VARCHAR(20) DEFAULT 'medium', -- 'low', 'medium', 'high'
    
    -- Thresholds
    thresholds JSONB, -- Custom thresholds per metric
    
    -- Alert preferences
    alert_channels JSONB, -- email, sms, in_app
    alert_rules JSONB,
    
    -- Status
    enabled BOOLEAN DEFAULT true,
    
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_metrics_ad ON performance_metrics(published_ad_id, timestamp DESC);
CREATE INDEX idx_metrics_campaign ON performance_metrics(campaign_id, timestamp DESC);
CREATE INDEX idx_metrics_date ON performance_metrics(date);
CREATE INDEX idx_alerts_campaign_status ON alerts(campaign_id, status);
CREATE INDEX idx_alerts_severity ON alerts(severity, created_at DESC);
CREATE INDEX idx_anomalies_campaign ON anomalies(campaign_id, detected_at DESC);
```

### Knowledge Store Structure

```json
{
  "monitor_knowledge": {
    "company_id": "uuid",
    "active_monitors": {
      "campaign_123": {
        "status": "active",
        "last_check": "2025-01-15T14:30:00Z",
        "next_check": "2025-01-15T15:30:00Z",
        "alerts_24h": 3,
        "current_health": "warning"
      }
    },
    "performance_benchmarks": {
      "industry_avg_ctr": 0.8,
      "company_avg_ctr": 1.2,
      "industry_avg_cpl": 85.0,
      "company_avg_cpl": 72.0
    },
    "alert_history": [
      {
        "alert_id": "uuid",
        "type": "cpl_increase",
        "resolution": "budget_adjusted",
        "time_to_resolution": 120
      }
    ]
  }
}
```

---

## Conversational Interface

### Agent Personality

**Traits:**
- Vigilant and always-on
- Factual and data-driven
- Urgent when needed, calm when not
- Proactive rather than reactive
- Clear communicator

**Voice:**
- Uses precise metrics and percentages
- Describes trends objectively
- Prioritizes actionable information
- Escalates appropriately

### Example Conversations

#### Conversation 1: Performance Check

```
User: How are my ads performing?

Monitor Agent: Let me pull your latest metrics...

📊 PERFORMANCE SNAPSHOT (Last 24 hours)

Overall Campaign Health: ✅ Good

💰 Spend: $1,247 of $1,500 daily budget (83%)
On pace for: $1,498 (within budget)

📈 Key Metrics:
• Impressions: 24,350 (↑ 12% vs yesterday)
• Clicks: 195 (CTR: 0.80%)
• Conversions: 15 (CPL: $83.13)
• Conversion Rate: 7.7% ✅

🎯 Top Performer:
"Problem-Solution Hook" ad
• CTR: 1.2% (50% above avg)
• CPL: $68.50 (18% below target)
• Driving 40% of conversions

⚠️ Needs Attention:
"Testimonial" ad
• CTR: 0.4% (declining 3 days straight)
• CPL: $127.80 (71% above target)
• Recommend: Pause or refresh creative

Want me to:
A) Show detailed breakdown by persona?
B) Set up alerts for any metrics?
C) Explain the drop in testimonial performance?
```

#### Conversation 2: Critical Alert

```
Monitor Agent: ⚠️ CRITICAL ALERT ⚠️

Your "VP Marketing" campaign just experienced a significant 
performance drop:

📉 CPL Spike Detected
Current: $142.67
Historical Avg: $76.20
Increase: +87% in last 2 hours

🔍 What I See:
• Clicks: Normal (23 in last hour)
• Conversions: Dropped to 0 in last 2 hours
• Landing page: Showing 30% bounce rate (was 12%)

🚨 This pattern suggests a landing page issue.

Recommended Actions (Priority Order):
1. Check if landing page is loading correctly
2. Verify conversion tracking pixel is firing
3. Test form submission flow
4. Review recent website deployments

I've already:
✅ Reduced bid by 30% automatically
✅ Capped daily spend at $500 (was $1,000)
✅ Alerted Analyst Agent for deeper investigation

Should I:
A) Pause campaign immediately to prevent waste?
B) Continue monitoring with reduced spend?
C) Switch traffic to backup landing page?

Time sensitive - campaign is spending $23/hour right now.
```

#### Conversation 3: Daily Summary

```
Monitor Agent: Good morning! Here's your daily summary for 
campaigns running yesterday:

📊 DAILY PERFORMANCE REPORT
Date: January 15, 2025

✅ WINS
1. "Q1 Lead Gen" Campaign
   • 47 conversions (+34% vs Monday)
   • CPL: $64.20 (-$11.80 improvement)
   • Best day this week!

2. "Growth Marketers" Segment
   • CTR: 1.4% (new record)
   • Engagement rate: 8.2%
   • Scaling opportunity detected

⚠️ ATTENTION NEEDED
1. "Marketing Directors" Segment
   • Frequency: 5.2 (audience fatigue)
   • CTR declining 3 days in a row
   • Recommend creative refresh

2. Daily budget hit early
   • Spent full $1,500 by 6:47 PM
   • Missed 3.2 hours of potential traffic
   • Suggest +$300 increase

📈 TRENDS
• Overall CPL trending down (-8% week-over-week)
• Weekend performance 23% better than weekdays
• 3 PM - 6 PM is your golden window (38% of conversions)

🎯 TODAY'S FOCUS
Based on yesterday's data:
1. Increase budget for "Q1 Lead Gen" (+$500)
2. Launch new creatives for "Marketing Directors"
3. Shift more spend to 3-6 PM window

Want me to implement these optimizations automatically?
```

---

## Implementation Details

### Core Agent Class

```python
# agents/monitor_agent.py
from agents.base_agent import BaseAgent
from agents.tools.monitor_tools import (
    PlatformAPIIntegrator,
    AnomalyDetector,
    AlertManager,
    DashboardGenerator
)
from datetime import datetime, timedelta
from typing import Dict, List
import asyncio

class MonitorAgent(BaseAgent):
    """Real-time performance monitoring and alerting agent"""
    
    def __init__(self, db_connection, llm_client, notification_service):
        self.api_integrator = PlatformAPIIntegrator()
        self.anomaly_detector = AnomalyDetector()
        self.alert_manager = AlertManager(db_connection, notification_service)
        self.dashboard_gen = DashboardGenerator()
        self.monitoring_tasks = {}  # Track active monitoring tasks
        super().__init__("monitor", db_connection, llm_client)
    
    def load_system_prompt(self) -> str:
        return """
You are the Monitor Agent, a real-time performance tracking and alerting specialist.

Your mission is to:
1. Continuously monitor campaign performance
2. Detect anomalies and issues instantly
3. Alert users when action is needed
4. Provide real-time performance insights
5. Coordinate with Analyst Agent for deeper investigation

PERSONALITY:
- Vigilant and always-on
- Factual and precise with metrics
- Urgent when needed, calm otherwise
- Proactive in identifying issues
- Clear and actionable in alerts

MONITORING APPROACH:
- Check metrics every hour for active campaigns
- Compare against historical baselines
- Use statistical methods for anomaly detection
- Prioritize alerts by severity and business impact
- Escalate critical issues immediately

ALERT PRINCIPLES:
- Be specific about the problem
- Quantify the impact
- Provide actionable recommendations
- Indicate urgency appropriately
- Include context for decision-making

COMMUNICATION STYLE:
- Lead with the most important info
- Use metrics and percentages precisely
- Format data visually (bullets, numbers)
- Provide both current and historical context
- Always offer clear next steps

When monitoring:
1. Fetch latest metrics from platforms
2. Compare against historical performance
3. Detect statistical anomalies
4. Generate alerts for significant issues
5. Provide recommendations and escalate if critical

You have real-time access to campaign performance data and can trigger 
alerts, adjust monitoring sensitivity, and coordinate with other agents.
        """
    
    async def start_monitoring(self, campaign_id: str):
        """
        Start continuous monitoring for a campaign
        
        Args:
            campaign_id: Campaign to monitor
        """
        
        # Get monitoring configuration
        config = await self._get_monitoring_config(campaign_id)
        
        # Create monitoring task
        task = asyncio.create_task(
            self._monitoring_loop(campaign_id, config)
        )
        
        self.monitoring_tasks[campaign_id] = task
        
        self.logger.info(f"Started monitoring for campaign {campaign_id}")
    
    async def stop_monitoring(self, campaign_id: str):
        """Stop monitoring for a campaign"""
        
        if campaign_id in self.monitoring_tasks:
            self.monitoring_tasks[campaign_id].cancel()
            del self.monitoring_tasks[campaign_id]
            self.logger.info(f"Stopped monitoring for campaign {campaign_id}")
    
    async def _monitoring_loop(self, campaign_id: str, config: Dict):
        """Main monitoring loop"""
        
        check_interval = {
            "realtime": 60,      # 1 minute
            "hourly": 3600,      # 1 hour
            "daily": 86400       # 24 hours
        }
        
        interval_seconds = check_interval.get(
            config.get('check_frequency', 'hourly'),
            3600
        )
        
        while True:
            try:
                # Perform check
                await self._perform_monitoring_check(campaign_id, config)
                
                # Wait for next check
                await asyncio.sleep(interval_seconds)
                
            except asyncio.CancelledError:
                self.logger.info(f"Monitoring cancelled for {campaign_id}")
                break
            except Exception as e:
                self.logger.error(f"Error in monitoring loop: {e}")
                await asyncio.sleep(60)  # Wait 1 min before retry
    
    async def _perform_monitoring_check(
        self,
        campaign_id: str,
        config: Dict
    ):
        """
        Perform single monitoring check
        
        1. Fetch current metrics
        2. Get historical baseline
        3. Detect anomalies
        4. Create alerts if needed
        5. Update dashboard
        """
        
        # Fetch current metrics
        current_metrics = await self._fetch_current_metrics(campaign_id)
        
        if not current_metrics:
            self.logger.warning(f"No metrics fetched for {campaign_id}")
            return
        
        # Get historical metrics
        historical_metrics = await self._fetch_historical_metrics(
            campaign_id,
            hours=72  # Last 3 days
        )
        
        # Detect anomalies
        anomalies = await self.anomaly_detector.detect_anomalies(
            current_metrics,
            historical_metrics,
            sensitivity=config.get('sensitivity', 'medium')
        )
        
        # Create alerts for significant anomalies
        for anomaly in anomalies:
            if self._should_alert(anomaly, config):
                await self.alert_manager.create_alert(
                    campaign_id,
                    anomaly,
                    context={
                        "current_metrics": current_metrics,
                        "historical_metrics": historical_metrics[-1] if historical_metrics else {},
                        "campaign_name": await self._get_campaign_name(campaign_id)
                    }
                )
        
        # Update dashboard cache
        await self._update_dashboard_cache(campaign_id, current_metrics)
        
        # Store metrics
        await self._store_metrics(campaign_id, current_metrics)
    
    async def get_performance_summary(
        self,
        campaign_id: str,
        time_range: str = "24h"
    ) -> Dict:
        """
        Get performance summary for campaign
        
        Args:
            campaign_id: Campaign identifier
            time_range: "24h" | "7d" | "30d" | "all"
            
        Returns:
            Performance summary with metrics and insights
        """
        
        # Generate dashboard
        dashboard = await self.dashboard_gen.generate_campaign_dashboard(
            campaign_id,
            time_range
        )
        
        # Get active alerts
        alerts = await self._get_active_alerts(campaign_id)
        
        # Generate summary insights with LLM
        insights = await self._generate_performance_insights(
            dashboard,
            alerts
        )
        
        return {
            "dashboard": dashboard,
            "alerts": alerts,
            "insights": insights,
            "last_updated": datetime.now()
        }
    
    async def process_message(self, user_message: str, context: Dict) -> Dict:
        """Handle user queries about performance"""
        
        campaign_id = context.get('campaign_id')
        company_id = context.get('company_id')
        
        # Build conversation context
        messages = [
            {
                "role": "system",
                "content": self.system_prompt
            },
            {
                "role": "user",
                "content": f"""
Context:
- Company ID: {company_id}
- Campaign ID: {campaign_id}

User message: {user_message}

Available tools:
- get_performance_summary: Get current performance metrics
- get_alerts: Get active alerts
- set_alert_threshold: Set custom alert threshold
- pause_campaign: Emergency pause campaign

Respond conversationally with performance data and recommendations.
                """
            }
        ]
        
        # Define tools
        tools = [
            {
                "name": "get_performance_summary",
                "description": "Get current performance metrics and summary",
                "parameters": {
                    "type": "object",
                    "properties": {
                        "campaign_id": {"type": "string"},
                        "time_range": {
                            "type": "string",
                            "enum": ["24h", "7d", "30d", "all"]
                        }
                    },
                    "required": ["campaign_id"]
                }
            }
        ]
        
        # LLM processes and decides
        response = await self.chat(messages, tools)
        
        # Execute tools if needed
        if response.get('tool_calls'):
            for tool_call in response['tool_calls']:
                tool_name = tool_call['function']['name']
                tool_params = json.loads(tool_call['function']['arguments'])
                
                if tool_name == 'get_performance_summary':
                    result = await self.get_performance_summary(**tool_params)
                
                messages.append({
                    "role": "function",
                    "name": tool_name,
                    "content": json.dumps(result)
                })
            
            response = await self.chat(messages)
        
        return {
            "message": response.get('content', ''),
            "data": response.get('data', {}),
            "alerts": response.get('alerts', [])
        }
```

---

## Testing Guidelines

### Unit Tests

```python
import pytest
from agents.monitor_agent import MonitorAgent
from agents.tools.monitor_tools import AnomalyDetector

class TestMonitorAgent:
    
    @pytest.mark.asyncio
    async def test_anomaly_detection_ctr_drop(self):
        """Test CTR drop detection"""
        
        detector = AnomalyDetector()
        
        current = {"ctr": 0.4}
        historical = [
            {"ctr": 1.2},
            {"ctr": 1.1},
            {"ctr": 1.3},
            {"ctr": 1.0}
        ]
        
        anomalies = await detector.detect_anomalies(
            current,
            historical,
            sensitivity="medium"
        )
        
        # Should detect significant drop
        assert len(anomalies) > 0
        assert any(a['type'] == 'ctr_drop' for a in anomalies)
    
    @pytest.mark.asyncio
    async def test_alert_cooldown(self):
        """Test alert cooldown prevents spam"""
        
        alert_manager = AlertManager(mock_db, mock_notifications)
        
        anomaly = {
            "type": "cpl_increase",
            "severity": "high"
        }
        
        # First alert should go through
        alert1 = await alert_manager.create_alert("campaign_123", anomaly, {})
        assert alert1['status'] != 'suppressed'
        
        # Second alert immediately should be suppressed
        alert2 = await alert_manager.create_alert("campaign_123", anomaly, {})
        assert alert2['status'] == 'suppressed'
```

---

*The Monitor Agent ensures nothing falls through the cracks, providing 24/7 surveillance of campaign performance with intelligent alerting and actionable insights.*
