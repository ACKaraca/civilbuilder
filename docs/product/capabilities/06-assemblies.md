# Cross-section components and assemblies

This area defines typical cross-sections. Cross-section components are parametric definitions
authored as node graphs inside CivilBuilder; assemblies arrange component instances around a
baseline attachment point and feed corridors.

## Domain objects

- **Component definition**: a node graph with typed parameters and targets that outputs points, links and shapes with codes.
- **Component instance**: a definition reference plus parameter values, side and attachment.
- **Component library**: a versioned collection of definitions and assemblies stored as text files.
- **Assembly**: a baseline attachment point with left and right chains of component instances.
- **Code**: a named point, link or shape code from the document code catalog.
- **Target input**: a declared surface, offset or elevation input of a definition.

## Components

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ASM-001 | Component definition | A definition is a node graph that, given parameter values, targets, attachment point, side and superelevation, outputs ordered points, links and closed shapes with codes. Evaluation is deterministic and has no side effects, so any station can be evaluated independently. | T1 | 3 |
| CB-ASM-002 | Component editor | A visual graph editor offers geometry nodes (point by offset and elevation, slope and distance, or intersection; links; shapes; auxiliary construction geometry), logic nodes (conditions, switches, bounded loops) and expressions. A live preview evaluates the graph with editable test targets. | T1 | 3 |
| CB-ASM-003 | Typed parameters | Parameters are typed (length, slope as percent or ratio, angle, integer, enumeration, boolean, text, code) with defaults, limits, units, descriptions and a schematic image region. Values outside limits are rejected at entry. | T1 | 3 |
| CB-ASM-004 | Target inputs | A definition declares surface, offset and elevation targets and states its behavior when a target is missing (use a default value or omit the dependent geometry). Missing targets are reported per station by the corridor. | T1 | 3 |
| CB-ASM-005 | Superelevation inputs | Definitions read lane and shoulder slopes, axis of rotation and breakover rules from the alignment superelevation set at the evaluated station. | T1 | 3 |
| CB-ASM-006 | Codes | Points, links and shapes carry one or more codes from the document code catalog. Codes drive corridor feature lines, surfaces, quantities, labels and display. | T1 | 3 |
| CB-ASM-007 | Definition tests | A definition carries test cases (inputs with expected outputs) that run in the editor and headless through the CLI, so a library can be verified in continuous integration. | T2 | 3 |
| CB-ASM-008 | Component libraries | Definitions and assemblies are stored as text-diffable files in versioned libraries with a manifest. Libraries are shared through folders or Arc Hub, and a document keeps a resolved copy so it opens without the library. | T1 | 3 |
| CB-ASM-009 | Standard component library | The application ships definitions for lanes with superelevation, curbs and gutters, sidewalks, shoulders, medians, ditches, daylight slopes, retaining walls, pavement layers, trenches, rail track, bridge decks, channel linings and generic links, slopes and widths. | T1 | 3 |
| CB-ASM-010 | Daylighting | Daylight definitions intersect the target surface using cut and fill slope rules that vary with height, benching with width and height, rounding, and a maximum width; when no intersection exists within the maximum width, the stated fallback applies and the station is reported. | T1 | 3 |
| CB-ASM-011 | Conditional geometry | Definitions branch on cut or fill condition, distance to a target, elevation difference and parameter values, so one instance adapts along a corridor. | T1 | 3 |
| CB-ASM-012 | Definition versions | Each definition has a version; updating a library offers instances the new version with a parameter mapping, and instances on an older version keep evaluating with their recorded version until upgraded. | T2 | 3 |

## Assemblies

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-ASM-013 | Assembly object | An assembly has a baseline attachment point and left and right ordered chains of component instances; each instance attaches to a named output point of the previous instance. | T1 | 3 |
| CB-ASM-014 | Assembly editing | Instances are inserted, replaced, reordered, copied and mirrored to the other side; one grid edits all instance parameters; codes can be renamed per instance. | T1 | 3 |
| CB-ASM-015 | Assembly preview | A section preview evaluates the assembly against sample targets and chosen superelevation states and shows codes and dimensions. | T1 | 3 |
| CB-ASM-016 | Secondary attachments | An assembly can attach part of its chain to an offset alignment and profile, so divided roads and lanes that follow offset baselines use one assembly. | T2 | 3 |
| CB-ASM-017 | Assembly libraries | Assemblies are saved to and inserted from libraries with their instance parameters. | T1 | 3 |
| CB-ASM-018 | Assembly validation | Validation reports unattached instances, missing codes, invalid parameters and unresolved definition versions before the assembly is used in a corridor. | T1 | 3 |
