# Profiles and profile views

This area defines vertical geometry along alignments and the views that present it: surface and
layout profiles, derived and superimposed profiles, vertical design criteria, and profile views with
data bands and projected objects.

## Domain objects

- **Profile**: kind surface, layout, derived (from corridor, feature line, 3D polyline, network or file) or superimposed; belongs to one alignment.
- **Vertical element**: tangent, symmetric parabola, asymmetric parabola or circular curve.
- **Vertical intersection point**: station and elevation where tangents meet.
- **Profile view**: a graph object with station and elevation ranges, exaggeration and displayed profiles.
- **Data band**: a strip of values along a profile view.
- **Projected object**: a model object shown in a profile view at its station and elevation.

## Profiles

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-PRF-001 | Surface profile | A surface profile samples one or more surfaces along an alignment, optionally at an offset and over a station range, at every triangle edge crossing so the profile is exact. It regenerates when the surface or the alignment changes, for the changed station range only. | T1 | 3 |
| CB-PRF-002 | Layout profile | A layout profile is a chain of tangents and vertical curves (symmetric parabola, asymmetric parabola, circular) defined by vertical intersection points, with fixed, floating and free constraint states. Elevation, grade and curvature are queryable at any station. | T1 | 3 |
| CB-PRF-003 | Profile layout tools | Tangents are drawn with or without curves; vertical intersection points are inserted, deleted and moved; curves are set by length, K value, radius or a pass-through point; tangents are constrained by grade or drawn through points. | T1 | 3 |
| CB-PRF-004 | Best-fit profile | A layout profile fits a surface profile or a set of points within a tolerance and reports the maximum deviation. | T2 | 3 |
| CB-PRF-005 | Profile parameter grid | A grid edits station, elevation, grades in and out, curve length, K value, grade change and curve start and end values; edits re-solve dependent elements immediately. | T1 | 3 |
| CB-PRF-006 | Derived profiles | Profiles derive from a corridor feature line, a feature line, a 3D polyline, a gravity network run or a station-elevation text file, either linked (regenerating with the source) or static. | T1 | 3 |
| CB-PRF-007 | Superimposed profiles | A profile of another alignment is mapped onto this alignment's stations by perpendicular projection or crossing and regenerates when either alignment or the source profile changes. | T2 | 3 |
| CB-PRF-008 | Offset profiles | A profile along an offset alignment derives from a layout profile and a cross slope or the superelevation set. | T2 | 3 |
| CB-PRF-009 | Vertical design criteria | Minimum K values for crest and sag curves by speed, stopping and passing sight distance, grade limits and minimum curve length are checked live, with markers in profile views and flags in the grid. | T1 | 3 |
| CB-PRF-010 | Alignment change handling | When the alignment length changes, layout profile intersection points keep their stations; points that fall outside the new station range are flagged and listed, never silently removed. | T1 | 3 |
| CB-PRF-011 | Sight distance along a profile | Stopping and passing sight distance are evaluated against vertical geometry with stated eye and object heights; deficient station ranges are listed and marked. | T2 | 3 |
| CB-PRF-012 | Profile reports | Reports list vertical intersection points, curve data and station-elevation values at an interval. | T1 | 3 |

## Profile views

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-PRF-013 | Profile view | A profile view shows chosen profiles over a station range with an automatic or fixed elevation range, vertical exaggeration and datum elevation. With automatic height the view resizes when the profiles change. | T1 | 3 |
| CB-PRF-014 | Split and stacked views | When the elevation range exceeds the view height, the view splits into segments with grid breaks; stacked views place consecutive station ranges one above another. | T2 | 3 |
| CB-PRF-015 | Multiple profile views | A series of views is generated along an alignment by station length per view and an arrangement grid, or matched to sheet frames (CB-PLAN-005). | T1 | 3 |
| CB-PRF-016 | Data bands | Bands above or below a view show profile elevations, cut and fill depth, stations, horizontal geometry, vertical geometry, superelevation, section data and network data. Band items reference any profile and label at set intervals or at geometry points. | T1 | 3 |
| CB-PRF-017 | Projected objects | Points, feature lines, figures, solids and network parts project into the view at their station and elevation, perpendicular to the alignment, and stay linked to the source objects. | T1 | 3 |
| CB-PRF-018 | Editing in profile views | Layout profile points and network parts edit by grips inside the view, with snapping to grades, stations and elevations. | T1 | 3 |
| CB-PRF-019 | Cut and fill shading | Areas between two profiles shade by cut and fill with areas reported per station range. | T2 | 3 |
| CB-PRF-020 | Crossing markers | Alignments, pipes and utilities crossing the alignment show as markers at the crossing station with their elevations, linked to the crossing objects. | T2 | 3 |
| CB-PRF-021 | View styling | Grids, axes, ticks, titles and annotations of profile views come from view styles (CB-STY-001). | T1 | 3 |
