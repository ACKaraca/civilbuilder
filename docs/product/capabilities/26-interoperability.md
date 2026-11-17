# Interoperability

This area lists the exchange capabilities of the product. Fidelity levels, mapping rules and
validation are specified in [the interoperability architecture](../../architecture/interoperability.md);
GIS formats are covered in [coordinate systems and geospatial data](01-geospatial.md).

## Domain objects

- **Import session**: the original file, mapping choices, created objects and loss report.
- **Loss report**: every source item not modeled, approximated or preserved as foreign data.
- **Preserved foreign data**: unmodeled source content kept in the document package for round trips.
- **Export profile**: format, version, CRS and object mapping options saved for reuse.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-IO-001 | LandXML import | LandXML 1.2 and 2.0 import points, surfaces, alignments with superelevation and cant, profiles, cross sections, parcels, gravity and pressure networks, feature lines and survey data as editable objects, with a loss report. | T1 | 3 |
| CB-IO-002 | LandXML export | The same object types export to LandXML 1.2 or 2.0, validated against the published schema. | T1 | 3 |
| CB-IO-003 | IFC 4.3 export | Alignments (horizontal, vertical, cant), road, railway and bridge spatial structures, corridor solids classified by shape code, surfaces, networks and structures export to IFC 4.3 with property sets and map conversion to the document CRS. | T1 | 3 |
| CB-IO-004 | IFC import | IFC 4.3 alignments import as editable alignments and profiles, surfaces as surfaces, and other entities as referenced context with properties. | T2 | 3 |
| CB-IO-005 | DWG and DXF import | Linework, 3D faces, points, blocks with attributes and text import as source geometry for civil objects, with layer mapping and georeferencing. | T1 | 3 |
| CB-IO-006 | DWG and DXF export | Civil objects export as plain drafting entities (polylines, 3D faces, text, blocks) with their display styles applied, layers from naming rules and object identifiers in extended data; sheets export as layouts. | T1 | 3 |
| CB-IO-007 | PDF | Sheets publish as vector PDF with layers; PDF pages attach as underlays. | T1 | 3 |
| CB-IO-008 | Machine-control export | Surfaces, corridor feature lines and alignments export for machine guidance as LandXML, IFC 4.3 and 3D DXF; manufacturer-specific formats are added by plug-ins. | T2 | 4 |
| CB-IO-009 | Hydraulic model exchange | Storm and sewer models import and export as SWMM-class input files and pressure models as EPANET-class input files, with object mapping retained. | T2 | 5 |
| CB-IO-010 | railML export | Track topology, turnouts and track geometry export to railML. | T3 | 5 |
| CB-IO-011 | 3D visualization exchange | Model and context export as glTF and 3D Tiles; rendering scenes stream to RenderBuilder through the Arc Scene. | T2 | 4 |
| CB-IO-012 | City model import | CityGML and CityJSON import as context layers with attributes. | T2 | 4 |
| CB-IO-013 | BCF | BCF topics import and export with links to objects and views. | T2 | 4 |
| CB-IO-014 | Loss reports and preservation | Every import produces a loss report and keeps the original file and unmodeled content as preserved foreign data, so a re-export can include it where the format allows. | T1 | 3 |
| CB-IO-015 | Source identifier mapping | Imported objects record source identifiers so repeated imports update existing objects instead of duplicating them. | T1 | 3 |
| CB-IO-016 | Export validation | Exports pass an independent reader in continuous integration; failures are release blockers. | T1 | 3 |
