# 0005 Hydraulic engines behind a process boundary

- Status: Accepted
- Capabilities: CB-HYD-006, CB-HYD-007, CB-HYD-018, CB-HYD-019, CB-ANL-006, CB-IO-009

## Context

Storm, sewer and pressure network analysis requires validated solvers. The public-domain EPA SWMM
and EPANET engines are the reference implementations practitioners and agencies trust, but they are
written in C. Linking them would bring `unsafe` FFI into the product and let a solver fault terminate
the application. Writing new solvers from scratch first would delay analysis and leave results
without a trusted reference.

## Decision

- `civilbuilder-hydraulics` translates design objects into an analysis model and keeps a mapping from
  every solver element to its design object.
- Analysis runs in a separate worker process that speaks a documented message protocol (model in,
  progress and results out). The first workers wrap the reference SWMM-class and EPANET-class engines
  built from their published sources; they communicate through each engine's documented input format
  and result files.
- No solver code links into the desktop application or the model crates; a worker crash produces a
  failed run with its log.
- Results are revision-tagged and stale when the model changes. Native Rust solvers may replace a
  worker once they match the reference engines on the result corpus within the tolerances set by
  [OQ-08](../product/open-questions.md).

## Consequences

- Analysis results are comparable with the reference engines from the first networks release.
- The product keeps the suite rules on `unsafe` and crash isolation; the worker binaries are
  separate build artifacts with their own licence records.
- Process start and file exchange add overhead, acceptable for runs measured in seconds or longer;
  interactive design checks (cover, slope) stay in the model crates.
- The same boundary serves flood screening and later traffic engines.

## Alternatives considered

- **Linking the engines through FFI.** Rejected: `unsafe` in the product and no crash isolation.
- **Native Rust solvers only.** Rejected for the first release: no trusted reference results and a
  long path to validation.
- **Export-only workflow to external tools.** Rejected: loses the automatic model derivation and
  result display that make analysis part of design; export remains available (CB-IO-009).

## Trigger to reopen

Reopen when a native solver matches the reference corpus, or if process overhead prevents a required
interactive analysis.
