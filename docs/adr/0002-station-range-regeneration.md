# 0002 Station-range invalidation and per-station parallel evaluation

- Status: Accepted
- Capabilities: CB-COR-007 to CB-COR-011, CB-PRF-001, CB-SEC-004, CB-QTY-002

## Context

The chain surface → alignment → profile → corridor → sections → quantities dominates rebuild time on
linear projects. Rebuilding whole objects after every edit makes long corridors slow and forces users
to split projects into many documents for performance. Most edits are local in station: a vertical
curve change affects a few hundred meters.

The suite regeneration graph (suite ADR-0007) supports revision-tagged background work; it leaves the
granularity of invalidation to each product.

## Decision

- Changes to linear objects produce change extents expressed as internal-distance ranges; the
  regeneration graph propagates and merges ranges along edges as specified in
  [the dependency chain](../architecture/dependency-chain.md).
- A corridor station section is a pure function of its inputs at that station, cached per station
  with the revision it was computed from, and evaluated in parallel batches.
- Downstream outputs (feature lines, corridor surfaces, sections, material lists) rebuild by
  station interval; mass haul rebuilds from the first affected interval because it is cumulative.
- Failures are recorded per station range and never abort other ranges.

## Consequences

- Edit latency scales with the size of the change, not with the corridor length.
- Component definitions must be side-effect free and deterministic (enforced by
  [ADR-0003](0003-node-graph-cross-section-components.md)).
- Every edge must declare how it maps an incoming extent to an outgoing one; edges that cannot do so
  fall back to whole-object invalidation, which is correct but slower.
- Equivalence tests (incremental equals full rebuild) become a mandatory part of the test suite.

## Alternatives considered

- **Whole-object invalidation.** Simple and correct, rejected because it fails the performance
  targets on long corridors.
- **Fine-grained invalidation at component-instance level within a station.** Rejected: station
  evaluation is cheap compared with scheduling overhead at that granularity.

## Trigger to reopen

Reopen if measured rebuilds show scheduling or range bookkeeping exceeding 20 percent of rebuild
time, or if a required edge cannot express its extent mapping.
