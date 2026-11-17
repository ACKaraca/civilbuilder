# Product vision

CivilBuilder is the Arc application for civil infrastructure design. This document states the
problem it addresses, who it serves, the principles it follows, its scope and non-goals, and what
distinguishes it.

## Problem and purpose

Civil infrastructure is designed as a chain of dependent models: survey becomes terrain, terrain and
alignments define profiles, profiles and cross-sections define corridors, corridors yield sections,
quantities, grading and drainage, and all of it must become sheets and exchange files that agencies,
contractors and machines accept. Practitioners today face four recurring problems with this chain:
rebuilds that block work and cascade unpredictably on large projects; display and annotation
standards that are hard to maintain and audit; references between project files that break; and
exchange formats that lose meaning between concept and detailed design, between disciplines, and
into construction.

CivilBuilder models the whole chain in one semantic document on the Arc foundation. Derived data is
computed incrementally in the background, styles are kept apart from design data, references are by
stable identifier, and open formats (LandXML, IFC 4.3, GIS formats) are first-class.

## Primary users and deliverables

| User | Typical deliverables |
|---|---|
| Transportation engineers and designers (roads, highways, rail) | Alignments, profiles, corridors, superelevation, intersections, plan and profile sheets, cross-section sheets, quantities, IFC and LandXML models |
| Land development and site engineers | Grading plans, parcel and lot layouts, earthwork balance, storm drainage, parking and access layouts |
| Surveyors | Adjusted control, existing ground surfaces, figures, stakeout data, legal descriptions |
| Drainage and utility engineers | Gravity and pressure networks, catchment and hydraulic analyses, pond and culvert designs, profiles and reports |
| Planners and early-phase designers | Concept alternatives in geospatial context, quick quantities and costs, visibility, flood and traffic screening, presentation sequences |
| Rail designers | Track geometry, cant, turnouts, platforms, clearance checks |
| CAD and standards managers | Templates, style libraries, criteria sets, component libraries, headless standards audits |
| Contractors | Machine-control models, quantity takeoff, as-built comparison |

## Product principles

1. **One model from concept to construction.** Concept objects are detailed objects with fewer
   parameters set; refinement happens in place.
2. **The dependency chain is explicit.** Every derived object shows what it depends on, whether it
   is current, and which station ranges are stale or failed.
3. **Never block the designer.** Regeneration runs in parallel in the background, is cancellable and
   rebuilds only what changed.
4. **Display is not design.** Styles and labels never alter or recompute design data.
5. **Geospatial by default.** Every document has a CRS; GIS sources are referenced live, not converted.
6. **Open exchange.** LandXML, IFC 4.3 and GIS formats are primary; every import reports its losses.
7. **Standards are data.** Design criteria, components, catalogs and styles are text-diffable
   libraries that can be reviewed, versioned and tested.
8. **Automatable.** Every operation is a command; the CLI runs checks and exports without a display.

## Scope

CivilBuilder covers the 26 capability areas listed in the [capability index](capabilities/README.md):
geospatial data, survey, surfaces, alignments, profiles, cross-section components and assemblies,
corridors, intersections and roundabouts, sections, quantities and mass haul, grading, parcels,
gravity and pressure networks, hydrology and hydraulics, rail, bridges and structures, plan
production, styles and labels, shared references and collaboration, concept modeling and analysis,
swept paths and parking, reality and subsurface data, automation and interoperability.

## Non-goals

| Non-goal | Reason |
|---|---|
| Structural analysis, design and reinforcement detailing of bridges and structures | Structural engineering belongs to ArchBuilder's structural discipline and to dedicated analysis tools; CivilBuilder provides geometry, clearances and IFC handover (CB-BRG-012). |
| Full point cloud registration and scan processing | Registration of raw scans is a separate processing discipline; CivilBuilder consumes registered clouds and aligns them by control (CB-REAL-010). |
| GNSS and total-station raw data processing and field controller software | Field data processing is instrument-specific; CivilBuilder imports results through open formats and plug-ins. |
| Full cost estimating and scheduling | CivilBuilder produces quantities and simple cost totals; estimating, 4D and 5D belong to Arc Review and dedicated tools. |
| Pedestrian crowd simulation | No documented, testable method is selected and no workflow depends on it; revisit when a validated open model is available. |
| Two-dimensional unsteady river modeling and sediment transport | Specialized, validated river solvers exist; CivilBuilder exports river geometry (CB-HYD-020) and screens flooding at concept level (CB-ANL-006). |
| Storing the civil model as drawing entities | The model lives in the Arc document package; drawings are an output and exchange format ([ADR-0001](../adr/0001-civil-model-in-document-package.md)). |
| Reading or writing proprietary formats without a published specification | Exchange runs through open formats in line with the suite interoperability policy. |

## Positioning

CivilBuilder covers the professional scope addressed by tools such as Autodesk Civil 3D,
Autodesk InfraWorks and Autodesk Vehicle Tracking, Bentley OpenRoads, OpenRail, OpenSite and
OpenBridge, Trimble Business Center and Novapoint, 12d Model, Carlson Civil and AutoTURN: survey,
terrain, linear design, site design, utilities, drainage analysis, rail, concept planning and
swept-path analysis.

## Differentiators

| Differentiator | Capabilities |
|---|---|
| GIS data as a first-class source: CRS-aware referenced layers, streaming tiles and conversion with refresh, with no conversion step | CB-GEO-013 to CB-GEO-022, CB-CON-001 |
| IFC 4.3 infrastructure entities and LandXML as primary exchange, with loss reports and identifier mapping | CB-IO-001 to CB-IO-004, CB-IO-014, CB-IO-015 |
| Integrated open hydraulic engines for storm, sewer and pressure systems | CB-HYD-006, CB-HYD-007, CB-HYD-018 |
| Multi-threaded corridor rebuild with station-range invalidation and per-station failure reporting | CB-COR-007 to CB-COR-011 |
| Concept and detailed design in one application and one model | CB-CON-003, CB-CON-013 |
| Cross-section components authored as node graphs inside the product, with test cases | CB-ASM-001, CB-ASM-002, CB-ASM-007 |
| Machine-control exports from the design model | CB-IO-008, CB-COR-019 |
| Survey database stored in the document, journaled and shareable through Hub | CB-SURV-015 |
| Every object type referenceable across documents, including corridors and points | CB-REF-001, CB-REF-007 |
| Semantic comparison of revisions and element-level multi-user editing | CB-REF-011, CB-REF-012, CB-SEC-014 |
| Styles, criteria and components as text-diffable libraries with headless audits | CB-STY-020, CB-STY-022, CB-AUTO-011 |
| Swept paths linked to design geometry and regenerated with it | CB-VEH-005, CB-VEH-010, CB-INT-016 |
| Haul optimization and grading optimization in the desktop application, offline | CB-QTY-018, CB-GRD-018 |
| Reliable headless operation for batch export, checks and reports | CB-AUTO-004, CB-AUTO-012 |
| Cross-platform, offline, account-free operation | Suite principles |
