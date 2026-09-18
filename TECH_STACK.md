# Project Kepler Technology Stack

## 1. Language

### Python

Python is the primary language.

Reasons:

- Mature data-science ecosystem
- Mature statistical libraries
- Strong machine-learning ecosystem
- Extensive LLM tooling
- Rapid experimentation
- Strong testing and automation support

Performance-critical components may be separated later if profiling demonstrates a genuine bottleneck.

---

# 2. AI and Agent Orchestration

## OpenAI API

Used for:

- Natural-language question interpretation
- Analytical planning
- Hypothesis generation
- Tool selection
- Result interpretation
- Critique
- Report generation

The LLM is not the numerical source of truth.

## LangGraph

Used for:

- Stateful agent workflows
- Conditional transitions
- Iterative loops
- Checkpointing
- Future multi-agent orchestration

Kepler will initially use a single-agent architecture.

---

# 3. Data Science

## Pandas

Used for:

- Tabular data ingestion
- Data manipulation
- Data inspection
- Dataset transformations

## NumPy

Used for:

- Numerical operations
- Array processing
- Statistical support operations

## SciPy

Used for:

- Statistical tests
- Probability distributions
- Statistical utilities

---

# 4. Machine Learning

## scikit-learn

Primary library for:

- Baseline models
- Preprocessing
- Model evaluation
- Cross-validation
- Clustering
- Anomaly detection

## PyTorch

Reserved initially for:

- Advanced ML experiments
- Neural-network experimentation
- Future specialised models

PyTorch should not be introduced where a simpler scikit-learn solution is sufficient.

---

# 5. Visualisation

## Matplotlib

Used for:

- Reproducible analytical plots
- Statistical visualisation
- Model evaluation plots

## Plotly

Used later where interactive visualisation provides a meaningful advantage, particularly in the dashboard.

---

# 6. API

## FastAPI

Used for the service/API layer.

Potential responsibilities:

- Dataset submission
- Investigation creation
- Investigation status
- Experiment retrieval
- Findings retrieval
- Report retrieval

OpenAPI documentation will be generated from the API definitions.

---

# 7. Database

## PostgreSQL

Primary persistent store for:

- Dataset metadata
- Experiments
- Analyses
- Hypotheses
- Findings
- Critiques
- Tool executions
- Reports

## pgvector

Optional.

It should only be introduced if semantic retrieval is shown to provide value for Kepler's scientific memory.

---

# 8. Experiment Tracking

## MLflow

Used for machine-learning experiments.

Record:

- Model
- Parameters
- Dataset/version
- Metrics
- Artifacts
- Run metadata

MLflow complements rather than replaces Kepler's application-level experiment model.

---

# 9. Testing

## Pytest

Used for:

- Unit tests
- Integration tests
- Tool-contract tests
- Workflow tests
- Evaluation tests

Important deterministic components should have strong automated coverage.

---

# 10. Code Quality

## Ruff

Used for:

- Linting
- Formatting

## mypy

Used for:

- Static type checking

The codebase should use type hints consistently in core interfaces.

---

# 11. Dependency Management

## uv

Used for:

- Python environment management
- Dependency management
- Reproducible project setup

---

# 12. Infrastructure

## Docker

Used to standardise:

- PostgreSQL
- MLflow
- Kepler services
- Local development environments

## GitHub Actions

Used for CI:

```text
Commit
  ↓
Install
  ↓
Lint
  ↓
Type Check
  ↓
Tests
  ↓
Build
```

---

# 13. Observability

## LangSmith

Potentially used for:

- Agent traces
- Tool calls
- LLM interactions
- Debugging
- Evaluation

It should be introduced when agent workflows become sufficiently complex to justify external tracing.

## Structured application logging

Kepler should maintain structured logs independently of LLM observability.

---

# 14. Documentation

Primary formats:

- Markdown
- Mermaid diagrams
- ADRs

Potential later documentation tooling:

- MkDocs

Documentation should describe current behaviour rather than speculative future implementation.

---

# 15. Frontend

Planned later:

- React
- TypeScript

The frontend is intentionally deferred until the analytical backend provides useful functionality.

---

# 16. Security

Planned controls:

- Input validation
- Dataset isolation
- Restricted filesystem access
- Tool allowlists
- Execution timeouts
- Resource limits
- Sandboxing for any future arbitrary code execution

---

# 17. Technology Selection Principle

Technology should be selected because it solves a project requirement.

Kepler should avoid:

- Frameworks added only for CV keywords
- Multiple overlapping libraries
- Premature distributed infrastructure
- Unnecessary vector databases
- Unrestricted code execution
- Complex multi-agent frameworks before the single-agent system works
