# Bridges and structures

This area models bridges, culverts, retaining walls and tunnels as parametric structures driven by
the linear design, to the level needed for layout, clearances, quantities and handover. Structural
analysis and reinforcement detailing are outside this product (see
[non-goals](../vision.md#non-goals)).

## Domain objects

- **Bridge**: start and end stations on a baseline, span arrangement, deck and supports.
- **Bearing line**: a support location with skew.
- **Deck section**: a cross-section built from components (slab, girders, overhangs, barriers).
- **Girder line**: a girder path with spacing and flare.
- **Pier** and **abutment**: parametric supports with foundations.
- **Culvert structure**, **retaining wall** and **tunnel**.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-BRG-001 | Bridge object | A bridge is defined on a corridor baseline by start and end stations and bearing lines with skew per support. The deck follows the alignment, profile and superelevation and regenerates when any of them change. | T2 | 5 |
| CB-BRG-002 | Deck sections | Deck sections are built from cross-section components (slab, girders, overhangs, barriers, sidewalks); girder lines are laid out by spacing with flare between supports. | T2 | 5 |
| CB-BRG-003 | Girder families and haunch | Precast, box and steel plate girders are parametric families; haunch depth along each girder is computed from deck geometry and girder camber input. | T3 | 5 |
| CB-BRG-004 | Supports | Piers (columns, cap, foundation) and abutments (stem, seat, wing walls) are placed at bearing lines; foundation levels relate to the ground surface. | T2 | 5 |
| CB-BRG-005 | Bearing seat elevations | Bearing seat elevations are computed from deck geometry, girder depth and bearing height and listed in a table. | T2 | 5 |
| CB-BRG-006 | Vertical clearance checks | Clearance under the bridge is checked against roads, tracks and water levels from surfaces, profiles and corridors with a minimum clearance; deficiencies are listed by location. | T2 | 5 |
| CB-BRG-007 | Bridge quantities | Concrete volumes, deck area, girder lengths and support counts feed quantities. | T2 | 5 |
| CB-BRG-008 | Culvert structures | Box and pipe culverts are placed under corridors with skew, headwalls and wing walls, and link to culvert hydraulics (CB-HYD-014). | T2 | 5 |
| CB-BRG-009 | Retaining walls | Walls are placed along a feature line or offset with top and bottom profiles, stem and footing parameters; height limits are checked and quantities computed. | T2 | 4 |
| CB-BRG-010 | Tunnels | A tunnel is defined by portal stations, a section profile and a construction type (bored or cut-and-cover), and yields excavation volumes and clearance checks. | T3 | 5 |
| CB-BRG-011 | Structure drawings | General arrangement plans, elevations and sections of structures are produced as model views for sheets. | T2 | 5 |
| CB-BRG-012 | Structure handover | Bridges and structures export as IFC 4.3 entities with geometry, alignment reference and properties for structural design in ArchBuilder or analysis tools. | T2 | 5 |
