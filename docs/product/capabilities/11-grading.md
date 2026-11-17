# Grading

This area shapes sites: feature lines with editable elevations, gradings that project slopes from
feature lines to targets, grading sets with surfaces and volumes, and optimization of proposed
surfaces against earthwork and drainage constraints.

## Domain objects

- **Feature line**: 3D linework with vertices and elevation-only points, line and arc segments.
- **Layout site**: a topology container in which feature lines, alignments and parcels interact.
- **Grading**: a slope projection from a feature line footprint under a criteria set.
- **Grading criteria**: named rules for slopes, distances, targets and corner treatment.
- **Grading set**: gradings, infills, a set surface and volumes against a base surface.
- **Optimization study**: region, constraints, objective, runs and results.
- **Retaining wall line**: a feature line pair with top and bottom elevations.

## Feature lines

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-GRD-001 | Feature line object | A feature line is 3D linework with vertices and elevation-only points on line and arc segments. Grade and slope of every segment are computed and available to labels and checks. | T1 | 3 |
| CB-GRD-002 | Feature line creation | Feature lines are created from linework, figures, corridor feature lines, alignments with profiles and network inverts or rims, or drawn with elevation, grade or slope input at each vertex. | T1 | 3 |
| CB-GRD-003 | Elevation editing | A grid edits vertex elevations; commands set elevation, grade or slope between points, raise and lower, insert and delete elevation points, and take elevations from a surface once or linked. A quick-edit mode shows grades live while picking vertices. | T1 | 3 |
| CB-GRD-004 | Geometry editing | Feature lines break, trim, extend, join, reverse, fillet, fit curves, weed vertices by tolerance and offset with a grade or elevation difference. | T1 | 3 |
| CB-GRD-005 | Site topology | Feature lines in the same layout site share elevations at crossings through split points, so editing one updates the crossing elevation on the other; siteless feature lines do not interact. | T1 | 3 |
| CB-GRD-006 | Draping | A feature line drapes onto a surface with vertices inserted at every triangle edge crossing. | T1 | 3 |
| CB-GRD-007 | Relative elevations | Elevations are set relative to another feature line or alignment and profile by offset and slope, linked or one-time. | T2 | 3 |
| CB-GRD-008 | Feature line labels | Grade, length, slope and spot elevation labels apply through label styles and update with the feature line. | T1 | 3 |

## Gradings

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-GRD-009 | Grading object | A grading projects from a feature line to a surface, an elevation, a relative elevation or a distance, with separate cut and fill slopes and a side. It computes its daylight line and regenerates when the feature line, target or criteria change. | T1 | 3 |
| CB-GRD-010 | Grading criteria library | Named criteria sets hold slopes, grades, distances, targets and conflict rules, and are reused across documents through libraries. | T1 | 3 |
| CB-GRD-011 | Grading sets and surfaces | A grading set collects gradings and infills between them, maintains a set surface, and reports cut, fill and net volume against a base surface, updating dynamically. | T1 | 3 |
| CB-GRD-012 | Corner treatment | Projections at convex corners use radial or mitered treatment; overlaps at concave corners are cleaned; the chosen treatment is part of the criteria. | T1 | 3 |
| CB-GRD-013 | Ranged criteria | Different criteria apply over ranges along one footprint, with transition lengths between ranges. | T2 | 3 |
| CB-GRD-014 | Volume balancing by elevation | A grading set is raised or lowered to reach a target net volume (with factors) by solving for the vertical offset; the result reports the offset and achieved balance. | T2 | 3 |
| CB-GRD-015 | Daylight lines | A daylight line to a surface is created from any edge with slope rules without creating a grading set. | T2 | 3 |
| CB-GRD-016 | Retaining walls in grading | A retaining wall line pair holds top and bottom elevations; wall height displays along the wall and feeds quantities and checks (CB-BRG-009). | T2 | 4 |
| CB-GRD-017 | Grading check | Proposed surfaces are checked for slopes outside limits, flat areas below a minimum drainage grade and depressions that would pond; each finding has a locate action. | T2 | 3 |

## Optimization

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-GRD-018 | Grading optimization study | Given a design region, existing surface, constraints (slope limits, minimum drainage grades toward outlets, fixed elevations, tie-ins, flat pads, maximum wall heights) and an objective (minimum earthwork, balance, minimum import or export), a background study produces a proposed surface and feature lines and reports constraint satisfaction. It is cancellable. | T3 | 4 |
| CB-GRD-019 | Study comparison and adoption | Several runs with different parameters are compared by volumes and constraint violations; a chosen result is adopted into the design through a command. | T3 | 4 |
