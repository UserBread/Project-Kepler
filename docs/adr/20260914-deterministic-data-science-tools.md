# ADR-004: Deterministic Analytical Tools

- **Status:** Accepted
- **Date:** 2026-09-18

## Context

Kepler requires the LLM to interact with data-science functionality without allowing the reasoning model to become the computational authority.

If the agent directly performs calculations or manipulates analysis logic, correctness becomes difficult to test, audit and reproduce. Each analytical operation therefore needs explicitly defined inputs, outputs, validation and provenance.

## Decision Drivers

- Results must be reproducible and testable.
- The reasoning layer should not redefine analytical behaviour ad hoc.
- Individual analysis operations must be independently verified.
- Tool outputs should be suitable as evidence for downstream reasoning and reporting.

## Decision

Analytical capabilities will be exposed through explicit deterministic tools with defined contracts.

Initial tool categories:

- Dataset tools
- Profiling tools
- Statistical tools
- Machine-learning tools
- Visualisation tools
- Experiment tools

Initial capabilities include:

### Dataset tools

- Load dataset
- Inspect dataset
- Inspect column
- Retrieve dataset metadata

### Profiling tools

- Profile dataset
- Analyse missing values
- Detect duplicates
- Detect outliers
- Analyse categorical variables

### Statistical tools

- Calculate correlation
- Run hypothesis test
- Compare groups
- Analyse categorical relationships

### Machine-learning tools

- Prepare dataset
- Train model
- Evaluate model
- Compare models
- Generate predictions
- Detect anomalies

### Visualisation tools

- Generate distribution plot
- Generate correlation plot
- Generate scatter plot
- Generate categorical plot

Each tool should define:

- Name
- Purpose
- Input schema
- Output schema
- Validation
- Errors
- Side effects
- Reproducibility requirements
- Failure modes and errors

## Alternatives Considered

### Arbitrary Python execution

Flexible and easy to prototype, but weakens reproducibility, security and observability.

### Monolithic analysis engine

Simple initially, but couples capabilities and makes independent testing and debugging harder.

### Deterministic tool-based analytical layer

Makes operations explicit and auditable, with each tool validated in isolation.

## Example

```text
calculate_correlation

Input:
    column_a
    column_b
    method

Output:
    coefficient
    p_value
    sample_size
    confidence_interval
    warnings
```

## Rationale

Explicit contracts improve:

- Validation
- Testing
- Observability
- Reproducibility
- Agent reliability

## Consequences

### Positive

- Controlled agent capabilities
- Easier testing
- Structured evidence
- Reduced dependence on arbitrary generated code
- Individual components can be tested independently.
- Tool execution can be logged and audited.
- Results can be tied to specific experiments and investigations.
- The LLM cannot arbitrarily redefine analytical operations.
- Tool results provide clear evidence for generated conclusions.

### Negative

- New analytical capabilities require new tools
- Tool schemas require maintenance
- Highly specialised tasks may require additional tool definitions.

## Reconsideration

Arbitrary code execution can be investigated separately if benchmark evidence shows that fixed tools prevent useful analyses.
