# AGENTS.md

Guidance for people and agents working in the CivilBuilder repository.

## What this repository is

CivilBuilder: the Arc application for civil infrastructure design (survey, surfaces, alignments,
profiles, corridors, grading, parcels, networks, hydraulics, rail, bridges, concept modeling, swept paths).
Rust end to end, built on `arc-core`; native documents are `.civilb` Arc document packages.

## Status and where to start

Design phase: no code and no builds exist. Read in this order: `README.md`, `docs/product/vision.md`,
`docs/product/capabilities/README.md`, `docs/architecture/overview.md`,
`docs/architecture/domain-model.md`, `docs/architecture/dependency-chain.md`, `docs/roadmap.md`,
`docs/adr/README.md`.

## Repository layout (target)

```
crates/civilbuilder-model/       domain objects, rules, regeneration nodes (headless)
crates/civilbuilder-commands/    commands and queries (headless)
crates/civilbuilder-io/          format mappings (headless)
crates/civilbuilder-hydraulics/  hydraulic engine boundary (headless)
crates/civilbuilder-ui/          tools, panels, editors (egui)
apps/civilbuilder/               desktop application (wiring only)
apps/civilbuilder-cli/           headless CLI and automation protocol server
docs/                            product, architecture, roadmap, ADRs
xtask/                           workspace tasks
```

## Commands

No build exists yet. Once code lands, these apply:

- `cargo fmt --check`
- `cargo clippy --workspace --all-targets -- -D warnings`
- `cargo nextest run --workspace`
- `cargo xtask layers`

## Suite rules

These rules apply in every Arc repository. The canonical text is
[`docs/engineering/agent-rules.md`](https://github.com/ACKaraca/arc-suite/blob/main/docs/engineering/agent-rules.md)
in `arc-suite`; change it there first.

1. **A person is accountable.** Whoever runs an agent answers for what it submits.
2. **Start from an issue.** Search issues and pull requests, check that nobody else is assigned,
   assign yourself and set the status to *In Progress* before changing files. When you finish,
   comment with what changed, the commit or pull request link and open items, then update the status.
   *Done* requires met and verified acceptance criteria.
3. **Verify, do not guess.** Open a definition before using it. Confirm a cause in the code.
4. **The document is the authority and everything is a command.** No change reaches a document
   except through a validated command inside a transaction. Programmatic paths never open dialogs.
5. **Respect the layers.** A crate depends only on lower layers. Nothing below the UI layer depends
   on windowing, GPU or UI crates. Products never depend on other products.
6. **Never crash, never lose work.** No `unwrap`, `expect`, `panic!`, `todo!` or `unreachable!` in
   production code. No `unsafe` outside the FFI crates named in an ADR. Treat every file and message
   as hostile: bound recursion, allocation and counts. A crash fix ships with a regression test.
7. **Clean room.** Implement from published specifications, observed behavior and original
   reasoning. Never copy or consult another product's code, decompiled output, file-format reverse
   engineering, documentation text, icons, fonts, templates or sample files. Do not name our
   features after another company's features.
8. **Licenses.** Add a dependency only if its license is on the allowlist in
   `docs/engineering/dependency-policy.md` in `arc-suite`. Record every asset's origin and license.
9. **Rust only in desktop applications.** No web view, no JavaScript or TypeScript.
10. **Small, tested changes.** One concern per pull request, with the test that fails without it.
    Update the documents that describe the behavior you change in the same pull request.
11. **Report only what ran.** Say what you tested and what you could not run.
12. **Ask a human before** adding a license outside the allowlist, publishing or releasing,
    changing a file format or public protocol, adding a new repository or remote, spending money,
    handling secrets, or any destructive git operation. Otherwise keep working.
13. **Keep secrets and personal data out** of repositories, logs and requests.
14. **Commit directly to `main` for now.** Until the project has a second maintainer and this
    repository has reached its MVP release (for `arc-suite` and `arc-core`: the first product MVP),
    work on `main`: no feature branches and no pull requests. Wherever these rules or the documents
    say "pull request", read "commit". Run the checks before every push and name the issue in the
    commit message. This rule is temporary and is deleted from a repository when that point is
    reached.

## Repository-specific invariants

- The civil model lives in the `.civilb` document package, never in drawing entities; sheets use
  `arc-draft`; DWG/DXF are exchange formats only (ADR-0001).
- Derived data (station sections, surfaces, sections, volumes, analysis results) carries the revision
  it was computed from; a stale result is never shown as current.
- Linear changes invalidate by station range; incremental rebuild must equal full rebuild (ADR-0002).
- Component definitions are deterministic, side-effect free and bounded; they read only declared
  inputs (ADR-0003).
- Styles never feed regeneration; labels read design data and never write it (ADR-0004).
- Hydraulic solvers run only in worker processes; no solver code links into product crates (ADR-0005).
- Concept objects are the same types as detailed objects; refinement keeps identifiers (ADR-0006).
- Lengths in meters, angles in radians, f64 in the document CRS; tolerances come from `arc-base`.
- Every import writes a loss report and keeps the original file.
- Dependency cycles are rejected at commit with the objects on the cycle named.

## Documentation rules

- No mention of planning processes, internal research or conversations; never describe the product
  or a feature as derived from, a copy of, a substitute for or a counterpart of another product.
- Other companies' names only as formats and standards, in factual interoperability statements,
  once in the Positioning paragraph of `docs/product/vision.md`, and for libraries and standards.
- Use our own descriptive vocabulary; never name a feature after another vendor's feature.
- Each fact once; link suite-wide rules in `arc-suite` instead of copying them.
- Write behavior in original words; do not reproduce another product's documentation, dialogs or
  default value lists.
- Capability IDs are permanent and used once; status lives in issues, never in capability tables.

## Issue workflow

Search issues and pull requests first; confirm nobody is assigned; assign yourself and set
*In Progress*. Statuses: Backlog, Ready, In Progress, In Review, Blocked, Done. Labels: `type: *`,
`tier: 1|2|3`, `phase: 0…5`, `area: <token>`, `status: blocked`, `needs: verification`. On finishing,
comment with what changed, the commit or pull request link and open items; create follow-up issues
after searching for duplicates. Conventional Commits with DCO sign-off.

## Verification

Run the narrowest relevant check first (the affected crate's tests, then clippy and fmt for changed
files, `cargo xtask layers` when dependencies change). Report only what ran and what could not run.

## Ask a human about

Anything in suite rule 12; changes to the `.civilb` schema, the automation protocol or the hydraulic
worker protocol; new crates; shipping design criteria, vehicle data or catalogs whose licence is
unclear; and decisions listed in `docs/product/open-questions.md`.
