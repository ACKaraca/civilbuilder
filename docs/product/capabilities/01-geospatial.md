# Coordinate systems and geospatial data

This area places every CivilBuilder document on the earth and lets geospatial sources take part in
design without a conversion step. It covers coordinate reference systems, datums, ground and grid
coordinates, units, and live geospatial layers that are referenced rather than copied.

## Domain objects

- **Coordinate reference record**: horizontal CRS, vertical reference, transformation pipeline and
  local origin of a document.
- **Scale settings**: grid scale factor, elevation factor and combined factor used for ground
  coordinates.
- **Geospatial source**: a referenced vector, raster, elevation or web-service layer with its own CRS.
- **Attribute mapping profile**: a saved rule set that maps source attributes to model properties.
- **Tile cache**: local storage of streamed imagery and elevation tiles with a size limit.

## Coordinate reference

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-GEO-001 | Document coordinate reference | Every document stores a horizontal CRS, a vertical reference and linear units in its coordinate reference record. Changing the CRS of a document that contains geometry requires choosing between reprojecting the geometry and reassigning the CRS; the command reports the maximum displacement before it commits. | T1 | 3 |
| CB-GEO-002 | CRS catalog | The user searches an offline catalog by code, name or area of use; each entry shows its definition as WKT2 and its area of use on a map. The catalog ships with the application and works without a network. | T1 | 3 |
| CB-GEO-003 | Local and custom grids | The user defines a local engineering grid by origin, rotation and scale, or by fitting a similarity transformation to two or more control point pairs. The fit reports residuals per point and the resulting parameters. | T1 | 3 |
| CB-GEO-004 | Datum transformations | When source and target datums differ, the application lists candidate transformation pipelines ranked by stated accuracy and area of use, and uses grid-based transformations when the grid files are present. The chosen pipeline is recorded in the document so the same input always produces the same coordinates. | T1 | 3 |
| CB-GEO-005 | Vertical datums and geoid models | Elevations convert between ellipsoidal and orthometric heights through a selected geoid grid. Each elevation source records its vertical datum, and an import whose vertical datum differs from the document is flagged before commit. | T2 | 3 |
| CB-GEO-006 | Ground and grid coordinates | The application computes grid scale factor, elevation factor and combined factor at a point or as a project average. Geometry is stored in grid coordinates; a ground display mode scales displayed and reported distances, and every reported distance states whether it is grid or ground. | T1 | 3 |
| CB-GEO-007 | North references and convergence | The application reports grid north, true north and magnetic north (from a user-entered declination or a declination model and date) and the convergence angle at any point. Directions display as bearings or azimuths referenced to the chosen north. | T2 | 3 |
| CB-GEO-008 | Local origin and precision | Geometry is stored in meters in the document CRS with f64 coordinates and a local origin near the project; display and export always use full CRS coordinates. Viewports render relative to the camera so georeferenced coordinates keep sub-millimeter precision. | T1 | 3 |
| CB-GEO-009 | Display units and formats | Linear units (meter, international foot, US survey foot), angle formats (degrees-minutes-seconds, decimal degrees, gradians) and station formats are document settings. Changing a display unit never modifies stored values. | T1 | 3 |
| CB-GEO-010 | Project location | The user sets an approximate project location by entering coordinates or picking a point on a basemap. The application then proposes CRSs whose area of use contains the location. | T2 | 3 |
| CB-GEO-011 | Coordinate conversion tools | The user converts coordinates between any two catalog CRSs, computes geodetic inverse and forward problems on the ellipsoid, and sees the cursor position in up to three CRSs at once. | T2 | 3 |
| CB-GEO-012 | Georeference check on import | Every import declares or asks for its CRS. If the imported extent lies outside the area of use of the document CRS, or far from existing data, the import shows the mismatch and waits for confirmation. | T1 | 3 |

## Geospatial sources

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-GEO-013 | Vector sources as live layers | GeoPackage, Shapefile, GeoJSON, FlatGeobuf, KML and delimited text with coordinates attach as referenced layers that are reprojected on the fly to the document CRS. Attached features are visible, selectable and queryable but are not copied into the model. | T1 | 3 |
| CB-GEO-014 | Raster imagery | GeoTIFF, Cloud Optimized GeoTIFF and images with world files attach as referenced layers. Overview pyramids build in the background, and imagery drapes over surfaces in 3D views. | T1 | 3 |
| CB-GEO-015 | Elevation rasters | Elevation rasters attach as context layers and can be used directly as surface definition items (CB-SURF-011) without an intermediate conversion. | T1 | 3 |
| CB-GEO-016 | Web map services | The user configures WMS, WMTS, WFS, OGC API Features, OGC API Tiles and XYZ tile endpoints. No service is preconfigured or required; layers stream through the tile cache and remain usable offline from cached content. | T2 | 4 |
| CB-GEO-017 | Streaming and offline cache | Imagery and elevation stream by level of detail over areas of 100 km and more with a configurable cache limit. The user can prefetch a polygon at chosen levels for offline work. | T2 | 4 |
| CB-GEO-018 | Attribute filters and spatial queries | Layers filter by attribute expressions and by spatial relations (inside a boundary, within a distance of an alignment, intersecting an object). Filters are saved with the layer and update when the source changes. | T2 | 3 |
| CB-GEO-019 | Feature conversion to design objects | Selected features convert into design objects through commands: lines to alignments or feature lines, points to survey points, polygons to parcels or boundaries, linear assets to network parts. Converted objects keep the source feature identifier and attribute mapping profile. | T1 | 3 |
| CB-GEO-020 | Source refresh | When a source changes, context layers update automatically. Objects converted from it list added, changed and removed source features, and the user applies the differences through a command. | T2 | 4 |
| CB-GEO-021 | Attribute mapping profiles | A mapping profile assigns source attributes to model properties (for example invert elevation, diameter, material) with unit conversion and default values. Profiles are saved in libraries and reused across imports and refreshes. | T2 | 3 |
| CB-GEO-022 | Rule-based layer display | Context layers display through attribute-driven rules for color, symbol, line style, extrusion height and texture, in plan and 3D. Rules are style resources (CB-STY-001) and do not alter source data. | T2 | 4 |
| CB-GEO-023 | Export to GIS formats | Design objects export as GeoPackage, Shapefile or GeoJSON features with their properties as attributes, in the document CRS or a chosen CRS. | T1 | 3 |
