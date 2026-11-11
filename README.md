# Axiomatic Software Design with RequirementsHCL

RequirementsHCL describes software requirements, design choices, and their effects in `.ad.hcl` files.
This repository contains the language specification. A Go implementation is intended but is not implemented.
Authors and reviewers can inspect incomplete designs without treating unknown effects as zeros.

A functional requirement (FR) states an outcome.
A design parameter (DP) controls an outcome.
You write needs, FRs, DPs, influences, decisions, and module contracts.
The specification defines these derived reports:

- Sibling matrices with supported and conditional classifications.
- A master matrix with explicit effects and parent refinement obligations.
- Module junctions and required design sequences.
- Change impact across parent contracts and branches.
- A dependency matrix that distinguishes unknown effects from zeros.
- Source-positioned errors, coverage gaps, and evidence limits.

## Specification and implementation status

Read [the language reference](docs/language.md) for the authoritative syntax and semantics.
The intended Go tool will use `github.com/hashicorp/hcl/v2` and native HCL syntax.
No Go executable or supported command workflow exists yet.

The accepted design separates core `.ad.hcl` facts from tool attachments in `.ad.ext.hcl` files.
A `.ad.project.hcl` manifest lists the core files, attachment files, and trusted installed extension owners.
Core-only models can remain one file or a directory of `.ad.hcl` files.

The earlier Python experiment and its generated views are available in Git history.
They do not implement the current specification.
The last commit that contains them is `9fef41f`.

## Examples and historical reports

The examples have different evidence limits:

- `examples/library_system/` reconstructs Kim, Suh, and Kim (1991), with unresolved synonym premises. It shows a model that spans several files.
- `examples/rib_design.ad.hcl` reconstructs the same paper, with conditional molding effects and retained coupling.
- `examples/robot_calibration.ad.hcl` retains an unverified transcription and unnamed modules from Hintersteiner and Nain (1999).
- `examples/requirements_hcl.ad.hcl` models the planned core pipeline and extension owners. Their independence remains conditional.

The rib example retains different evidence limits in its two contexts.
The tight context selects the stated warpage effect.
The relaxed context leaves that effect unknown because the source supplies no replacement model.
An omitted context does not establish unconditional independence.

Read [the design rationale](docs/design-rationale.md) for the conditional architecture and its acceptance criteria.
The [dated review](docs/review-2026-10-28.md) records historical findings about the Python experiment.
The [accepted extension RFC](docs/rfc-uncoupled-language.md) records the adopted attachment design and the limits of whole-language independence.
Its historical baseline run is not validation of the adopted specification or evidence of a Go implementation.

The [assessment contract](docs/assessment-contract.md) defines deterministic assessment rules from the November review.
The language self-design records proposed controls and explicit evidence gaps.
