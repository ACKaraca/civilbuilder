# Intersections and roundabouts

This area designs at-grade junctions as parametric objects that generate alignments, profiles and
corridor regions, and keeps them consistent when the legs change.

## Domain objects

- **Intersection**: legs, crown rule, corners with curb returns, turn lanes and generated corridor regions.
- **Leg**: an alignment and profile approaching the intersection, with offsets.
- **Curb return**: a connector alignment and profile at a corner.
- **Turn lane**: a widening with taper and storage length on a leg.
- **Roundabout**: central island, apron, circulatory roadway, entries, exits and splitter islands.
- **Geometric check result**: computed paths, angles and radii compared with a criteria set.

## Intersections

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-INT-001 | Intersection object | An intersection is created from two or more alignments that cross or meet (T, four-leg, skewed, multi-leg). It is parametric: when a leg alignment or profile changes, the generated geometry regenerates. | T2 | 4 |
| CB-INT-002 | Crown rules | The intersection maintains the primary road crown, all crowns, or a planar surface; secondary profiles adjust to meet the primary road edges. | T2 | 4 |
| CB-INT-003 | Curb returns | Each corner gets a simple radius, three-centered compound curve or radius with taper, generated as connector alignments (CB-ALN-014) with profiles. | T2 | 4 |
| CB-INT-004 | Curb return profiles | Corner profiles follow vertical rules (maximum grade, maximum grade change, tie to edge elevations). Manually edited profile points are kept on regeneration or reported if they can no longer apply. | T2 | 4 |
| CB-INT-005 | Turn lanes and slip lanes | Left and right turn lanes and slip lanes with taper and storage length generate as widenings on leg offsets. | T2 | 4 |
| CB-INT-006 | Generated corridor regions | The intersection creates corridor regions and target mappings for legs and corners using chosen assemblies, and updates them when parameters change. | T2 | 4 |
| CB-INT-007 | Intersection editing | Parameters edit in properties and by grips; generated objects edited by hand are marked as modified and either preserved or listed on regeneration. | T2 | 4 |
| CB-INT-008 | Sight triangles | Intersection sight triangles are computed per approach from design speed and geometry and checked against surfaces and objects for obstructions (CB-ANL-001). | T2 | 4 |
| CB-INT-009 | Ramps | A ramp alignment and profile generate from a gore location, taper and offset to a mainline, using offset baselines. | T3 | 4 |
| CB-INT-010 | Intersection reports | Reports list leg, corner and turn-lane geometry and check results. | T2 | 4 |

## Roundabouts

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-INT-011 | Roundabout object | A roundabout is defined by inscribed diameter, central island, truck apron, circulatory lane count and width, and per-leg entry and exit radii, widths and flare lengths. It generates alignments, profiles and island geometry and regenerates when legs move. | T2 | 4 |
| CB-INT-012 | Lane arrangements | Each entry and exit has a lane count, bypass lanes and lane assignment; circulatory lanes and markings follow the arrangement. | T3 | 4 |
| CB-INT-013 | Splitter islands | Splitter islands generate per leg from entry and exit geometry with nose offsets and lengths. | T2 | 4 |
| CB-INT-014 | Roundabout vertical design | The circulatory roadway takes an outward or inward cross slope and a profile; entry and exit profiles tie to leg profiles. | T2 | 4 |
| CB-INT-015 | Geometric checks | Fastest paths through each entry, circulation and exit are computed with their radii, together with deflection, entry angle and visibility, and compared with a criteria set; violations are marked. | T2 | 4 |
| CB-INT-016 | Movement swept-path checks | Swept paths for chosen design vehicles run for every movement (CB-VEH-005) and regenerate when the geometry changes; conflicts with curbs and islands are listed. | T2 | 4 |
| CB-INT-017 | Roundabout corridor generation | Corridor regions generate for circulatory roadway, apron and islands with their assemblies. | T2 | 4 |
