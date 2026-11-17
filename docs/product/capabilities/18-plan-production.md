# Plan production

This area produces construction documents from the model: sheet frames along alignments, match
lines, plan and profile sheets, section sheets, sheet sets and publishing. Sheets are layouts in the
shared drafting engine (`arc-draft`), as recorded in [ADR-0001](../../adr/0001-civil-model-in-document-package.md).

## Domain objects

- **Sheet frame set**: frames along an alignment with size, scale, overlap and orientation.
- **Sheet frame**: one frame with station range, rotation and number.
- **Match line**: a line between adjacent frames with station and sheet references.
- **Sheet template**: an `arc-draft` layout with named placeholders.
- **Sheet**: an `arc-draft` layout generated from a frame or a section arrangement.
- **Sheet set**: an ordered, numbered collection of sheets.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-PLAN-001 | Sheet frame sets | Frames generate along an alignment from the template viewport size and scale, overlap and station range, rotated to follow the alignment. Frames are numbered and individually movable, rotatable and resizable. | T1 | 3 |
| CB-PLAN-002 | Match lines | Match lines generate between adjacent frames with station and labels that reference the adjacent sheet numbers, and regenerate with the frames. | T1 | 3 |
| CB-PLAN-003 | Plan and profile sheets | Sheets generate per frame as plan-only, plan and profile, or profile-only layouts, with viewports rotated and clipped to the frame and title block fields filled from document and frame properties. | T1 | 3 |
| CB-PLAN-004 | Sheet templates | Templates are `arc-draft` layouts with named placeholders for plan viewport, profile viewport, north arrow and title block fields, stored in libraries. | T1 | 3 |
| CB-PLAN-005 | Profile views per frame | Profile views generate for each frame matching its station range, with the chosen view style and bands. | T1 | 3 |
| CB-PLAN-006 | Incremental sheet update | When the alignment, frames or model change, only affected sheets regenerate. Annotations added on sheets stay attached to model positions, and annotations that lose their position are listed. | T1 | 3 |
| CB-PLAN-007 | Section sheets | Section arrangements (CB-SEC-007) place onto sheets from a template with numbering. | T1 | 3 |
| CB-PLAN-008 | Annotation scale | Label and text sizes are specified in paper units and scale with each viewport, so one model serves several scales. | T1 | 3 |
| CB-PLAN-009 | Plan-readable orientation | Labels orient relative to the sheet rotation and flip to stay readable beyond a set angle. | T1 | 3 |
| CB-PLAN-010 | Viewport display sets | Each sheet viewport can apply a display set that overrides style components and visibility for that viewport only. | T2 | 3 |
| CB-PLAN-011 | Sheet sets | Sheets form ordered sets with numbering, a generated sheet index table and revision fields. | T2 | 4 |
| CB-PLAN-012 | Publishing | Sheets publish in batch to vector PDF with layers and to DWG or DXF, interactively or through the CLI. | T1 | 3 |
| CB-PLAN-013 | Drafting on sheets | The full drafting toolset of the shared drafting engine (dimensions, leaders, hatches, tables, blocks) is available on sheets and model views. | T1 | 3 |
