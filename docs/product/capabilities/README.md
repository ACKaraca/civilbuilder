# Capability specification

This index explains how CivilBuilder capabilities are identified and lists the area files that
specify them.

## Legend

| Field | Meaning |
|---|---|
| ID | `CB-<AREA>-<NNN>`. `CB` is the CivilBuilder prefix, `AREA` the token of the area file, `NNN` a number unique within the area. Identifiers are permanent; a withdrawn capability keeps its number and is marked withdrawn in its Behavior cell. |
| Capability | A short descriptive name. |
| Behavior | Observable behavior precise enough to implement and test: inputs, result, what updates automatically, limits. |
| Tier | **T1 Core**: required for first production use. **T2 Professional**: required for parity with established professional tools. **T3 Advanced**: specialized or differentiating. |
| Phase | The suite phase in which the capability is planned (see the [product roadmap](../../roadmap.md), which maps milestones onto the suite phases). CivilBuilder starts in phase 3. |

Implementation status is never recorded in these tables; it is tracked in GitHub issues and the
project board.

## Areas

| File | Area token | Scope | Rows |
|---|---|---|---|
| [01-geospatial.md](01-geospatial.md) | `GEO` | Coordinate reference systems, datums, ground and grid, units, live geospatial sources | 23 |
| [02-survey.md](02-survey.md) | `SURV` | Points, point groups, description keys, survey database, field data and raw observation reduction, figures, networks, adjustment, stakeout | 38 |
| [03-surfaces.md](03-surfaces.md) | `SURF` | Surface kinds, definition, editing, analysis, volumes | 37 |
| [04-alignments.md](04-alignments.md) | `ALN` | Horizontal geometry, stationing, offsets and widenings, criteria, superelevation | 26 |
| [05-profiles.md](05-profiles.md) | `PRF` | Surface and layout profiles, vertical criteria, profile views and bands | 21 |
| [06-assemblies.md](06-assemblies.md) | `ASM` | Node-graph cross-section components, component libraries, assemblies | 18 |
| [07-corridors.md](07-corridors.md) | `COR` | Baselines, regions, targets, station-range rebuild, corridor outputs | 23 |
| [08-intersections.md](08-intersections.md) | `INT` | Intersections, curb returns, turn lanes, roundabouts and their checks | 17 |
| [09-sections.md](09-sections.md) | `SEC` | Sample lines, sections, section views and arrangements | 14 |
| [10-quantities.md](10-quantities.md) | `QTY` | Materials, earthwork volumes, pay items, mass haul and haul optimization | 18 |
| [11-grading.md](11-grading.md) | `GRD` | Feature lines, gradings, grading sets, grading optimization | 19 |
| [12-parcels.md](12-parcels.md) | `PCL` | Parcel topology, lot layout, right of way, labels, map checks | 15 |
| [13-gravity-networks.md](13-gravity-networks.md) | `GRAV` | Storm and sanitary pipes and structures, rules, interference, trenches | 16 |
| [14-pressure-networks.md](14-pressure-networks.md) | `PRES` | Pressure pipes, fittings, appurtenances, cover and deflection rules | 11 |
| [15-hydrology.md](15-hydrology.md) | `HYD` | Catchments, rainfall, runoff, network hydraulics, channels, culverts, storage, pressure hydraulics, two-dimensional flood modeling | 27 |
| [16-rail.md](16-rail.md) | `RAIL` | Track geometry, cant, turnouts, platforms, gauges and envelopes | 15 |
| [17-bridges.md](17-bridges.md) | `BRG` | Bridges, culvert structures, retaining walls, tunnels | 12 |
| [18-plan-production.md](18-plan-production.md) | `PLAN` | Sheet frames, match lines, plan, profile and section sheets, publishing | 13 |
| [19-styles-labels.md](19-styles-labels.md) | `STY` | Object styles, label styles and expressions, tables, libraries and settings | 24 |
| [20-collaboration.md](20-collaboration.md) | `REF` | Shared references, project workspace, comparison, Hub collaboration | 15 |
| [21-concept-modeling.md](21-concept-modeling.md) | `CON` | Concept roads, structures and drainage in geospatial context, options, visualization | 18 |
| [22-concept-analysis.md](22-concept-analysis.md) | `ANL` | Sight, visibility, sun, regional hydrology, flood, traffic, pedestrian movement, noise, optimization | 16 |
| [23-swept-paths.md](23-swept-paths.md) | `VEH` | Vehicles, swept paths, conflicts, parking and loading layout | 24 |
| [24-reality-data.md](24-reality-data.md) | `REAL` | Point clouds, reality meshes, as-built comparison, boreholes and strata | 15 |
| [25-automation.md](25-automation.md) | `AUTO` | Commands, protocol, CLI, Python, node graphs, plug-ins, reports, checks | 15 |
| [26-interoperability.md](26-interoperability.md) | `IO` | LandXML, IFC 4.3, DWG/DXF, PDF, machine control, hydraulic and rail exchange | 16 |
| [27-application-connectors.md](27-application-connectors.md) | `CONNECT` | Exchange of native civil objects with other applications through connectors, licensed bridges and open readers | 15 |
| [28-web-and-tablet.md](28-web-and-tablet.md) | `TOUCH` | Browser, tablet and phone builds: viewing, position inspection, markups, issues, offline use | 16 |
| [29-assistance.md](29-assistance.md) | `ASSIST` | Optional assistance: design questions, survey and surface review, criteria findings, alignment, profile, grading and parcel options, network sizing checks, report and sheet drafting | 19 |

Total: 556 capabilities.

## Capabilities and issues

- Every implementation issue names the capability IDs it delivers in its Scope section; an epic
  covers a contiguous group of IDs from one milestone of the [roadmap](../../roadmap.md).
- An issue is *Done* only when the Behavior text of each listed capability is met and verified by a
  test or an acceptance scenario from [workflows](../workflows.md).
- Behavior that cannot yet be specified with confidence is tracked in
  [open questions](../open-questions.md); the capability row states the intended behavior and the
  open question records what must be settled.
- Issues use the label `area: <token>` with the lower-case area token (for example `area: cor`).
