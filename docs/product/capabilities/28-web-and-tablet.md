# Web and tablet

This area covers field and review use of CivilBuilder in a browser and on tablets and phones, as
decided in
[suite ADR-0018](https://github.com/ACKaraca/arc-suite/blob/main/docs/adr/0018-web-and-mobile-targets.md):
viewing the model, inspecting design values at a position in the manner of a stakeout check, markups
and issues, and offline use. The browser build is the same Rust crates compiled to WebAssembly with
the same UI kit, and the tablet and phone builds are the same crates on iOS and Android. They are
targets of one code base, not separate applications, and they use the same document model, commands,
formats and Hub API as the desktop application.

These builds expose a subset of commands. Design editing, regeneration of large corridors and
hydraulic or other solver runs stay on the desktop; field builds show derived results that were
computed there and carried in the work package, each tagged with its revision.

## Domain objects

- **Field view**: a saved combination of visible objects, design option, camera and display set.
- **Work package**: the part of a document selected for field use, with its derived results, tile
  caches and sheets, stored on the device.
- **Field position**: a location from the device, a receiver streaming standard position sentences,
  or a picked point, with its CRS and a stated accuracy.
- **Field record**: an addition made in the field (check shot, markup, issue, photo) kept apart from
  design data until it is synchronized.

## Targets and interaction

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-TOUCH-001 | Browser build | CivilBuilder compiles to WebAssembly from the same crates and UI kit and opens documents from Arc Hub or from a local file in the browser. The page contains only the loader the platform requires. The build states which commands and views it supports. | T3 | 5 |
| CB-TOUCH-002 | Tablet and phone builds | The same crates build for iOS and Android with platform integration kept in `arc-app`. Documents open from device storage, Arc Hub or shared folders. | T3 | 5 |
| CB-TOUCH-003 | Touch and pen interaction | Pan, zoom, orbit, selection, snapping and measurement work with touch and pen input using the conventions of the `arc-ui` kit, with enlarged targets and a visible snap candidate before a point is accepted. | T3 | 5 |
| CB-TOUCH-004 | Limits and capability reporting | A command or view that exceeds the memory or threading limits of the target, or depends on a desktop-only function, is disabled with the reason shown. The user is never left with a partial result; large documents load by level of detail within the stated limits. | T3 | 5 |

## Viewing the model

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-TOUCH-005 | Model viewing | Plan, 3D, profile and section views of surfaces, alignments, profiles, corridors, networks, parcels and context display from the document, with object and layer visibility, design options and display sets. Stale or failed derived results are marked as in the desktop application. | T3 | 5 |
| CB-TOUCH-006 | Sheets and saved views | Published sheets and saved field views open for reading, with zoom to a sheet frame and linking from a sheet position to the model. | T3 | 5 |
| CB-TOUCH-007 | Measurement and queries | Distances, areas, slopes, station and offset to a chosen alignment, and the properties of a selected object are read in any view. | T3 | 5 |

## Inspection of design values at a position

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-TOUCH-008 | Field position | A position comes from the device location service, from a receiver that streams standard position sentences, or from a picked point. The position is transformed through the document CRS and its transformation, and its stated accuracy is always displayed. CivilBuilder does not control instruments. | T3 | 5 |
| CB-TOUCH-009 | Design values at a position | At a field position the application reports station and offset to the nearest alignments, design and existing surface elevations, cut or fill, cross slope, corridor region and component at that station, pipe invert and cover, and the parcel, each with the object and revision it came from. | T3 | 5 |
| CB-TOUCH-010 | Guided navigation to design points | From a stakeout list (CB-SURV-032) or a chosen object, the application shows direction, distance and the difference in elevation to the next target and advances through the list. | T3 | 5 |
| CB-TOUCH-011 | Check shots | A check shot stores the field position, accuracy, time and the design values at that position as a field record, and lists deviations against tolerance. Check shots export as CSV or LandXML and never modify design points. | T3 | 5 |

## Markups, issues and offline use

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-TOUCH-012 | Markups | Freehand, text, dimension and symbol markups are placed on views and sheets as a layer owned by their author. They are field records, anchored to object, station or coordinates, and do not alter design data. | T3 | 5 |
| CB-TOUCH-013 | Issues in the field | BCF issues are created with a saved view, linked objects or station, photos and an assignee, and round-trip with Arc Hub and Arc Review (CB-REF-013). | T3 | 5 |
| CB-TOUCH-014 | Work packages and offline use | A work package is prepared from a document by area, objects or sheets, with derived results and cached tiles included, and is stored in the sandboxed storage of the device. Viewing, position inspection, check shots, markups and issues work without a connection. | T3 | 5 |
| CB-TOUCH-015 | Synchronization of field records | Reconnected, the device sends its field records and receives updated issues and a newer work package through Arc Hub. Field records only add, so synchronization cannot overwrite design data; a package built on an older revision is marked as such. | T3 | 5 |
| CB-TOUCH-016 | Browser opening through Hub | A document opened from Arc Hub in a browser opens in the browser build of CivilBuilder, with the same locks, permissions and versions as in the desktop application. | T3 | 5 |
