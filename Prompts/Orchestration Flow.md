# The Orchestration Flow

## Overview

This document outlines the complete workflow for ScaleFox's AI-powered LinkedIn advertising campaign creation system, from company onboarding through final ad generation.

## Workflow Stages

### Stage 1: Initial Company Setup

- **User Action**: Enter URL + name
- **Background Process**: Agents start running
  - 1. Company info prompt launches
  - 2. Target Audience (ICP)

### Stage 2: Competitor Selection

- **User Screen**: Onboarding/competitors screen
- **User Action**: Enter 3 competitors + tap continue

### Stage 3: Competitor Analysis (Per Competitor)

#### 3.1 Data Collection

- **Scrapper**: Collects all ads of a competitor
- **Check**: Verify if we already have the data

#### 3.2 Data Organization

- **Aggregator**: Show overall stats of each competitor
- **Clusterer**: Combines similar ads
  - Embedding (Bedrock titan AWS)
  - HDBscan (clustering model)
  - Choose the best Ad per cluster
  - Reach (only) - it shouldn't matter that much, because they should be similar

#### 3.3 Cluster Scoring

Score each cluster based on:
- Size of cluster
- Number of duplications

#### 3.4 Analyze + Summarize Ads (30 best clusters + 10 worst)

- **Analyzed**: The best ad in each cluster (4. analyze ad prompt)
- **Summarizer**: Summarize all the results of the previous one (8. summarize ad analysis)

### Stage 4: Market Analysis

- **Overall Market Agent** (6.): Aggregates and organizes and gives insights
  - Maybe algorithmically analyze success patterns

### Stage 5: Insights Generation

- **Insights Agent** (7. Analyze insight agent):
  - Combines ICP insights + market insights
  - Create effective themes, success patterns and ads of competitors inside them

### Stage 6: Persona Selection

- **User Screen**: Onboarding/Idealpersonas
- **Process** (2.a icp-suggest personas):
  - Suggest 6 detailed personas
  - User selects at least 2 (or suggest more/customize until she selects)

### Stage 7: Brand Development

While Insights agent is running in the background, user continues to:

- **User Screen**: Onboarding/Brand screen
- **Brand Agents**: Understand company brand + company info
  - Create visual branding
  - Tone
  - Messaging and USPs
- **User Action**: Approve

### Stage 8: Loading State

Until insights agent finished running and effective themes are created, user is on a loader screen.

### Stage 9: Theme Selection

- **User Screen**: Onboarding/Effective themes
- **Condition**: When insights agent (7.) finished running
- **User Action**: Select at least 5 ads from effective themes

### Stage 10: Brief Creation

- **Brief Creator** (14.): Takes inputs and creates 6 briefs for ads

#### Inputs:
- Insights_Data: effective_themes[], common_pitfalls[], competitive_landscape
- ICP_Data: personas, demographics, pains, goals, jobs-to-be-done
- Company_Info: name, industry, positioning, product, brand_identity
- Campaign_Stage: awareness | consideration | conversion
- Test_Tactics (optional): hypotheses, split variants, constraints (budget/time)
- Brand guidelines: the essence of the brand in terms of tone, style, messaging, etc.

### Stage 11: Ad Generation

#### Template Generator (17.)

- Takes the briefs and create ads out of them
- Templates randomly selected that have some of the content elements tags in the brief (templates are tagged)

#### Remix Ad (13.)

- Used on the ads user selected to create more ads
