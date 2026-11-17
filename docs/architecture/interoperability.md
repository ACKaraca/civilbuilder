# Interoperability

Every format CivilBuilder reads or writes, by direction and fidelity level, with mapping principles,
validation, loss reporting and what is deliberately unsupported. Fidelity levels follow the suite
interoperability policy: **view** (geometry and appearance), **data** (semantics, properties,
relationships), **edit** (native, parametric editing in CivilBuilder).

## Format matrix

| Format | Import | Export | Notes |
|---|---|---|---|
| Native `.civilb` (Arc document package) | edit | edit | The authority ([ADR-0001](../adr/0001-civil-model-in-document-package.md)) |
| LandXML 1.2 and 2.0 | edit for points, surfaces, alignments, profiles, superelevation and cant, parcels, feature lines, networks; data for cross sections and survey observations | edit for the same set | Primary civil exchange (CB-IO-001, CB-IO-002) |
| IFC 4.3 | edit for alignments and profiles; data for surfaces; view and data for other entities as context | data for alignments, spatial structure (road, railway, bridge), corridor solids, surfaces, networks, structures | Primary model exchange (CB-IO-003, CB-IO-004) |
| DWG and DXF | data (linework, 3D faces, points, blocks, attributes, text as definition sources) | view (civil objects as plain entities with styles applied); data for object identifiers in extended data | Through `arc-draft` and `arc-io-dxf`/`arc-io-dwg` |
| PDF | view (underlays) | view (vector sheets with layers) | `arc-io-pdf` |
| GeoPackage, Shapefile, GeoJSON, FlatGeobuf, KML, delimited text | data (live layers and conversion with attribute mapping) | data | `arc-io-geo` (CB-GEO-013, CB-GEO-023) |
| GeoTIFF and Cloud Optimized GeoTIFF, images with world files, ASCII grids | data (imagery and elevation) | data (analysis rasters) | |
| WMS, WMTS, WFS, OGC API Features and Tiles, XYZ tiles | view or data by service type | not applicable | User-configured endpoints only |
| CityGML, CityJSON | view and data as context | not exported | CB-IO-012 |
| LAS, LAZ, COPC, E57 | view and data (referenced) | not exported | `arc-io-pointcloud` |
| glTF, OBJ, 3D Tiles | view (reality meshes, assets, context) | view (model and context) | `arc-io-mesh` |
| Arc Scene (OpenUSD-aligned) | not applicable | view for rendering | RenderBuilder contract |
| Arc exchange package | edit or data, by object kind and the host interface (surfaces, alignments, profiles, corridors, networks, parcels, points, figures, concept objects; styles where mapped) | edit or data for the same set | Written and read by connectors inside other applications ([ADR-0017](https://github.com/ACKaraca/arc-suite/blob/main/docs/adr/0017-exchange-connectors-and-licensed-bridges.md)); CB-CONNECT-001 to CB-CONNECT-013 |
| DGN V7 | data (linework, points, text and cells as source geometry) | not exported | Open reader behind an `arc-io-*` crate; CB-CONNECT-015 |
| Field book text format (documented by the project) | data (observations) | not exported | CB-SURV-018 |
| Total-station observation files in open or published formats | data (raw observations) | not exported | CB-SURV-033 |
| RINEX observation and navigation files, SP3 precise orbits and clocks | data (raw observations, orbit products) | not exported | CB-SURV-035 |
| Delimited point formats | data | data | CB-SURV-003 |
| AGS geotechnical files, borehole CSV | data | not exported | CB-REAL-012 |
| SWMM-class input files | data (network, catchments, storage) | data | CB-IO-009 |
| EPANET-class input files | data | data | CB-IO-009 |
| railML | not imported | data | CB-IO-010, [OQ-13](../product/open-questions.md) |
| BCF 2.1 and 3.0 | data | data | `arc-io-bcf` |
| Pay item catalogs (CSV, documented structured format) | data | data | CB-QTY-009 |
| CSV and XLSX reports | not applicable | data | Report templates |

## Mapping principles

- Format crates in `arc-core` produce neutral models of each format; `civilbuilder-io` owns every
  mapping into and out of the civil model.
- Imports map to the richest object the source supports: a LandXML alignment becomes an editable
  alignment with element constraints inferred (tangency checked, fixed where unknown), not a polyline.
- Exports derive from the current revision only; stale derived data is rebuilt (or the export is
  refused with the stale list when run headless under a frozen policy).
- Coordinates are transformed through the document coordinate reference; every export writes CRS and
  units explicitly (IFC map conversion and projected CRS, LandXML coordinate system element, GIS CRS).
- Stations, superelevation and cant export with their native semantics, not as sampled points, where
  the format supports it.
- Identifiers round-trip: IFC GlobalIds derive from object identifiers; LandXML and DXF carry
  identifiers in names or extended data; re-import matches on them (CB-IO-015).
- Codes map to IFC classifications through a mapping table that is part of the export profile
  ([OQ-15](../product/open-questions.md)).

## Validation

- Connector packages validate against the published exchange package schema and the `arc-core`
  conformance suite before any object is created (CB-CONNECT-013).
- LandXML exports validate against the published schemas; IFC exports validate with an independent
  IFC reader and schema checks in continuous integration; DXF exports reopen in an independent reader.
- Round-trip tests (import, export, re-import) compare objects semantically with tolerances.
- Hydraulic exports run in the reference engines and compare results with the internal run.
- Test files come from the corpus repositories with owner, licence and checksum rows; no vendor sample
  files are used.

## Loss reporting

Every import produces a loss report listing, per source item: mapped, approximated (with the
approximation stated, for example spiral type substituted), preserved as foreign data, or dropped
(with the reason). The original file is stored in the document package, and unmapped content is kept
as preserved foreign data so a later export to the same format can include it. Exports produce a
report of objects or properties the target format cannot carry.

## Connectors, bridges and open readers

Native civil design objects held in other applications' drawings and concept models (surfaces,
alignments, profiles, corridors, pipe networks, parcels, points, figures, and styles where they map)
are exchanged through three routes, in this order of preference:

1. **Open readers** for formats with a published specification or a permissively licensed open-source
   reader, read natively behind an `arc-io-*` crate (DGN V7).
2. **Connectors**, add-ins running inside the user's own licensed copy of the other application
   through its public API, which read and write the Arc exchange package. They live in the
   `arc-connectors` repository. CivilBuilder reads and writes the package in `civilbuilder-io` and
   applies it through the same import path as any other format (CB-CONNECT-012).
3. **User-licensed bridges**: a conversion library that the user has installed and licensed, called
   as a separate process. It is never distributed with Arc and no core workflow requires it
   (CB-CONNECT-014).

All three produce the loss report, source identifier map and preserved foreign data described below.
The exchange identifier map is kept on both sides so that repeated round trips update objects
(CB-CONNECT-009), and each side's revision stamps detect changes on both sides before anything is
overwritten (CB-CONNECT-010). Mapping of assemblies and styles is partial by nature: what does not
map is preserved as foreign data and listed, never dropped silently. LandXML and IFC 4.3 stay the
default for any application that exports them well.

## Deliberately unsupported

Reverse engineering undocumented formats or binaries, running compiled or protected script files of
other applications, and codecs whose licence forbids open distribution are excluded because each is
a legal problem. The rows below are formats that CivilBuilder does not read or write directly, with
the route that exists instead.

| Format | Reason | Exchange instead |
|---|---|---|
| Proprietary point cloud project formats | No published specification | LAS, LAZ, COPC, E57 |
| Manufacturer machine-control formats without published specifications | Specification not public | LandXML, IFC 4.3, 3D DXF; plug-ins where a manufacturer publishes a format ([OQ-19](../product/open-questions.md)) |
| Instrument raw formats without published specifications | Specification not public | LandXML survey data, field book format, open observation formats (CB-SURV-033, CB-SURV-035), plug-ins ([OQ-02](../product/open-questions.md)) |
