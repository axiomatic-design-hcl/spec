# Design rationale: RequirementsHCL through Axiomatic Design

This page helps language authors review the design of RequirementsHCL and its
analyzer. It separates the abandoned experimental Python prototype from the
target architecture. The [self-design example](../examples/requirements_hcl.ad.hcl)
records the proposed core assessment pipeline. Neither document proves
implementation independence or completion of the planned Go tool.

A functional requirement (FR) states an outcome. A design parameter (DP)
states a mechanism that controls that outcome. A process variable (PV)
realizes a DP. This page treats architectural mechanisms as DPs. This adapts
Kim, Suh, and Kim (1991), which often uses input data as DPs and routines as PVs.
The skill's source notes explain this distinction.

## Boundary and evidence

The boundary covers authoring, syntax admission, typed resolution, candidate
selection, AD analysis, and reports. It also defines a future boundary for
binding observations. Deployment and enforcement of a designed system's runtime
behavior remain outside the analyzer.

The stakeholders are design authors, reviewers, AI agents, and automated
callers. Native HCL, language-neutral models, and separate external behavior
models are fixed choices. The planned tool uses Go `github.com/hashicorp/hcl/v2` for
native HCL syntax. Its expression policy admits literal values and static
traversals, not computed expressions, templates, or functions. Native numbers
and heredocs do not inherit the experimental Python parser's syntax limits.
The Python tool was never released and is not a future technology constraint.

The [2026-10-28 review](review-2026-10-28.md) supplies baseline observations,
not proof that the revised design meets its criteria. Its R1–R12 findings show
loss of facts, unsafe decoding, and conclusions without sufficient conditions.
No probe, probability measurement, or passing acceptance run is claimed here.

## Needs and proposed targets

The five needs retain their original identifiers. They state stakeholder
outcomes rather than chosen mechanisms. Drift detection remains a need even
though its implementation lies beyond the prototype.

| Need | Outcome | Reason |
|---|---|---|
| N1 | Preserve the meaning of an AD design. | Reviewers need to distinguish authored facts from conclusions. |
| N2 | Reject unsafe or ambiguous input. | People and AI agents need diagnostics instead of silent data loss. |
| N3 | Keep design changes and implementation evidence traceable. | An accepted design is not proof of its implementation. |
| N4 | Exchange design information with other tools. | Behavior, infrastructure, and design models retain separate ownership. |
| N5 | Make source changes and reports readable. | Reviewers need to locate each changed fact and its effects. |

The operating range includes incomplete designs, source reconstructions,
malformed input, alternative candidates, and named conditions. No scale,
latency, or availability threshold is supplied. The criteria below are proposed
acceptance predicates, not measured guarantees.

## Reconstructed prototype mapping

The baseline implementation combines responsibilities across `Parser`, `Model`,
and command functions. Its authored records do not imply that their intended
behavior exists. The review supplies the following reconstruction.

| FR | Existing mechanism | Baseline evidence and limit |
|---|---|---|
| FR1: preserve design meaning | Parser and model dictionaries | R1–R4 and R8–R10 show lost identity, overwritten facts, and incomplete typed resolution. |
| FR5: trace design changes | Decision, source, and lifecycle records | Records exist, but R9 shows that they do not select a coherent candidate. |
| FR3: detect implementation drift | PV declarations and proposed binding probes | Declarations exist. Observation adapters and drift comparison do not. |
| FR2: identify method violations | Validation and classification functions | R2–R4 show unsafe prerequisites and incomplete qualification. |
| FR4: present derived views | Matrix, master, junction, DSM, and impact commands | R1 and R7 show inconsistent cell resolution. R5 shows unreliable failure status. |

The original five-by-five implementation mapping is unresolved. Its drift
control is missing, and the claimed ownership boundaries lack evidence. A
read-only rule engine does not, by itself, establish the crucial zero below.

| Outcome / proposed control | DP3: observations and comparison | DP2: analysis policy |
|---|---|---|
| FR3: detect drift | ? until an adapter exists | ? |
| FR2: identify method violations | X when binding facts change realization findings | X as a proposed control |

DP2 → FR3 is zero only if DP3 owns both observation and drift comparison.
If DP2 decides whether observations constitute drift, both controls affect
both outcomes. That pairing contains a material cycle. Renaming the rule
engine or placing it behind an interface does not remove the cycle.

## Revised hierarchy

FR0 is the parent outcome: produce a traceable AD assessment for a named design
and condition. DP0 is a staged assessment pipeline with explicit ownership.
Selecting DP0 gives the following child outcomes. This is a target design,
not a statement that all stages exist.

| FR / needs | Proposed acceptance predicate | Selected design mechanism |
|---|---|---|
| FR1 / N1,N2,N5 | Accepted entities, values, references, and source positions retain identity. Invalid structure cannot enter dependent analysis. | DP1: a versioned syntax profile, schema, and typed resolver. |
| FR5 / N1,N3 | Every analyzed relation retains its candidate, origin, and applicable premises. Other alternatives remain available for review. | DP5: candidate snapshots and provenance records. |
| FR3 / N3,N4 | A seeded binding mismatch yields drift. Missing observations yield unknown, never verified. | DP3: observation adapters that own comparison with declared bindings. |
| FR2 / N1,N2 | Each conclusion states its scope, premises, evidence status, and unresolved obligations. A pairing alone cannot establish an effective diagonal. | DP2: one qualified influence model and pure analysis over it. |
| FR4 / N4,N5 | Reports agree on cells and findings for one snapshot. Invalid input and failed assertions produce failure status. | DP4: read-only reports and a command-line interface over common results. |

After selecting DP1, split FR1 into two children. FR1.1 admits the documented
syntax and expression profile. FR1.2 preserves valid AD entities and typed
links. DP1.1 owns syntax admission, while DP1.2 owns schema decoding and typed
resolution. Each child criterion contributes to FR1. Neither child inherits
the complete parent outcome without an explicit allocation.

The remaining branches stop at logical module contracts. They need no artificial
children to match the depth of FR1. The leaf contracts define responsibilities,
owned information, dependencies, failure behavior, and acceptance scenarios.
Implementation completion still requires evidence against those contracts.

The adopted attachment design adds a separate extension subtree. The pipeline
above does not model that subtree or prove its local diagonal. Keep its
conditional result separate from the core pipeline's conditional decoupled result.
Neither result establishes global independence.

## Conditional influence model

An influence matrix has FRs as rows and DPs as columns. `X` means a material
effect on the stated outcome. `0` means a defended absence of such an effect.
`?` means that the effect is unknown. A call alone does not establish `X`.

The following matrix is a semantic-change hypothesis. It applies within a fixed
schema version, fixed contracts, and one candidate and workload. It excludes
shared-resource failures and makes no performance claim. Every diagonal is a
proposed effective control, with a mechanism and a criterion to assess it.

| Outcome / control | DP1 | DP5 | DP3 | DP2 | DP4 |
|---|---|---|---|---|---|
| FR1 | X | 0 | 0 | 0 | 0 |
| FR5 | X | X | 0 | 0 | 0 |
| FR3 | X | X | X | 0 | 0 |
| FR2 | X | X | X | X | 0 |
| FR4 | X | X | X | X | X |

If the contracts hold and the intended controls meet their criteria, this
pairing is decoupled. Its design order is DP1 → DP5 → DP3 → DP2 → DP4.
Unvalidated premises leave support for that conclusion unresolved. The example
records them as `to_validate`, not as established facts.

The lower entries describe effects on acceptance predicates. Lost references
change traceability, binding comparison, conclusions, and report fidelity.
Candidate selection changes the applicable bindings and relations. Drift facts
change realization findings. Analysis changes the findings that reports must
preserve. None of these entries comes only from a dependency arrow.

The zeros require the following contracts:

| Zero region | Required reason |
|---|---|
| DP5, DP3, DP2, DP4 → FR1 | These controls cannot mutate the admitted graph or redefine its syntax and schema. A schema extension is a DP1 change. |
| DP3, DP2, DP4 → FR5 | These controls consume snapshots without changing candidate history or applicability policy. |
| DP2, DP4 → FR3 | Binding assessment owns comparison. Analysis and reports cannot redefine a mismatch or turn missing observations into success. |
| DP4 → FR2 | Presentation preserves the common assessment. It cannot drop conflicts or reinterpret unknown cells. |

An upstream change invalidates downstream results. A schema change requires
new resolution, candidate selection, binding assessment, analysis, and reports.
A candidate change invalidates its observations and assessments. A change to
binding comparison requires new drift facts and dependent findings. A report
change must preserve semantic results, not merely leave the files untouched.

The child mapping uses the same discipline. DP1.1 controls syntax admission
and affects identity preservation. DP1.2 controls AD decoding and cannot change
syntax admission under a fixed expression profile. If a schema change expands
the expression profile, this zero no longer applies.

| Outcome / control | DP1.1 | DP1.2 |
|---|---|---|
| FR1.1 | X | 0 |
| FR1.2 | X | X |

These local matrices do not establish global independence. A parent effect is
a refinement obligation, not an effect on every descendant. The example leaves
cross-branch allocation unknown where no leaf contract establishes it. An exact
leaf effect must remain visible even if it contradicts a parent zero.

Shared memory, CPU use, file access, and process failure can affect several
outcomes together. Their effects are unknown because no workload bounds or
failure-isolation measurements exist. The failure context in the example keeps
those unknowns separate from the semantic hypothesis. Functional independence
also does not prove that successful outcomes are statistically independent.

## Module contracts and composition

A module is a logical responsibility, not a deployment unit. The modules can
share one process. Their contracts prevent consumers from changing upstream
meaning, but those contracts still need acceptance evidence.

| Module | Input → output | Owned information and invariant | Failure behavior |
|---|---|---|---|
| Syntax admission | Source text → syntax with positions | Owns the admitted expression profile and syntax diagnostics. It never silently changes an unsupported expression. | Reject malformed syntax, duplicates, and unsupported forms with positions. Do not supply a successful graph. |
| AD resolution | Syntax → checked graph | Owns typed identities, references, hierarchy, and schema diagnostics. It preserves every accepted fact. | Collect independent diagnostics. Stop analyses that require an invalid graph. |
| Candidate selection | Graph and requested candidate/context → snapshot | Owns selection and provenance. It retains inactive alternatives and all matching influence records. | Diagnose incoherent selection and conflicting applicable facts. Do not choose the last record silently. |
| Binding assessment | Snapshot and observations → versioned drift facts | Owns comparison and observation provenance. Missing access is not evidence of conformance. | Return unknown for unavailable observations. Retain the cause and candidate identity. This module is not implemented. |
| AD analysis | Snapshot and available drift facts → qualified assessment | Owns exact cells, refinement obligations, classification, and partial order. Unknown never means zero. | Keep conflicts visible. Suppress only conclusions whose prerequisites fail. |
| Presentation | Assessment → reports and process status | Owns formatting. It preserves findings, qualifications, labels, and failure status. | Report input and assertion failures without a traceback. Do not present a missing assessment as success. |

The target design uses C junctions for required design order. A C junction
controls the order of choices. At runtime, syntax must precede resolution, and
resolution must precede analysis. Binding observation is not an implemented
runtime step, and source-only analysis does not require a successful probe.

S combines independently established outcomes. It does not mean arithmetic
addition or concurrent execution. Report formats can compose under a shared
assessment contract, but they still share failure risks. The example records
the source-analysis path as a target flow, not an implemented Go scheduler
or a probe runner.

F exposes residual coupled iteration. A matrix cannot synthesize a safe repair
loop. After a diagnostic, the author decides whether to revise the design.
Any future automated revision needs a stopping condition and failure behavior.

## Alternatives and the Information Axiom

The Information Axiom compares the chance of meeting the same acceptance
predicates. Information content is `I = -log2(p)`. The relevant `p` is joint
success across the required outcomes under one workload and time horizon.
Neither smaller code nor fewer edits is a substitute for that probability.

| Alternative | Feasibility and limits | Decision |
|---|---|---|
| Bounded Python subset with typed decoding | Historical experimental baseline. Its syntax limits do not define native HCL or the target expression policy. | Abandoned, not retained as a shipping target. |
| Go HCL parser with typed AD resolution | Selected technology for native HCL syntax with bounded expression semantics. Parsing does not supply AD semantics or prove the proposed zeros. | Adopt for the planned tool. Implementation and independence still need evidence. |
| Shared behavior and design schema | Changes the fixed separation between behavior and design. Its effect on both schemas requires a separate design comparison. | Outside the selected boundary, not a proven inferior probability. |
| Code annotations alone | Cannot directly represent a rejected mechanism that has no code. They can supply observations for a separate design record. | Do not use as the only design source. |
| Viewer or graded scores before reliable resolution | Does not correct contradictory cells or missing premises. It fails the proposed assessment criteria. | Defer until the underlying facts are reliable. |

No comparable joint observations or confidence bounds are available. Information
content therefore remains unknown. The selected technology is not a measured
Information Axiom ranking.
A trial must use the same versioned corpus, acceptance predicates, candidate identity,
workload distribution, and exposure horizon for each feasible alternative.
The trial must include malformed input, incomplete designs, and shared failures.

Counts require a sampling model and uncertainty method. Zero failures do not
establish `p = 1`. Do not multiply marginal success rates without a justified
dependence model. Edit counts and maintenance effort remain separate costs.
The self-design example records unknown information and invents no evidence.

## File layout of a model

A model can span several files. This decision is a small design problem of
its own. Its outcomes are: FRa, review one zigzag step in one place. FRb,
change realization with the code and infrastructure, without edits to design
facts. FRc, review the needs apart from the design. FRd, give the analyzer the
same model for any layout.

The first candidate used one file per domain and one file for the matrices.
It fails FRa. A child FR refers to its parent DP, and that DP refers back to
the FRs that it controls. Separate FR and DP files therefore depend on each
other. One zigzag step needs edits in three files: FRs, DPs, and the matrix.
A written matrix also repeats facts that the analyzer derives.

The adopted design uses a `.ad.project.hcl` manifest to list `core_files` and
`attachment_files`. Core files use `.ad.hcl`. Attachment files use `.ad.ext.hcl`
and do not enter core decoding. Split core facts by domain and branch.
The directory merge rule below describes the earlier layout analysis, not
the adopted project's file-discovery contract.

| Outcome / control | DPd: merge rule | DPc: needs file | DPa: branch files | DPb: process file |
|---|---|---|---|---|
| FRd: same model for any layout | X | 0 | 0 | 0 |
| FRc: review needs apart | X | X | 0 | 0 |
| FRa: one zigzag step in one place | X | X | X | 0 |
| FRb: realization changes alone | X | 0 | X | X |

Under that earlier merge rule, the matrix is conditionally decoupled.
Set the merge rule first, then the needs, then the
branch design, then the process files. The merge rule affects every outcome,
because it decides which files form the model. A needs change can change the
FRs of a branch. A branch change can change the DPs that PVs realize. A PV
change does not change a need or a design fact, because PVs only refer to DPs.
The zeros depend on that rule. A future DP-to-PV influence model must keep its
edges in the process files.

The historical regression checks a split model against a single-file model.
It does not test manifest loading or attachment dispatch in the planned Go tool.
The earlier result does not prove independence for the adopted layout.

## Attachment ownership

Each manifest extension label selects a trusted installed owner with a role
and a contract. A label does not load arbitrary code. Each attachment contains
`owner = extension.x`, a typed core `subject`, and a literal object `data`.
The owner decodes its own data. Core decoding and core AD analysis do not
interpret tool-specific fields.

The roles have separate subjects and contracts:

| Role | Subject | Owner contract |
|---|---|---|
| `binding` | PV | Terraform `address` and `observation_source` strings. |
| `behavior_link` | Module | `model`, `revision`, `target_kind`, and `target_label` strings. |
| `view` | Design | `layout` is `requirements_first` or `matrices_first`. `show_source_locations` is `true`. |

Generic PV `kind`, `address`, and `note` remain core fields. Tool-specific
values moved to attachments have one authority there, not a second core copy.
The current core has no `import` block or `module.handles`. Behavior links
belong to the `behavior_link` owner and do not merge external behavior schemas into AD.

The local extension diagonal is conditional on fixed core contracts, separate
owner data, and owners that cannot rewrite core facts or each other's results.
Changing one owner's data must not change another owner's outcome under those
conditions. That is a contract to assess, not measured implementation evidence.
Shared resources and owner failures can still affect several outcomes.

Keep core and extension results separate. A binding observation can qualify
realization findings, but it cannot silently change the core influence matrix.
A behavior-link failure or view failure is an owner result, not a new core
AD fact. A successful core assessment does not establish successful extensions.
These boundaries do not prove that the whole design is uncoupled.
The self-design includes a conditional extension subtree. Its premises remain
unvalidated. No adapter or Go implementation is claimed here.

## Change and failure scenarios

The following scenarios are proposed acceptance work, not completed runs.
They test both the intended controls and the defended zeros. Their results
must qualify or withdraw the relevant matrix claim.

| Scenario | Expected result and affected outcomes |
|---|---|
| Move an FR to a new parent | Preserve identity and provenance. Recompute sibling scopes, refinement obligations, and downstream views. Do not promise one edit when contracts also change. |
| Add an exact leaf effect that contradicts a parent zero | Preserve the exact effect in every view. Report the parent conflict and withdraw unsupported descendant zeros. |
| Change the selected candidate | Keep alternative records. Invalidate old observation bindings, conclusions, and reports. |
| Invalidate a premise | Remove its support from dependent conclusions. An assumed zero cannot remain unconditional. |
| Add a binding owner | Add its manifest declaration and owned attachments without changing core AD fields. A change to a shared core contract still requires a versioned DP1 change. |
| Rename a Terraform address | Without observations, report unknown. With a future adapter, compare against the correct candidate and report the mismatch. No probe exists here. |
| Reject duplicate facts or a mistyped reference | Give a source-positioned diagnostic before graph-dependent analysis. Never replace an earlier fact silently. |
| Change report formatting | Preserve all cells, conditions, findings, and process status for the same assessment. |
| Exhaust shared process memory | Do not infer isolation from local zeros. Record the unavailable assessment rather than verified success. Availability bounds remain unspecified. |
| Compare two valid orders for incomparable controls | Accept either order if both contain every control once and respect all required precedence. Do not invent an influence to force display order. |

The architecture remains a conditional hypothesis until these obligations have
evidence. The self-design example supplies criteria and contracts, not evidence
that the planned Go tool implements them. Reassess the matrices whenever ownership,
operating ranges, schema contracts, or failure assumptions change.

## Changes from the first sketch

The first sketch stored several derived facts. It remains in Git history at commit `91880f7`.
The revised language keeps each authored fact in one place. These changes reduce
duplicate ownership but do not prove that every remaining influence is known.

| Earlier choice | Problem | Revised direction |
|---|---|---|
| Authored classification, junction kind, and order | One influence change can invalidate several records. | Derive views and use `expect` only as an assertion. |
| Repeated hierarchy in mappings | Moving an FR requires duplicate edits. | Resolve flat influences against the hierarchy. |
| One status for decision and implementation | Selecting a design can look like implementing it. | Keep authored decisions separate from evidence-derived implementation status. |
| Assumed one-to-one controls | A list can conceal missing independent control. | Preserve unique rows and columns. Assess pairing and effectiveness explicitly. |
| Tool bindings inside core DPs | Each binding kind can change unrelated core facts. | Keep generic realization facts in PVs and tool-specific data in owned attachments. |
| Repeated child criteria | Copies can drift or assert an unsupported allocation. | Record explicit contributions with `allocated_from`. |
| Shared state without ownership | Responsibility and failure effects remain hidden. | Name leaf ownership and investigate cross-branch effects. |
| Typed-in success probability | A number can conceal missing evidence. | Keep probability unknown until comparable evidence supports it. |
