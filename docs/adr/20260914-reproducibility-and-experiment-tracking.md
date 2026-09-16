# Reproducibility and Experiment Tracking

- Status: Accepted
- Date: 2026-09-14
- Tags: reproducibility, tracking, mlflow, postgres

## Context and Problem Statement

One of Kepler's primary goals is to determine how reliably an autonomous AI system can perform data-science tasks. That requirement makes repeatability and traceability essential: an investigation is not sufficiently reproducible if the system only stores a final natural-language answer.

The project therefore needs a structured record of the dataset, workflow, decisions, and results associated with each investigation.

## Decision Drivers

- The research question depends on repeatable and comparable experiments.
- Agent behaviour and analytical choices are part of the research subject, not just the final output.
- The system must support debugging, auditing, and result comparison.
- Deterministic and stochastic components must be distinguished clearly.

## Considered Options

- Store only final reports
- Store only ML experiment metadata
- Store complete raw execution data indefinitely
- Maintain structured experiment records for each investigation

## Decision Outcome

Chosen option: "Maintain structured experiment records for each investigation", because it preserves the full context needed to audit and compare system behaviour without requiring every raw detail to be retained forever.

Kepler will record, where applicable:

```text
Experiment
├── Dataset
├── Dataset version/hash
├── User question
├── Agent plan
├── Tool calls
├── Tool parameters
├── Analytical results
├── Model configurations
├── Random seeds
├── Evaluation metrics
├── Critic results
├── Findings
└── Final report
```

MLflow will be used for machine-learning experiment tracking, and PostgreSQL will store persistent application and investigation state.

### Positive Consequences

- Experiments can be audited after completion.
- Results can be compared across system versions and benchmarks.
- Agent decisions can be traced to concrete outcomes.
- Research findings become more credible and reviewable.
- Bugs and incorrect conclusions can be traced back to their source.

### Negative Consequences

- Increases storage and infrastructure requirements.
- Adds implementation complexity.
- Some LLM outputs may not be perfectly reproducible.
- The experiment schema will need to evolve as the system grows.

## Pros and Cons of the Options

### Store only final reports

- Good, because it is simple and lightweight.
- Bad, because it discards the analytical process and makes auditability impossible.

### Store only ML experiment metadata

- Good, because it captures model-level outcomes.
- Bad, because it omits the autonomous planning and reasoning process central to the research.

### Store complete raw execution data indefinitely

- Good, because it preserves maximum traceability.
- Bad, because storage costs and retention policy complexity become excessive.

### Maintain structured experiment records for each investigation

- Good, because it balances traceability, reproducibility, and practical storage needs.
- Good, because it supports auditing of both deterministic and stochastic components.
- Bad, because it requires ongoing schema design and operational support.

## Links

- This decision complements the tool-based model described in [ADR-004](ADR-004%20—%20Deterministic%20Data%20Science%20Tools.md).