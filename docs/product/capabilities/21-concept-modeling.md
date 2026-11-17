# Concept infrastructure modeling

This area supports early-stage design in a geospatial context. Concept roads, structures and
drainage are the same objects used in detailed design, created with simplified parameters, so a
concept refines in place without export ([ADR-0006](../../adr/0006-one-model-for-concept-and-detail.md)).

## Domain objects

- **Context layer**: a referenced geospatial source shown in the model (terrain, imagery, buildings, roads, water, land use).
- **Road style**: a concept-level assembly built from standard components.
- **Concept road**: an alignment, profile and corridor created from a sketched centerline and a road style.
- **Terrain modification**: the combined design-over-existing surface of concept objects.
- **Design option**: a named alternative containing alternative objects over shared context.
- **Presentation sequence**: camera keyframes with option, time and caption states.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-CON-001 | Context assembly | A project area is assembled from local files and user-configured open-data services into context layers for terrain, imagery, roads, buildings, water and land use, each refreshable from its source. | T2 | 4 |
| CB-CON-002 | Context buildings | Buildings appear from footprints with height attributes, CityGML or CityJSON models and IFC or glTF models, displayed through rule-based styles. | T2 | 4 |
| CB-CON-003 | Concept roads | The user sketches a centerline over terrain in 3D and picks a road style; the command creates a real alignment, profile, assembly and corridor with defaults from the criteria set. | T2 | 4 |
| CB-CON-004 | Road styles | Road styles define lane configuration, medians, shoulders, sidewalks and side slopes from standard components, are kept in libraries and are user-defined for any region. | T2 | 4 |
| CB-CON-005 | Terrain modification | Concept objects combine with existing terrain into a modified terrain surface with cut and fill volumes, regenerating as objects move. | T2 | 4 |
| CB-CON-006 | Proposed structures | Where a concept road rises above or falls below terrain beyond set thresholds, or crosses mapped water, the application proposes a bridge, tunnel or culvert; the user accepts or dismisses each proposal. | T3 | 4 |
| CB-CON-007 | Live propagation | Moving a concept road updates its intersections, structures, terrain modification and quantities in background regeneration. | T2 | 4 |
| CB-CON-008 | Concept intersections | Crossing concept roads create intersections automatically within an elevation tolerance and leave grade-separated crossings when the difference exceeds it. | T2 | 4 |
| CB-CON-009 | Concept bridges and drainage | Bridges with span, girder type and pier parameters, culverts at crossings and simple drainage networks are placed at concept level of detail using the same objects as detailed design. | T2 | 4 |
| CB-CON-010 | Concept rail | Concept rail lines use track alignments and a track style. | T3 | 5 |
| CB-CON-011 | Design options | Named options share context and hold alternative objects; the user switches the active option and compares options by length, volumes, structures and cost side by side. | T2 | 4 |
| CB-CON-012 | Concept quantities and costs | Quick volumes, areas, lengths and structure counts multiply by unit cost tables per option. | T2 | 4 |
| CB-CON-013 | Refinement in place | Concept objects refine into detailed design by editing their assemblies, criteria and parameters; no export or re-creation is involved and the object identifiers stay the same. | T2 | 4 |
| CB-CON-014 | Assets along roads | Street furniture, lighting and vegetation from a glTF asset library are placed along roads by spacing rules and update when the road moves. | T3 | 4 |
| CB-CON-015 | Real-time visualization | 3D views show sun and sky by date and time, shadows and draped imagery; photoreal frames come from RenderBuilder through the Arc Scene. | T2 | 4 |
| CB-CON-016 | Presentation sequences | Camera keyframes with option, time-of-day and caption states play in the viewport and export as video or stills through viewport capture or RenderBuilder. | T3 | 4 |
| CB-CON-017 | Navigation modes | Views orbit, walk, fly and drive along a corridor lane at a set speed. | T2 | 4 |
| CB-CON-018 | 3D annotation and bookmarks | Measurements, notes and camera bookmarks are placed in 3D views and saved with the document. | T2 | 4 |
