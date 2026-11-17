# Alignments

This area defines horizontal geometry measured by station: the elements of an alignment and their
constraints, stationing and station equations, offset alignments and widenings, design criteria with
live checks, and superelevation.

## Domain objects

- **Alignment**: kind centerline, offset, connector (curb return), rail or miscellaneous; an ordered chain of elements with stationing.
- **Element**: line, circular arc or spiral, with a constraint state of fixed, floating or free.
- **Station equation**: back and ahead station pair with direction.
- **Widening**: a station range with an offset change and entry and exit transitions.
- **Design criteria set**: tables keyed by design speed plus custom check expressions.
- **Design speed range**: a station range with a design speed.
- **Superelevation set**: per-curve transition regions and critical stations for each lane and shoulder.

## Geometry

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ALN-001 | Alignment object | An alignment is an ordered chain of lines, circular arcs and spirals with stationing from a start station. Position, direction, curvature and station and offset of any point are queryable; geometry is continuous in position and, where constrained, in direction. | T1 | 3 |
| CB-ALN-002 | Element constraints | Each element is fixed (fully specified), floating (tangent to one neighbor) or free (tangent to both neighbors). Editing one element re-solves its dependent neighbors; an edit that cannot be satisfied is rejected with a message and the alignment is unchanged. | T1 | 3 |
| CB-ALN-003 | Layout by points of intersection | Tangents are drawn through points of intersection, with arcs and optional entry and exit spirals inserted automatically from default radius and spiral lengths. Points of intersection are inserted, deleted and moved afterwards. | T1 | 3 |
| CB-ALN-004 | Element layout tools | Fixed lines by two points or bearing and length; fixed arcs by three points, by center and radius, or tangent to an element; floating arcs through a point or by radius or length; free arcs between two elements by radius or through a point; free spiral-arc-spiral, reverse and compound groups; spiral-spiral transitions. | T1 | 3 |
| CB-ALN-005 | Spiral types | Clothoid, cubic parabola, Bloss, sinusoidal, cosine half-wave and biquadratic spirals are supported, defined by length or parameter, including incomplete spirals between two radii. | T1 | 3 |
| CB-ALN-006 | Best-fit geometry | Lines, arcs or a complete alignment fit to points or linework by least squares; the result reports residuals and maximum deviation against a tolerance before it is accepted. | T2 | 3 |
| CB-ALN-007 | Alignments from objects | Alignments are created from polylines, lines and arcs, feature lines, 3D polylines, corridor feature lines, gravity network runs and imported LandXML or IFC alignments, with optional spiral insertion at arc ends. | T1 | 3 |
| CB-ALN-008 | Alignment editing | Grips edit points of intersection, element ends, radii and pass-through points while honoring constraints; a parameter grid edits every element value; commands reverse direction, split, join, trim, extend and change constraint states. | T1 | 3 |
| CB-ALN-009 | Station control and equations | The start station references a chosen point; station equations define back and ahead stations, increasing or decreasing. Internal distance and displayed station are kept separately and every label, view and report shows displayed stations. | T1 | 3 |
| CB-ALN-010 | Geometry points and queries | The alignment lists its geometry points (start, end, arc and spiral ends, points of intersection) with station and coordinates, and answers station-at-point, point-at-station-offset and nearest-station queries for commands and automation. | T1 | 3 |
| CB-ALN-011 | Alignment kinds and topology | The kind sets defaults for styles and checks. An alignment placed in a layout site takes part in parcel topology (CB-PCL-003); a siteless alignment does not. | T1 | 3 |

## Offsets and widenings

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ALN-012 | Offset alignments | An offset alignment follows its parent at a constant offset over a station range and regenerates when the parent changes. | T1 | 3 |
| CB-ALN-013 | Widenings | A widening changes the offset over a station range with entry and exit transitions (linear, reverse arc, parabolic or ratio taper) of given length, on either side. Widenings edit by grips and in a table. | T1 | 3 |
| CB-ALN-014 | Connector alignments | A connector alignment joins offsets of two alignments with a simple radius or a three-centered compound curve and regenerates when either parent changes; intersections use it for curb returns (CB-INT-003). | T1 | 3 |

## Design criteria

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ALN-015 | Design criteria sets | A criteria set holds tables keyed by design speed (minimum radius by superelevation rate, minimum tangent, spiral and arc lengths, reverse and compound curve limits, vertical curvature and sight distance values) in an open text format. Sets are user-authored or loaded from libraries; the application ships only example sets clearly marked as examples. | T1 | 3 |
| CB-ALN-016 | Design speeds by station | Design speeds are assigned to station ranges and drive criteria lookup for alignments, profiles and superelevation. | T1 | 3 |
| CB-ALN-017 | Live design checks | Every element is evaluated against the criteria set whenever it changes. Violations appear as markers in plan views, as flagged cells in the parameter grid and in a checks panel with navigation; checks never block editing. | T1 | 3 |
| CB-ALN-018 | Custom checks | Users define checks as boolean expressions over element properties (radius, length, speed, deflection) in the shared expression language; custom checks appear with built-in ones. | T2 | 3 |

## Superelevation

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ALN-019 | Superelevation calculation | Each curve receives a superelevation rate from the criteria table for its speed and radius, runoff and runout lengths from the selected attainment method, and the share of runoff placed on the tangent. Undivided and divided cross-section types and axes of rotation (centerline, inside edge, outside edge, median edges) are supported. | T1 | 3 |
| CB-ALN-020 | Critical station editing | Critical stations (end of normal crown, level crown, reverse crown, full superelevation) edit per side, lane and shoulder in a table and by grips. Manually edited values are flagged and kept when the set recalculates. | T1 | 3 |
| CB-ALN-021 | Superelevation diagram | A diagram plots cross slope against station for every lane and shoulder, supports grip editing, and can be placed in the model and on sheets. | T1 | 3 |
| CB-ALN-022 | Overlapping transitions | When transitions of adjacent curves overlap, a selected rule (merge, shorten, flag) resolves them and the result lists every resolved overlap. | T2 | 3 |
| CB-ALN-023 | Shoulder and lane rules | Shoulder rollover limits, lane-specific rates and breakover limits are part of the set and are read by cross-section components (CB-ASM-005). | T2 | 3 |
| CB-ALN-024 | Superelevation reports and exchange | Superelevation reports list critical stations and rates; superelevation imports and exports with LandXML and IFC alignments. | T2 | 3 |

## Reports

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ALN-025 | Geometry reports | Reports list elements with stations, bearings, lengths, radii and spiral parameters, station and offset of selected points, and stakeout coordinates at an interval. | T1 | 3 |
| CB-ALN-026 | Alignment annotation | Major and minor station labels, geometry point labels, station equation labels, design speed labels and segment tables apply through label sets (CB-STY-011) and update with the geometry. | T1 | 3 |
