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

The [field schema](docs/schema.md) defines exact types, references, and absence rules.
The [assessment contract](docs/assessment-contract.md) defines how the tool derives qualified conclusions.
The [diagnostic contract](docs/diagnostics.md) defines rule codes, profile severity, and partial failure.
These contracts apply together.

The accepted design separates core `.ad.hcl` facts from tool attachments in `.ad.ext.hcl` files.
A `.ad.project.hcl` manifest lists the core files, attachment files, and trusted installed extension owners.
Core-only models can remain one file or a directory of `.ad.hcl` files.

The earlier Python experiment and its generated views are available in Git history.
They do not implement the current specification.
The last commit that contains them is `9fef41f`.

## Examples and historical reports

The examples have different evidence limits:

- `examples/requirements_hcl.ad.hcl` models the planned core pipeline and extension owners. Its independence remains conditional.
- `examples/starter/` contains a small architecture model, a manifest, and all three attachment roles.
- `conformance/core-1/` contains versioned inputs and expected findings for future implementations.

The starter uses proposed criteria and authored influence arguments.
It supplies no measured implementation evidence or accepted qualitative review.
Its external owner results remain unknown without caller-supplied observations and behavior models.
The conformance expectations are acceptance rules, not observed validator output.

Historical library, rib, and robot reconstructions are not present in this checkout.
Their earlier results do not establish conformance with the adopted contracts.
Read [the design rationale](docs/design-rationale.md) for the conditional architecture and its acceptance criteria.
The [November review](docs/review-2026-11-11.md) records the gaps that motivated the schema and assessment contracts.

The [assessment contract](docs/assessment-contract.md) defines deterministic assessment rules from the November review.
The language self-design records proposed controls and explicit evidence gaps.
