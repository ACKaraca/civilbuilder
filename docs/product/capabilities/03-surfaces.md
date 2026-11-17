# Surfaces

This area models terrain and design surfaces: their definition from points, breaklines, boundaries,
rasters and point clouds; their editing as an ordered, replayable list of operations; terrain analysis;
and surface-to-surface volumes.

## Domain objects

- **Surface**: kind TIN, grid, TIN volume, grid volume, composite, or sourced from a corridor or grading set.
- **Definition item**: one input to a surface (point group, breakline set, boundary, contour set, raster, point cloud region, drawing geometry).
- **Edit operation**: a recorded change to the triangulation (add line, swap edge, smooth, simplify).
- **Boundary**: outer, hide, show or data clip polygon.
- **Snapshot**: a frozen triangulation kept alongside the definition.
- **Analysis set**: elevation, slope, aspect, watershed or contour ranges with display colors.
- **Volume comparison**: base surface, comparison surface, boundaries and factors with results.

## Surface kinds

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURF-001 | TIN surface | A constrained Delaunay triangulation is built from the definition items, honoring breaklines and boundaries, with optional maximum edge length and maximum angle exclusion. Elevation, slope and normal are queryable at any planar location; locations outside the surface return no value rather than an extrapolation. | T1 | 3 |
| CB-SURF-002 | Grid surface | A regular grid with spacing, origin and rotation is created from an elevation raster or resampled from another surface. Cells without data are kept as no-data, and elevation queries interpolate bilinearly or bicubically by setting. | T1 | 3 |
| CB-SURF-003 | Volume surfaces | A TIN volume surface is the difference of a comparison and a base surface over their merged triangulation; a grid volume surface does the same on a grid. Both regenerate when either input changes. | T1 | 3 |
| CB-SURF-004 | Composite surfaces | A composite surface pastes surfaces in priority order (for example design over existing ground), optionally inside boundaries, and regenerates when any input changes. | T1 | 3 |
| CB-SURF-005 | Surfaces from design objects | Corridor surfaces (CB-COR-012) and grading set surfaces (CB-GRD-011) are surfaces whose definition items come from those objects, so every surface command, analysis and volume works on them unchanged. | T1 | 3 |
| CB-SURF-006 | Very large surfaces | Surfaces above 100 million points are stored as tiles with level-of-detail display; edits rebuild only the affected tiles. | T3 | 4 |

## Definition

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURF-007 | Point definition data | Points, point groups (dynamic), point files and LandXML points add as definition items, with optional weeding by minimum spacing and duplicate-point resolution. | T1 | 3 |
| CB-SURF-008 | Breaklines | Breaklines are standard, proximity (snap to existing points), wall (two-sided with top and bottom offset) or non-destructive (adds crossing points without forcing edges). Sources are polylines, feature lines, figures and 3D polylines; arcs tessellate by mid-ordinate distance; weeding and supplementing factors apply. | T1 | 3 |
| CB-SURF-009 | Boundaries | Outer, hide, show and data clip boundaries come from closed linework. A non-destructive option clips triangles exactly at the boundary instead of dropping the triangles it crosses. | T1 | 3 |
| CB-SURF-010 | Contours as definition data | Contour linework adds with weeding and supplementing, followed by automatic removal of flat triangles between equal contours (CB-SURF-021). | T1 | 3 |
| CB-SURF-011 | Elevation rasters as definition data | Elevation rasters add with clip region, resampling interval, CRS transformation and no-data handling, either as a grid surface or as points into a TIN. | T1 | 3 |
| CB-SURF-012 | Point cloud definition data | A point cloud region adds with classification filter, thinning method and outlier removal (CB-REAL-005); the item regenerates when the filter changes. | T1 | 4 |
| CB-SURF-013 | Imported drawing geometry | 3D faces, meshes, points, lines and block insertion points from imported DWG or DXF content add as definition items. | T2 | 3 |
| CB-SURF-014 | Ordered operations list | Definition items and edits form one ordered list; each entry can be disabled, reordered or removed and the surface rebuilds by replaying the list. The same list always produces the same triangulation. | T1 | 3 |
| CB-SURF-015 | Surface rebuild policy | Each surface rebuilds automatically or on demand, and shows a stale state while its inputs have changed since the last build. A locked surface rejects definition changes. | T1 | 3 |
| CB-SURF-016 | Surface snapshots | A snapshot freezes the current triangulation while keeping the definition, so downstream objects use the frozen state until the snapshot is released or refreshed. Snapshots also record a state such as pre-construction ground. | T2 | 3 |

## Editing

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURF-017 | Triangulation edits | Add line, delete line, swap edge, add, delete, move and modify point, and delete triangles inside a polygon are recorded as operations in the list. | T1 | 3 |
| CB-SURF-018 | Smoothing | Natural neighbor interpolation or kriging resamples a region onto a grid or onto chosen points and adds the result as an operation. | T2 | 3 |
| CB-SURF-019 | Simplification | Point count reduces by edge contraction or point removal inside a region, bounded by a maximum vertical change and a target percentage, with the achieved error reported. | T2 | 3 |
| CB-SURF-020 | Raise, lower and flatten | A whole surface or a region is shifted vertically or flattened to an elevation as a recorded operation. | T1 | 3 |
| CB-SURF-021 | Flat-area removal | Edge swaps and inserted points remove flat triangles that occur between equal-elevation contours. | T2 | 3 |
| CB-SURF-022 | Surface integrity check | A check reports crossing breaklines, coincident points with different elevations, spikes detected as statistical outliers and slivers, each with a locate action. | T2 | 3 |

## Analysis and display

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURF-023 | Elevation analysis | Elevation ranges defined by count, interval or quantile display with a color scheme; a legend table lists range limits and area. | T1 | 3 |
| CB-SURF-024 | Slope and aspect analysis | Slope ranges and aspect directions display with colors and arrows; the legend lists area per range. | T1 | 3 |
| CB-SURF-025 | Contours | Major and minor contours with interval, base elevation and user contours display through the surface style; smoothing applies to display only and never alters the surface. | T1 | 3 |
| CB-SURF-026 | Surface labels | Contour labels along or at intervals, spot elevations and slope labels attach to the surface and update when it changes. | T1 | 3 |
| CB-SURF-027 | Watershed analysis | Drainage basins, depressions, flat areas and outlets are delineated on the surface with minimum depth and minimum area merge rules. Basins convert to catchments (CB-HYD-001). | T2 | 4 |
| CB-SURF-028 | Flow path tracing | From picked points, the steepest-descent path across the surface is traced to its end point and output as linework with length and fall. | T2 | 3 |
| CB-SURF-029 | Surface statistics | Planar and sloped area, minimum, maximum and mean elevation, mean slope, point and triangle counts and extents are reported and available to labels and queries. | T1 | 3 |
| CB-SURF-030 | Quick profile and section | A temporary profile or section samples the surface along picked linework without creating persistent objects. | T1 | 3 |
| CB-SURF-031 | 3D display | Surfaces display shaded, hillshaded or with draped imagery in 3D, and export to the Arc Scene for rendering. | T1 | 3 |
| CB-SURF-032 | Geometry extraction | Contours, triangles, border and grid points extract as drafting entities or GIS features, as static copies. | T1 | 3 |

## Volumes

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURF-033 | Surface-to-surface volume | Cut, fill and net volume between two surfaces are computed exactly on the merged triangulation, optionally inside boundaries, with cut and fill factors. The result regenerates when either surface changes. | T1 | 3 |
| CB-SURF-034 | Volume table | A table of comparison rows (base, comparison, boundary, factors) recomputes on change and exports as CSV; each row links to its volume surface. | T1 | 3 |
| CB-SURF-035 | Bounded volumes | Several closed boundaries each receive their own volume result and table row from one comparison. | T1 | 3 |
| CB-SURF-036 | Cut and fill map | A volume surface displays as a color-coded depth map with a legend of depth ranges and areas. | T1 | 3 |
| CB-SURF-037 | Volume against a datum | Volume between a surface and a horizontal or sloped plane inside a boundary is computed for stockpiles, ponds and excavations. | T1 | 3 |
