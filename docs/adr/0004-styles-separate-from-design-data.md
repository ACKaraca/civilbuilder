# 0004 Styles and labels as resources separate from design data

- Status: Accepted
- Capabilities: CB-STY-001 to CB-STY-024, CB-PLAN-008, CB-PLAN-010

## Context

Civil documents carry large numbers of display styles, label styles and tables. When display
settings are entangled with design objects, style changes trigger recomputation, standards drift
between documents, and audits are impractical. Organizations maintain standards as templates that
are hard to review or version.

## Decision

- Style resources are separate document resources; design objects store only a style identifier and
  label attachments.
- No regeneration node takes a style as input. Display is produced by a presentation pass that reads
  design data and resolved styles and writes viewport display lists or `arc-draft` entities.
- Label content uses property fields and expressions from the shared `arc-solve` expression engine;
  labels read design data and never write it.
- Styles support single-parent inheritance; libraries are text-diffable files referenced by documents,
  with a resolved local copy in each document and difference-based updates.

The full design is in [styles and labels](../architecture/styles-and-labels.md).

## Consequences

- Re-styling is fast and safe; it cannot change quantities or geometry.
- Standards are reviewable as text, versioned, and auditable headless (CB-STY-022).
- Every label type must publish its anchor names and properties as a stable contract.
- Labels that need computed values not exposed as properties require adding properties to the object
  type, not computing them in the style.

## Alternatives considered

- **Display properties stored on each object.** Rejected: no shared standards, high document size,
  no audit.
- **Styles as opaque binary resources in templates.** Rejected: not reviewable or diffable.
- **Unrestricted scripting inside labels.** Rejected: unbounded cost and possible side effects;
  expressions cover the need.

## Trigger to reopen

Reopen if a required annotation cannot be expressed with properties and expressions after adding the
missing properties to the object type.
