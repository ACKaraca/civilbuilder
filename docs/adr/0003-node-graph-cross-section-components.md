# 0003 Cross-section components as node graphs

- Status: Accepted
- Capabilities: CB-ASM-001 to CB-ASM-012, CB-AUTO-006

## Context

Typical cross-sections need parametric, conditional components (lanes, daylight with benching,
ditches, track beds). Users and agencies need custom components, but authoring them in a general
programming language excludes most designers, and a separate authoring application splits the
workflow and the file formats. Components are evaluated thousands of times per corridor and must be
deterministic for station-range regeneration ([ADR-0002](0002-station-range-regeneration.md)).

## Decision

- A component definition is an `arc-nodes` graph with typed parameters, declared targets and an
  output contract of ordered points, links and shapes with codes.
- The graph editor is part of CivilBuilder (on the `arc-ui` node editor); there is no separate
  authoring tool.
- Graph evaluation is side-effect free, bounded (loop and step limits) and deterministic; a
  definition cannot read the document except through its declared inputs.
- Definitions are text-diffable library files with versions, manifests and test cases runnable
  headless.
- The shipped standard library is written in the same graph form, so it serves as reference and test
  corpus.
- Algorithms that graphs cannot express efficiently are added as new node types in the product or
  through sandboxed plug-ins that register nodes (CB-AUTO-008), not as opaque components.

## Consequences

- Designers author and test components where they use them, with live preview against real targets.
- The same graph engine serves automation graphs, reducing the number of concepts to learn.
- Node types become a public contract that needs versioning and migration (CB-ASM-012).
- Graph evaluation performance is on the corridor critical path; the evaluator compiles graphs into
  an evaluation plan once per definition version.

## Alternatives considered

- **Components written in a general programming language only.** Rejected as the primary path:
  excludes most users; kept possible through plug-in nodes.
- **A separate authoring application with its own package format.** Rejected: splits workflow and
  formats.
- **A fixed catalog of components with parameters only.** Rejected: cannot cover regional standards
  and project-specific sections.

## Trigger to reopen

Reopen if graph evaluation cannot meet the corridor rebuild targets after plan compilation, or if a
widely needed component class cannot be expressed without plug-in nodes.
