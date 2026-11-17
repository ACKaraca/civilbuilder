# Analysis in geospatial context

This area evaluates designs against their surroundings: sight distance, visibility, sun and shadow,
regional hydrology, flood screening, traffic simulation, pedestrian movement, noise screening, profile optimization and
scenario comparison. Results are layers that can be displayed, compared and exported.

## Domain objects

- **Analysis study**: inputs, parameters, the objects analyzed and the model revision used.
- **Result layer**: raster or vector output with legend, tagged with the revision it was computed from.
- **Scenario**: a named parameter set evaluated across design options.
- **Traffic network**: lanes, connectors and movements derived from corridors and intersections.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ANL-001 | 3D sight distance | Stopping and passing sight distance along a corridor lane are computed in 3D against terrain, corridor surfaces, structures and context objects with stated eye and object heights; deficient ranges display colored and list with the obstructing object. | T2 | 4 |
| CB-ANL-002 | Line of sight and viewshed | Lines of sight between points report the first obstruction; viewsheds from one or more observer points produce a visible-area raster over terrain and context. | T2 | 4 |
| CB-ANL-003 | Visual impact | Visibility of proposed objects from a set of viewpoints is computed, including a zone of theoretical visibility raster for a proposed structure. | T3 | 4 |
| CB-ANL-004 | Sun and shadow | Shadows for a date, time and location display in 3D views; shadow-duration maps over a day are computed for an area. | T2 | 4 |
| CB-ANL-005 | Regional raster hydrology | On elevation rasters, depression filling, flow direction, flow accumulation and stream extraction delineate catchments at regional scale. | T2 | 4 |
| CB-ANL-006 | Flood screening | Inundation from a water level and rain-on-grid screening over terrain produce depth and extent rasters at concept level, through the hydraulic engine boundary. | T3 | 5 |
| CB-ANL-007 | Traffic network derivation | Lanes, connectors and turning movements derive automatically from corridors, intersections and roundabouts and update when they change. | T3 | 5 |
| CB-ANL-008 | Traffic simulation | Microscopic simulation on the derived network uses demands (turning volumes or origin-destination matrices), vehicle classes and priority or signal control, and reports travel times, delays, queue lengths and level-of-service measures with animation. | T3 | 5 |
| CB-ANL-009 | Noise screening | Road traffic noise levels are estimated at receiver points and on a grid from traffic volumes, speeds, terrain and barriers using a documented calculation method. | T3 | 5 |
| CB-ANL-010 | Profile optimization | A layout profile is optimized within grade, curvature and control-point constraints to minimize earthwork cost from the mass haul; the result is offered as a new profile for comparison. | T3 | 4 |
| CB-ANL-011 | Design check overlays | Criteria violations from alignments, profiles, superelevation and sight distance display as markers in 3D views. | T2 | 4 |
| CB-ANL-012 | Scenarios and comparison | Scenarios evaluate the same analyses across design options and present the results in one comparison table. | T2 | 4 |
| CB-ANL-013 | Result layers | Results display as layers with legends, are tagged with the revision they were computed from, show stale when inputs change, and export as GeoTIFF or GeoPackage. | T2 | 4 |
| CB-ANL-014 | Pedestrian network derivation | Walkable areas, crossings, stairs, ramps, platforms and obstacles derive from sidewalks, corridors, intersections, structures and drawn areas, and update when those objects change. Gaps and unreachable areas are listed. | T3 | 5 |
| CB-ANL-015 | Pedestrian movement simulation | Pedestrian flow on the derived network uses demands (origin-destination matrices or entry rates over time), walking speed distributions and signal phases, and runs through an open, validated model in a worker process behind an adapter. Results report flows, densities, walking times, queues and waiting areas with animation. | T3 | 5 |
| CB-ANL-016 | Pedestrian comfort and capacity | Density and flow results are classified against stated level-of-service criteria and effective widths, and evacuation or clearing times are computed for a defined set of exits; deficient locations list with the controlling object. | T3 | 5 |
