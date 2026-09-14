# ADR-002: Primary Language and Runtime

- Status: Accepted
- Date: 2026-09-14
- Tags: runtime, python, stack, implementation

## Context and Problem Statement

Kepler must combine data science, statistical analysis, machine learning, AI orchestration, and backend functionality into one coherent system. The project therefore needs a language and ecosystem that supports experimentation, integration with LLM tooling, API development, testing, and ML workflow tracking.

Python is a strong fit for these tasks, but the decision must be explicit because it shapes the rest of the project architecture and engineering approach.

## Decision Drivers

- The project heavily depends on scientific computing and statistical tooling.
- The system must integrate with model orchestration, LLM services, and backend APIs.
- Rapid iteration and experimentation are essential for research work.
- The stack needs mature libraries for testing, workflow tracking, and machine learning.

## Considered Options

- TypeScript as the primary language
- C++ as the primary language
- Rust as the primary language
- Python as the primary language

## Decision Outcome

Chosen option: "Python as the primary language", because it provides the broadest mature ecosystem for data science, machine learning, AI tooling, and experimentation while allowing fast project iteration.

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

### Positive Consequences

- Strong ecosystem for data science and machine learning.
- Mature AI and LLM integration tooling.
- Rapid prototyping and experimentation.
- Broad scientific computing support.
- Good fit with the planned backend and orchestration architecture.
- Lower implementation overhead than lower-level alternatives.

### Negative Consequences

- Lower runtime performance than C++ for some workloads.
- Greater reliance on third-party libraries.
- Dynamic typing requires additional tooling and discipline for safety and maintainability.
- Very large datasets may eventually require more specialised execution strategies.

## Pros and Cons of the Options

### TypeScript

- Good, because it offers strong web and tooling ecosystems.
- Bad, because it is not as mature for scientific computing and ML workflows as Python.

### C++

- Good, because it offers high performance and deterministic low-level execution.
- Bad, because it increases implementation complexity and weakens the experimental workflow needed for research.

### Rust

- Good, because it provides strong safety and performance characteristics.
- Bad, because the project's primary challenge is not systems-level performance but AI and data-science orchestration.

### Python

- Good, because it has mature data-science, ML, and LLM ecosystems.
- Good, because it supports rapid development and experimentation.
- Bad, because some computational workloads may require specialised optimisation later.

## Links

- This decision informs the deterministic tool architecture described in [ADR-004](ADR-004%20—%20Deterministic%20Data%20Science%20Tools.md).