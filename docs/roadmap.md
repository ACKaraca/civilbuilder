# Roadmap

CivilBuilder milestones mapped onto the suite phases. Milestones have exit criteria, not dates;
scopes are capability ID ranges from the [capability index](product/capabilities/README.md).

| Milestone | Suite phase | Goal |
|---|---|---|
| M1 Terrain and survey | 3 | Georeferenced documents, points, survey import and surfaces |
| M2 Linear design chain | 3 | Alignments, profiles, components, assemblies and corridors on the regeneration graph |
| M3 First production release | 3 | Sections, quantities, grading, styles, plan production, shared references, LandXML and IFC |
| M4 Site, concept and access | 4 | Parcels, intersections, roundabouts, swept paths, concept modeling and analysis, point clouds, survey adjustment |
| M5 Networks and hydraulics | 5 | Gravity and pressure networks with hydrology and hydraulic analysis |
| M6 Rail, structures and scale | 5 | Rail, bridges, multi-user editing, advanced analysis |
| M7 Exchange, field data and field use | 5 | Connectors for other applications, raw survey observations, browser and tablet builds |

## M1 Terrain and survey (phase 3)

- **Scope:** CB-GEO-001 to CB-GEO-015, CB-GEO-018, CB-GEO-019, CB-GEO-021, CB-GEO-023;
  CB-SURV-001 to CB-SURV-016, CB-SURV-018 to CB-SURV-020, CB-SURV-026 to CB-SURV-029, CB-SURV-031;
  CB-SURF-001 to CB-SURF-005, CB-SURF-007 to CB-SURF-011, CB-SURF-013 to CB-SURF-026,
  CB-SURF-028 to CB-SURF-037; CB-STY-001, CB-STY-002, CB-STY-007, CB-STY-008, CB-STY-012;
  CB-AUTO-001 to CB-AUTO-005; CB-IO-001 (points and surfaces), CB-IO-005, CB-IO-014, CB-IO-015.
- **Depends on `arc-core`:** `arc-base`, `arc-geom` (TIN, regions, spatial index), `arc-doc`
  (transactions, regeneration graph, package), `arc-command`, `arc-io-geo`, `arc-io-dxf`, `arc-gpu`,
  `arc-ui`, `arc-app` at the phase 0 minimum.
- **Depends on other products:** none.
- **Exit criteria:** workflow 1 steps 1, 2 and 4 to 7 pass headless and interactively; a 10 million
  point surface meets its build target; LandXML surfaces round-trip with an independent reader.

## M2 Linear design chain (phase 3)

- **Scope:** CB-ALN-001 to CB-ALN-026; CB-PRF-001 to CB-PRF-021; CB-ASM-001 to CB-ASM-018;
  CB-COR-001 to CB-COR-018, CB-COR-020 to CB-COR-023; CB-STY-009 to CB-STY-011;
  CB-AUTO-013; CB-IO-001 and CB-IO-002 (alignments and profiles), CB-IO-003 (alignments).
- **Depends on `arc-core`:** `arc-nodes` (component graphs), `arc-solve` (expression engine),
  `arc-mesh` (corridor meshes), `arc-io-ifc`, `arc-scene`.
- **Depends on other products:** none.
- **Exit criteria:** workflow 2 passes; incremental station-range rebuild equals a full rebuild in the
  regeneration equivalence tests; the profile edit target on a 10 km corridor is met; every shipped
  component passes its definition tests in CI.

## M3 First production release (phase 3)

- **Scope:** CB-SEC-001 to CB-SEC-010, CB-SEC-012, CB-SEC-013; CB-QTY-001 to CB-QTY-007; CB-GRD-001 to CB-GRD-015,
  CB-GRD-017; CB-PLAN-001 to CB-PLAN-010, CB-PLAN-012, CB-PLAN-013; CB-STY-003 to CB-STY-006,
  CB-STY-013, CB-STY-014, CB-STY-016 to CB-STY-024; CB-REF-001 to CB-REF-008, CB-REF-015;
  CB-AUTO-009, CB-AUTO-011; CB-IO-001 to CB-IO-007, CB-IO-014 to
  CB-IO-016 complete.
- **Depends on `arc-core`:** `arc-draft` (layouts, plotting), `arc-view`, `arc-io-pdf`, `arc-io-dwg`
  write.
- **Depends on other products:** DraftBuilder's phase 1 drafting core proves the shared `arc-draft`
  engine used for sheets; Arc Review opens exported IFC for coordination.
- **Exit criteria:** workflows 2, 3, 4, 9 and 10 pass; IFC 4.3 exports pass independent validation;
  sheets regenerate incrementally; the standards audit runs headless in CI.

## M4 Site, concept and access (phase 4)

- **Scope:** CB-PCL-001 to CB-PCL-015; CB-INT-001 to CB-INT-017; CB-VEH-001 to CB-VEH-003,
  CB-VEH-005 to CB-VEH-023; CB-CON-001 to CB-CON-009, CB-CON-011 to CB-CON-018; CB-ANL-001 to
  CB-ANL-005, CB-ANL-010 to CB-ANL-013; CB-REAL-001 to CB-REAL-015; CB-SURV-017, CB-SURV-021 to
  CB-SURV-025, CB-SURV-030, CB-SURV-032; CB-GEO-016, CB-GEO-017, CB-GEO-020, CB-GEO-022;
  CB-SURF-006, CB-SURF-012, CB-SURF-027; CB-QTY-008 to CB-QTY-018; CB-GRD-016, CB-GRD-018,
  CB-GRD-019; CB-COR-019; CB-SEC-014; CB-PLAN-011; CB-STY-015; CB-REF-009 to CB-REF-011,
  CB-REF-013, CB-REF-014; CB-BRG-009; CB-AUTO-006 to CB-AUTO-008, CB-AUTO-010, CB-AUTO-012,
  CB-AUTO-014; CB-IO-008, CB-IO-011 to CB-IO-013.
- **Depends on `arc-core`:** `arc-io-pointcloud`, `arc-io-mesh`, `arc-io-bcf`, `arc-hub-api`.
- **Depends on other products:** RenderBuilder for photoreal frames through the Arc Scene; Arc Hub
  documents module for file collaboration and issues.
- **Exit criteria:** workflows 1 (complete with adjustment), 7, 8, 11, 13 and 14 pass.

## M5 Networks and hydraulics (phase 5)

- **Scope:** CB-GRAV-001 to CB-GRAV-016; CB-PRES-001 to CB-PRES-011; CB-HYD-001 to CB-HYD-027;
  CB-SEC-011; CB-IO-009.
- **Depends on `arc-core`:** no new crates; `civilbuilder-hydraulics` adds the engine boundary and the
  two-dimensional solver adapter.
- **Depends on other products:** none at compile time; Arc Hub automation jobs may run analyses
  headless.
- **Exit criteria:** workflows 5 and 6 pass; hydraulic results match the reference engines within the
  tolerances fixed by [OQ-08](product/open-questions.md); two-dimensional flood results match the
  published benchmark cases within the tolerances fixed by [OQ-31](product/open-questions.md).

## M6 Rail, structures and scale (phase 5)

- **Scope:** CB-RAIL-001 to CB-RAIL-015; CB-BRG-001 to CB-BRG-008, CB-BRG-010 to CB-BRG-012;
  CB-CON-010; CB-ANL-006 to CB-ANL-009, CB-ANL-014 to CB-ANL-016; CB-VEH-004, CB-VEH-024; CB-REF-012; CB-AUTO-015;
  CB-IO-010.
- **Depends on `arc-core`:** `arc-hub-api` change sets for element-level editing.
- **Depends on other products:** Arc Hub stage 2 multi-user editing; ArchBuilder structural import
  of IFC bridge handover.
- **Exit criteria:** workflow 12 passes; two users edit different corridors of one document
  concurrently through Arc Hub and both edits survive; bridge handover opens in ArchBuilder with
  geometry and alignment reference; pedestrian simulation results match reference flows within the
  tolerances fixed by [OQ-32](product/open-questions.md).

## M7 Exchange, field data and field use (phase 5)

- **Scope:** CB-CONNECT-001 to CB-CONNECT-015; CB-TOUCH-001 to CB-TOUCH-016; CB-SURV-033 to
  CB-SURV-038.
- **Depends on `arc-core`:** the Arc exchange package contract and its `arc-io-*` crate, the
  WebAssembly and mobile builds of the layers below the UI, `arc-ui` touch input, `arc-app` platform
  integration, `arc-hub-api` for work packages and field records.
- **Depends on other products:** connectors from the `arc-connectors` repository; Arc Hub for
  browser opening and synchronization of field records.
- **Exit criteria:** a round trip through a connector updates paired objects without duplicates and
  writes a loss report; a work package opens offline on a tablet, reports design values at a position
  and synchronizes field records without changing design data; a raw observation set reduces and
  adjusts to results that match independently computed reference results
  ([OQ-01](product/open-questions.md), [OQ-30](product/open-questions.md)).
