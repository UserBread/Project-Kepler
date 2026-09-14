# ADR-001: Initial Scope for Tabular Data

- Status: Accepted
- Date: 2026-09-14
- Tags: scope, data, tabular-data, research

## Context and Problem Statement

Project Kepler is intended to test whether an AI system can autonomously perform meaningful data-science work. The project could support many data types, including text, images, audio, video, documents, databases, and streaming data, but supporting them all at once would make the system too broad to evaluate reliably.

The initial system therefore needs a constrained problem domain that is complex enough to demonstrate agentic reasoning while remaining measurable, reproducible, and feasible to implement.

## Decision Drivers

- The research objective is to evaluate autonomous data-science workflows rather than general-purpose AI behaviour.
- The initial problem must be broad enough to require reasoning but narrow enough to remain tractable.
- Results must be reproducible and comparable across experiments and model versions.
- Tabular datasets allow a rich range of analysis, including EDA, statistics, ML, anomaly detection, and reporting.

## Considered Options

- General-purpose AI research agent
- Autonomous coding agent
- Multi-modal data scientist
- Initial tabular-data scope

## Decision Outcome

Chosen option: "Initial tabular-data scope", because it creates a focused evaluation domain that is sufficiently rich for data-science autonomy while remaining manageable and testable.

The system will initially support structured tabular datasets in CSV and Parquet formats and will focus on the following capability areas:

- Exploratory data analysis
- Statistical analysis
- Machine learning
- Reporting and provenance

### Positive Consequences

- Keeps the initial implementation manageable.
- Establishes a well-defined evaluation domain.
- Enables reproducible experiments and benchmarking.
- Allows analytical correctness to be measured reliably.
- Provides enough complexity to investigate agentic reasoning.
- Makes it easier to compare agent architectures and system versions.

### Negative Consequences

- Kepler will initially be unable to analyse many real-world data types.
- The architecture may need extension if the project later expands beyond tabular data.
- Some interesting capabilities will be deliberately deferred.

## Pros and Cons of the Options

### General-purpose AI research agent

- Good, because it offers broad capability and flexibility.
- Bad, because the problem domain would be too broad to evaluate meaningfully.

### Autonomous coding agent

- Good, because it can support software-oriented workflows.
- Bad, because Kepler's core research question is autonomous data analysis, not software development.

### Multi-modal data scientist

- Good, because it would support a wider range of real-world data types.
- Bad, because supporting multiple modalities would significantly increase complexity without directly strengthening the core research goal.

### Initial tabular-data scope

- Good, because it constrains the problem while still enabling sophisticated analytical workflows.
- Good, because it keeps the system measurable, reproducible, and comparable.
- Bad, because it excludes many interesting data types and future capabilities until the initial system matures.

## Links

- Revisited by future ADRs that extend platform scope beyond tabular inputs.