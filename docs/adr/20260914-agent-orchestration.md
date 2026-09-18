# ADR-005: Agent Orchestration

- **Status:** Accepted
- **Date:** 2026-09-18

## Context

Kepler needs to represent stateful analytical workflows involving planning, tool execution, observations, critique and potentially repeated iterations.

A simple linear chain will become insufficient once autonomous iteration is introduced.

## Decision Drivers

- Investigations require iterative reasoning and repeated validation.
- The workflow must maintain state across steps.
- The system may eventually benefit from specialist agents or task decomposition.
- Tool execution needs observability and controlled branching.

## Decision

LangGraph will be used for stateful agent orchestration.

Kepler will initially implement a single-agent workflow and add specialist agents only when justified by evaluation.

The workflow will support planning, tool selection, execution, observation and re-planning.

## Initial Workflow

```text
Question
  ↓
Plan
  ↓
Tool
  ↓
Observation
  ↓
Decision
  ↓
Finish / Continue
```

Later:

```text
Plan
  ↓
Analyse
  ↓
Critique
  ↓
Pass / Re-plan
```

## Alternatives Considered

### Custom orchestration

Would provide maximum control but introduce unnecessary infrastructure before the workflow is understood.

### Simple sequential chains

Insufficient for conditional branching and iterative investigation.

### Multi-agent from the beginning

Rejected because it introduces complexity before demonstrating that multiple agents provide measurable value.

### Other agent frameworks

May offer different strengths, but there is no immediate evidence that another framework is necessary.

## Consequences

### Positive

- Explicit workflow state
- Conditional transitions
- Iteration
- Checkpointing potential
- Natural path to multi-agent workflows
- Explicit representation of investigation steps
- Persistent state across workflow execution
- Better observability of agent behaviour and workflow decisions

### Negative

- Additional framework dependency
- Workflow design becomes an explicit engineering concern
- Adds a framework dependency and learning curve.
- The abstraction may be unnecessary for very simple workflows.
- Requires understanding of graph-based workflow design and debugging.

## Reconsideration

The orchestration framework may be changed if it becomes a limitation or if evaluation demonstrates that simpler orchestration is preferable.
