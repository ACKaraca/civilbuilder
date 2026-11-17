# Rail

This area designs track: rail alignments and profiles, cant, turnouts and crossovers, track
assemblies, platforms, structure gauge and kinematic envelope checks, and rail exchange.

## Domain objects

- **Track alignment**: an alignment of kind rail with gauge and rail spiral options.
- **Cant set**: applied cant, transitions and critical stations along a track.
- **Turnout definition** and **turnout instance**: catalog geometry and its placement on a track.
- **Crossover**: a pair of turnouts connecting parallel tracks.
- **Platform**: a parametric edge along a track.
- **Gauge profile** and **kinematic envelope**: clearance outlines swept along a track.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-RAIL-001 | Track alignments | A track alignment uses rail spiral types (clothoid, cubic parabola, Bloss, sinusoidal) with chord-based or arc-based length options and holds the track gauge. | T1 | 5 |
| CB-RAIL-002 | Cant calculation | Equilibrium cant is computed from speed and radius; applied cant is set within cant deficiency and excess limits with rounding; transitions are linear or curved and aligned with spirals. Separate speed classes are supported. | T1 | 5 |
| CB-RAIL-003 | Cant diagram | A diagram plots applied cant, deficiency and excess against station, and critical stations edit by grips and in a table. | T1 | 5 |
| CB-RAIL-004 | Rail design criteria | Gradient limits, minimum radius, cant and deficiency limits, rate of change of cant and transition length rules are checked live from a rail criteria set. | T1 | 5 |
| CB-RAIL-005 | Track profiles | Track profiles use circular or parabolic vertical curves with rail-specific minimum radius and grade checks. | T1 | 5 |
| CB-RAIL-006 | Turnout catalog | Parametric turnout definitions (switch type, crossing angle, diverging radius, lead and lengths, diverging geometry) are stored in an open catalog format that users extend. | T2 | 5 |
| CB-RAIL-007 | Turnout placement | A turnout is placed on a track at a station with hand and direction; it creates the diverging track alignment, stays connected to the parent track and moves with it. | T2 | 5 |
| CB-RAIL-008 | Crossovers and diamonds | Crossovers between parallel tracks are created from track spacing and a turnout definition; diamond crossings are created at track crossings. | T2 | 5 |
| CB-RAIL-009 | Track assemblies | Track components model rails, sleepers, ballast, slab track and formation, and rotate about the low rail, high rail or centerline according to cant. | T1 | 5 |
| CB-RAIL-010 | Platforms | A platform edge is offset from the track with corrections for cant and curvature, with length and height; edge clearance and height are checked against limits. | T2 | 5 |
| CB-RAIL-011 | Structure gauge and kinematic envelopes | Gauge profiles sweep along the track with cant applied; kinematic envelopes derive from rail vehicle definitions (CB-VEH-004). Conflicts with structures, solids and corridors are reported by station. | T2 | 5 |
| CB-RAIL-012 | Track spacing check | Spacing between adjacent tracks is checked with curve widening allowances. | T2 | 5 |
| CB-RAIL-013 | Overhead line supports | Overhead line support locations are placed along a track by span rules, with clearance to structures checked. | T3 | 5 |
| CB-RAIL-014 | Rail annotation and reports | Cant, gauge, turnout and platform labels and track geometry tables apply through styles. | T1 | 5 |
| CB-RAIL-015 | Rail exchange | Tracks, cant and turnouts export to IFC 4.3 rail entities and LandXML; track topology exports to railML. | T2 | 5 |
