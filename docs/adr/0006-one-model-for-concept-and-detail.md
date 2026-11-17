# 0006 One model for concept and detailed design

- Status: Accepted
- Capabilities: CB-CON-001 to CB-CON-018, CB-GEO-013 to CB-GEO-022

## Context

Concept planning happens in a large geospatial context with quick, approximate objects; detailed
design needs precise, standards-checked objects. Keeping them in different applications or models
forces exports between stages, loses parameters on every round trip and leaves two versions of the
truth when a project returns to concept work.

## Decision

- Concept roads, intersections, structures and drainage are the same object types as in detailed
  design (alignments, profiles, assemblies, corridors, networks, bridges), created by concept
  commands with simplified parameters and concept-level road styles.
- Refinement changes parameters, assemblies and criteria on the same objects; identifiers persist.
- Geospatial context (terrain, imagery, buildings, networks) is referenced live through the CRS-aware
  layers of the geospatial area, not converted into a separate model.
- Concept-specific behavior (automatic intersections, proposed structures, terrain modification)
  is implemented as commands and regeneration nodes over the shared objects.
- Design options hold alternative objects within the one document.

## Consequences

- No export or re-creation between concept and detailed design; quantities and checks are
  comparable across stages.
- Concept commands must produce valid detailed objects, so defaults and road styles carry real
  component definitions.
- Large-area context must stream efficiently in the same application that does detailed design,
  which raises viewport and tile-cache requirements.
- Very coarse sketches still create full objects; the cost is accepted because regeneration is
  incremental.

## Alternatives considered

- **A separate concept application with exchange to detailed design.** Rejected: round-trip loss and
  duplicate truth.
- **Separate lightweight concept object types inside the same application.** Rejected: requires a
  conversion step and duplicate tooling.

## Trigger to reopen

Reopen if concept-scale projects (tens of kilometers of roads with options) cannot meet interactive
performance targets with full objects after optimization.
