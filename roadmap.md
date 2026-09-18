# Project Kepler Roadmap

## Guiding Principle

Kepler will be developed from deterministic analytical foundations toward increasingly autonomous reasoning.

The project should not introduce an agent, critic, memory system, or multi-agent architecture merely because it is technically interesting. Each layer must provide a measurable capability.

---

# Phase 0 — Definition and Foundation

**Goal:** Establish project scope, architecture, tooling and research direction.

### Tasks

- Define project scope
- Define MVP
- Define research questions
- Create repository
- Establish architecture
- Establish development environment
- Create initial ADRs
- Configure CI
- Define evaluation strategy

### Definition of Done

A fresh clone can be configured and the project documentation clearly explains what Kepler is, what it is not, and how it will eventually be evaluated.

---

# Phase 1 — Kepler Foundation

**Goal:** Build the core software architecture without AI.

### Tasks

- Define Dataset
- Define DatasetVersion
- Define Analysis
- Define Experiment
- Define Hypothesis
- Define Observation
- Define Model
- Define Metric
- Define Finding
- Define Report
- Define experiment lifecycle
- Implement structured logging
- Implement error handling

### Target lifecycle

```text
CREATED
  ↓
PROFILING
  ↓
ANALYSING
  ↓
MODELLING
  ↓
VALIDATING
  ↓
COMPLETED
```

Failure paths should be represented explicitly.

---

# Phase 2 — Data Ingestion

**Goal:** Reliably ingest unfamiliar tabular datasets.

### Tasks

- CSV loader
- Parquet loader
- Dataset schema detection
- Data types
- Missing-value detection
- Duplicate detection
- Constant-column detection
- Suspicious identifier detection
- Memory usage
- Dataset hashing
- Dataset version identity
- Input validation
- Dataset metadata

### Definition of Done

Kepler can ingest a supported dataset and produce a structured representation describing what was loaded and what its basic risks are.

---

# Phase 3 — Kepler Analyst

**Goal:** Produce a meaningful machine-readable dataset profile.

### Numerical analysis

- Mean
- Median
- Variance
- Standard deviation
- Quartiles
- Min/max
- Skewness
- Distribution information
- Outlier indicators

### Categorical analysis

- Cardinality
- Frequency tables
- Dominant categories
- Rare categories
- Missing categories

### Relationships

- Correlations
- Group differences
- Feature-target relationships

### Definition of Done

Kepler can profile an unfamiliar dataset without relying on an LLM to calculate statistics.

---

# Phase 4 — Visual Analytics

**Goal:** Produce useful visual evidence.

### Visualisations

- Histograms
- Box plots
- Scatter plots
- Correlation matrices
- Categorical distributions
- Feature relationships
- Model evaluation plots

The LLM interprets generated evidence; the plotting system generates it.

---

# Phase 5 — Statistical Engine

**Goal:** Perform statistically appropriate analyses.

### Tests

- Pearson correlation
- Spearman correlation
- Independent t-test
- Welch's t-test
- Mann–Whitney U
- ANOVA
- Kruskal–Wallis
- Chi-square
- Fisher's exact test

### Result requirements

Every statistical result should record, where applicable:

- Test
- Inputs
- Sample size
- Statistic
- p-value
- Confidence interval
- Effect size
- Assumptions
- Warnings

Kepler should be capable of determining that a requested test is inappropriate.

---

# Phase 6 — ML Engine

**Goal:** Provide reliable baseline machine-learning experimentation.

## Classification

Initial models:

- Logistic Regression
- Random Forest
- Gradient Boosting

Metrics:

- Accuracy
- Precision
- Recall
- F1
- ROC-AUC
- PR-AUC
- Confusion matrix

## Regression

Initial models:

- Linear Regression
- Random Forest
- Gradient Boosting

Metrics:

- MAE
- RMSE
- R²

## Clustering

Initial models:

- K-Means
- DBSCAN

Metrics:

- Silhouette score
- Cluster sizes
- Stability

## Anomaly Detection

Initial models:

- Isolation Forest
- Local Outlier Factor

---

# Phase 7 — Reproducible Experimentation

**Goal:** Make every investigation auditable.

Record:

- Dataset identity
- Dataset version
- Question
- Plan
- Tool calls
- Tool parameters
- Algorithms
- Features
- Preprocessing
- Random seeds
- Metrics
- Results
- Critiques
- Findings
- Timestamps

Integrate MLflow for machine-learning experiment tracking.

---

# Phase 8 — First AI Agent

**Goal:** Connect reasoning to deterministic tools.

Initial tools:

- load_dataset
- profile_dataset
- inspect_column
- calculate_correlation
- run_statistical_test
- generate_visualisation
- train_model
- evaluate_model
- compare_models

The initial agent should be single-agent.

---

# Phase 9 — Planning

**Goal:** Turn natural-language questions into explicit analytical plans.

Example:

```text
Question
  ↓
Inspect dataset
  ↓
Identify target
  ↓
Check data quality
  ↓
Understand target distribution
  ↓
Investigate relationships
  ↓
Perform appropriate statistics
  ↓
Train baseline models if relevant
  ↓
Validate findings
  ↓
Report
```

---

# Phase 10 — Hypothesis Generation

**Goal:** Make analytical reasoning explicit.

Example:

```text
Question:
"What factors are associated with customer churn?"

H1:
Customers with shorter tenure have higher churn rates.

H2:
Customers with higher monthly charges have higher churn rates.

H3:
Contract type is associated with churn.
```

Each hypothesis should be represented as structured data and linked to analyses that test it.

---

# Phase 11 — Kepler Critic

**Goal:** Detect methodological problems.

The critic checks:

- Wrong test selection
- Missing assumptions
- Invalid comparisons
- Data leakage
- Overfitting
- Poor evaluation methodology
- Correlation vs causation
- Unsupported conclusions
- Small sample sizes
- Multiple-comparison concerns
- Irrelevant analyses
- Contradictory evidence

---

# Phase 12 — Autonomous Iteration

**Goal:** Allow Kepler to revise its investigation.

```text
PLAN
  ↓
ANALYSE
  ↓
RESULT
  ↓
CRITIQUE
  ↓
PASS ─────→ REPORT
  |
  ↓
RE-PLAN
  |
  └────────→ ANALYSE
```

Safety limits:

- Maximum iterations
- Maximum tool calls
- Maximum runtime
- Maximum token usage
- Maximum cost

---

# Phase 13 — Multi-Agent Kepler

**Goal:** Introduce specialist roles only where evaluation demonstrates value.

Potential roles:

- Planner
- Analyst
- Statistician
- ML Scientist
- Critic
- Reporter

The multi-agent design must be compared against a simpler architecture.

---

# Phase 14 — Scientific Memory

**Goal:** Persist useful analytical knowledge.

PostgreSQL stores structured investigation state.

Potential semantic retrieval:

- Previous hypotheses
- Similar analyses
- Previous failed approaches
- Prior findings

Vector search should only be introduced where it provides measurable value.

---

# Phase 15 — Report Generation

**Goal:** Produce a complete analytical report.

Structure:

1. Executive summary
2. Research question
3. Dataset
4. Data quality
5. Hypotheses
6. Statistical analysis
7. Machine learning
8. Findings
9. Limitations
10. Reproducibility information

Every important finding should trace back to evidence.

---

# Phase 16 — Provenance

**Goal:** Make findings auditable.

Target relationship:

```text
Finding
   ↓
Analysis
   ↓
Tool Execution
   ↓
Parameters
   ↓
Dataset Version
```

A user should be able to determine how a conclusion was produced.

---

# Phase 17 — Kepler Lab

**Goal:** Build a web interface.

Potential interface:

- Dataset browser
- Experiment browser
- Run details
- Agent trace
- Model results
- Findings
- Reports
- Provenance graph

Example live trace:

```text
✓ Dataset loaded
✓ Dataset profiled
✓ Target identified
✓ Class imbalance detected
✓ Hypotheses generated
✓ Statistical test selected
⚠ Critic identified assumption violation
✓ Alternative test selected
✓ Analysis repeated
✓ Findings validated
✓ Report generated
```

---

# Phase 18 — Evaluation

**Goal:** Measure Kepler scientifically.

Compare:

1. LLM alone
2. LLM + deterministic tools
3. Single autonomous agent
4. Multi-agent system
5. Multi-agent system + critic

Metrics:

- Analytical correctness
- Statistical errors
- Model-selection errors
- Hallucinations
- Leakage
- Reproducibility
- Runtime
- Tool calls
- Token usage
- Cost
- Human interventions

---

# Phase 19 — Failure Analysis

Catalog failures such as:

- Wrong statistical test
- Incorrect interpretation
- Data leakage
- Hallucinated relationships
- Unnecessary ML
- Poor feature selection
- Infinite or repetitive loops
- Unsupported causal claims

For each failure:

```text
Failure
  ↓
Observed behaviour
  ↓
Likely cause
  ↓
Detection method
  ↓
Mitigation
  ↓
Did mitigation work?
```

---

# Phase 20 — Advanced Kepler

Potential capabilities:

- Autonomous feature engineering
- Automated model selection
- Hyperparameter optimisation
- Dataset drift detection
- Multiple LLMs
- Human-in-the-loop workflows
- Cost-aware planning
- Confidence-aware conclusions

These are not required for the initial release.

---

# Phase 21 — Production Hardening

Tasks:

- Sandboxed execution
- Filesystem restrictions
- Dataset isolation
- Input validation
- Timeouts
- Retries
- Recovery
- Checkpointing
- Structured logs
- Metrics
- Tracing
- Agent observability

---

# Phase 22 — Final Research

Final experimental question:

> **Does iterative multi-agent reasoning improve the correctness and reliability of autonomous data science compared with a single agent, and what computational cost does that improvement introduce?**

The final release should contain actual benchmark results rather than claims based on demonstrations.

---

# Release Path

```text
0.1  Laboratory
     |
0.2  Analyst
     |
0.3  Scientist
     |
0.4  ML
     |
0.5  Agent
     |
0.6  Critic
     |
0.7  Multi-Agent
     |
0.8  Lab
     |
0.9  Interface
     |
1.0  Autonomous Scientist
```
