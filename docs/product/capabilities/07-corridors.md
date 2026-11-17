# Corridors

This area builds 3D linear models by evaluating assemblies along baselines. A corridor is derived
data on the regeneration graph: it is computed station by station, rebuilt only where its inputs
changed, and reports failures per station. The rebuild mechanics are specified in
[the dependency chain architecture](../../architecture/dependency-chain.md).

## Domain objects

- **Corridor**: a set of baselines with regions, plus outputs.
- **Baseline**: an alignment with a profile, or a feature line or 3D polyline path.
- **Region**: a station range on a baseline with an assembly, frequency, target mapping and overrides.
- **Frequency set**: sampling increments and added stations.
- **Target mapping**: the binding of component targets to model objects.
- **Override**: a parameter value replaced over a station range or at one station.
- **Station section**: the computed points, links and shapes at one station (derived, cached).
- **Corridor outputs**: feature lines, surfaces, boundaries, solids and points.

## Structure

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-COR-001 | Corridor object | A corridor holds baselines and regions and computes station sections from them. Its outputs are derived data that can be discarded and rebuilt from the inputs at any time. | T1 | 3 |
| CB-COR-002 | Baselines | A baseline is an alignment with a profile, or a feature line or 3D polyline path that supplies both. A corridor holds any number of baselines, including offset baselines that follow offset alignments with their own profiles. | T1 | 3 |
| CB-COR-003 | Regions | Regions are station ranges on a baseline, each with its own assembly, frequency, target mapping and overrides. Regions split, merge, copy and snap to geometry points; gaps between regions are allowed, and overlapping regions are reported. | T1 | 3 |
| CB-COR-004 | Frequency | Increments are set separately for lines, arcs, spirals and vertical curves; stations are added at horizontal and vertical geometry points, superelevation critical stations, target geometry points and explicit stations. Stations closer than the station tolerance merge. | T1 | 3 |
| CB-COR-005 | Target mapping | Component targets are mapped per region to surfaces, alignments, profiles, feature lines, polylines and network parts, with priority when several candidates apply. Unresolved targets are listed with their station ranges. | T1 | 3 |
| CB-COR-006 | Parameter overrides | Any component parameter is overridden over a station range or at a single station, with linear or curved interpolation between overridden stations. Overrides are listed in a table and shown in the section editor. | T1 | 3 |

## Computation

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-COR-007 | Station-independent evaluation | Each station section is evaluated independently from the assembly, the baseline state at that station and the targets, so stations compute in parallel on all available cores. Results are cached per station with the revision they were computed from. | T1 | 3 |
| CB-COR-008 | Station-range invalidation | An input change invalidates only the stations whose inputs it affects (for example a profile edit invalidates the station range of the changed vertical elements), and only those stations and their downstream outputs rebuild. | T1 | 3 |
| CB-COR-009 | Rebuild policies | Each corridor rebuilds automatically, on demand (showing a stale state and the stale station ranges), or frozen (outputs kept while inputs change until the corridor is unfrozen). A static copy detaches outputs from inputs entirely. | T1 | 3 |
| CB-COR-010 | Failure reporting | Failures (target not found, component error, invalid geometry) are reported per station with the component and message. Failing stations are omitted from outputs while every other station completes, and the report links to the section editor. | T1 | 3 |
| CB-COR-011 | Progressive and cancellable rebuild | Stations in visible views and selected ranges compute first; progress is shown; a rebuild is cancellable and never blocks editing. A result computed for an older revision is discarded. | T1 | 3 |

## Outputs

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-COR-012 | Corridor surfaces | Surfaces are built from selected link codes and feature lines, bounded by code-derived outlines, corridor extents or user polygons, with overhang correction for top and datum surfaces. They regenerate with the corridor for the changed station ranges. | T1 | 3 |
| CB-COR-013 | Corridor feature lines | Points with the same code connect across stations into feature lines per baseline, optionally broken at gaps. They regenerate with the corridor and serve as targets, breaklines and grading references. | T1 | 3 |
| CB-COR-014 | Corridor solids and meshes | Shapes sweep between stations into closed solids or meshes per shape code, carrying station range, region, code and material properties, for IFC export and coordination in Arc Review. | T1 | 3 |
| CB-COR-015 | Section editor | The editor steps through stations of a baseline, shows the section with codes, targets and dimensions, and edits overrides at the current station or a range. | T1 | 3 |
| CB-COR-016 | Points from corridors | Points are created at code locations at corridor stations, either linked to the corridor or as static copies. | T2 | 3 |
| CB-COR-017 | Slope patterns | Cut and fill slope symbols display in plan between chosen feature line pairs and regenerate with the corridor. | T2 | 3 |
| CB-COR-018 | Corridor display | Corridors display in 3D with materials assigned through code style sets and export to the Arc Scene for rendering. | T1 | 3 |
| CB-COR-019 | Slope stake reports | Slope stake reports list offsets, elevations and cut or fill from hinge points to catch points at chosen stations, and export as LandXML or CSV. | T2 | 4 |

## Interaction and transitions

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-COR-020 | Baselines targeting baselines | A baseline may target outputs of another baseline (for example a side road tying into main road edges). The regeneration graph orders the dependency and rejects mappings that would form a cycle, naming the objects involved. | T1 | 3 |
| CB-COR-021 | Transitions | Width, slope and daylight transitions over station ranges are expressed through targets and interpolated overrides, without splitting regions. | T1 | 3 |
| CB-COR-022 | Feature-line corridors | Corridors on feature line paths model ditches, channels, berms and pond edges with the same assemblies and outputs. | T2 | 3 |
| CB-COR-023 | Corridor quantities source | Shape areas per station are available to material lists (CB-QTY-002) and pay item rules without extracting solids. | T1 | 3 |
