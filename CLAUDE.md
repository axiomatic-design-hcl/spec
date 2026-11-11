# CLAUDE.md

## What this repo is

The specification of an HCL-based language for Axiomatic Design (AD) of
software, working name **RequirementsHCL**, file extension `.ad.hcl`.

It is a typed, machine-checked spec that gives AI-based development a model
of the software: needs, functional requirements (FRs), design parameters
(DPs), process variables (PVs), the influences between them, design
decisions, modules and runtime flow. A tool derives the design matrices,
classifies coupling and checks the method rules.

`.ad.hcl` holds requirements, design decisions, and coupling analysis.
Behavior links use attachments with a separate owner. Terraform holds
infrastructure. In AD terms, Terraform resources and code paths are process
variables (PVs) that realize DPs.

## Layout

```
docs/language.md          language reference (blocks, attributes, rules)
docs/design-rationale.md  the language analysed with AD itself, and why v0 changed
docs/references.md        papers, what each contributes, known errata in them
examples/                 source reconstructions and the proposed language self-design
examples/library_system/  the library model split over several files
```

## Implementation status and verification

The planned tool uses Go `github.com/hashicorp/hcl/v2` for native HCL syntax.
The Go tool is not implemented. Do not invent its executable name or commands.
The earlier Python experiment is available in Git history at commit `9fef41f`.
Its behavior does not define the current specification.

The specification accepts core files, core directories, and explicit `.ad.project.hcl` manifests.
A manifest lists core `.ad.hcl` files, `.ad.ext.hcl` attachment files, and installed extension owners.
Attachments own tool-specific bindings, external behavior links, and presentation configuration.
Core `import` and `module.handles` are removed, with no compatibility aliases.

Split a core model by domain and branch, never into separate FR and DP files.
Never author a matrix file. See `docs/language.md` for the authoritative contracts.
After a specification or example change, exercise its HCL with the native Go parser.
Parsing alone does not prove typed resolution, owner behavior, or AD conclusions.
Keep implementation acceptance work distinct from measured results.

Historical Python runs reported the following conditional structural results.
They are not conformance evidence for the adopted specification or unconditional independence claims:

- Library: decoupled / decoupled / coupled / uncoupled. Conditional junctions
  are C, C, S, F, as in Fig. 5 of Kim et al. (1991).
- Rib: decoupled three times, then coupled under DP21 in `tight_warpage`.
  The relaxed context leaves the cross-section model unresolved.
- Robot: a conditional decoupled 7×7 mapping. Seven missing-module gaps are
  warnings in the source profile. The matrix transcription remains unverified.
- RequirementsHCL: conditional uncoupled / decoupled / decoupled. The
  `semantic_changes` context also passes the architecture profile.
  Supported independence remains unresolved because the premises lack evidence.


## Core principles of the language

1. Write each fact once. Never write derived facts by hand: IDs and
   numbering, matrices, classification, design order, S/C/F junctions,
   information content, implementation status. `expect` blocks are
   assertions (tests), not data.
2. Influences are a flat list of edges. The tool decides whether each one
   belongs to a sibling matrix or crosses branches. An unlisted cell means
   "unknown", not zero.
3. `effect = "none"` needs `because`. `effect = "material"` needs a
   `mechanism`. Mark mechanisms that are not stated by the source with
   `mechanism_source = "inferred"`.
4. A design decision (`decision`: proposed | selected | rejected |
   superseded) is authored. Implementation and verification status are
   derived from PV bindings and evidence.
5. Keep the core schema small and stable. Tool-specific bindings belong in
   attachments to PVs, behavior links in attachments to modules, and views in
   attachments to designs. Owners cannot change core facts or one another's inputs.
6. Probability estimates require qualified joint empirical `evidence`, including
   the candidate version, context, workload, horizon, predicates, and sampling model.
   Zero failures never establish p = 1. Missing evidence leaves information unknown.
7. Facts from a source cite it (`cites = source.x`). Statements copied from a
   paper are verbatim. Anything Claude adds is marked `origin = "inferred"`
   or `mechanism_source = "inferred"`.

## Conventions

- Write block labels in snake_case. Use `alias` for the IDs a source uses
  (FR11, DP121, M22).
- Write comments and prose in the examples in plain, simple English.
- When you design or review with the method, use the
  `axiomatic-software-design` skill.
- Do not invent acceptance criteria, mechanisms or probabilities for a source
  example. Leave the gap and let `validate` report it.

## Open work

See the syntax limits and implementation boundaries in `docs/language.md`.
The Go tool, typed project loader, extension owners, and live observations remain unimplemented.
