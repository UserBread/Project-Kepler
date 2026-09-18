# ADR-006: Reproducibility and Experiment Tracking

- **Status:** Accepted
- **Date:** 2026-09-18

## Context

Kepler is intended to investigate autonomous data science scientifically. Results must therefore be traceable and reproducible where technically possible.

LLM behaviour may be non-deterministic, so exact replay cannot always be guaranteed.

## Decision Drivers

- The research question depends on repeatable and comparable experiments.
- Agent behaviour and analytical choices are part of the research subject, not just the final output.
- The system must support debugging, auditing and result comparison.
- Deterministic and stochastic components must be distinguished clearly.

## Decision

Every Kepler investigation will create an experiment record.

The record should include:

- Dataset identity
- Dataset version
- User question
- System configuration
- Plan
- Hypotheses
- Tool calls
- Tool parameters
- Analytical results
- Model configuration
- Random seeds
- Metrics
- Critic results
- Findings
- Report
- Timestamps

The experiment record should preserve the dataset, workflow, decisions and results associated with each investigation. This includes the full execution trace for non-deterministic reasoning where retaining exact replay is not possible.

MLflow will be used for machine-learning experiment tracking.

PostgreSQL will store Kepler's application-level investigation state.

## Reproducibility Model

Kepler distinguishes:

### Deterministically reproducible

Examples:

- Dataset transformations
- Statistical calculations
- Fixed-seed ML experiments where supported

### Traceable but potentially non-deterministic

Examples:

- LLM-generated plans
- Hypotheses
- Interpretations
- Natural-language reports

The full execution trace should be retained for the second category.

## Alternatives Considered

### Store only final reports

Simple and lightweight, but discards the analytical process and makes auditability impossible.

### Store only ML experiment metadata

Captures model-level outcomes, but omits the autonomous planning and reasoning process central to the research.

### Store complete raw execution data indefinitely

Preserves maximum traceability, but creates excessive storage costs and retention-policy complexity.

### Maintain structured experiment records for each investigation

Balances traceability, reproducibility and practical storage needs without requiring every raw detail to be retained forever.

## Consequences

### Positive

- Auditable investigations
- Better debugging
- Scientific evaluation
- Easier comparison between system versions
- Experiments can be audited after completion.
- Agent decisions can be traced to concrete outcomes.
- Research findings become more credible and reviewable.
- Bugs and incorrect conclusions can be traced back to their source.

### Negative

- Increased storage requirements
- More complex experiment schemas
- LLM results may still not be exactly replayable
- Some LLM outputs may not be perfectly reproducible.
- The experiment schema will need to evolve as the system grows.

## Reconsideration

The exact experiment schema may evolve as the evaluation framework matures.
