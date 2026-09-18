# ADR-003: LLM as Reasoning Layer

- **Status:** Accepted
- **Date:** 2026-09-18

## Context

LLMs are useful for natural-language reasoning, planning and interpretation but can produce incorrect numerical or statistical claims.

Kepler needs both flexible reasoning and reliable computation.

## Decision Drivers

- The project requires high reliability for numerical results.
- The system should be reproducible and auditable.
- The agent must plan and interpret investigations without becoming a source of truth for results.
- The architecture should separate reasoning from computation.

## Decision

The LLM will act as the reasoning and orchestration layer rather than the numerical source of truth.

The LLM is responsible for:

- Understanding questions
- Planning investigations
- Selecting tools
- Generating hypotheses
- Interpreting results
- Critiquing findings
- Producing explanations

Deterministic software is responsible for:

- Data manipulation
- Statistical calculations
- Model training
- Metric calculation
- Validation
- Visualisation
- Experiment recording

## Core Principle

> The LLM decides what should be done; deterministic tools determine what the data says.

## Alternatives Considered

### LLM-generated Python

Rejected as the default because arbitrary generated code is harder to validate, constrain and reproduce.

### LLM-only analysis

Rejected because numerical correctness and statistical reliability cannot depend solely on language-model output.

### Fully deterministic pipeline

Rejected because it would not investigate the autonomous reasoning question central to Kepler.

### LLM as reasoning layer over deterministic tools

Enables adaptive reasoning while preserving computational integrity.

## Consequences

### Positive

- Better numerical reliability
- Explicit separation of reasoning and computation
- Easier auditing
- Easier testing
- Clearer research comparisons
- Improved numerical reliability and reproducibility.
- Individual tools can be tested independently.
- Different LLMs can be benchmarked without changing the analytical engine.

### Negative

- More engineering effort
- Tool interfaces must be designed carefully
- Some analytical flexibility is constrained by available tools
- The LLM may still misinterpret correct results.
- Tool interfaces must be carefully designed and maintained.

## Links

- This ADR underpins the deterministic tool architecture described in [Deterministic Data Science Tools](20260914-deterministic-data-science-tools.md).

## Reconsideration

Sandboxed code generation may be evaluated later as an experimental capability, but it must have explicit safety and evaluation boundaries.
