# ADR-003: LLM as Reasoning Layer

- Status: Accepted
- Date: 2026-09-14
- Tags: llm, reasoning, architecture, determinism

## Context and Problem Statement

Kepler needs to combine language-model reasoning with deterministic data-science operations. LLMs are strong at understanding natural-language questions, generating hypotheses, selecting approaches, and interpreting results, but they are not reliable numerical computation engines and can produce unsupported or incorrect statistical conclusions.

If the LLM were allowed to independently calculate statistical results, the system would become much harder to evaluate, audit, and reproduce.

## Decision Drivers

- The project requires high reliability for numerical results.
- The system should be reproducible and auditable.
- The agent must plan and interpret investigations without becoming a source of truth for results.
- The architecture should separate reasoning from computation.

## Considered Options

- LLM-only analysis
- Fully deterministic pipeline
- LLM-generated Python execution
- LLM as reasoning layer over deterministic tools

## Decision Outcome

Chosen option: "LLM as reasoning layer over deterministic tools", because it preserves the agent's ability to plan and interpret while ensuring all numerical and statistical outputs come from validated software components.

The LLM is responsible for:

- Understanding user questions
- Planning investigations
- Selecting tools and workflows
- Generating hypotheses
- Interpreting analysis results
- Critiquing prior steps
- Deciding whether more investigation is needed
- Producing natural-language explanations

Deterministic software components remain responsible for:

- Statistical calculations
- Data manipulation
- Model training and evaluation
- Metric calculation
- Data validation
- Visualisation generation
- Experiment recording

> The LLM decides what should be done; deterministic tools determine what the data says.

### Positive Consequences

- Improved numerical reliability and reproducibility.
- Easier evaluation of analytical correctness.
- Clear separation between reasoning and computation.
- Individual tools can be tested independently.
- Different LLMs can be benchmarked without changing the analytical engine.

### Negative Consequences

- Requires a substantial deterministic tool layer.
- Adds architectural complexity compared with unrestricted direct code generation.
- The LLM may still misinterpret correct results.
- Tool interfaces must be carefully designed and maintained.

## Pros and Cons of the Options

### LLM-only analysis

- Good, because it is simple and conversational.
- Bad, because it is not reliable for data science and statistics.

### Fully deterministic pipeline

- Good, because it is reproducible and easier to validate.
- Bad, because it does not meaningfully investigate autonomous reasoning or adaptive workflow selection.

### LLM-generated Python execution

- Good, because it may be flexible and expressive.
- Bad, because it introduces security, reproducibility, and validation challenges.

### LLM as reasoning layer over deterministic tools

- Good, because it enables adaptive reasoning while preserving computational integrity.
- Good, because it creates a clean separation between decision-making and execution.
- Bad, because it requires more infrastructure and disciplined interface design.

## Links

- This ADR underpins the deterministic tool architecture in [ADR-004](ADR-004%20—%20Deterministic%20Data%20Science%20Tools.md).