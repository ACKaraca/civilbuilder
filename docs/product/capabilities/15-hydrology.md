# Hydrology and hydraulics

This area computes runoff and the hydraulic behavior of drainage, sewer, channel, culvert, storage
and pressure systems, and two-dimensional unsteady flood flow. Analysis models derive from design objects automatically; solvers run behind
an engine boundary in background processes (see [ADR-0005](../../adr/0005-hydraulic-engine-boundary.md)).

## Domain objects

- **Catchment**: boundary, discharge point, land cover and runoff parameters.
- **Flow path**: longest flow path with segments for time of concentration.
- **Rainfall definition**: intensity-duration-frequency data, design storms and hyetographs.
- **Channel**, **culvert**, **inlet**, **storage** and **outlet structure**.
- **Analysis model**: the solver representation derived from design objects, with an object mapping.
- **Scenario**: a named combination of rainfall, loads, network state and parameters.
- **Result set**: time series and summaries of one scenario run, tagged with the model revision.

## Hydrology

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-HYD-001 | Catchments | Catchments come from watershed analysis (CB-SURF-027) or are drawn, and hold area, slope, runoff coefficient, curve number and impervious fraction, with a discharge point linked to a structure or node. | T1 | 5 |
| CB-HYD-002 | Flow paths and time of concentration | The longest flow path is computed on the surface and split into sheet, shallow concentrated and channel segments, each with a selected method; the time of concentration updates when the surface or catchment changes. | T1 | 5 |
| CB-HYD-003 | Rainfall definitions | Intensity-duration-frequency data (tables or equations), synthetic design storms, user hyetographs and recorded series are stored in a document library. | T1 | 5 |
| CB-HYD-004 | Runoff methods | Runoff computes by rational method, curve number with unit hydrograph, or nonlinear reservoir routing, producing peak flows and hydrographs per catchment. | T1 | 5 |
| CB-HYD-005 | Composite parameters from GIS | Composite runoff coefficients and curve numbers compute by overlaying catchments with soil and land-cover layers through a lookup table. | T2 | 5 |

## Storm and sanitary hydraulics

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-HYD-006 | Derived analysis models | Gravity networks, channels, culverts, storage and catchments translate into an analysis model automatically, with a mapping from every solver element to its design object. A model change marks existing results stale. | T1 | 5 |
| CB-HYD-007 | Storm and sewer routing | Steady, kinematic wave and dynamic wave routing run through a SWMM-class engine in a background process; runs are cancellable and results are tagged with the model revision. | T1 | 5 |
| CB-HYD-008 | Hydraulic and energy grade lines | Steady storm sewer design computes hydraulic and energy grade lines with selectable structure loss methods; both lines display in profile views. | T1 | 5 |
| CB-HYD-009 | Results display | Flows, velocities, depths, surcharge and flooding display color-coded in plan, along profiles (with time animation) and in tables; result sets are kept per scenario. | T1 | 5 |
| CB-HYD-010 | Sanitary loads | Dry-weather flows come from population or unit counts with peaking factors, plus infiltration and inflow allowances. | T2 | 5 |
| CB-HYD-011 | Scenarios | Scenarios combine rainfall, loads, network state and parameters; results of two scenarios compare side by side. | T2 | 5 |
| CB-HYD-012 | Design flows to sizing | Peak design flows from a scenario feed pipe sizing (CB-GRAV-015) and inlet design. | T2 | 5 |

## Channels, culverts, inlets and storage

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-HYD-013 | Channels | A channel runs along an alignment and profile with a trapezoidal, rectangular, triangular, parabolic or assembly-derived section and a lining; normal depth, capacity, velocity and Froude number are computed per reach. | T1 | 5 |
| CB-HYD-014 | Culverts | A culvert has barrels, shape, size, inlet configuration and headwalls; headwater is computed under inlet and outlet control, including roadway overtopping. | T1 | 5 |
| CB-HYD-015 | Inlets and gutter spread | Gutter spread and inlet interception on grade and in sag are computed for road drainage, with bypass flow carried to the next inlet. | T2 | 5 |
| CB-HYD-016 | Storage | Ponds take stage-storage relations from their grading surfaces; underground storage takes chamber geometry and porosity; outlet structures combine orifices, weirs and risers into stage-discharge relations. | T1 | 5 |
| CB-HYD-017 | Detention routing | Level-pool routing checks peak outflow, maximum stage and freeboard against targets for each design storm. | T1 | 5 |

## Pressure hydraulics and exchange

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-HYD-018 | Pressure network analysis | Steady-state and extended-period simulation run through an EPANET-class engine with demands, patterns, pumps, tanks and valves, reporting pressures, flows, velocities and head losses on the design objects. | T2 | 5 |
| CB-HYD-019 | Fire flow analysis | Available fire flow at a residual pressure is computed per hydrant or node. | T2 | 5 |
| CB-HYD-020 | River geometry export | Channel and corridor cross sections with stations, reach lengths and roughness export for external river analysis tools in documented text formats. | T3 | 5 |
| CB-HYD-021 | Hydrology and hydraulics reports | Reports list catchment parameters, hydrographs, network results and storage routing from report templates. | T1 | 5 |

## Two-dimensional unsteady flood modeling

Two-dimensional shallow-water flow over terrain runs through an open, validated solver in a worker
process behind an adapter, on the same boundary as the other engines
([ADR-0005](../../adr/0005-hydraulic-engine-boundary.md)). Concept-level screening stays in
CB-ANL-006.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-HYD-022 | Two-dimensional model domain | A domain is defined by a boundary and a computational mesh derived from surfaces, with refinement regions and breaklines from embankments, roads, walls and channels. Roughness comes from land cover through a lookup table and from objects. Mesh quality is checked and reported before a run. | T3 | 5 |
| CB-HYD-023 | Boundary and source conditions | Inflow hydrographs (CB-HYD-004), stage and rating boundaries, tidal series and rainfall on the domain are assigned per boundary segment and per scenario, with consistency checks on units and time ranges. | T3 | 5 |
| CB-HYD-024 | Unsteady two-dimensional solution | The solver adapter translates the model into the input of an open solver validated on published benchmark cases, runs it in a worker process with progress and cancellation, and imports results tagged with the model revision. A solver fault produces a failed run with its log. | T3 | 5 |
| CB-HYD-025 | Structures in the two-dimensional domain | Culverts (CB-HYD-014), bridge openings, weirs and gates inside the domain are represented as linked structures with their stage-discharge behavior; the object mapping from solver elements back to design objects is kept. | T3 | 5 |
| CB-HYD-026 | Coupling with drainage networks | Nodes of a gravity network (CB-HYD-007) exchange flow with the surface domain at inlets and manholes, so that surcharge appears as surface flooding and surface water enters inlets. Coupling points are mapped objects. | T3 | 5 |
| CB-HYD-027 | Flood results | Depth, velocity, specific discharge, hazard classes and arrival time display as maps and time animations, with maximum envelopes, hydrographs at gauge locations and cross-section flows. Results are result layers (CB-ANL-013), stale when the model changes. | T3 | 5 |
