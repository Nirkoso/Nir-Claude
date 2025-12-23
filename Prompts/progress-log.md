# Progress Log – Prompts Folder Formatting Project

[2025-12-04 00:00] orchestrator: initiated formatting project for 12 remaining markdown files
[2025-12-04 00:01] orchestrator: formatted 4 Analyze ad prompt.md - added proper headers, formatted JSON blocks, fixed lists and spacing
[2025-12-04 00:02] orchestrator: formatted 5 Ads Insight Prompt.md - restructured sections with proper headers, formatted JSON blocks
[2025-12-04 00:03] orchestrator: formatted 6 Overall Market summary prompt.md - converted XML tags to headers, formatted JSON examples
[2025-12-04 00:03] orchestrator: Batch 1 complete (3/12 files done)
[2025-12-04 00:04] orchestrator: formatted 7 Analyze Insight prompt.md - converted XML tags to headers, structured JSON examples
[2025-12-04 00:05] orchestrator: formatted 8 Summarize Ads Analysis prompt.md - proper headers and JSON formatting
[2025-12-04 00:06] orchestrator: formatted 9 mini company info prompt.md - restructured sections with proper headers
[2025-12-04 00:06] orchestrator: Batch 2 complete (6/12 files done)
[2025-12-04 00:07] orchestrator: formatted 13 remix ad prompt.md - converted XML tags to headers, proper structure
[2025-12-04 00:08] orchestrator: formatted 14 Brief Creator.md - major restructuring with headers and lists
[2025-12-04 00:09] orchestrator: formatted 16 Copy Generation.md - simple structure with JSON code block
[2025-12-04 00:09] orchestrator: Batch 3 complete (9/12 files done)
[2025-12-04 00:10] orchestrator: formatted 17 Template Generation Prompt.md - consolidated duplicates, proper structure
[2025-12-04 00:11] orchestrator: formatted 18 Briefs without Insights Prompt.md - similar to #14 but without insights
[2025-12-04 00:12] orchestrator: formatted Orchestration Flow.md - structured workflow documentation
[2025-12-04 00:12] orchestrator: Batch 4 complete - ALL 12 FILES FORMATTED SUCCESSFULLY

## Recent Updates

[2025-12-19 14:30] claude: Enhanced 13 remix ad prompt.md - Added quality assurance requirements
  - Added "Quality Assurance" subsection under Copy Rules with spell-check requirements
  - Added spelling/grammar PASS/FAIL checks to Audit section
  - Created new "Copy Quality Standards" section with 5-step checklist
  - Added prohibition against spelling/grammatical errors to Negative List
  - Ensures all generated ads are free from spelling and grammar mistakes

[2025-12-19 14:45] claude: Created 19 edit image.md - New image editing prompt
  - Created comprehensive prompt for editing ad images based on user requests
  - Prioritized text changes as highest priority (must be applied exactly)
  - Integrated CompanyLogo as required input (SECOND_ATTACHED_IMAGE)
  - Added logo integrity verification (check presence, insert if missing, preserve 100%)
  - Included quality checks for spelling/grammar in all text edits
  - Optimized for LLM context (concise, scannable format with bullets and checklists)
  - Inputs: OriginalImage, CompanyLogo, UserRequest, CompanyInfo, Brand, BestPractices
  - Priority hierarchy: 1) Logo integrity, 2) Text accuracy, 3) Copy quality, 4) Brand consistency

[2025-12-21 15:30] claude: Created 20 analyze ad output.md - Comprehensive ad quality auditor
  - Created comprehensive prompt for auditing generated ads against production standards
  - Validates 10 technical compliance checks (spelling, grammar, logo, contrast, legibility, etc.)
  - Rates creative quality across 4 brand alignment + 6 creative quality dimensions
  - Calculates overall quality score with weighted algorithm (Technical 30%, Brand 20%, Creative 30%, Brief 20%)
  - Generates specific, actionable image improvement suggestions for edit modal
  - Creates detailed video transformation instructions focused on main image animation
  - Inputs: GeneratedAd, Brief, CompanyInfo, Brand, BestPractices
  - Outputs: Structured JSON with audit results, scores, critical issues, improvements, and video instructions
  - File size: ~8KB, optimized for LLM context

[2025-12-21 15:45] claude: Updated 20 analyze ad output.md - Added logo verification and subtle video motion
  - Added CompanyLogo input (SECOND_ATTACHED_IMAGE) for logo verification
  - Updated logo audit to check against reference CompanyLogo for exact match
  - Refined video transformation instructions to emphasize minimal, subtle motion
  - Motion philosophy: Main image priority (people, products), minimal text motion, no fade-ins
  - People animations: Micro-expressions (smiles, nods, eye shifts toward CTA/headline)
  - Product animations: Gentle rotation (3-5°), floating, subtle shine effects
  - Text/CTA: Static preferred, minimal pulse/glow enhancements only
  - Logo: Always static, no motion
  - Updated examples to show subtle looping motion with smooth transitions
  - All motion scaled to prevent jumps (1-3% max movement)

[2025-12-21 16:00] claude: Created 21 image to video.md - Video prompt generator
  - Created prompt for transforming static ads into video animations for Kling01 model
  - Absolute content preservation: Zero changes to text, colors, layout, or branding
  - Generates optimized video prompts that add motion without modifying original content
  - Motion categories: People (micro-expressions), Products (rotation/floating), Scenes (parallax/zoom)
  - Includes detailed examples with technical specs (duration, loop type, intensity)
  - Quality checklist ensures logo stays static, text remains readable, seamless looping
  - Inputs: StaticAd, VideoInstructions (from ad analysis), CompanyInfo, Brand
  - Output: Plain-text video prompt ready for direct Kling01 input
  - File size: ~7KB, optimized for LLM context

[2025-12-21 16:15] claude: Updated 21 image to video.md - Added UserInput support as highest priority
  - Added UserInput parameter as optional, highest-priority input
  - Dual-mode operation: Mode 1 (UserInput provided) vs Mode 2 (Auto from VideoInstructions)
  - Mode 1 process: Parse UserInput → Quality Check (spell/grammar) → Enrich → Safety Validate → Construct
  - Quality checks fix spelling/grammar errors in user input before enriching
  - Safety validation adjusts aggressive requests (e.g., "spin" → "gentle rotation")
  - Enrichment adds technical details while preserving user's creative intent
  - Added 3 UserInput examples: clean input, aggressive adjusted, spelling fixed
  - Updated quality checklist with separate UserInput verification section
  - Important section emphasizes: User intent is HIGHEST PRIORITY, optimize don't override
  - Final output always reflects user's vision while ensuring brand safety and quality
