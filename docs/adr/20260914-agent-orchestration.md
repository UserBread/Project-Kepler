# Agent Orchestration

- Status: Accepted
- Date: 2026-09-14
- Tags: orchestration, langgraph, workflow, agents

## Context and Problem Statement

Kepler is designed to execute multi-step investigations, not merely answer a single prompt. An investigation may involve understanding a user question, inspecting a dataset, forming hypotheses, choosing analyses, running tools, reviewing results, identifying weaknesses, and repeating the cycle until a final report is produced.

This requires persistent state, conditional branching, loops, error handling, and eventually specialised agents. A simple request/response pattern would become difficult to manage as the workflow becomes more autonomous.

## Decision Drivers

- Investigations require iterative reasoning and repeated validation.
- The workflow must maintain state across steps.
- The system may eventually benefit from specialist agents or task decomposition.
- Tool execution needs observability and controlled branching.

## Considered Options

- Custom orchestration layer
- Simple Python control flow
- Other agent frameworks
- LangGraph-based orchestration

## Decision Outcome

Chosen option: "LangGraph-based orchestration", because it provides explicit workflow representation, stateful execution, and conditional transitions suitable for iterative scientific investigations.

The system will initially use a single agent and will only introduce additional specialised roles when justified by project requirements. The workflow will support planning, tool selection, execution, observation, and re-planning.

### Positive Consequences

- Explicit representation of investigation steps.
- Persistent state across workflow execution.
- Conditional branching and iterative reasoning.
- Clear support for future multi-agent patterns.
- Better observability of agent behaviour and workflow decisions.

### Negative Consequences

- Adds another framework dependency to the stack.
- The abstraction may be unnecessary for very simple workflows.
- Requires understanding of graph-based workflow design and debugging.

## Pros and Cons of the Options

### Custom orchestration

- Good, because it can be tailored precisely to the project.
- Bad, because it would require substantial time and complexity to implement reliable state management and workflows.

### Simple Python control flow

- Good, because it is straightforward for early prototypes.
- Bad, because it becomes harder to maintain as workflows become nested, iterative, and multi-step.

### Other agent frameworks

- Good, because they may offer different strengths and abstractions.
- Bad, because there is no immediate evidence that a different framework is necessary.

### LangGraph-based orchestration

- Good, because it supports stateful, graph-based workflow management.
- Good, because it provides a natural foundation for multi-agent or specialist workflows.
- Bad, because it adds a framework dependency and learning curve.

## Links

- This decision integrates with the LLM reasoning pattern in [ADR-003](ADR-003%20—%20LLM%20as%20Reasoning%20Layer.md).