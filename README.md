# Project Kepler

> **An autonomous system for discovering patterns, testing hypotheses, and extracting knowledge from data.**

## Overview

Project Kepler is an autonomous data science system designed to investigate structured datasets from end to end.

Given a tabular dataset and a natural-language analytical question, Kepler aims to:

1. Understand and validate the dataset.
2. Profile data quality and structure.
3. Explore distributions and relationships.
4. Form explicit analytical hypotheses.
5. Select appropriate statistical analyses and machine-learning approaches.
6. Execute analyses through deterministic tools.
7. Critique analytical decisions and findings.
8. Iterate when evidence or methodology is insufficient.
9. Preserve experiment provenance and reproducibility.
10. Produce a structured final report.

The central design principle is:

> **The LLM decides what should be done; deterministic tools determine what the data says.**

Kepler is intended as both a software-engineering project and an experimental platform for studying autonomous data science workflows.

---

## Problem

Large language models can reason about analytical tasks and interact with software tools, but natural-language reasoning alone is not a reliable substitute for deterministic statistical computation, machine-learning evaluation, data validation, or experiment tracking.

Kepler explores an alternative architecture in which an LLM provides planning, reasoning, hypothesis generation, interpretation, and critique while deterministic software performs the numerical and analytical work.

The project therefore focuses not only on whether an agent can produce an answer, but whether it can produce an answer that is:

- Correct
- Statistically appropriate
- Reproducible
- Traceable to evidence
- Explicit about limitations

---

## Research Question

> **Does iterative autonomous reasoning improve the correctness and reliability of automated data science compared with a single-pass agent, and what is the computational cost of that improvement?**

Supporting questions include:

- Can an agent correctly understand unfamiliar datasets?
- Can it identify data-quality problems?
- Can it select appropriate statistical tests?
- Can it identify when a statistical test is inappropriate?
- Can it select useful machine-learning approaches?
- Can it detect common analytical errors such as leakage?
- Does iterative critique reduce analytical errors?
- How reproducible are Kepler's investigations?
- What computational and financial cost is associated with additional reasoning?

---

## Initial Scope

### Supported initially

- Structured tabular datasets
- CSV
- Parquet
- Exploratory data analysis
- Data-quality analysis
- Statistical analysis
- Classification
- Regression
- Clustering
- Anomaly detection
- Visualisation
- Experiment tracking
- Report generation

### Initially out of scope

- Images
- Audio
- Video
- Real-time streaming
- Autonomous production deployment
- Unrestricted arbitrary code execution
- Fully autonomous modification of external systems

These boundaries may change through documented architecture decisions.

---

## High-Level Workflow

```text
Dataset + Question
        |
        v
   Data Ingestion
        |
        v
   Data Profiling
        |
        v
   Analytical Planning
        |
        v
 Hypothesis Generation
        |
        v
 Statistical / ML Analysis
        |
        v
      Critique
        |
   +----+----+
   |         |
   v         v
Re-plan     Pass
   |         |
   +----+----+
        |
        v
  Findings + Evidence
        |
        v
   Final Report
```

---

## Architecture Principle

Kepler separates reasoning from computation.

```text
                 LLM
                  |
           plans / decides
                  |
                  v
          Deterministic Tool
                  |
             computes
                  |
                  v
              Result
                  |
              observed
                  |
                  v
                 LLM
```

The LLM should not be treated as the numerical source of truth.

For example, the LLM may decide that a Pearson correlation is appropriate, but the actual correlation coefficient, confidence interval, p-value, sample size, and warnings must come from deterministic analytical software.

---

## Major Components

| Component | Responsibility |
|---|---|
| Kepler Core | Orchestration, state, lifecycle and workflow control |
| Kepler Analyst | Profiling, EDA and data-quality analysis |
| Kepler Statistician | Statistical tests, assumptions and effect sizes |
| Kepler Scientist | Hypothesis generation and analytical planning |
| Kepler Critic | Validation and identification of methodological problems |
| ML Engine | Model training, evaluation and comparison |
| Kepler Lab | Experiment tracking and persistence |
| Kepler Report | Structured report generation |
| Deterministic Tools | Numerical and analytical computation |

---

## Technology

- Python
- LangGraph
- OpenAI API
- Pandas
- NumPy
- SciPy
- scikit-learn
- PyTorch
- Matplotlib
- Plotly
- FastAPI
- PostgreSQL
- MLflow
- Docker
- Pytest
- Ruff
- mypy
- uv
- GitHub Actions

See [TECH_STACK.md](TECH_STACK.md) for details.

---

## Repository Structure

```text
Project-Kepler/
├── README.md
├── ROADMAP.md
├── ARCHITECTURE.md
├── TECH_STACK.md
├── RESEARCH.md
├── LICENSE
├── docs/
│   ├── decisions/
│   ├── architecture/
│   └── evaluation/
├── src/
├── tests/
├── datasets/
└── experiments/
```

---

## Development Philosophy

Kepler prioritises:

1. Correctness over apparent intelligence.
2. Deterministic computation over LLM-generated numerical claims.
3. Explicit tool contracts over unrestricted code execution.
4. Reproducibility over opaque experimentation.
5. Measurable evaluation over anecdotal demonstrations.
6. Simplicity before multi-agent complexity.
7. Evidence-backed findings over persuasive language.

---

## Project Status

**Current phase:** Foundation / Week 0

The initial work is focused on project definition, architecture, tooling, reproducibility, and development infrastructure.

---

## Planned Releases

| Version | Focus |
|---|---|
| 0.1 | Laboratory — ingestion and profiling |
| 0.2 | Analyst — EDA and visualisation |
| 0.3 | Scientist — statistics and hypotheses |
| 0.4 | ML — modelling and anomaly detection |
| 0.5 | Agent — LLM and tools |
| 0.6 | Critic — validation and correction |
| 0.7 | Multi-Agent |
| 0.8 | Lab — persistence and provenance |
| 0.9 | Interface |
| 1.0 | Autonomous Scientist — benchmarked release |

---

## License
[Liscense](LICENSE)
