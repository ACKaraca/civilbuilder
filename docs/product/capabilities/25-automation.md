# Automation and extensibility

This area exposes CivilBuilder to scripts, node graphs, plug-ins, batch jobs and assistants through
the suite command model and automation protocol. Every capability in the other areas is reachable
from here without a dialog.

## Domain objects

- **Command**: a registered, typed, undoable operation with a parameter schema.
- **Query**: a read-only typed request (station, elevation, section, volume).
- **Node graph**: an `arc-nodes` graph using civil nodes, saved in the document or a library.
- **Plug-in package**: a sandboxed WebAssembly module with a manifest.
- **Report template**: a definition that turns query results into HTML, PDF or CSV.
- **Check rule**: a named rule evaluated on the model with findings.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-AUTO-001 | Complete command coverage | Every civil operation is a registered command with a parameter schema and a non-interactive run, appears in the command palette, and records into macros. | T1 | 3 |
| CB-AUTO-002 | Automation protocol | Commands and queries are available through the Arc Automation Protocol over stdio or a local socket, with the same validation and undo behavior as interactive use. | T1 | 3 |
| CB-AUTO-003 | Civil queries | Typed read-only queries return station and offset, point at station, profile elevation and grade, surface elevation and samples, corridor section at a station, material volumes and check findings. | T1 | 3 |
| CB-AUTO-004 | Headless CLI | `civilbuilder-cli` opens documents, runs commands, scripts and graphs, rebuilds, validates, exports (LandXML, IFC, PDF sheets), generates reports and compares documents, with documented exit codes for continuous integration. | T1 | 3 |
| CB-AUTO-005 | Python client | The official Python client wraps the automation protocol with typed functions for commands and queries, and runs out of process. | T1 | 3 |
| CB-AUTO-006 | Civil node graphs | Node graphs use civil nodes to create and modify objects (alignments from data, points, profiles, corridors, style assignments) by issuing commands; one graph engine and editor serve cross-section components and automation. | T2 | 4 |
| CB-AUTO-007 | Graph player | A graph runs with exposed inputs in a simple form, without opening the editor. | T2 | 4 |
| CB-AUTO-008 | Plug-ins | Sandboxed WebAssembly plug-ins add commands, import and export formats (for example instrument and machine-control formats), design checks, report functions and label functions. Plug-ins have no ambient file or network access and act only through commands in transactions. | T2 | 4 |
| CB-AUTO-009 | Report templates | Report templates are user-editable files that query the model and produce HTML, PDF and CSV; every report in the product is defined this way. | T1 | 3 |
| CB-AUTO-010 | Custom check rules | Rules registered by scripts or plug-ins appear in check panels beside built-in criteria checks. | T2 | 4 |
| CB-AUTO-011 | Headless model checking | The CLI runs checks (criteria compliance, standards audit, reference validity, rebuild failures) and writes findings as BCF and JUnit-style reports for continuous integration. | T2 | 3 |
| CB-AUTO-012 | Batch processing | Scripts and graphs run across all documents of a folder or Arc Hub project, with a per-document result log. | T2 | 4 |
| CB-AUTO-013 | Change events | Protocol clients subscribe to object changes and regeneration completion events. | T2 | 3 |
| CB-AUTO-014 | Model Context Protocol endpoint | The command registry and queries are exposed through a Model Context Protocol endpoint derived from the same schemas. | T2 | 4 |
| CB-AUTO-015 | Optional assistant | An optional, provider-neutral assistant proposes command sequences that the user previews and applies explicitly; no document content leaves the machine without an explicit user action. | T3 | 5 |
