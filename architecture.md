# Project Kepler Architecture

## 1. Architectural Goal

Kepler is designed as a layered autonomous data science system.

The architecture separates:

- Reasoning
- Orchestration
- Deterministic analysis
- Persistence
- Evaluation
- Presentation

The most important architectural constraint is:

> **The LLM decides what should be done; deterministic tools determine what the data says.**

---

# 2. High-Level Architecture

```text
                           USER
                             |
                             v
                        Kepler API
                             |
                             v
                       Kepler Core
                             |
              +--------------+--------------+
              |              |              |
              v              v              v
           Analyst      Statistician      ML Engine
              |              |              |
              +--------------+--------------+
                             |
                             v
                    Deterministic Tools
                             |
                             v
                          Dataset
                             |
                             v
                     Evidence / Results
                             |
                             v
                          Critic
                             |
                    +--------+--------+
                    |                 |
                  PASS             RE-PLAN
                    |                 |
                    v                 |
                 Findings <-----------+
                    |
                    v
                  Report
```

---

# 3. Architectural Layers

## Layer 1 — Interface

Responsibilities:

- Accept analytical questions
- Accept datasets
- Expose investigation status
- Return reports and findings

Initial interface:

- CLI/internal API

Later:

- FastAPI
- React/TypeScript dashboard

---

## Layer 2 — Kepler Core

Kepler Core owns orchestration.

Responsibilities:

- Workflow state
- Agent state
- Experiment lifecycle
- Tool execution
- Iteration limits
- Error handling
- Checkpointing
- Routing

Kepler Core should not contain statistical calculations itself.

---

# 4. Analyst

The Analyst transforms raw data into structured observations.

Responsibilities:

- Dataset profiling
- Data-quality checks
- Distribution analysis
- Categorical analysis
- Relationship analysis
- EDA
- Visualisation requests

Example:

```text
Dataset
   ↓
Profile
   ↓
Observations
```

Example observation:

```text
Column: monthly_charges
Type: numerical
Missing: 0.3%
Median: ...
Outlier_indicator: ...
```

---

# 5. Statistician

The Statistician handles statistical reasoning and execution.

Responsibilities:

- Test selection
- Assumption checking
- Statistical execution
- Effect sizes
- Confidence intervals
- Interpretation support
- Warnings

The LLM may recommend a test, but the deterministic statistical engine executes it.

---

# 6. Scientist

The Scientist is responsible for analytical planning and hypothesis generation.

Responsibilities:

- Interpret user question
- Decompose question
- Generate hypotheses
- Determine evidence requirements
- Propose investigation plans

Example:

```text
Question
   ↓
Hypothesis
   ↓
Required evidence
   ↓
Analysis
```

---

# 7. ML Engine

Responsibilities:

- Preprocessing
- Dataset splitting
- Model training
- Cross-validation
- Evaluation
- Model comparison
- Feature importance
- Error analysis

The ML engine must explicitly guard against data leakage.

---

# 8. Critic

The Critic validates the investigation.

It should evaluate both:

### Methodology

- Was the analysis appropriate?
- Were assumptions checked?
- Was the dataset split correctly?
- Is there leakage?
- Is the sample size adequate?

### Interpretation

- Does the conclusion match the result?
- Is correlation being presented as causation?
- Is the effect practically meaningful?
- Are limitations disclosed?
- Are contradictory results acknowledged?

The critic should produce structured issues rather than only natural-language criticism.

---

# 9. Deterministic Tool Layer

Tools provide explicit contracts between the reasoning system and analytical software.

Example conceptual contract:

```text
Tool:
    calculate_correlation

Input:
    column_a
    column_b
    method

Output:
    coefficient
    p_value
    confidence_interval
    sample_size
    warnings
```

Tools should:

- Validate inputs
- Execute deterministic operations
- Return structured results
- Report errors explicitly
- Avoid hidden side effects

---

# 10. Experiment Model

A Kepler investigation should be represented as an experiment.

Conceptually:

```text
Experiment
├── DatasetVersion
├── Question
├── Plan
├── Hypotheses
├── ToolExecutions
├── Analyses
├── Models
├── Critiques
├── Findings
└── Report
```

---

# 11. Core Domain Objects

Initial domain concepts:

- Dataset
- DatasetVersion
- Experiment
- Analysis
- Hypothesis
- Observation
- ToolExecution
- Model
- Metric
- Critique
- Finding
- Report

These should remain conceptually separate even if implementation details evolve.

---

# 12. Experiment Lifecycle

```text
CREATED
   |
   v
PROFILING
   |
   v
ANALYSING
   |
   v
MODELLING
   |
   v
VALIDATING
   |
   v
COMPLETED
```

Failure can occur at any stage:

```text
Any State
   |
   v
FAILED
```

Later, checkpointing may allow recovery.

---

# 13. Agent State

The agent should maintain structured state rather than relying exclusively on conversation history.

Conceptual state:

```text
AgentState
├── experiment_id
├── dataset_id
├── question
├── current_plan
├── hypotheses
├── observations
├── analyses
├── model_results
├── critiques
├── findings
├── iteration
└── limits
```

---

# 14. Agent Loop

Initial single-agent architecture:

```text
                +----------+
                |  Question|
                +----+-----+
                     |
                     v
                  PLAN
                     |
                     v
                  TOOL
                     |
                     v
                OBSERVATION
                     |
                     v
                  DECIDE
                  /                   TOOL     FINISH
                |
                +-----> OBSERVATION
```

Later autonomous iteration:

```text
PLAN
 ↓
ANALYSE
 ↓
CRITIQUE
 ↓
PASS? ---- yes ---> REPORT
 |
 no
 |
 v
RE-PLAN
 |
 +----> ANALYSE
```

---

# 15. Persistence

PostgreSQL is the planned source of persistent application state.

Store:

- Experiments
- Dataset metadata
- Tool executions
- Analyses
- Hypotheses
- Findings
- Critiques
- Reports
- Model metadata

MLflow is used for ML experiment tracking.

Vector search should only be introduced where semantic retrieval provides a demonstrated benefit.

---

# 16. Provenance

Every important finding should have an evidence chain.

```text
Finding
   |
   v
Analysis
   |
   v
ToolExecution
   |
   +--> parameters
   +--> output
   +--> timestamp
   |
   v
DatasetVersion
```

This allows Kepler to answer:

> "Why did you make this conclusion?"

with a traceable chain of evidence.

---

# 17. Error Handling

Errors should be classified.

### Input errors

Examples:

- Unsupported file
- Malformed dataset
- Missing required column

### Analytical errors

Examples:

- Invalid statistical test
- Insufficient sample size
- Assumption violation

### Tool errors

Examples:

- Model training failure
- Numerical instability
- Visualisation failure

### Agent errors

Examples:

- Repeated tool calls
- Invalid tool arguments
- Planning loop

### Infrastructure errors

Examples:

- Database failure
- API failure
- Timeout

The system should distinguish recoverable from unrecoverable errors.

---

# 18. Safety and Execution Boundaries

Kepler should not initially execute unrestricted LLM-generated code.

Tool execution should be:

- Explicit
- Validated
- Observable
- Time-limited
- Resource-limited

Sandboxed arbitrary code execution may be investigated later as a separate architectural decision.

---

# 19. Scalability

Initial priority is correctness and experimental clarity, not distributed scale.

Potential future scaling:

```text
API
 |
 v
Orchestrator
 |
 +---- Worker
 +---- Worker
 +---- Worker
 |
 v
Database / Experiment Store
```

Distributed execution should only be introduced when workloads justify it.

---

# 20. Architectural Evolution

Kepler should evolve in this order:

```text
Deterministic foundation
        ↓
Single agent + tools
        ↓
Planning
        ↓
Critic
        ↓
Iteration
        ↓
Multi-agent
        ↓
Memory
        ↓
Production hardening
```

Complexity should be justified by evaluation.

---

# 21. Architecture Quality Goals

The architecture should optimise for:

1. Correctness
2. Reproducibility
3. Observability
4. Testability
5. Modularity
6. Explainability
7. Extensibility

Raw agent autonomy is not itself a quality metric.
