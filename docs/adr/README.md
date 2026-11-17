# Architecture decision records

Decisions specific to CivilBuilder. Suite-wide decisions are recorded in the
[suite ADRs](https://github.com/ACKaraca/arc-suite/tree/main/docs/adr) and are not restated here.

## Index

| ADR | Title | Status |
|---|---|---|
| [0001](0001-civil-model-in-document-package.md) | Civil model in the Arc document package; drawings through the shared drafting engine | Accepted |
| [0002](0002-station-range-regeneration.md) | Station-range invalidation and per-station parallel evaluation | Accepted |
| [0003](0003-node-graph-cross-section-components.md) | Cross-section components as node graphs | Accepted |
| [0004](0004-styles-separate-from-design-data.md) | Styles and labels as resources separate from design data | Accepted |
| [0005](0005-hydraulic-engine-boundary.md) | Hydraulic engines behind a process boundary | Accepted |
| [0006](0006-one-model-for-concept-and-detail.md) | One model for concept and detailed design | Accepted |

## Template

```markdown
# NNNN Title

- Status: Proposed | Accepted | Superseded by NNNN
- Capabilities: CB-XXX-NNN, ...

## Context

The forces at play and the problem to decide.

## Decision

What is decided, stated in present tense.

## Consequences

What becomes easier, what becomes harder, what follows.

## Alternatives considered

Each option with the reason it was not chosen.

## Trigger to reopen

The observable condition under which this decision is revisited.
```
