# Gravity networks

This area designs storm and sanitary gravity systems: pipes and structures from parametric part
catalogs, layout under design rules, editing in plan, profile and section, interference checks,
trenches and quantities. Hydraulic analysis is specified in [hydrology and hydraulics](15-hydrology.md).

## Domain objects

- **Gravity network**: pipes and structures with a connectivity graph, a reference surface and an optional reference alignment.
- **Pipe** and **structure**: part instances with size, material, inverts, rim, sump and status.
- **Part catalog**: parametric part families with size tables and hydraulic properties.
- **Parts list**: the subset of a catalog allowed in a network, with rule assignments.
- **Rule set**: cover, slope, length and drop rules.
- **Interference check**: participating objects, clearance and results.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-GRAV-001 | Gravity network object | A network holds pipes and structures with a connectivity graph, flow direction, a reference surface for rims and an optional reference alignment. Each part has a status (existing, proposed, to be removed). | T1 | 5 |
| CB-GRAV-002 | Part catalogs | Catalogs hold parametric families (circular, elliptical, egg, box and arch pipes; manholes, inlets, junctions, headwalls, outfalls) with size tables, materials, wall thickness, roughness and 3D shape definitions, stored as open text files. | T1 | 5 |
| CB-GRAV-003 | Part family authoring | New parametric families are defined with dimensions, constraints and 3D shapes using the shared constraint and expression engine, and validated before they enter a catalog. | T3 | 5 |
| CB-GRAV-004 | Parts lists | A network uses a parts list that restricts allowed families and sizes and assigns rule sets per part type. | T1 | 5 |
| CB-GRAV-005 | Network layout | Pipes and structures are placed interactively with rules applied during placement, or created from linework, feature lines, alignments, LandXML networks and GIS features. | T1 | 5 |
| CB-GRAV-006 | Design rules | Rules for minimum and maximum cover, minimum and maximum slope, maximum pipe length and structure drop (match crowns, match inverts, fixed drop, maximum drop) are evaluated live; violations are marked on parts and listed. | T1 | 5 |
| CB-GRAV-007 | Network editing | Structures move; inverts, rims and sumps edit; parts swap size or family; pipes connect, disconnect and reroute. An option reapplies rules to dependent parts after each edit. | T1 | 5 |
| CB-GRAV-008 | Rims from surface | Structure rims follow the reference surface dynamically, with a per-structure offset and sump depth. | T1 | 5 |
| CB-GRAV-009 | Profile and section display | Pipes and structures display in profile views and section views with true geometry and edit by grips in profile views. | T1 | 5 |
| CB-GRAV-010 | Network labels and tables | Pipe labels (size, slope, length, inverts, material) and structure labels (name, rim, sump, inverts) and part tables apply through styles. | T1 | 5 |
| CB-GRAV-011 | Interference checks | 3D clearance checks run between gravity networks, pressure networks, solids and corridor solids with a clearance distance. Results are listed with locations and markers and re-evaluate when participating objects change. | T1 | 5 |
| CB-GRAV-012 | Network tracing and validation | Upstream and downstream tracing selects subnetworks; validation reports loops, disconnected parts, adverse slopes and missing outfalls. | T1 | 5 |
| CB-GRAV-013 | Trenches and excavation | Trench geometry comes from bedding, backfill and side slope rules per part, and yields excavation and backfill volumes by station range. | T2 | 5 |
| CB-GRAV-014 | Network quantities | Pipe lengths by size and material, structure counts and trench volumes feed pay items and reports. | T1 | 5 |
| CB-GRAV-015 | Sizing from flows | Given design flows from analysis (CB-HYD-012), pipes are sized against minimum velocity and maximum flow ratio rules; proposed sizes are reviewed and applied through a command. | T2 | 5 |
| CB-GRAV-016 | Existing utilities from GIS | Existing networks import from GIS asset data with attributes through mapping profiles and remain linked for refresh. | T2 | 5 |
