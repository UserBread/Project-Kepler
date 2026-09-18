# Project Kepler Research

## 1. Research Purpose

Kepler is both a software project and an experimental platform for investigating autonomous data science.

The central question is not simply:

> Can an LLM analyse data?

Instead:

> Can an autonomous system combining language-model reasoning with deterministic analytical tools perform end-to-end data science while maintaining correctness, reproducibility and transparency?

---

# 2. Primary Research Question

> **Does iterative autonomous reasoning improve the correctness and reliability of autonomous data science compared with a single-pass agent, and what computational cost does that improvement introduce?**

---

# 3. Supporting Questions

### Dataset understanding

- Can Kepler correctly identify variable types?
- Can it identify missingness and suspicious columns?
- Can it recognise potential identifiers?
- Can it detect data-quality problems?

### Statistical reasoning

- Can Kepler select an appropriate test?
- Can it recognise assumption violations?
- Can it distinguish statistical significance from practical significance?
- Can it avoid causal claims unsupported by observational evidence?

### Machine learning

- Can Kepler select suitable baseline models?
- Can it construct valid train/test workflows?
- Can it avoid data leakage?
- Can it choose appropriate evaluation metrics?

### Autonomous reasoning

- Does explicit planning improve analysis quality?
- Does hypothesis generation improve investigation quality?
- Does a critic detect meaningful errors?
- Does iterative re-planning reduce errors?

### Reproducibility

- Can an investigation be replayed?
- Can findings be traced to exact computations?
- Which parts are deterministic?
- Which parts depend on stochastic LLM behaviour?

### Cost

- How many tool calls are required?
- How long does an investigation take?
- What is the token/API cost?
- Does additional reasoning improve results enough to justify its cost?

---

# 4. Research Hypotheses

Potential hypotheses:

### H1 — Deterministic tools improve numerical correctness

An agent with deterministic analytical tools should produce fewer numerical/statistical errors than an LLM-only system.

### H2 — Planning improves analytical coverage

Explicit planning should reduce omitted analytical steps compared with unstructured single-pass analysis.

### H3 — Critique reduces methodological errors

Adding a critic should reduce identifiable methodological errors.

### H4 — Iteration improves reliability

Allowing the system to revise an investigation after critique should improve correctness compared with a single-pass workflow.

### H5 — Additional reasoning has a measurable cost

More extensive autonomous reasoning should increase runtime, tool calls, and/or LLM cost.

These hypotheses are to be tested rather than assumed to be true.

---

# 5. Experimental Comparisons

The major comparison should eventually contain several system configurations.

```text
A — LLM only

B — LLM + deterministic tools

C — Single autonomous agent

D — Multi-agent system

E — Multi-agent + critic
```

The exact experimental design should be refined before final benchmarking.

---

# 6. Evaluation Dimensions

## Correctness

Did Kepler calculate the correct result?

## Statistical validity

Was the selected method appropriate?

## Model validity

Was the ML evaluation methodologically sound?

## Interpretation

Did the explanation match the evidence?

## Reproducibility

Can the analysis be reproduced from recorded state?

## Transparency

Can findings be traced to computations?

## Efficiency

How many:

- Tool calls?
- LLM calls?
- Tokens?
- Seconds?
- Computational resources?

## Human intervention

How often was human correction required?

---

# 7. Failure Taxonomy

Kepler should explicitly track failure types.

### Data understanding failures

- Incorrect type inference
- Missed missing values
- Misidentified target
- Missed identifier
- Misinterpreted categories

### Statistical failures

- Wrong test
- Assumption violation
- Incorrect interpretation
- Multiple-comparison issue
- Confusing correlation with causation

### ML failures

- Data leakage
- Wrong metric
- Invalid split
- Overfitting
- Poor preprocessing

### Agent failures

- Tool misuse
- Repeated actions
- Infinite loops
- Unsupported conclusions
- Irrelevant analysis

### Reporting failures

- Missing evidence
- Contradictory findings
- Overstated conclusions
- Missing limitations

---

# 8. Benchmark Dataset Design

The final benchmark should include datasets with varied characteristics.

Potential categories:

- Binary classification
- Multiclass classification
- Regression
- Imbalanced classification
- Small datasets
- Large datasets
- Missing data
- Mixed numerical/categorical data
- Correlated features
- Outliers
- Potential leakage
- Confounding variables

Each benchmark should have a documented expected analytical answer or evaluation rubric.

---

# 9. Ground Truth

Ground truth may come from:

- Known synthetic relationships
- Established statistical calculations
- Human-authored analytical expectations
- Reference implementations
- Public benchmark datasets with independently verified properties

Synthetic datasets are particularly useful for testing whether Kepler discovers relationships that are deliberately known.

---

# 10. Reproducibility Strategy

Every investigation should record:

```text
Dataset identity
Dataset version
Question
System configuration
Model configuration
Prompt/configuration version
Plan
Tool calls
Tool parameters
Random seeds
Results
Critiques
Findings
Timestamp
```

Exact LLM reproduction may not always be possible.

The system should therefore distinguish:

```text
Deterministically reproducible
vs.
Traceable but potentially non-deterministic
```

---

# 11. Scientific Reporting Principle

Kepler should distinguish:

### Observation

What the data directly shows.

### Statistical result

What a formal test reports.

### Model result

What a trained model demonstrates.

### Interpretation

What the evidence may mean.

### Limitation

What cannot be concluded.

### Hypothesis

What remains to be tested.

This distinction is important for preventing unsupported conclusions.

---

# 12. Research Deliverables

The final research stage should produce:

- Benchmark datasets
- Evaluation methodology
- Experimental configurations
- Results tables
- Error analysis
- Cost analysis
- Reproducibility information
- Limitations
- Conclusions

The project should not claim that one architecture is superior without comparative evidence.

---

# 13. Literature Areas to Investigate

Research should cover:

- Autonomous agents
- Agentic workflows
- LLM tool use
- AI-assisted data science
- Automated machine learning
- Statistical reasoning with LLMs
- LLM hallucination
- LLM evaluation
- Multi-agent systems
- Scientific discovery agents
- Reproducible computational science
- Data leakage and ML evaluation
- Automated experiment design

Specific papers and systems should be added to this document as the literature review develops.

---

# 14. Research Integrity

Kepler should avoid evaluating itself using only examples it was designed around.

The benchmark should include:

- Known-answer tasks
- Adversarial cases
- Ambiguous cases
- Methodologically invalid requests
- Data-quality problems
- Cases where no ML model is necessary

The system should receive credit for correctly saying that an analysis is inappropriate.

---

# 15. Final Research Goal

The desired final result is not:

> "Kepler is an AI data scientist."

It is a measurable investigation into:

> **How autonomous reasoning, deterministic tools, iterative critique, and multi-agent organisation affect the correctness, reliability, reproducibility, and cost of automated data science.**
