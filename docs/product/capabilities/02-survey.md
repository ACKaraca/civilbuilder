# Survey

This area turns field measurements into coordinated points and linework. It covers points, point
groups, description keys, the survey database, field data import, raw observation reduction, figures, networks, traverse and
least-squares adjustment, and stakeout output.

## Domain objects

- **Point**: a numbered position with elevation, descriptions, lock state and user properties.
- **Point group**: a rule-defined, automatically maintained set of points.
- **Description key set**: ordered rules that turn raw field descriptions into display and properties.
- **Survey database**: networks, observations, figures, equipment and settings stored inside the document.
- **Survey network**: control points, setups, directions and observations, adjusted as one system.
- **Figure**: survey linework built from coded points, optionally used as a breakline.
- **Linework code set** and **figure prefix rule**: the configuration that builds and classifies figures.
- **Equipment profile**: instrument precision used to weight observations.

## Points

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURV-001 | Point object | A point has a number unique in the document, an optional name, northing, easting, optional elevation, raw and full description, a lock flag and user properties. Point storage is designed for millions of points per document without loss of interactive selection. | T1 | 3 |
| CB-SURV-002 | Point creation | Points are created at picked locations, at station and offset of an alignment, at intersections (bearing-bearing, distance-distance, bearing-distance), along an object by interval or division, at object vertices, at surface elevation, and by slope, grade and distance from another point. Numbering uses the next free number or a given start, with a collision policy. | T1 | 3 |
| CB-SURV-003 | Point import | Delimited text imports through format definitions (column order, separators, skipped columns, header lines, units, CRS). The duplicate-number policy (skip, renumber, merge, overwrite) is chosen per import; malformed rows are reported by line number without aborting the import. | T1 | 3 |
| CB-SURV-004 | Point export | Points export through the same format definitions, filtered by group or selection, in the document CRS or another CRS, as grid or ground coordinates. | T1 | 3 |
| CB-SURV-005 | Tabular point editing | A table synchronized with viewport selection sorts, filters and edits points, including multi-row edits. Locked points refuse edits and the refusal is reported per point. | T1 | 3 |
| CB-SURV-006 | Point transformations and renumbering | Selected points are translated, rotated and scaled, elevations are shifted by a delta, and numbers are renumbered by offset or sequence with collision checks. | T1 | 3 |
| CB-SURV-007 | Point groups | Membership is defined by include and exclude rules: number ranges, names, raw description patterns with wildcards, elevation ranges, explicit lists, other groups, a spatial boundary and property queries. Membership re-evaluates automatically when points change, and groups have a draw order. | T1 | 3 |
| CB-SURV-008 | Group display overrides | A group can override point style and label style for its members; when a point belongs to several groups, group priority resolves the override. Overrides never modify the points. | T1 | 3 |
| CB-SURV-009 | Description keys | Ordered rule sets match raw descriptions by pattern and parameters and assign point style, label style, layer, symbol scale, rotation from a parameter and the full-description format. Rules apply on creation and import and can be reapplied on demand; several sets combine by precedence. | T1 | 3 |
| CB-SURV-010 | User-defined point properties | Typed property classifications (text, integer, real, enumeration, length, angle) attach to points, edit in the table, and are available in labels, point group rules and exports. | T2 | 3 |
| CB-SURV-011 | Elevations from surface | Point elevations are assigned from a surface once, or linked so that the points follow later surface changes. The command reports every changed point. | T1 | 3 |
| CB-SURV-012 | Geodetic point coordinates | Points show and accept latitude, longitude and ellipsoidal height, converted through the document CRS and its recorded transformation. | T2 | 3 |
| CB-SURV-013 | Point reports | Reports list points, inverses between points and station and offset to an alignment, output as CSV, PDF or HTML from report templates (CB-AUTO-009). | T1 | 3 |
| CB-SURV-014 | Point copy between documents | Points copy between documents with a number-collision policy, and the copies record the source document and point identifiers. | T2 | 3 |

## Survey database and field data

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURV-015 | Survey database in the document | Networks, observations, figures, equipment and settings are stored in the document package, so they are saved atomically, journaled and undoable like any other model data. Through Arc Hub the survey database follows the document locking and versioning rules. | T1 | 3 |
| CB-SURV-016 | Survey settings | Settings define units, angle conventions, tolerances, default standard errors, curvature and refraction, sea-level and grid scale corrections, and point naming. Changing a setting marks computed coordinates stale until recomputed. | T1 | 3 |
| CB-SURV-017 | Equipment profiles | Profiles store instrument precision (angle, distance constant and ppm, centering, target and instrument height errors) and are referenced by setups to weight observations. | T2 | 4 |
| CB-SURV-018 | Field book import | An openly documented field book text format with commands for setups, backsights, sideshots, traverses, curves, offsets and line begin and end imports into a network. Errors are reported by line with the computation that failed. | T1 | 3 |
| CB-SURV-019 | Structured survey import | LandXML survey data imports into networks with observations and points. Raw instrument observation files import through CB-SURV-033 and CB-SURV-035; formats without a published specification import through format plug-ins (CB-AUTO-008). | T1 | 3 |
| CB-SURV-020 | Raw observations | Observations are kept as measured (directions, distances, height differences, instrument and target heights) separately from computed coordinates, and coordinates recompute from them when settings or control change. | T1 | 3 |
| CB-SURV-021 | Survey networks | A network holds control points (fixed or weighted), setups, directions and observations. A network view shows the observation graph and reports disconnected parts and points without redundancy. | T1 | 4 |
| CB-SURV-022 | Traverse closure and balancing | Traverses report angular and linear misclosure and precision ratio, and balance by compass rule, transit rule, Crandall method or least squares. The user previews the balanced result before accepting it. | T1 | 4 |
| CB-SURV-023 | Least-squares adjustment | Networks adjust in 1D, 2D or 3D with weights from equipment profiles. Results include adjusted coordinates, residuals, standardized residuals, error ellipses, the a-posteriori variance factor with a chi-square test, and flagged likely blunders. | T2 | 4 |
| CB-SURV-024 | Leveling runs | Differential leveling runs import or are entered as observations, report misclosure and adjust together with the vertical network. | T2 | 4 |
| CB-SURV-025 | Accepting adjusted coordinates | A command writes adjusted coordinates to the points; the previous values remain in history and the points keep their link to the observations they came from. | T1 | 4 |
| CB-SURV-026 | Survey-to-design transformation | Survey data transforms to the design grid by entered parameters or by fitting control point pairs, with residuals reported before acceptance. | T2 | 3 |

## Figures and linework

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURV-027 | Figures | A figure is 3D linework with a name, style, closed flag and breakline flag, whose vertices take elevations from their points. Figures edit with survey-aware commands and convert to feature lines (CB-GRD-002). | T1 | 3 |
| CB-SURV-028 | Linework code sets | A configurable code set (begin, end, close, curve start and end, rectangle, offset, join to point) parses raw descriptions into figures automatically. A preview shows the parsed figures and marks ambiguous or unmatched codes before commit. | T1 | 3 |
| CB-SURV-029 | Figure prefix rules | Rules map figure name prefixes to style, layer, breakline flag and inclusion in surface definitions. | T1 | 3 |
| CB-SURV-030 | Survey queries | Queries filter observations, points and figures by property and location, and their results insert into the model or a point group. | T2 | 4 |
| CB-SURV-031 | Coordinate geometry entry | Bearings, distances and curves are entered as a traverse to create boundary linework or parcels (CB-PCL-002); closure is reported before the geometry is created. | T1 | 3 |
| CB-SURV-032 | Stakeout output | Stakeout lists are generated from points, from alignments at station and offset, and from corridors as slope stakes (CB-COR-019), and export as LandXML or CSV. | T2 | 4 |

## Raw observation files and reduction

Files from total stations and GNSS receivers are read when their format is open or published.
Formats without a published specification stay with format plug-ins (CB-AUTO-008). Controlling
instruments and running field controller software are outside the product.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SURV-033 | Total-station observation import | Observation files in open or published total-station formats import into a network as setups, backsights, directions, distances, zenith angles, instrument and target heights and codes, preserving face-left and face-right pairs and repeated rounds. Unreadable records are reported by line and the original file is kept. | T3 | 5 |
| CB-SURV-034 | Observation reduction | Raw observations reduce to horizontal directions and distances: face and round averaging with spread checks, slope to horizontal and height difference, curvature and refraction, atmospheric, sea-level and grid scale corrections from the survey settings (CB-SURV-016). Each reduced value links to the raw observations behind it, and observations outside the tolerance are listed for review. | T3 | 5 |
| CB-SURV-035 | GNSS observation import | Receiver-independent observation and navigation files (RINEX) and published precise orbit and clock products import with their time span, site, antenna and receiver metadata. Unsupported versions or constellations are reported before use. | T3 | 5 |
| CB-SURV-036 | GNSS baseline processing | Static and rapid-static sessions between stations reduce to baseline vectors with covariance, with the processing options, ambiguity status and quality statistics stored; sessions that fail quality thresholds are flagged, not discarded. | T3 | 5 |
| CB-SURV-037 | GNSS vectors in adjustment | Baseline vectors enter the network as observations next to terrestrial ones (CB-SURV-023), weighted by their covariance, with the transformation from the receiver reference frame to the document CRS recorded and its residuals reported. | T3 | 5 |
| CB-SURV-038 | Raw data review and reporting | A review view shows each file, setup and session with accepted, rejected and edited observations and the reason; edits are recorded without altering the raw values, and a report lists the files used, the corrections applied and the quality statistics. | T3 | 5 |
