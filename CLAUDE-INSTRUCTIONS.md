# Claude Instructions: Generate Agentic R&D Documentation Framework

> Use this prompt to instruct Claude (Claude Code, Claude.ai, or API) to generate a complete R&D documentation framework for any research project.

---

## How to Use This Document

**Copy everything below the line into Claude with your project details filled in.**

---

# START OF PROMPT

## Your Task

You are an AI engineering assistant helping me set up a document-driven agentic R&D workflow. I need you to create a complete documentation framework for systematic research and development that will:

1. Pass Australian R&D Tax Incentive (RDTI) audit criteria
2. Enable context-efficient AI-assisted experimentation
3. Produce clear, timestamped evidence of research activities
4. Document both successful findings AND rejected hypotheses

---

## Project Details

**Fill in these fields before sending to Claude:**

```
PROJECT_NAME: [e.g., Engage AI]
PROJECT_REFERENCE: [e.g., ENGAGE-AI-LLM-FM-2025]
RESEARCH_TITLE: [e.g., Investigating LLM Failure Modes in Restaurant Information Extraction]

RESEARCH_QUESTION: [The core unknown you're investigating]
Example: "What triggers LLMs to fail when extracting restaurant information, and what content structures prevent each failure mode?"

TARGET_USERS: [Who will use this research]
Example: "RDTI auditors, internal dev team, future researchers"

KNOWLEDGE_GAP: [What a competent professional cannot predict without experimentation]
Example: "These triggers cannot be predicted from first principles because they arise from complex interactions between content structure, LLM training data, and model architecture."

FAILURE_MODES_OR_RESEARCH_AREAS: [List 3-5 specific areas to investigate]
Example:
1. Price Hallucination - Why LLMs invent or misread prices
2. Menu Item Invention - What triggers fabrication of non-existent items
3. Dietary Misclassification - Why dietary attributes are missed
4. Information Blending - What causes cross-contamination between sections
5. Temporal Confusion - What triggers stale event presentation

TECH_STACK: [Technologies used in research]
Example: Node.js, MongoDB Atlas, OpenAI API, Anthropic API, xAI API, HuggingFace embeddings

SUCCESS_CRITERIA: [How you'll know research succeeded]
Example: 
- Each failure mode has identified trigger(s) validated by modification testing
- Prevention strategies documented with before/after accuracy metrics
- Findings are non-obvious and couldn't be predicted from first principles
```

---

## Files to Generate

Create the following directory structure and files:

```
{project-name}-rd/
├── PRD.md
├── GLOBAL-RULES.md
├── CLAUDE-INSTRUCTIONS.md (this file, for reference)
├── reference/
│   ├── RDTI-AUDIT-CRITERIA.md
│   ├── FAILURE-MODE-TAXONOMY.md (optional)
│   └── CONTENT-FORMAT-SPECS.md (optional)
├── experiments/
│   ├── STRUCTURED-PLAN-TEMPLATE.md
│   ├── RESULTS-TEMPLATE.md
│   ├── {failure-mode-1}/
│   │   ├── PLAN.md
│   │   ├── RESULTS.md
│   │   ├── data/
│   │   ├── queries/
│   │   └── results/
│   ├── {failure-mode-2}/
│   │   └── [same structure]
│   └── [etc for each failure mode]
└── outputs/
    └── [final deliverables go here]
```

---

## File Specifications

### 1. PRD.md (Product Requirements Document)

This is the "North Star" document. Include:

- **Project Identity Table:** Name, reference, title, version, date
- **Target Users:** Who uses this research
- **Mission Statement:** One clear statement of what you're investigating
- **Knowledge Gap:** Why this requires experimentation (RDTI justification)
- **In-Scope:** 3-5 specific failure modes/research areas with:
  - Research question
  - Hypothesis candidates
  - Evidence metric (simple Yes/No or percentage)
- **Out-of-Scope:** What you're NOT investigating (Phase 2 candidates)
- **Architecture/Tech Stack:** Diagram and table of technologies
- **Success Criteria:** Research success AND RDTI compliance success
- **Document Hierarchy:** Visual tree of all documentation

### 2. GLOBAL-RULES.md

Rules that govern ALL documentation and experimentation:

**Section 1: Documentation Standards**
- Header metadata requirements (name, version, date, author)
- Character count tracking for RDTI fields
- Writing style (active voice, specific claims, no hedging)
- RDTI-specific language to AVOID (red flags) and USE (defensible phrases)

**Section 2: Experiment Execution Rules**
- Pre-experiment checklist (read PRD, read PLAN, verify data, check APIs)
- During-experiment rules (log everything, no cherry-picking, version control, isolate variables)
- Classification codes table:
  - PASS, FAIL-HALLUCINATION, FAIL-OMISSION, FAIL-MUTATION, FAIL-BLEND, FAIL-TEMPORAL
- Statistical requirements (minimum sample sizes)

**Section 3: Code Standards**
- Test run data structure (what to capture)
- Content file versioning rules (semantic versioning)
- Directory structure specification

**Section 4: Hypothesis-Experiment-Finding Flow**
- Required narrative template for each finding
- Rejected hypothesis documentation template (critical for RDTI)

**Section 5: Context Window Management**
- `/prime` command: Load PRD + GLOBAL-RULES, identify next step
- `/execute` command: Context reset protocol, load only PLAN.md
- `/reflect` command: Post-execution system improvement

**Section 6: Quality Gates**
- Before merging results checklist
- Before updating RDTI application checklist

### 3. reference/RDTI-AUDIT-CRITERIA.md

Self-audit checklist with 5 criteria:

1. **Unknown Outcomes:** Pass/fail indicators, self-audit questions
2. **Testable Hypothesis:** "If X then Y because Z" format requirements
3. **Systematic Experimentation:** Variable isolation, sample size, controls
4. **Observation and Evaluation:** Data preservation, causal analysis
5. **New Knowledge:** Quantified thresholds, generalizable principles

Also include:
- Red flag phrases to avoid (with better alternatives)
- Evidence checklist for experiments and findings
- Quick audit scorecard (1-5 rating per criterion)
- Common audit challenges and defense scripts

### 4. experiments/STRUCTURED-PLAN-TEMPLATE.md

Template for experiment planning with these sections:

1. **Experiment Metadata:** Failure mode, version, status, PRD reference
2. **Research Question:** Primary and secondary questions
3. **Background Context:** What observed, existing knowledge, knowledge gap
4. **Hypotheses:** 3-5 testable hypotheses in "If X then Y because Z" format
5. **Experimental Design:**
   - Variables table (independent, dependent, control)
   - Test conditions table
   - Sample size with justification
6. **Task Breakdown:** Phased tasks with checkboxes, deliverables, acceptance criteria
   - Phase 1: Setup
   - Phase 2: Baseline testing
   - Phase 3+: Hypothesis testing (one phase per hypothesis)
   - Final Phase: Analysis and integration
7. **Test Queries:** Table or reference to query file
8. **Success Criteria:** Experiment-specific and RDTI compliance
9. **Risks and Mitigations:** Table format
10. **Resources Required:** Table with status
11. **Change Log:** Date, version, change, author

### 5. experiments/RESULTS-TEMPLATE.md

Template for documenting results with these sections:

1. **Results Metadata:** Failure mode, plan version, status, investigator
2. **Executive Summary:** Primary finding, triggers, prevention strategies (write LAST)
3. **Baseline Results:**
   - Test configuration table
   - Accuracy by LLM table
   - Failure mode breakdown table
   - Example failures with query/expected/actual/classification
4. **Hypothesis Testing Results:** One subsection per hypothesis with:
   - Statement
   - Test configuration (baseline vs modified)
   - Results table (before/after accuracy per LLM)
   - Verdict: ✅ CONFIRMED / ❌ REJECTED / ⚠️ INCONCLUSIVE
   - Interpretation
5. **Confirmed Findings:** Full documentation using GLOBAL-RULES template
6. **Rejected Hypotheses:** Full documentation (critical for RDTI)
7. **Cross-LLM Analysis:** Universal vs model-specific triggers table
8. **Prevention Strategies:** Actionable strategies with effectiveness metrics
9. **New Knowledge Summary:** Thresholds, unexpected findings, generalizable principles
10. **Limitations and Future Work**
11. **Raw Data References:** Table with file locations
12. **Change Log**

### 6. First Experiment PLAN.md

Create a complete, filled-in PLAN.md for the FIRST failure mode/research area. This should be detailed enough to execute immediately, including:

- All hypotheses written out
- All test conditions defined
- All tasks with specific deliverables
- Sample queries listed
- Specific success criteria with numbers

### 7. First Experiment RESULTS.md

Create a placeholder RESULTS.md for the first experiment with:
- All sections from template
- Status: NOT STARTED
- Tables with placeholder dashes (-)
- Ready to be filled in during execution

---

## Agentic Workflow Commands

Include these commands in GLOBAL-RULES.md:

### /prime
```
Read PRD.md and GLOBAL-RULES.md. Based on the research objectives 
and current state of experiments/, what is the most logical next step?
```

### /execute
```
CONTEXT RESET: Clear conversation history or start new session before this.

Read ONLY the experiments/{failure-mode}/PLAN.md provided. 
Execute the tasks listed in the plan one by one. 
Perform self-validation after each step.
Document results in RESULTS.md.
```

### /reflect
```
I noticed [describe bug/error/issue]. Instead of just fixing it:
1. Is there a missing rule in GLOBAL-RULES.md?
2. Do we need a new reference document?
3. How should we update STRUCTURED-PLAN-TEMPLATE.md to prevent this?
```

---

## Critical Requirements

1. **All documents must be markdown (.md)** for Git version control
2. **Include character counts** for any RDTI fields with limits
3. **Use tables extensively** for structured information
4. **Include change logs** at the bottom of every document
5. **Make templates copy-paste ready** with clear placeholders
6. **Focus on EVIDENCE** — timestamps, version numbers, raw counts
7. **Document REJECTED hypotheses** — this proves real experimentation

---

## Output Format

After generating all files:

1. Show the directory tree
2. Provide a summary of what was created
3. Explain how to start using the framework:
   - First: Read PRD.md
   - Then: Use /prime to get oriented
   - Then: Execute first experiment with /execute
   - Finally: Document results and /reflect

---

## Example Execution

If I provide:
```
PROJECT_NAME: Engage AI
RESEARCH_TITLE: Investigating LLM Failure Modes in Restaurant Information Extraction
FAILURE_MODES:
1. Price Hallucination
2. Menu Item Invention
3. Dietary Misclassification
```

You should generate:
- PRD.md customized for Engage AI
- GLOBAL-RULES.md with restaurant/LLM specific examples
- RDTI-AUDIT-CRITERIA.md
- STRUCTURED-PLAN-TEMPLATE.md
- RESULTS-TEMPLATE.md
- experiments/price-hallucination/PLAN.md (fully detailed)
- experiments/price-hallucination/RESULTS.md (placeholder)
- Empty directories for menu-invention and dietary-misclassification

---

# END OF PROMPT

---

## Notes for User

- **Customize the PROJECT DETAILS section** before sending to Claude
- **Save this file** — you can reuse it for future R&D projects
- **Claude Code users:** Open this in your project directory, Claude will create files in place
- **Claude.ai users:** Claude will create files and you can download them

---

## Version History

| Date | Version | Notes |
|------|---------|-------|
| 2026-01-26 | 1.0 | Initial creation for Engage AI project |
