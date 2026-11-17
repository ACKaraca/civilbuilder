# Vehicle swept paths and parking

This area checks how vehicles move through designs and lays out parking. Swept paths are model
objects linked to their guide geometry, so they regenerate when the design changes. Roundabout
geometry is defined in [intersections and roundabouts](08-intersections.md).

## Domain objects

- **Vehicle definition**: units (body, tractor, semitrailer, trailer, dolly), axles, articulation, steering and outline.
- **Vehicle library**: a collection of vehicle definitions in an open file format.
- **Swept path**: a vehicle, a guide or driven path, speed and direction, with computed envelopes.
- **Turning template**: a standard turn of a vehicle at a radius and angle.
- **Parking standard**: bay and aisle dimensions by angle and bay type.
- **Parking row** and **parking area**: generated bays, aisles and islands.

## Vehicles

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-VEH-001 | Vehicle definitions | A vehicle is defined by its units with length, width, front and rear overhang, wheelbase, track width, axle groups, articulation points and maximum articulation angles, steering lock angle, lock-to-lock time, body outline and wheels, plus ground clearance geometry for vertical checks. | T2 | 4 |
| CB-VEH-002 | Vehicle libraries | Vehicles are stored in an open library format. The application ships generic design vehicle archetypes; users build, import and export their own libraries. | T2 | 4 |
| CB-VEH-003 | Vehicle editor | The editor edits vehicles parametrically with a preview and validates physical feasibility (positive dimensions, reachable steering, consistent articulation). | T2 | 4 |
| CB-VEH-004 | Rail and special vehicles | Bogie rail vehicles provide kinematic envelopes for rail checks (CB-RAIL-011); aircraft definitions support ground maneuvering checks (CB-VEH-024). | T3 | 5 |

## Swept paths

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-VEH-005 | Path along guide geometry | A vehicle follows a polyline, alignment, feature line or corridor lane; steering is computed by a low-speed kinematic model limited by steering lock and steering rate, and the path stays linked to its guide. | T2 | 4 |
| CB-VEH-006 | Interactive driving | The user drives a vehicle with the pointer forward and in reverse, with straight, arc and fixed-radius segments; segments remain editable afterwards. | T2 | 4 |
| CB-VEH-007 | Speed-dependent steering | At a given speed, steering is limited by lateral acceleration and side friction, and the path reports where the limit applies. | T2 | 4 |
| CB-VEH-008 | Reverse maneuvers | Reverse segments respect articulation limits and warn where a jackknife condition is reached. | T2 | 4 |
| CB-VEH-009 | Envelopes and outputs | Results include body outer and inner envelopes, wheel paths per axle, overhang swing and a clearance buffer, with vehicle positions at intervals, displayed through styles and exportable as drafting entities. | T2 | 4 |
| CB-VEH-010 | Linked regeneration | When the guide geometry or the vehicle changes, the swept path regenerates and its conflicts re-evaluate. | T2 | 4 |
| CB-VEH-011 | Conflict detection | Envelopes are tested against curbs and edges (corridor feature lines), obstacles and other envelopes; conflicts show as markers and list with location and overlap. | T2 | 4 |
| CB-VEH-012 | Automatic paths | A path is planned automatically between a start and an end pose under vehicle constraints, and reports when no feasible path exists. | T3 | 4 |
| CB-VEH-013 | 3D and vertical clearance | Paths over surfaces and corridors compute ground strike (breakover, approach and departure angles) and overhead clearance to structures. | T2 | 4 |
| CB-VEH-014 | Turning templates | Templates for standard turns (for example 90 and 180 degrees at a radius) generate for quick junction checks. | T2 | 4 |
| CB-VEH-015 | Multiple vehicles | Several vehicles and opposing movements are analyzed together and checked against each other. | T2 | 4 |
| CB-VEH-016 | Path reports | Reports list vehicle parameters and path data (steering angle and articulation against distance). | T2 | 4 |
| CB-VEH-017 | Path animation and labels | Vehicles animate along paths in 2D and 3D views; vehicle and path labels apply through styles. | T2 | 4 |

## Parking and loading

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-VEH-018 | Parking standards | Standards define bay dimensions by angle (parallel, 30, 45, 60, 90 degrees), one-way and two-way aisle widths, and accessible and other special bay types; standards are user-defined. | T2 | 4 |
| CB-VEH-019 | Parking rows | Bays generate along a line, polyline or offset by angle, side and standard, with end islands and counts, and regenerate when the edge geometry changes. | T2 | 4 |
| CB-VEH-020 | Parking area layout | A polygon fills with rows and aisles for a chosen orientation and access points; alternative layouts compare by bay count. | T3 | 4 |
| CB-VEH-021 | Parking numbering and tables | Bays number automatically; tables count bays by type and area. | T2 | 4 |
| CB-VEH-022 | Aisle and ramp checks | Swept paths verify aisles and bays for a design vehicle; ramp grades and transitions are checked for vehicle ground clearance. | T2 | 4 |
| CB-VEH-023 | Loading bays | Templates place loading bays and docks with reverse-in swept path checks. | T2 | 4 |
| CB-VEH-024 | Aircraft ground maneuvering | Aircraft paths along taxiways report wingtip clearance and generate taxiway fillet geometry. | T3 | 5 |
