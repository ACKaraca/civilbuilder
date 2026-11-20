# Assistance

This area specifies what the optional assistant does in CivilBuilder: answering questions about the
design at stations and offsets, reviewing survey data and surfaces, generating alignment, profile,
grading and parcel options under the project's design criteria, explaining criteria findings,
sizing checks and quantities, and drafting reports and sheets, always as previewed commands checked
by the product's own criteria, rebuild and analysis engines. The suite rules for levels, grounding,
data handling, provenance and evaluation are in
[assistance](https://github.com/ACKaraca/arc-suite/blob/main/docs/architecture/assistance.md); the
panel is [CB-AUTO-015](25-automation.md) and the protocol endpoint is
[CB-AUTO-014](25-automation.md). Every capability here also has a manual and scripted path.

## Domain objects

| Object | Key properties | Relationships |
|---|---|---|
| Assistance request | Text, level, scope (objects, station range, sites, documents), protected objects, base revision | Produces answers or proposals |
| Design option | Kind (alignment, profile, grading, parcel layout), parameters, metrics, criteria findings, status | Proposed against a criteria set; stored as an alternative until accepted |
| Survey review finding | Point or figure, issue (unknown code, outlier, crossing breakline, duplicate), proposed correction | Refers to survey points and figures |
| Report draft | Sections, tables from reports, citations to objects, stations and criteria | Saved as a document by the user |
| Provenance mark | Origin, proposal, revision | On objects created or changed by an applied proposal until reviewed |

## Questions and review

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ASSIST-001 | Design questions | The assistant answers questions such as "what is the cut depth at station 1+240 on the left edge", "which curves fall below the minimum radius" or "how much fill does site B need" from object queries, sampled sections and reports, cites the objects and stations, and selects them on request; values come from the product's computations. | T2 | 4 |
| CB-ASSIST-002 | Survey import review | After a survey import, the assistant lists points with unknown or inconsistent descriptions, figures with broken prefix rules, duplicates and elevation outliers against neighbors, and proposes corrections to description keys and linework code sets (CB-SURV-009, CB-SURV-028) that the point reports (CB-SURV-013) confirm. | T3 | 4 |
| CB-ASSIST-003 | Surface cleanup | The assistant runs the surface integrity check and statistics (CB-SURF-022, CB-SURF-029), explains spikes, long edge triangles, crossing breaklines and missing boundaries, and proposes boundaries, breaklines from figures and triangulation edits (CB-SURF-008, CB-SURF-009, CB-SURF-017) added to the surface's operations list; the check runs again on the rebuilt surface. | T3 | 4 |
| CB-ASSIST-004 | Corridor rebuild triage | For corridor rebuild failures (CB-COR-010), the assistant groups failed stations by cause (missing target, surface gap, assembly conflict), shows them in plan and section, and proposes target and region changes that a rebuild of the affected station range confirms. | T3 | 4 |
| CB-ASSIST-005 | Criteria findings explained | For live design checks and criteria sets (CB-ALN-015, CB-ALN-017, CB-PRF-009, CB-GRD-017), the assistant explains each violation with the criteria table row, the design speed or class it applies to and the station range, groups related findings, and proposes geometry changes that the same checks evaluate; it never states that a design meets a standard. | T3 | 4 |
| CB-ASSIST-006 | As-built comparison narrative | After an as-built comparison (CB-REAL-008), the assistant summarizes deviations by area and object with magnitudes and tolerances, citing the comparison results. | T3 | 4 |

## Options under design criteria

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ASSIST-007 | Alignment options | Between given end points and through or around user-drawn control and avoidance areas, the assistant proposes horizontal alignments built from the layout tools (CB-ALN-004) for the selected criteria set; each option is evaluated by the live design checks and reports length, minimum radius, criteria findings and an earthwork estimate from a quick corridor on the existing surface. | T3 | 4 |
| CB-ASSIST-008 | Profile options | For an alignment and surface, the assistant sets up profile optimization runs (CB-ANL-010) with constraints from the vertical criteria and fixed points the user marks, presents the resulting profiles with grades, curve lengths, sight checks and earthwork balance, and applies the chosen one as a layout profile. | T3 | 4 |
| CB-ASSIST-009 | Grading and earthwork balance | For a site with pads and feature lines, the assistant proposes pad elevations and grading criteria variants, runs the grading optimization study (CB-GRD-018) and earthwork reports (CB-QTY-006), and presents variants with cut, fill and net volume; the grading check (CB-GRD-017) runs on each variant. | T3 | 4 |
| CB-ASSIST-010 | Parcel layout options | Within a boundary and right of way, the assistant proposes lot layouts using slide-line and swing-line tools (CB-PCL-004, CB-PCL-005) to meet minimum area and frontage rules; map checks and area tables verify every lot. | T3 | 4 |
| CB-ASSIST-011 | Concept options in context | From a written description and the geospatial context, the assistant proposes concept roads and drainage (CB-CON-003) as options with quantities and costs (CB-CON-012) and the design-check overlays (CB-ANL-011). | T3 | 4 |

## Networks and analysis

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ASSIST-012 | Pipe network sizing check | The assistant sets up design flows and runs network sizing and hydraulics (CB-GRAV-015, CB-HYD-012, CB-HYD-008), explains surcharged pipes, low velocities and cover or slope rule violations (CB-GRAV-006), and proposes size and invert changes that a new hydraulic run evaluates. | T3 | 5 |
| CB-ASSIST-013 | Network layout proposals | From the road alignments, lots and an outfall, the assistant proposes gravity network layouts with structures at junctions and rule-based spacing; design rules, interference checks (CB-GRAV-011) and sizing evaluate each option. | T3 | 5 |
| CB-ASSIST-014 | Analysis results explained | After hydrology, hydraulics, swept-path or sight analyses (CB-HYD-021, CB-VEH-016, CB-ANL-001), the assistant summarizes the results and their governing cases, citing the report rows and objects. | T3 | 4 |
| CB-ASSIST-015 | Point cloud features | On a classified point cloud (CB-REAL-003), the assistant proposes curbs, edges of pavement, walls and utilities from the feature extraction (CB-REAL-006) as feature lines and points on layers by kind, with the deviation from the cloud shown per object. | T3 | 4 |

## Documents and scripts

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ASSIST-016 | Quantity and design report drafting | The assistant drafts a design or quantity report from the project's report templates (CB-AUTO-009) with tables taken from the earthwork, quantity and geometry reports (CB-QTY-012, CB-ALN-025, CB-PRF-012), explains assumptions, and cites objects, stations and criteria; numbers come only from the reports. | T3 | 4 |
| CB-ASSIST-017 | Plan production setup | Along an alignment the assistant proposes sheet frames, match lines and plan, profile and section sheets (CB-PLAN-001) with label sets (CB-STY-011) from the project's standards, previewed as the sheet list and frames. | T3 | 4 |
| CB-ASSIST-018 | Script and graph drafting | The assistant drafts a Python script, a node graph or a cross-section component graph for a described task, shown as source or graph with an explanation; it runs only when the user starts it. | T3 | 4 |
| CB-ASSIST-019 | Assisted content review | Objects carrying a provenance mark show a distinct overlay and filter; the user reviews and clears marks, and publishing sheets or exporting reports lists unreviewed objects first. | T3 | 4 |

## Readiness

Readiness classes are defined in
[assistance](https://github.com/ACKaraca/arc-suite/blob/main/docs/architecture/assistance.md#readiness-classes).

| Class | ID | Checked by | Depends on |
|---|---|---|---|
| R1 | CB-ASSIST-001 | Queries, sections, reports | CB-AUTO-014, CB-AUTO-015 |
| R1 | CB-ASSIST-002 | Description keys, point reports | CB-SURV-009, CB-SURV-013, CB-SURV-028 |
| R1 | CB-ASSIST-003 | Surface integrity check, statistics | CB-SURF-017, CB-SURF-022, CB-SURF-029 |
| R1 | CB-ASSIST-004 | Corridor rebuild | CB-COR-010 |
| R2 | CB-ASSIST-005 | Live design checks, grading check | Criteria sets for the project's jurisdiction (CB-ALN-015, CB-PRF-009, CB-GRD-010) |
| R1 | CB-ASSIST-006 | As-built comparison | CB-REAL-008 |
| R2 | CB-ASSIST-007 | Live design checks, quick corridor earthwork | CB-ALN-004, CB-ALN-017, an alignment option search |
| R1 | CB-ASSIST-008 | Vertical criteria, profile optimization | CB-ANL-010, CB-PRF-009 |
| R1 | CB-ASSIST-009 | Grading check, earthwork reports | CB-GRD-017, CB-GRD-018, CB-QTY-006 |
| R1 | CB-ASSIST-010 | Map checks, area tables | CB-PCL-004, CB-PCL-005 |
| R2 | CB-ASSIST-011 | Design-check overlays, concept quantities | CB-CON-003, CB-CON-012, CB-ANL-011 |
| R2 | CB-ASSIST-012 | Network sizing and hydraulics | CB-GRAV-006, CB-GRAV-015, CB-HYD-008, CB-HYD-012 |
| R3 | CB-ASSIST-013 | Design rules, interference checks, sizing | CB-GRAV-005, CB-GRAV-011 |
| R1 | CB-ASSIST-014 | Analysis reports | CB-HYD-021, CB-VEH-016, CB-ANL-001 |
| R2 | CB-ASSIST-015 | Deviation from the cloud | CB-REAL-003, CB-REAL-006 |
| R1 | CB-ASSIST-016 | Report tables | CB-AUTO-009, CB-QTY-012 |
| R1 | CB-ASSIST-017 | Sheet list preview | CB-PLAN-001, CB-STY-011 |
| R1 | CB-ASSIST-018 | Static check of scripts and graphs | CB-AUTO-005, node graphs |
| R1 | CB-ASSIST-019 | Provenance query | Provenance marks in `arc-core` |

## Evaluation

The assistance task suite is built from the [reference workflows](../workflows.md): workflow 1
(CB-ASSIST-002, CB-ASSIST-003), 2 (CB-ASSIST-004, CB-ASSIST-005, CB-ASSIST-007, CB-ASSIST-008),
3 (CB-ASSIST-001, CB-ASSIST-016), 4 (CB-ASSIST-009), 5 and 6 (CB-ASSIST-012, CB-ASSIST-013),
7 (CB-ASSIST-010), 9 (CB-ASSIST-017), 11 (CB-ASSIST-011) and 13 (CB-ASSIST-006, CB-ASSIST-015).
Thresholds are settled under [OQ-36](../open-questions.md).
