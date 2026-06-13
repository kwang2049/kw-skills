---
name: implement
description: Develop a new idea or feature through an approval-gated implementation workflow. Use when the user asks to implement, build, add, design, or ship a feature and wants an implementation proposal first, including Markdown, Mermaid diagrams, code snippets, user-feedback refinement, and implementation only after explicit approval.
---

# Implement

Turn a feature idea into working code through a proposal-first workflow. Do not make implementation edits until the user approves the proposal.

## Workflow

1. Understand the request and inspect the codebase:
   - Read relevant `README*`, `AGENTS.md`, package manifests, tests, and nearby code.
   - Use `rg --files` and targeted searches to find the affected modules.
   - Ask only for missing information that blocks a coherent proposal.
2. Present an implementation proposal in Markdown:
   - Include the problem statement, goals, non-goals, affected files, data or control flow, implementation steps, risks, and validation plan.
   - Include at least one Mermaid diagram when it clarifies architecture, flow, state, sequence, or dependencies.
   - Include short code snippets or pseudocode for the key API, data model, interface, or algorithm.
   - Keep snippets illustrative; do not pretend they are final diffs.
3. Refine with user feedback:
   - Incorporate requested changes into a revised proposal.
   - Resolve tradeoffs explicitly when feedback changes scope, risk, migration strategy, or compatibility.
   - Continue revising until the user approves implementation.
4. Implement only after explicit approval:
   - Treat words such as "approved", "go ahead", "implement it", "ship it", or equivalent clear confirmation as approval.
   - If approval is ambiguous, ask before editing files.
   - Keep changes scoped to the approved proposal unless a discovered blocker requires a small adjustment.
   - If implementation must materially diverge from the approved proposal, stop and get approval for the revised approach.
5. Validate and report:
   - Run the most relevant tests, linters, type checks, or focused commands supported by the project.
   - Update docs or examples when the implemented behavior changes user-facing usage.
   - Summarize what changed, validation results, and any remaining risks.

## Proposal Format

Use this shape unless the project calls for a different one:

````markdown
## Implementation Proposal

### Summary

### Goals

### Non-Goals

### Current Flow

```mermaid
flowchart TD
  A[Current entry point] --> B[Relevant component]
```

### Proposed Flow

```mermaid
sequenceDiagram
  participant User
  participant App
  User->>App: New feature action
  App-->>User: Updated behavior
```

### Key Changes

### Code Sketch

```ts
type Example = {
  id: string;
};
```

### Validation Plan

### Risks and Tradeoffs
````

## Guardrails

- Do not edit source files during the proposal phase.
- Do not skip the proposal just because the implementation looks straightforward.
- Do not run broad, expensive, or destructive commands as part of discovery.
- Do not over-specify low-level details before reading the relevant code.
- Prefer the repository's existing patterns over new abstractions.
- Keep the final implementation traceable to the approved proposal.
