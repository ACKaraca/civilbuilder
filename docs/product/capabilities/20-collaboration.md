# Shared references and collaboration

This area lets a project be split across documents and people: shared references to objects in other
documents, a project workspace, comparison of revisions, and collaboration through Arc Hub.

## Domain objects

- **Shared reference**: a read-only link from a consumer document to an object in a source document by document and object identifier.
- **Project workspace**: a folder or an Arc Hub project listing documents, references and libraries.
- **Reference graph**: the project-wide set of shared references between documents.
- **Comparison result**: the semantic differences between two revisions of objects.
- **Issue**: a BCF topic linked to objects, stations and views.

| ID | Capability | Behavior | Tier | Phase |
|---|---|---|---|---|
| CB-REF-001 | Referenceable objects | Every model object type can be the target of a shared reference, including points and point groups, surfaces, alignments, profiles, corridors and their outputs, networks, parcels, sample line sets and sheet frame sets. | T1 | 3 |
| CB-REF-002 | Creating shared references | A consumer document references objects of a source document by document and object identifier. Referenced geometry is read-only in the consumer; style and labels are set locally. | T1 | 3 |
| CB-REF-003 | Synchronization | Consumers detect when a source has a newer saved revision, mark affected references stale, and synchronize in one transaction that lists changed, added and removed objects. | T1 | 3 |
| CB-REF-004 | Promotion to local copy | A reference converts to a local, editable copy that records its source document, object and revision. | T1 | 3 |
| CB-REF-005 | Reference repair | When a source moves or is renamed, references relink by document identifier; unresolved references are listed and never deleted automatically. | T1 | 3 |
| CB-REF-006 | Objects built on references | Profiles, corridors, sections and other objects can depend on referenced objects; after synchronization they regenerate for the changed station ranges only. | T1 | 3 |
| CB-REF-007 | Reference graph and impact | A project view shows which documents reference which objects, and before a source object is edited the user can see which consumers it affects. | T2 | 3 |
| CB-REF-008 | Project workspace | A project workspace lists documents, references, libraries and templates; it works from a plain folder offline or from an Arc Hub project. | T1 | 3 |
| CB-REF-009 | Project-wide object browser | A table lists objects across all project documents with filtering and grouping; bulk changes (for example style assignments) execute as commands in each affected document. | T2 | 4 |
| CB-REF-010 | Hub file collaboration | Through Arc Hub, documents check out and in with locks, keep versions and lifecycle states, and take part in reviews and transmittals. | T1 | 4 |
| CB-REF-011 | Semantic comparison | Two revisions of a document or object compare semantically: changed elements of alignments and profiles, changed station ranges of corridors, surface elevation differences and volume changes, with a visual overlay. | T2 | 4 |
| CB-REF-012 | Element-level multi-user editing | Through Arc Hub, users borrow objects and exchange change sets from the operation journal, so several people edit one document concurrently; conflicting edits keep both versions for comparison. | T3 | 5 |
| CB-REF-013 | Issues | BCF issues link to objects, stations and saved views, and round-trip with Arc Review and Arc Hub. | T2 | 4 |
| CB-REF-014 | Federated building and structure context | ArchBuilder documents and IFC models attach as context in shared coordinates, read-only, for coordination with buildings and structures. | T2 | 4 |
| CB-REF-015 | Shared coordinates | Survey point, project base point and CRS are exchanged with other Arc documents through the document package metadata, so linked models align without manual transformation. | T1 | 3 |
