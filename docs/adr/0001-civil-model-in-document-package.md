# 0001 Civil model in the Arc document package; drawings through the shared drafting engine

- Status: Accepted
- Capabilities: CB-PLAN-001 to CB-PLAN-013, CB-IO-005, CB-IO-006, CB-STY-006

## Context

Civil design produces large amounts of drawing output (plan, profile and section sheets) and is
exchanged widely as DWG and DXF. A tempting design is to store civil objects as custom entities in a
drawing database, as DraftBuilder stores its native model. But civil objects are semantic and
dependent (alignments, profiles, corridors, station-keyed derived data), need stable identifiers,
partial loading, a journal for multi-user change sets and caches for derived data. Drawing entity
models carry none of this natively, and custom civil entities are unreadable to other applications
anyway.

DraftBuilder and every other Arc product share one drafting engine, `arc-draft`, for sheets,
annotation, plotting and DWG/DXF entity exchange.

## Decision

- The civil model is stored in the Arc document package (`.civilb`) as typed objects in the `arc-doc`
  store. It is never stored as drawing entities.
- Sheets, layouts, drafting annotation, plot styles and plotting use `arc-draft`, inside the same
  document package. Sheet viewports display model content produced by the presentation pass
  ([styles and labels](../architecture/styles-and-labels.md)).
- DWG and DXF are interoperability formats. Import reads drafting entities as definition sources for
  civil objects. Export writes civil objects as plain entities with styles applied and object
  identifiers in extended data, and writes sheets as layouts.
- DraftBuilder opens CivilBuilder's DWG/DXF exports like any drawing; CivilBuilder does not depend on
  DraftBuilder at compile time or run time.

## Consequences

- Civil objects get stable identifiers, transactions, journaled undo, partial loading and
  revision-tagged caches from `arc-doc` without a parallel storage path.
- Sheet production quality and the plot pipeline are identical to the rest of the suite.
- DWG/DXF recipients see geometry and annotation, not editable civil objects; semantic exchange uses
  LandXML and IFC 4.3. This is stated in every DWG export report.
- Users who work drawing-first must import linework as definition data instead of drawing civil
  objects as entities.

## Alternatives considered

- **Civil objects as custom drawing entities in DWG.** Rejected: no published way for other
  applications to read them, no element-level journal, weak partial loading, and drawing files would
  become the authority for derived data.
- **Separate sheet documents per sheet set.** Rejected for the first release: sheets that live with
  the model regenerate incrementally and need no reference resolution; shared references
  (CB-REF-002) still allow production documents that reference design documents.

## Trigger to reopen

Reopen if a published, openly implementable specification for semantic civil objects inside DWG
appears and users require edit-level round trips through it.
