# ADR-001: Project Scope

- **Status:** Accepted
- **Date:** 2026-09-18

## Context

Kepler could potentially support many data types and analytical domains. Attempting to support arbitrary data and analysis from the beginning would make the system difficult to implement, test and evaluate.

A bounded scope is required for a measurable initial system.

## Decision Drivers

- The research objective is to evaluate autonomous data-science workflows rather than general-purpose AI behaviour.
- The initial problem must be broad enough to require reasoning but narrow enough to remain tractable.
- Results must be reproducible and comparable across experiments and model versions.
- Tabular datasets support exploratory analysis, statistics, machine learning, anomaly detection and reporting.

## Decision

Kepler will initially focus on structured tabular data.

Supported initial formats:

- CSV
- Parquet

Supported initial capabilities:

- Data ingestion
- Data profiling
- Exploratory data analysis
- Statistical analysis
- Classification
- Regression
- Clustering
- Anomaly detection
- Visualisation
- Experiment tracking
- Report generation

## Alternatives Considered

### General-purpose AI research agent

Would offer broad capability, but the problem domain would be too broad to evaluate meaningfully.

### Autonomous coding agent

Could support software-oriented workflows, but Kepler's core research question is autonomous data analysis rather than software development.

### Multi-modal data scientist

Would support more real-world data types, but would significantly increase complexity without directly strengthening the initial research goal.

### Initial tabular-data scope

Constrains the problem while retaining enough analytical depth for a measurable and reproducible evaluation.

## Out of Scope Initially

- Images
- Audio
- Video
- Real-time streaming
- Arbitrary document analysis
- Autonomous production deployment
- Unrestricted arbitrary code execution

## Rationale

Tabular data provides a sufficiently rich environment for investigating autonomous data science while allowing analytical results to be measured and reproduced.

## Consequences

### Positive

- Manageable implementation scope
- Clear evaluation criteria
- Strong existing Python ecosystem
- Easier reproducibility
- Easier benchmark construction
- Enables analytical correctness to be measured reliably.
- Provides enough complexity to investigate agentic reasoning.
- Makes it easier to compare agent architectures and system versions.

### Negative

- Kepler will not initially represent a general-purpose data scientist.
- Some future research questions cannot be explored until additional modalities are implemented.
- Kepler will initially be unable to analyse many real-world data types.
- The architecture may need extension if the project expands beyond tabular data.
- Some capabilities will be deliberately deferred.

## Reconsideration

Scope may be expanded when the existing system has a stable evaluation framework and the additional modality can be tested independently.
