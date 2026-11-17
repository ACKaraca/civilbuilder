# Object styles, label styles and tables

This area controls how design data is displayed and annotated, without being part of the design
data. The mechanics are specified in [the style and label architecture](../../architecture/styles-and-labels.md).

## Domain objects

- **Object style**: display components per view direction for one object type.
- **Label style**: components anchored to object geometry, with content built from properties and expressions.
- **Label set**: a named group of label styles applied together.
- **Table style** and **table**: column definitions and a live table bound to objects.
- **Code style set**: display and labels for corridor codes.
- **Marker definition**: a symbol with plan, 3D, profile and section representations.
- **Style library**: a versioned, text-diffable collection of styles and settings.
- **Document settings**: units, precision, abbreviations and command defaults in a three-level hierarchy.

## Object styles

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-STY-001 | Object styles | Each object type has styles that define its display components (for a surface: border, triangles, contours, points, slope arrows) separately for plan, 3D, profile and section views, with layer, color, linetype, lineweight, transparency and visibility per component. | T1 | 3 |
| CB-STY-002 | Style separation | Every object references a style by identifier. Changing a style or an object's style reference changes display only and never triggers regeneration of design data. | T1 | 3 |
| CB-STY-003 | Code style sets | Code style sets map point, link and shape codes to display, labels and render materials in plan, 3D, profile and section views. | T1 | 3 |
| CB-STY-004 | Marker definitions | Markers have separate plan, 3D, profile and section representations and scale with annotation scale or model units by setting. | T1 | 3 |
| CB-STY-005 | View display overrides | A view or viewport overrides component visibility and appearance by object type or style without editing styles. | T2 | 3 |
| CB-STY-006 | Layer naming rules | Layer names for drafting output are generated per object type from templates with object property tokens. | T2 | 3 |

## Label styles

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-STY-007 | Label components and anchors | A label style has components (text, line, tick, marker, direction arrow, reference text) anchored to object geometry points (start, end, midpoint, station, insertion) or to other components, with offsets, justification, borders and background masks. | T1 | 3 |
| CB-STY-008 | Property content | Label text combines literal text with property fields of the labeled object, each with formatting for precision, units, rounding, sign, direction format and station format. | T1 | 3 |
| CB-STY-009 | Label expressions | Expressions compute values from object properties with arithmetic, conditions and text functions in the shared unit-aware expression language. An expression error shows in place of the value and in the style validation list. | T1 | 3 |
| CB-STY-010 | Label behaviors | Labels orient to the object, view or world, flip for plan readability beyond a set angle, and switch to a dragged state with leader and stacked layout when moved; a reset command restores the default position. | T1 | 3 |
| CB-STY-011 | Label sets | Named label sets (for example alignment stations, geometry points and station equations together) apply in one step and can be replaced as a unit. | T1 | 3 |
| CB-STY-012 | Live labels | Labels follow their objects and update their content whenever the referenced properties change. | T1 | 3 |
| CB-STY-013 | Reference labels | A label can reference other objects (station and offset from an alignment, elevation of a surface, grade of a profile) and updates when those objects change. | T1 | 3 |
| CB-STY-014 | Label style editor | The editor lists components, shows a live preview on a sample object, and shows which values are inherited and which are overridden. | T1 | 3 |
| CB-STY-015 | Collision avoidance | Labels in a view can optionally be displaced to avoid overlapping other labels, with leaders added when displaced. | T3 | 4 |

## Tables

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-STY-016 | Table styles | Table styles define columns with property fields and expressions, title, header and data rows, sorting, row filters and splitting into stacked or side-by-side parts by row count. | T1 | 3 |
| CB-STY-017 | Live tables | Tables of points, segments, curves, parcels, pipes, structures, quantities and pay items update when their objects change. | T1 | 3 |
| CB-STY-018 | Tags | Labels can be replaced by tags that reference table rows, with automatic and manual tag numbering. | T2 | 3 |

## Libraries, inheritance and settings

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-STY-019 | Style inheritance | A style can derive from a parent style and override selected values; changes to the parent propagate to every value the child does not override. | T1 | 3 |
| CB-STY-020 | Style libraries | Styles, label sets, table styles and settings are stored as text-diffable library files. A document references libraries and keeps a resolved copy; updating from a library shows a difference report before applying. | T1 | 3 |
| CB-STY-021 | Document templates | Templates carry settings, styles, label sets, criteria sets, components, catalogs and sheet templates, and new documents start from a chosen template. | T1 | 3 |
| CB-STY-022 | Standards audit | An audit compares the document with its libraries and lists missing, modified and unused styles; unused styles are purged through a command. The audit also runs headless in the CLI. | T2 | 3 |
| CB-STY-023 | Settings hierarchy | Settings for units, precision, abbreviations and defaults resolve from document to object type to command, and the effective value shows where it comes from. | T1 | 3 |
| CB-STY-024 | Style import and merge | Styles import from another document or library with a conflict choice per style (rename, overwrite, skip). | T1 | 3 |
