# Deterministic Data Science Tools

- Status: Accepted
- Date: 2026-09-14
- Tags: tools, analytics, determinism, architecture

## Context and Problem Statement

Kepler must execute data-science operations based on decisions made by an AI agent. If the agent directly performs calculations or manipulates analysis logic, then correctness becomes difficult to test, audit, and reproduce.

The system therefore needs a contract-based tool layer in which every analytical operation has explicitly defined inputs, outputs, validation, and provenance.

## Decision Drivers

- Results must be reproducible and testable.
- The reasoning layer should not redefine analytical behaviour ad hoc.
- Individual analysis operations must be independently verified.
- Tool outputs should be suitable as evidence for downstream reasoning and reporting.

## Considered Options

- Arbitrary Python execution
- Monolithic analysis engine
- Deterministic tool-based analytical layer

## Decision Outcome

Chosen option: "Deterministic tool-based analytical layer", because it provides a clear contract for each operation, allows independent testing, and preserves auditability and reproducibility across investigations.

Initial tool categories will include:

### Dataset Tools

- Load dataset
- Inspect dataset
- Inspect column
- Retrieve dataset metadata

### Profiling Tools

- Profile dataset
- Analyse missing values
- Detect duplicates
- Detect outliers
- Analyse categorical variables

### Statistical Tools

- Calculate correlation
- Run hypothesis test
- Compare groups
- Analyse categorical relationships

### Machine Learning Tools

- Prepare dataset
- Train model
- Evaluate model
- Compare models
- Generate predictions
- Detect anomalies

### Visualisation Tools

- Generate distribution plot
- Generate correlation plot
- Generate scatter plot
- Generate categorical plot

Each tool will define:

- Required inputs
- Optional inputs
- Output structure
- Validation rules
- Failure modes and errors

### Positive Consequences

- Individual components can be tested independently.
- Tool execution can be logged and audited.
- Results can be tied to specific experiments and investigations.
- The LLM cannot arbitrarily redefine analytical operations.
- Tool results provide clear evidence for generated conclusions.

### Negative Consequences

- Requires more initial engineering work.
- Tool interfaces must be maintained as the system grows.
- Highly specialised tasks may require additional tool definitions.

## Pros and Cons of the Options

### Arbitrary Python execution

- Good, because it is flexible and easy to prototype.
- Bad, because it weakens reproducibility, security, and observability.

### Monolithic analysis engine

- Good, because it is conceptually simple at first.
- Bad, because it couples capabilities and makes independent testing and debugging harder.

### Deterministic tool-based analytical layer

- Good, because it makes operations explicit and auditable.
- Good, because each tool can be validated in isolation.
- Bad, because it requires more upfront design and maintenance effort.

## Links

- This decision operationalises the reasoning boundary described in [ADR-003](ADR-003%20—%20LLM%20as%20Reasoning%20Layer.md).