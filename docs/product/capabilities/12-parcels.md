# Parcels

This area subdivides land: parcels formed by the topology of a layout site, lot layout by area and
frontage rules, right-of-way parcels, numbering, labels, tables and closure reports.

## Domain objects

- **Layout site**: the topology container shared with feature lines and alignments.
- **Parcel**: a closed area formed by segments, with number, name, use and properties.
- **Parcel segment**: a line or arc boundary shared between parcels.
- **Setback and easement**: non-topological overlays tied to parcels.
- **Numbering scheme**: prefix, start and order rules.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-PCL-001 | Parcel object | A parcel is a closed area formed by segments in a layout site, with area, perimeter, number, name, use type and user properties. | T2 | 4 |
| CB-PCL-002 | Parcels from objects | Parcels form from linework, closed polylines and coordinate geometry entry (CB-SURV-031); input segments become site topology. | T2 | 4 |
| CB-PCL-003 | Topology | Alignments and segments in the same site split parcels. Editing a segment updates both adjacent parcels; overlapping and dangling segments are reported. | T2 | 4 |
| CB-PCL-004 | Slide-line layout | Lots of a target area are created along a frontage at a slide angle, honoring minimum area, frontage, width at setback and depth; the remainder is distributed, kept as a last lot or left separate by option. | T2 | 4 |
| CB-PCL-005 | Swing-line layout | A lot of a target area is created by swinging a line about a fixed point. | T2 | 4 |
| CB-PCL-006 | Automatic subdivision | A parcel subdivides into lots by rules, and the candidate solutions preview before one is committed. | T2 | 4 |
| CB-PCL-007 | Free-form lot lines | Lot lines are created by angle, perpendicular, bisector or through points. | T2 | 4 |
| CB-PCL-008 | Right-of-way parcels | Right-of-way parcels generate from alignment offsets with corner cleanup by fillet or chamfer, and regenerate with the alignment. | T2 | 4 |
| CB-PCL-009 | Parcel editing | Segments edit by grips and parameters; parcels merge and subtract; deleted segments merge parcels. | T2 | 4 |
| CB-PCL-010 | Numbering | Parcels number automatically and renumber along a picked path or by selection order with prefixes. | T2 | 4 |
| CB-PCL-011 | Labels and tables | Area and number labels, segment labels (bearing and distance, curve data) and tags with line and curve tables apply through styles and update with the topology. | T2 | 4 |
| CB-PCL-012 | Map check and closure | Map-check and inverse reports give closure error, precision ratio and area by coordinates, computed from exact geometry and, optionally, from the rounded label values. | T2 | 4 |
| CB-PCL-013 | Setbacks and easements | Setback lines offset from front, side and rear boundaries, and easements overlay parcels without changing their topology. | T2 | 4 |
| CB-PCL-014 | Parcel export | Parcels export as GIS features with attributes, as LandXML parcels and as legal description text reports. | T2 | 4 |
| CB-PCL-015 | Parcel queries | Parcels filter by area, use and properties; results select or populate tables. | T2 | 4 |
