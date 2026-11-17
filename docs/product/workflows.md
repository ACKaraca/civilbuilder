# Reference workflows

These fourteen end-to-end workflows are the acceptance scenarios of CivilBuilder. Each step names the
capabilities it exercises; each workflow ends with observable acceptance results.

## 1. Existing ground from survey

1. Create a document from a template and set the CRS, vertical reference and combined scale factor (CB-GEO-001, CB-GEO-005, CB-GEO-006).
2. Import a field book file into the survey database and attach equipment profiles (CB-SURV-018, CB-SURV-017).
3. Compute traverse closure and run a least-squares adjustment; accept the adjusted coordinates (CB-SURV-022, CB-SURV-023, CB-SURV-025).
4. Apply description keys and point groups to the resulting points (CB-SURV-009, CB-SURV-007).
5. Build figures from linework codes and mark them as breaklines through prefix rules (CB-SURV-028, CB-SURV-029).
6. Create a TIN surface from the point group, the figures and an outer boundary; fix spikes reported by the integrity check (CB-SURF-001, CB-SURF-008, CB-SURF-009, CB-SURF-022, CB-SURF-017).
7. Apply a surface style with contours and contour labels and run a slope analysis (CB-SURF-025, CB-SURF-026, CB-SURF-024).

**Acceptance**
- The adjustment report shows residuals, error ellipses and a passed variance test, and points carry the adjusted coordinates.
- Editing one observation and recomputing marks the points, the figures and the surface stale, and rebuilding updates them without manual steps.
- Contours honor every breakline; the surface operations list replays to an identical triangulation after reopening the document.

## 2. Road design along the dependency chain

1. Reference the existing ground surface from the survey document (CB-REF-002).
2. Lay out an alignment by points of intersection with spirals, assign design speeds and a criteria set, and calculate superelevation (CB-ALN-003, CB-ALN-016, CB-ALN-015, CB-ALN-019).
3. Create a surface profile and a profile view with bands; design a layout profile with live K-value checks (CB-PRF-001, CB-PRF-013, CB-PRF-016, CB-PRF-002, CB-PRF-009).
4. Build an assembly from standard lane, curb, shoulder and daylight components (CB-ASM-013, CB-ASM-009, CB-ASM-010).
5. Create a corridor with one region, frequencies and the surface as daylight target (CB-COR-001, CB-COR-003, CB-COR-004, CB-COR-005).
6. Inspect stations in the section editor and add a parameter override over a station range (CB-COR-015, CB-COR-006).
7. Create the corridor top surface with a code-derived boundary and corridor solids (CB-COR-012, CB-COR-014).

**Acceptance**
- Moving one vertical intersection point rebuilds only the stations within the changed vertical elements, and the viewport stays interactive during the rebuild.
- A station where daylight finds no intersection appears in the failure list with station and component, and every other station still produces output.
- Criteria violations appear as markers in plan and profile views and in the checks panel while editing continues.

## 3. Sections, quantities and mass haul

1. Create a sample line set at the corridor stations with existing ground, corridor surface and corridor shapes as sources (CB-SEC-001, CB-SEC-003).
2. Arrange section views on pages from a sheet template (CB-SEC-006, CB-SEC-007).
3. Apply quantity criteria with cut, fill and pavement materials and shrink and swell factors (CB-QTY-001, CB-QTY-002, CB-QTY-004).
4. Place a volume table and generate an earthwork report (CB-QTY-005, CB-QTY-006).
5. Create a mass haul line with a borrow site and a free-haul distance, and run haul optimization (CB-QTY-015, CB-QTY-016, CB-QTY-017, CB-QTY-018).
6. Generate section sheets and publish them to PDF (CB-PLAN-007, CB-PLAN-012).

**Acceptance**
- Changing the layout profile updates sections, volumes, the volume table and the mass haul view for the affected stations only.
- Reports state the volume method and show adjusted and unadjusted volumes.
- The haul plan totals equal the material list totals within tolerance.

## 4. Site grading and earthwork balance

1. Create a layout site with feature lines for a building pad, parking area edges and a swale (CB-GRD-001, CB-GRD-002, CB-GRD-005).
2. Set elevations and grades in the elevation grid (CB-GRD-003).
3. Add gradings with criteria from the library to the existing surface and infill a grading set (CB-GRD-009, CB-GRD-010, CB-GRD-011).
4. Balance the grading set to a target net volume, then run a grading optimization study and compare it with the manual result (CB-GRD-014, CB-GRD-018, CB-GRD-019).
5. Check the proposed surface for flat and ponding areas; label spot elevations and contours (CB-GRD-017, CB-SURF-026).

**Acceptance**
- Editing a pad elevation updates the crossing feature lines, gradings, set surface and volumes.
- The balanced result reports the applied vertical offset and a net volume within the requested tolerance.
- The adopted optimization result satisfies every stated constraint or lists those it could not meet.

## 5. Storm drainage with ponds

1. Delineate catchments by watershed analysis and compute flow paths and times of concentration (CB-SURF-027, CB-HYD-001, CB-HYD-002).
2. Define an IDF data set and a design storm (CB-HYD-003).
3. Lay out a gravity network from a parts list with cover and slope rules (CB-GRAV-004, CB-GRAV-005, CB-GRAV-006).
4. Grade a pond and define its outlet structure (CB-GRD-011, CB-HYD-016).
5. Run the storm analysis; review hydraulic grade lines in profile views and size pipes from design flows (CB-HYD-006, CB-HYD-007, CB-HYD-008, CB-GRAV-015).
6. Check detention routing and run an interference check against utilities (CB-HYD-017, CB-GRAV-011).
7. Label the network and produce tables and quantity reports (CB-GRAV-010, CB-GRAV-014).

**Acceptance**
- Moving a structure marks analysis results stale; a rerun produces results tagged with the new revision.
- Hydraulic grade lines display in profile views and surcharged structures are flagged.
- The pond stage-storage relation updates when its grading changes.

## 6. Water distribution network

1. Lay out a pressure network along an alignment from a catalog, with fittings inserted automatically (CB-PRES-002, CB-PRES-003).
2. Set vertical layout by cover and check deflection and cover rules (CB-PRES-004, CB-PRES-005).
3. Check crossing separation with the storm network (CB-PRES-008).
4. Run steady-state and fire flow analyses (CB-HYD-018, CB-HYD-019).
5. Export quantities, IFC 4.3 and an EPANET-class input file (CB-PRES-009, CB-PRES-011, CB-IO-009).

**Acceptance**
- Pressures and velocities display on the design objects and update after a rerun.
- Every crossing with less than the required separation is listed with its location.
- The exported analysis input reopens in the reference engine with the same results within tolerance.

## 7. Parcel subdivision

1. Create boundary parcels from a legal description and check closure (CB-SURV-031, CB-PCL-002).
2. Create right-of-way parcels from the road alignment (CB-PCL-008).
3. Lay out lots by slide line with minimum area and frontage (CB-PCL-004).
4. Number lots, add labels, tags and tables, and add setbacks (CB-PCL-010, CB-PCL-011, CB-PCL-013).
5. Run a map check and export parcels to GIS and LandXML (CB-PCL-012, CB-PCL-014).

**Acceptance**
- Moving the alignment updates right-of-way and adjacent lot areas and labels.
- Every generated lot meets the minimum area and frontage, or the layout reports the lot that does not.
- The map check reports closure for exact and rounded label values.

## 8. Intersection and roundabout with swept paths

1. Create a four-leg intersection with curb returns, a turn lane and generated corridor regions (CB-INT-001, CB-INT-003, CB-INT-005, CB-INT-006).
2. Adjust curb return profiles and rebuild (CB-INT-004).
3. Run swept paths for a design truck along every movement (CB-VEH-005, CB-VEH-009, CB-VEH-011).
4. Replace a second junction with a roundabout and run fastest-path and movement checks (CB-INT-011, CB-INT-015, CB-INT-016).
5. Check intersection sight triangles (CB-INT-008).

**Acceptance**
- Changing a curb radius regenerates the curb return, corridor regions and swept paths, and conflicts re-evaluate.
- Each roundabout entry reports its fastest-path radius against the criteria set.
- Manually edited corner profile points survive regeneration or are listed.

## 9. Plan production for a linear project

1. Generate a sheet frame set along the alignment from a plan and profile template (CB-PLAN-001, CB-PLAN-004).
2. Generate match lines, sheets and profile views per frame (CB-PLAN-002, CB-PLAN-003, CB-PLAN-005).
3. Apply label sets and annotation scale; add drafting annotation on a sheet (CB-STY-011, CB-PLAN-008, CB-PLAN-013).
4. Assemble a sheet set with an index and publish to PDF and DWG (CB-PLAN-011, CB-PLAN-012).

**Acceptance**
- Changing the alignment regenerates only the affected sheets, and sheet annotations stay attached to model positions or are listed.
- Labels read upright on every rotated viewport.
- Publishing from the CLI produces the same PDF as interactive publishing.

## 10. Multi-document project with shared references

1. Create a project workspace with survey, road and drainage documents (CB-REF-008).
2. Reference the surface and corridor from the road document in the drainage document and apply local styles (CB-REF-001, CB-REF-002).
3. Change the corridor in the road document and save; synchronize in the drainage document (CB-REF-003, CB-REF-006).
4. Review the reference graph before editing the surface (CB-REF-007).
5. Check documents in to Arc Hub and compare two revisions of the road document (CB-REF-010, CB-REF-011).

**Acceptance**
- The drainage document shows stale references after the source save and lists changed objects on synchronization.
- Moving the source document does not break references.
- The comparison lists changed alignment elements and changed corridor station ranges.

## 11. Concept to detailed design in geospatial context

1. Assemble a context model from terrain, imagery, buildings and roads (CB-CON-001, CB-GEO-013, CB-GEO-016).
2. Sketch two concept roads with road styles; accept a proposed bridge (CB-CON-003, CB-CON-004, CB-CON-006).
3. Create two design options and compare length, volumes and cost (CB-CON-011, CB-CON-012).
4. Run 3D sight distance and a viewshed for the preferred option (CB-ANL-001, CB-ANL-002).
5. Build a presentation sequence and render frames through RenderBuilder (CB-CON-016, CB-CON-015).
6. Refine the preferred road in place with detailed assemblies and criteria (CB-CON-013).

**Acceptance**
- Concept roads are alignments, profiles and corridors with the same identifiers before and after refinement.
- Moving a concept road updates intersections, structures and terrain modification in the background.
- Analysis results display stale after the design changes.

## 12. Rail corridor

1. Lay out a track alignment and compute cant for speed classes (CB-RAIL-001, CB-RAIL-002, CB-RAIL-003).
2. Place turnouts and a crossover from the catalog; add a platform (CB-RAIL-007, CB-RAIL-008, CB-RAIL-010).
3. Design the track profile and build a corridor with track components (CB-RAIL-005, CB-RAIL-009).
4. Sweep a kinematic envelope and check structure gauge clearances (CB-RAIL-011).
5. Export IFC 4.3 rail entities and railML (CB-RAIL-015).

**Acceptance**
- Moving the parent track moves the turnouts and their diverging tracks.
- Cant deficiency violations are marked live.
- Clearance conflicts list station and conflicting object.

## 13. Existing conditions from point clouds

1. Attach a LAZ cloud and classify ground (CB-REAL-001, CB-REAL-003).
2. Create a surface from the ground class with thinning (CB-REAL-005).
3. Extract curb lines as feature lines (CB-REAL-006).
4. Use the surface as the existing ground of a design and later compare an as-built cloud with the design corridor (CB-REAL-008).

**Acceptance**
- The cloud displays interactively while the index is still building.
- Changing the thinning parameters regenerates the surface and every dependent object.
- The deviation report lists statistics per region within the stated tolerance bands.

## 14. Parking and access check

1. Define a parking standard and generate parking rows along curb lines (CB-VEH-018, CB-VEH-019).
2. Run swept paths for refuse and fire vehicles through the entrance and aisles (CB-VEH-005, CB-VEH-022).
3. Place a loading bay and check the reverse-in maneuver (CB-VEH-023, CB-VEH-008).
4. Adjust curb geometry and review updated paths and counts; tabulate bays (CB-VEH-010, CB-VEH-021).

**Acceptance**
- Moving a curb line regenerates parking rows, counts and swept paths.
- Every conflict between an envelope and a curb is listed with its location.
- Bay tables match the generated bays by type.
