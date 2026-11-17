# Application connectors

This area exchanges native civil design objects held in other applications' drawings and concept
models: surfaces, alignments, profiles, corridors, pipe networks, parcels and styles where they map.
Exchange runs through connectors, optional user-licensed bridges and open readers, as decided in
[suite ADR-0017](https://github.com/ACKaraca/arc-suite/blob/main/docs/adr/0017-exchange-connectors-and-licensed-bridges.md).
A connector is a small add-in that runs inside the user's own licensed copy of the other application
through that application's public API; it reads and writes the Arc exchange package, an open,
documented container specified in the
[interchange architecture](https://github.com/ACKaraca/arc-core/blob/main/docs/architecture/interchange.md).
Connectors live in the `arc-connectors` repository, not in this one. Format mapping, fidelity levels
and loss reporting are specified in [the interoperability architecture](../../architecture/interoperability.md).

Reverse engineering of undocumented formats or binaries, and running the compiled or protected
script files of other applications, remain excluded because each is a legal problem.

## Domain objects

- **Exchange package**: the open container that a connector and CivilBuilder both read and write.
- **Connector session**: one exchange between a document and a host application, with its mapping
  profile, the objects exchanged, the identifier map and the loss report.
- **Exchange identifier map**: the pairing of CivilBuilder object identifiers with host object
  identifiers, kept on both sides so that repeated exchanges update objects.
- **Mapping profile**: saved choices for object kinds, styles, layers and codes, reused between sessions.
- **Bridge configuration**: the location and version of a user-installed, user-licensed conversion library.

## Civil objects through connectors

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-CONNECT-001 | Exchange of native civil objects | A connector running inside another application exports its native civil design objects to the exchange package and imports CivilBuilder objects from it. Geometry, semantics, parameters, types, identifiers and relationships travel in both directions at data fidelity; edit fidelity applies where the host API allows. | T3 | 5 |
| CB-CONNECT-002 | Surfaces | TIN and grid surfaces exchange with their definition items (points, breaklines, boundaries, edits) where the host exposes them, and as the computed triangulation or grid otherwise. The session states for each surface which of the two arrived. | T3 | 5 |
| CB-CONNECT-003 | Alignments and profiles | Alignments exchange as ordered elements (lines, arcs, spirals) with station equations, design speeds, criteria references and superelevation, and profiles as vertical intersection points and curves or as sampled geometry. Constraint state is inferred where the host does not expose it and marked as inferred. | T3 | 5 |
| CB-CONNECT-004 | Corridors | A corridor exchanges its baselines, regions, frequency, targets and outputs. Assemblies map to CivilBuilder component definitions where an equivalent exists; otherwise the corridor arrives as feature lines, surfaces and solids at data fidelity with the unmapped definition preserved as foreign data. | T3 | 5 |
| CB-CONNECT-005 | Pipe networks | Gravity and pressure networks exchange parts, sizes, positions, inverts, connections and rule references. Parts map to the parts list by family and size; unmatched parts arrive as generic parts with their source properties. | T3 | 5 |
| CB-CONNECT-006 | Parcels, points and linework | Parcels with their segments and properties, points with descriptions and user properties, survey figures and feature lines exchange with their identifiers. Parcel topology is rebuilt on arrival and differences from the source topology are reported. | T3 | 5 |
| CB-CONNECT-007 | Style mapping | Object styles and label styles exchange where they map onto CivilBuilder style components through a mapping profile. Unmapped styles are preserved as foreign data and the objects use a default style; styles never change design data on either side ([ADR-0004](../../adr/0004-styles-separate-from-design-data.md)). | T3 | 5 |
| CB-CONNECT-008 | Concept models | Roads, bridges, drainage and terrain modifications of another application's concept models exchange through a connector into the concept objects of [concept modeling](21-concept-modeling.md), keeping identifiers so that refinement in place continues in either application. | T3 | 5 |

## Identity, change tracking and reporting

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-CONNECT-009 | Identifiers for repeated round trips | The exchange identifier map pairs each object with its host counterpart, and both sides record the pairing. A repeated exchange updates the paired objects, adds new ones and reports deleted ones instead of duplicating anything (extends CB-IO-015). | T3 | 5 |
| CB-CONNECT-010 | Change detection and conflicts | Each side records a revision stamp per exchanged object. A session lists objects changed on one side, on both sides, or on neither; objects changed on both sides are never overwritten silently and are resolved per object by choosing a side or keeping both. | T3 | 5 |
| CB-CONNECT-011 | Loss report | Every session produces a loss report in the form of CB-IO-014: per object and property, mapped, approximated with the approximation stated, preserved as foreign data, or dropped with the reason. The report is stored with the session. | T3 | 5 |
| CB-CONNECT-012 | Review before apply | An incoming session shows what will be created, updated and removed, and applies in one transaction that can be undone as a unit. Mapping choices save as a mapping profile; a headless session applies a saved profile without prompts and fails with the loss report when a required mapping is missing. | T3 | 5 |
| CB-CONNECT-013 | Package validation | Every package is validated against the published schema before use, and malformed or oversized content is rejected with a located message. Connector and reader are tested against the conformance suite owned by `arc-core`. | T3 | 5 |

## Licensed bridges and open readers

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-CONNECT-014 | User-licensed bridge | Where a vendor or consortium licenses a conversion library for a format, the user points CivilBuilder to an installed copy, which runs as a separate process and exchanges data through the exchange package. The library is never distributed with Arc, and every workflow that can use a bridge also works without it. | T3 | 5 |
| CB-CONNECT-015 | Open readers | Formats with a published specification or a permissively licensed open-source reader are read natively behind an `arc-io-*` crate, including DGN V7 linework, points, text and cells as source geometry with level mapping and georeferencing. Each reader records its specification or licence and has its own loss report. | T3 | 5 |
