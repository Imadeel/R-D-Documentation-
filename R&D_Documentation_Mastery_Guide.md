# R&D Tax Incentive Documentation Mastery Guide

## Learnings from Engage AI Project & Audit Experience

*A comprehensive guide to writing audit-proof R&D documentation aligned with Section 355-25 and 355-30 of the Income Tax Assessment Act 1997*

---

## Executive Summary

This guide captures critical learnings from the Engage AI R&D project and subsequent audit simulations. The fundamental insight: **R&D documentation fails because it describes engineering work, not research investigation**. The shift from "we built and tested" to "we investigated why" is the core transformation needed for audit success.

---

## Part 1: The Mindset Shift

### From Engineering to Research

The single most important transformation is reframing your work as **investigation into unknowns** rather than **development toward goals**.

| Engineering Mindset (FAILS AUDIT) | Research Mindset (PASSES AUDIT) |
|-----------------------------------|--------------------------------|
| "We built a system that does X" | "We investigated what causes X to fail" |
| "We tested until it worked" | "We observed failures → hypothesised triggers → tested → validated" |
| "Our system achieves 95% accuracy" | "We discovered that accuracy degrades at threshold Y because of mechanism Z" |
| "We tried format A, then B, then C" | "We manipulated variable A while controlling B to measure effect on C" |
| "The outcome was better performance" | "The outcome was new knowledge about causal relationships" |

### The Core Question Test

Before writing any section, ask: **"Am I describing what we built, or what we learned?"**

- ❌ "We developed an AI system for restaurant ordering"
- ✅ "We investigated what triggers LLMs to fail when extracting restaurant information"

---

## Part 2: The Five Audit Criteria

Every R&D application must demonstrate ALL five criteria. Missing any one results in rejection.

### Criterion 1: Unknown Outcomes

**Legislative requirement:** "The outcome cannot be known or determined in advance on the basis of current knowledge, information or experience."

#### The Competent Professional Test

The critical question is NOT "Could YOUR company predict the outcome?" but "Could ANY competent professional in the field predict the outcome?"

**Weak (Will Fail):**
> "We didn't know if our system would work"

**Strong (Will Pass):**
> "A competent ML engineer with 10+ years experience, access to published literature and vendor documentation, could not determine the specific threshold at which LLM accuracy degrades because no published research addresses this question for our domain"

#### What Makes Outcomes Genuinely Unknown

| Predictable (FAILS) | Genuinely Unknown (PASSES) |
|--------------------|---------------------------|
| "Structured JSON parses better than prose" | "At what complexity threshold does extraction fail regardless of format?" |
| "More data improves accuracy" | "What specific corpus representation threshold causes safety-critical failures?" |
| "Ensemble methods reduce variance" | "What is the correlation strength between inter-model disagreement and extraction errors?" |
| "Format X works better than Y" | "WHY does format X trigger failures that format Y doesn't?" |

#### Counterintuitive Findings = Strong Evidence

The Engage AI project succeeded because findings contradicted professional expectations:

1. **Proximity doesn't matter** — Auditors expect nearby numbers cause price confusion; experimentation showed format consistency matters more
2. **Timestamps don't work** — "Tonight" outperforms "2025-01-15" for temporal content (counterintuitive)
3. **Position doesn't prevent blending** — Name similarity causes cross-contamination, not file organisation
4. **Schema.org markup provides zero benefit** — Null finding contradicts industry assumptions

**Key Insight:** Null findings and counterintuitive results are MORE valuable for R&D claims than expected outcomes.

---

### Criterion 2: Testable Hypothesis

**Legislative requirement:** Hypothesis must identify technical knowledge gaps expressed in terms of causal relationships between technical variables.

#### The Hypothesis Format

**WRONG FORMAT (Objective Disguised as Hypothesis):**
> "We hypothesize we can build a system that achieves X"

**CORRECT FORMAT:**
> "If [variable X changes in manner A], then [outcome Y] will occur, because of [scientific/engineering principle Z]"

#### Required Elements

| Element | Description | Example |
|---------|-------------|---------|
| Independent Variable | What you manipulate | Content format (JSON vs prose) |
| Dependent Variable | What you measure | Extraction error rate |
| Control Variables | What you hold constant | Query wording, LLM model, content amount |
| Causal Mechanism | Scientific principle explaining WHY | Transformer attention allocation theory |
| Falsification Criteria | What would prove hypothesis wrong | If error rate shows no significant difference |

#### Good Hypothesis Examples

**Example 1: Price Hallucination**
> "H1: If price format heterogeneity increases within a content file (measured by coefficient of variation in price notation), then LLM price extraction error rate will increase proportionally, because inconsistent patterns create ambiguous token boundaries during transformer parsing. We predict r > 0.5 correlation. Falsified if r < 0.3."

**Example 2: Multi-Model Disagreement**
> "H2: If inter-model disagreement between GPT-4 and Claude on extracted entities (measured as Jaccard distance) correlates with actual extraction error rate (r > 0.7), then disagreement can serve as confidence scoring without ground-truth labels, because model architectures produce independent errors on genuinely ambiguous content."

#### Hypothesis Quality Checklist

- [ ] States causal relationship: "If X, then Y because Z"
- [ ] Identifies independent variable (manipulated)
- [ ] Identifies dependent variable (measured)
- [ ] Identifies control variables (held constant)
- [ ] Proposes mechanism (WHY the relationship exists)
- [ ] Includes falsification criteria (what would disprove it)
- [ ] Is NOT a specification or performance target
- [ ] Could be published in a peer-reviewed venue

---

### Criterion 3: Systematic Experimentation

**Legislative requirement:** Activities must proceed from hypothesis to experiment, observation and evaluation based on principles of established science.

#### Experiments vs Development

| Iterative Development (FAILS) | Systematic Experimentation (PASSES) |
|------------------------------|-------------------------------------|
| Try A → fails → try B → fails → try C → works | Design experiment to test why A fails |
| Build feature, test if it works | Manipulate variables, measure dependent outcomes |
| Debug until passing | Observe failure modes, hypothesise causes |
| 80 tests across configurations | 1,460 observations with statistical analysis |
| "We tried until it worked" | "We isolated cause and effect" |

#### Required Experimental Elements

1. **Independent variables clearly identified and systematically varied**
2. **Dependent variables measured with defined metrics**
3. **Control variables held constant**
4. **Sample size justification**
5. **Randomisation or controlled ordering**
6. **Statistical analysis plan (significance thresholds)**
7. **Pre-registered success/failure criteria**

#### Experiment Description Template

> "To test H1 (price format heterogeneity increases errors), we designed a controlled experiment manipulating format consistency while holding other variables constant.
>
> **Independent Variable:** Price format heterogeneity (coefficient of variation 0-1)
>
> **Dependent Variable:** Extraction error rate (measured as false positive + false negative)
>
> **Control Variables:** Menu size, item count, query phrasing, LLM temperature
>
> **Method:** We generated 40 content versions with varying format heterogeneity levels (n=10 per quartile). Each version was tested with 25 standardised queries across 2 LLM engines (GPT-4, Claude), producing 2,000 observations. Results were analysed using Pearson correlation with significance threshold p < 0.05.
>
> **Falsification:** Hypothesis rejected if correlation r < 0.3 or p > 0.05."

#### What Failure Looks Like

**Critical requirement:** You must be able to articulate what a failed experiment would look like.

- "If error rates show no significant difference across format variations, the hypothesis is rejected"
- "If correlation is below threshold (r < 0.3), we conclude format heterogeneity is not a causal factor"

---

### Criterion 4: Observation and Evaluation

**Legislative requirement:** Results must be analysed to understand causal relationships and evaluate hypothesis validity.

#### The Key Distinction

| Recording WHAT Happened (Weak) | Analysing WHY It Happened (Strong) |
|-------------------------------|-----------------------------------|
| "Error rate was 28% baseline, 5% after" | "Error analysis revealed format inconsistency triggers tokenisation ambiguity" |
| "It worked better" | "Effect size (Cohen's d = 1.2) indicates large practical significance" |
| "We observed improvement" | "Causal mechanism identified: inconsistent notation creates competing parse interpretations" |

#### Required Evaluation Elements

1. **Statistical significance testing** (chi-square, t-test, ANOVA)
2. **Effect size calculation** (Cohen's d, partial η²)
3. **Confidence intervals** where applicable
4. **Causal mechanism identification** (WHY results occurred)
5. **Hypothesis disposition** (supported/partially supported/rejected)
6. **Failed experiment documentation** (equally valuable)

#### Evaluation Template

> "Analysis of experimental results used chi-square tests for categorical outcomes and Pearson correlation for continuous relationships. Results showed:
>
> **H1 (Price Format):** Supported. Correlation between format heterogeneity and error rate was significant (r = 0.67, p < 0.001). Causal mechanism identified: LLMs tokenise inconsistent price patterns as separate semantic units, triggering confusion.
>
> **H2 (Proximity):** Rejected. No significant correlation between numeric proximity and errors (r = 0.12, p = 0.34). This null finding contradicts initial expectation that nearby numbers cause confusion.
>
> Failure mode analysis revealed four distinct error categories: format ambiguity (34%), attention overflow (28%), token boundary misalignment (23%), training data contamination (15%). Each mode requires different mitigation strategies."

---

### Criterion 5: New Knowledge Generation

**Legislative requirement:** Activities must be conducted for the purpose of generating new knowledge.

#### New Knowledge vs System Benchmarks

| System-Specific Benchmarks (FAILS) | Generalisable Knowledge (PASSES) |
|-----------------------------------|--------------------------------|
| "Our system achieves 95% accuracy" | "Accuracy degrades at 1,847-token threshold (95% CI: 1,780-1,914)" |
| "Multi-file format works better" | "LLMs don't follow hyperlinks—contradicts llms.txt convention assumptions" |
| "We found the best configuration" | "Token distance correlates negatively with accuracy (r = -0.73, β = -0.042 per 100 tokens)" |

#### New Knowledge Checklist

- [ ] **Generalisable:** Applies beyond this specific system/dataset
- [ ] **Publishable:** Could appear in peer-reviewed journal
- [ ] **Novel:** Not available in existing literature
- [ ] **Quantified:** Includes specific measurements, not just qualitative claims
- [ ] **Transferable:** Other organisations could apply this knowledge
- [ ] **Not a benchmark:** Not just "our system achieves X performance"

#### New Knowledge Examples from Engage AI

1. **Price Error Triggers:** Format inconsistency is dominant trigger; numeric proximity has minimal effect (contradicts expectations)

2. **Invention Prevention:** Explicit completeness signals reduce fabrication—LLMs interpret incomplete-seeming content as invitation to fill gaps

3. **Structured vs Prose:** Identical information extracts reliably from dedicated fields but unreliably from prose (same content, different outcomes based on placement)

4. **Name Similarity Effect:** Information blending correlates with item name similarity, not file position (distinctive naming more important than careful positioning)

5. **Temporal Signal Processing:** Contextual language ("tonight") outperforms formal timestamps ("2025-01-15")—counterintuitive finding

---

## Part 3: The Failure Mode Framing Approach

### Why This Framing Works

The Engage AI project transformation succeeded by shifting from:
- ❌ "Testing formats to find the best one"
- ✅ "Investigating what TRIGGERS failures and WHY"

This reframing works because:

1. **Failure triggers are genuinely unknown** — You can't predict from first principles why THIS query fails but a similar one succeeds

2. **Investigation is demonstrable** — "Observe failure → hypothesise trigger → modify → test → evaluate" is clear scientific method

3. **Evidence is simple** — Error logs, file versions, pass/fail counts (no complex statistics needed)

4. **Counterintuitive findings emerge** — Investigation reveals things professionals wouldn't expect

### Failure Mode Investigation Structure

| Failure Mode | Unknown Being Investigated | Evidence Required |
|--------------|---------------------------|-------------------|
| Price Hallucination | What triggers price misreading? Proximity? Format? Density? | Error logs showing when/why prices fail |
| Item Invention | What causes fabrication? Missing data? Ambiguous signals? | Before/after comparison with completeness signals |
| Attribute Misclassification | Why are dietary tags missed? Format? Position? Conflicting signals? | Classification accuracy by content structure |
| Information Blending | What causes cross-contamination? Position? Similarity? Section boundaries? | Error patterns by content organisation |
| Temporal Confusion | What triggers stale content presentation? Date formats? Language? | Freshness accuracy by temporal signal type |

---

## Part 4: Evidence Requirements

### Contemporaneous Documentation Checklist

Documentation MUST be dated BEFORE the work it describes. Retrospective documentation raises audit flags.

| Evidence Type | Timing | Example |
|--------------|--------|---------|
| Literature review | BEFORE experimental work | "December 2024: Searched Google Scholar, vendor docs; no results for [specific question]" |
| Hypothesis statements | BEFORE experiments | "January 2025: H1 documented with falsification criteria" |
| Experimental design | BEFORE data collection | "January 2025: Test protocol with variables identified" |
| Test logs | DURING experiments | "February-March 2025: 2,000 observations with parameters recorded" |
| Analysis results | AFTER data collection | "April 2025: Statistical analysis completed" |

### Acceptable Evidence Types

- **Git commits and timestamps** — Shows iteration and decision points
- **Jupyter/MLflow experiment runs** — Demonstrates systematic testing
- **Architecture iteration notes** — Documents design decisions driven by experimental findings
- **Internal research notes** — Captures reasoning and uncertainty
- **Data analysis logs** — Shows evaluation methodology
- **Sprint planning documents** — Links work to experimental objectives
- **Error logs with timestamps** — Demonstrates failure observation

### Evidence Language (Git Commits Example)

**Avoid:**
- "fix", "final", "complete", "production", "deploy", "ship"

**Use:**
- "test", "trial", "experiment with", "investigate"
- "tune", "adjust", "calibrate", "modify"
- "evaluate", "measure", "benchmark", "assess"
- "analyse", "inspect", "examine"
- "log", "record", "capture"
- "compare", "contrast", "evaluate against"

**Good Commit Examples:**
```
2025-02-14 | test prose vs JSON format for dietary attribute extraction
2025-02-18 | evaluate impact of completeness signals on fabrication rate
2025-02-25 | analyse failure patterns in price extraction across format variants
2025-03-02 | tune section boundary markers to measure blending reduction
```

---

## Part 5: Red Flags to Avoid

### Language Red Flags

| Red Flag | Why It Fails | Better Alternative |
|----------|-------------|-------------------|
| "We built a system that..." | Describes development, not investigation | "We investigated what causes..." |
| "We hypothesise we can achieve..." | Objective disguised as hypothesis | "We hypothesise that [X] causes [Y] because [Z]" |
| "We tested until it worked" | Iterative development, not experimentation | "We systematically varied [X] to measure effect on [Y]" |
| "Unknown to us" | Company ignorance ≠ field uncertainty | "A competent professional could not determine because..." |
| "Novel combination of technologies" | Integration ≠ R&D | "The interaction produces scientifically unpredictable emergent properties because..." |
| "Nobody has built this exact system" | Not evidence of uncertainty | "No published research addresses [specific question]" |

### Structural Red Flags

- **Performance targets as hypotheses:** "We will achieve 95% accuracy" is a goal, not a hypothesis
- **No falsification criteria:** If you can't describe what failure looks like, it's not experimentation
- **No variables identified:** Without independent/dependent/control variables, it's not systematic
- **100% of expenditure claimed:** No project is 100% R&D—always apportion
- **Generic evidence claims:** "We kept documentation" without specifics

### Domain-Specific Red Flags

- **"Vendor documentation doesn't cover our use case"** — But could a skilled engineer figure it out?
- **"We tuned hyperparameters through experimentation"** — Hyperparameter optimisation is engineering, not R&D
- **"We A/B tested different approaches"** — A/B testing for user preferences is product development
- **"We integrated technologies in a new way"** — Integration is not R&D unless emergent properties investigated

---

## Part 6: Section-by-Section Writing Templates

### Project Objectives Template

> "The project objectives are to resolve technical uncertainties regarding [specific scientific/technical question] where existing knowledge provides no validated solution. Specifically, we seek to determine: (1) [knowledge gap 1], (2) [knowledge gap 2], (3) [knowledge gap 3]. These questions cannot be resolved through literature review, expert consultation, or application of standard engineering practices because [explanation of why experimentation required]."

**DON'T:** List product features, describe business objectives, state performance targets

### Core Activity Description Template

> "This core R&D activity investigates [scientific/technical question] through systematic experimentation. The activity tests hypotheses regarding [causal relationships being investigated]. Technical uncertainties exist because [explanation of knowledge gap]. The experimental approach involves [brief methodology]. This investigation is necessary because [why existing knowledge is insufficient]."

**DON'T:** Describe building the product, list technologies used, explain system architecture

### Literature Review Template

> "Prior to experimental work, systematic investigation was undertaken to establish whether existing knowledge could address the identified uncertainties.
>
> **[Source Category 1]:** [Specific search conducted], [specific papers/documentation reviewed], [specific gap identified].
>
> **[Source Category 2]:** [Specific vendor documentation reviewed], [what it covers], [what it doesn't address].
>
> **Conclusion:** Existing literature addresses [what is known] but does not provide guidance on [specific unknown], necessitating experimental investigation."

**DON'T:** "We reviewed the literature and found nothing" — must show specific searches with specific gaps

### Competent Professional Statement Template

> "A competent professional in [field], defined as someone with:
> - [Qualification level] in [relevant discipline]
> - [Years] industry experience in [specific domain]
> - Familiarity with [relevant technologies/literature]
> - Access to published literature and vendor documentation
>
> could not have determined the following outcomes in advance:
>
> **[Finding 1]:** While a competent professional would expect [general principle], they could not predict [specific finding] because [explanation of why prediction impossible].
>
> **[Finding 2]:** [Same structure]"

---

## Part 7: Validation Checklist

Before submitting, verify each section passes these tests:

### Overall Structure
- [ ] Framed as investigation, not development
- [ ] Focuses on what was LEARNED, not what was BUILT
- [ ] Uncertainty is about WHY, not WHETHER

### Criterion 1: Unknown Outcomes
- [ ] Competent professional test explicitly addressed
- [ ] Specific literature review with specific gaps
- [ ] Dated BEFORE experimental work

### Criterion 2: Hypothesis
- [ ] Causal format: "If X, then Y, because Z"
- [ ] Independent, dependent, control variables identified
- [ ] Scientific principle cited
- [ ] Falsification criteria stated

### Criterion 3: Experimentation
- [ ] Variables systematically manipulated
- [ ] Sample sizes justified
- [ ] Statistical methodology stated
- [ ] Failure criteria defined

### Criterion 4: Evaluation
- [ ] Statistical significance tested
- [ ] Causal mechanisms identified
- [ ] Hypothesis disposition stated
- [ ] Failed experiments documented

### Criterion 5: New Knowledge
- [ ] Generalisable beyond this project
- [ ] Quantified findings
- [ ] Could be published
- [ ] Not just system benchmarks

### Evidence
- [ ] Dated records for each phase
- [ ] Literature review dated BEFORE experiments
- [ ] Hypothesis dated BEFORE tests
- [ ] Specific evidence types listed

---

## Part 8: The Audit Defence Strategy

### Preparing for Audit Queries

**Query 1:** "How is this different from standard software development?"

**Response:** "Standard development asks 'does it work?' Our investigation asked 'why does it fail?' We documented systematic experimentation manipulating variables to identify causal triggers, not iterative debugging until passing."

**Query 2:** "Couldn't a competent professional predict these outcomes?"

**Response:** "A competent professional could predict general principles (e.g., structured data parses more reliably). They could NOT predict: (a) the specific threshold at which accuracy degrades, (b) which factors are causal vs coincidental, (c) the counterintuitive findings such as [specific example]."

**Query 3:** "This looks like A/B testing, which is excluded"

**Response:** "A/B testing compares user preferences between product variants. Our experimentation manipulated technical variables to understand causal mechanisms. The dependent variable was not user preference but technical performance metrics analysed for causal relationships."

**Query 4:** "Where is the new knowledge that advances the field?"

**Response:** "Our findings are generalisable beyond this implementation: (a) [Specific finding 1] applies to any system handling [domain], (b) [Specific finding 2] contradicts assumptions in published literature [citation], (c) [Specific finding 3] could be documented in a technical paper for [venue]."

---

## Conclusion: The Core Principles

1. **Investigation, not development** — Describe what you learned, not what you built

2. **Failure modes, not success metrics** — Understanding WHY things fail is R&D; achieving targets is engineering

3. **Causal mechanisms, not outcomes** — The knowledge is about cause-and-effect relationships, not performance numbers

4. **Counterintuitive findings** — Results that contradict professional expectations are strongest evidence

5. **Generalisable knowledge** — Findings must apply beyond your specific implementation

6. **Contemporaneous evidence** — Documentation dated BEFORE the work it describes

7. **Falsifiable hypotheses** — If you can't describe failure, you're not doing experiments

---

*Document Version: 1.0*
*Based on: Engage AI R&D Project Experience, AusIndustry Audit Simulations, Multiple R&D Application Reviews*
*Generated: January 2026*
