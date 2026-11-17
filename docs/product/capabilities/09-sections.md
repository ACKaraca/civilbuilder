# Sample lines and sections

This area cuts the model across an alignment: sample lines, sections sampled from surfaces,
corridors, networks and solids, and section views arranged for sheets.

## Domain objects

- **Sample line set**: sample lines along one alignment with their sources.
- **Sample line**: station, left and right swath widths, angle and optional vertices.
- **Section source**: a surface, corridor, network or solid sampled by the set, with its update mode.
- **Section**: the computed cut of one source by one sample line (derived).
- **Section view**: a graph of the sections of one sample line.
- **Section arrangement**: the placement of section views on sheet-sized pages.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-SEC-001 | Sample line sets | Sample lines are created along an alignment by station range and increment, at horizontal and vertical geometry points, at superelevation critical stations, at corridor stations, from a station list or by picking. | T1 | 3 |
| CB-SEC-002 | Sample line geometry | Each line has left and right swath widths; lines may be skewed or have intermediate vertices. Lines edit by grips and in a table. | T1 | 3 |
| CB-SEC-003 | Section sources | A set samples surfaces, corridor links and shapes, gravity and pressure networks and solids; each source has a style and an update mode (linked or static). | T1 | 3 |
| CB-SEC-004 | Sections | Sections are computed per source and sample line with codes preserved, and regenerate when a source changes, only at the affected sample lines. | T1 | 3 |
| CB-SEC-005 | Section overrides | Section geometry can be edited for quantity purposes; the edit is recorded as an override and flagged when the underlying source later changes. | T2 | 3 |
| CB-SEC-006 | Section views | A section view shows one sample line with automatic or fixed offset and elevation ranges, grid and scale. | T1 | 3 |
| CB-SEC-007 | Section arrangements | Section views arrange on pages by rows or columns with spacing, ordered by station, sized from a sheet template, and feed section sheets (CB-PLAN-007). | T1 | 3 |
| CB-SEC-008 | Section bands | Offset, elevation and cut or fill bands display along section views. | T2 | 3 |
| CB-SEC-009 | Section labels | Offset, elevation, grade break, link slope, code and catch-point labels apply through label styles and update with the sections. | T1 | 3 |
| CB-SEC-010 | Projected objects in sections | Points, feature lines, solids and network parts project into section views and stay linked. | T2 | 3 |
| CB-SEC-011 | Network parts in sections | Pipes cut by sample lines display with their true cut shape for the skew angle, and structures display as cut outlines. | T2 | 5 |
| CB-SEC-012 | Section data export | Station, offset and elevation data export as reports, CSV and LandXML cross sections. | T1 | 3 |
| CB-SEC-013 | Static section capture | A set's sections can be frozen at the current revision as a record, independent of later model changes. | T2 | 3 |
| CB-SEC-014 | Section comparison | Sections of two document revisions are compared per sample line and differences are highlighted with area changes. | T3 | 4 |
