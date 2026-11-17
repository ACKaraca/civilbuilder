# Point clouds, reality data and subsurface

This area brings measured reality into the model: referenced point clouds and reality meshes,
classification, surfaces and features from clouds, as-built comparison, and geotechnical boreholes
with strata surfaces.

## Domain objects

- **Point cloud**: a referenced LAS, LAZ, COPC or E57 source with a spatial index and CRS.
- **Cloud region**: a clip box, polygon or slice with a classification filter.
- **Reality mesh**: a referenced textured mesh or tile set.
- **Deviation result**: distances between a cloud and a design surface or corridor.
- **Borehole**: location, collar elevation, strata intervals, groundwater and test values.
- **Stratum surface**: an interpolated surface of a stratum interface.

## Point clouds and reality meshes

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-REAL-001 | Point cloud attachment | LAS, LAZ, COPC and E57 sources attach by reference with their CRS; an out-of-core spatial index builds in the background into a cache beside the document, and billions of points display by level of detail. | T1 | 4 |
| CB-REAL-002 | Point cloud display | Points color by RGB, intensity, elevation, classification or return number, with adjustable point size, clip boxes and slices. | T1 | 4 |
| CB-REAL-003 | Classification | Classes are viewed and edited; automatic ground classification runs with documented parameters; points reclassify inside a region. Edits are stored as a layer over the unmodified source. | T2 | 4 |
| CB-REAL-004 | Snapping to clouds | Commands snap to cloud points, to the nearest point within a radius or to local surface fits. | T1 | 4 |
| CB-REAL-005 | Surfaces from clouds | A cloud region becomes a surface definition item with classification filter, thinning (grid minimum, mean, curvature-aware) and outlier removal (CB-SURF-012). | T1 | 4 |
| CB-REAL-006 | Feature extraction | Linear features (curb lines, edges, breaklines) are traced semi-automatically along the cloud from picked seeds and output as feature lines; pole-like objects are detected as points. | T3 | 4 |
| CB-REAL-007 | Cloud sections | Cloud slices display in profile and section views as projected points along alignments and sample lines. | T2 | 4 |
| CB-REAL-008 | As-built comparison | Deviations between a cloud and a design surface or corridor display as a color map within tolerance bands and report statistics per region. | T2 | 4 |
| CB-REAL-009 | Cloud volumes | Volumes between a cloud-derived surface and a base surface or plane are computed for stockpiles and progress measurement. | T2 | 4 |
| CB-REAL-010 | Control-point alignment | A cloud aligns to the document by a rigid or similarity transformation fitted to control point pairs, with residuals reported. | T2 | 4 |
| CB-REAL-011 | Reality meshes | Textured meshes (glTF, OBJ, 3D Tiles) attach as referenced context with CRS and display in 3D views. | T2 | 4 |

## Geotechnical data

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-REAL-012 | Borehole import | Boreholes import from CSV and AGS-format files with location, collar, strata intervals, groundwater and test values, and display as 3D columns. | T2 | 4 |
| CB-REAL-013 | Stratum surfaces | Stratum interface surfaces interpolate from borehole data and serve volumes (for example rock excavation) and sections. | T2 | 4 |
| CB-REAL-014 | Boreholes in views | Boreholes project into profile and section views as strata columns linked to their data. | T2 | 4 |
| CB-REAL-015 | Groundwater surface | A groundwater surface interpolates from borehole observations and displays in views and analyses. | T3 | 4 |
