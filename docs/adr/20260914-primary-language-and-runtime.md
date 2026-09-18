# ADR-002: Primary Language and Runtime

- **Status:** Accepted
- **Date:** 2026-09-18

## Context

Kepler requires substantial data manipulation, statistical computation, machine learning, visualisation and LLM integration.

The primary language must support these areas while allowing rapid experimentation.

## Decision Drivers

- The project depends heavily on scientific computing and statistical tooling.
- The system must integrate with model orchestration, LLM services and backend APIs.
- Rapid iteration and experimentation are essential for research work.
- The stack needs mature libraries for testing, workflow tracking and machine learning.

## Decision

Python will be the primary implementation language.

The initial stack will include:

- Python
- Pandas
- NumPy
- SciPy
- scikit-learn
- PyTorch
- FastAPI
- LangGraph
- MLflow
- Pytest

Project dependency and environment management will initially use uv.

## Alternatives Considered

### TypeScript

Strong for application and web development, but less suitable as the primary language for the data-science portion of Kepler.

### C++

Strong for performance-sensitive computation, but would significantly increase implementation complexity for the core data-science and ML workflow.

### Rust

Strong safety and performance characteristics, but has a smaller data-science ecosystem relative to Python.

### Python

Provides the broadest mature ecosystem for data science, machine learning, AI tooling and experimentation while allowing fast project iteration.

## Rationale

Python provides mature ecosystems for:

- Data analysis
- Statistics
- Machine learning
- LLM integration
- Visualisation
- Testing

## Consequences

### Positive

- Fast experimentation
- Extensive scientific libraries
- Strong ML ecosystem
- Straightforward LLM integration
- Broad scientific computing support
- Good fit with the planned backend and orchestration architecture
- Lower implementation overhead than lower-level alternatives

### Negative

- Lower raw execution performance than native compiled languages
- Dynamic runtime behaviour requires disciplined typing and testing
- Greater reliance on third-party libraries
- Very large datasets may eventually require more specialised execution strategies

## Reconsideration

Performance-critical components may be moved to another language if profiling identifies a genuine bottleneck.
