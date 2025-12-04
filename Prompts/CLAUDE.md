# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a prompt library for ScaleFox.ai, an AI-powered marketing automation platform specializing in competitive intelligence-driven LinkedIn advertising. The prompts directory contains the core AI workflow prompts that power ScaleFox's automated campaign creation pipeline.

## Prompt Architecture

ScaleFox uses a sequential multi-stage prompt workflow to transform competitor intelligence into ready-to-launch LinkedIn campaigns. The prompts are numbered to indicate their execution order in the pipeline.

### Core Workflow Stages

**Stage 1: Foundation & Research (Prompts 1-2a)**
- `1 company info prompt.docx` - Extracts comprehensive company information and brand analysis
- `2 Target audience prompt.docx` - Identifies and analyzes target audience personas
- `2a ICP suggest prompt.docx` - Suggests Ideal Customer Profile (ICP) personas

**Stage 2: Competitive Analysis (Prompts 4-8)**
- `4 Analyze ad prompt.docx` - Analyzes individual competitor ads for patterns and insights
- `5 Ads Insight Prompt.docx` - Extracts actionable insights from ad analysis
- `6 Overall Market summary prompt.docx` - Synthesizes market-level competitive intelligence
- `7 Analyze Insight prompt.docx` - Deep-dive analysis of specific competitive insights
- `8 Summarize Ads Analysis prompt.docx` - Creates comprehensive ad analysis summaries

**Stage 3: GTM Strategy & Creation (Prompts 13-18)**
- `13 remix ad prompt.docx` - Adapts winning competitor patterns for new campaigns
- `14 Brief Creator.docx` - Generates comprehensive campaign briefs (220KB - extensive)
- `16 Copy Generation.docx` - Creates ad copy based on briefs and insights
- `17 Template Generation Prompt.docx` - Generates ad templates and variations
- `18 Briefs without Insights Prompt.docx` - Alternative brief creation without prior insights (220KB)

**Stage 4: Utilities**
- `9 mini company info prompt.docx` - Condensed company info extraction for quick contexts
- `Orchestration Flow.docx` - Master workflow orchestration document (213KB - comprehensive)

## Key Architectural Patterns

### Sequential Intelligence Building
Each prompt stage builds on outputs from previous stages:
1. Company context establishes brand foundation
2. ICP research defines target audience
3. Competitive analysis extracts market intelligence
4. GTM strategy synthesizes insights into actionable playbooks
5. Creative generation produces campaign assets

### Context Handoff Pattern
Prompts are designed to pass structured context forward:
- Early stages (1-2a) establish foundational context
- Middle stages (4-8) accumulate competitive intelligence
- Late stages (13-18) consume accumulated context to generate campaigns

### Two Brief Creation Paths
The system supports two campaign creation approaches:
- **Insight-driven**: Uses `14 Brief Creator.docx` with full competitive analysis
- **Direct creation**: Uses `18 Briefs without Insights Prompt.docx` for faster generation

## Product Context

ScaleFox's core value proposition centers on:
- **Competitive intelligence-first approach**: Analyzes competitor ads, landing pages, and social presence before creating campaigns
- **GTM Playbook methodology**: Structured, repeatable process based on winning patterns
- **Speed**: Under 5 minutes from competitor analysis to campaign-ready ads
- **LinkedIn specialization**: B2B-focused, targeting busy founders and marketers at startups

## Working with These Prompts

### When Modifying Prompts

Maintain consistency with ScaleFox's brand voice:
- Confident and results-oriented language
- Emphasis on speed, competitive advantage, and intelligence
- Professional yet accessible tone
- Quantifiable benefits where possible

### When Adding New Prompts

Follow the established numbering convention:
- Use sequential numbers for workflow stages
- Use letter suffixes (e.g., 2a) for variant approaches
- Large orchestration documents use descriptive names

### Document Relationships

The prompts reference and depend on:
- `../product-info.md` - ScaleFox brand and product context
- `../competitive-analysis.md` - 9-phase competitive analysis framework
- `../competitors.md` - Analyzed competitor intelligence database

## File Format Notes

All prompts are stored as `.docx` files (Microsoft Word format). The largest files are:
- `14 Brief Creator.docx` (220KB) - Most comprehensive brief generation
- `18 Briefs without Insights Prompt.docx` (220KB) - Alternative brief path
- `Orchestration Flow.docx` (213KB) - Master workflow documentation

These larger files likely contain extensive examples, templates, or multi-stage instructions.
