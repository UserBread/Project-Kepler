# Kepler Evaluation Plan

## Purpose

Evaluate whether increasingly autonomous architectures improve data-science correctness and reliability.

## System Variants

1. LLM only
2. LLM + deterministic tools
3. Single autonomous agent
4. Multi-agent
5. Multi-agent + critic

## Metrics

### Correctness

- Numerical correctness
- Statistical test correctness
- Model evaluation correctness
- Interpretation correctness

### Reliability

- Methodological error rate
- Data leakage rate
- Unsupported-claim rate
- Tool error rate

### Reproducibility

- Successful replay rate
- Trace completeness
- Deterministic result consistency

### Efficiency

- Runtime
- Tool calls
- LLM calls
- Token usage
- API cost

### Human Intervention

- Number of interventions
- Type of intervention
- Reason for intervention

## Evaluation Record

Each benchmark task should record:

```text
Task
Dataset
Question
System Variant
Expected Result
Observed Result
Errors
Tool Calls
Runtime
Cost
Human Intervention
```

## Important Principle

The evaluation must measure failures as well as successes.

A system that correctly refuses an inappropriate analysis should not automatically be treated as a failure.
