# Assessment contract

This document defines core version 1 assessment semantics.
It supplements the field definitions in the language reference.
If an assessment rule differs, this document takes precedence.
The rules describe required behavior, not completed implementation tests.

## Snapshot selection

A snapshot is the active model for one candidate and context.
Without a candidate request, activate all DPs whose decision is `selected`.
An explicit candidate activates exactly its `dps` list.
DPs outside any candidate are common only when their decision is `selected`.
Add these common DPs to each explicit candidate.
A DP listed in another candidate is never common.

Every active child FR requires its parent DP to be active.
Every active DP requires all its controlled FRs to be active.
Root FRs remain required across candidates of the same decision.
Reject an explicit selection that lacks an ancestor. Do not insert ancestors silently.
A candidate cannot select rejected or superseded DPs.
A proposed DP can participate in an explicit alternative snapshot.
The default selected candidate must agree with selected DP lifecycle states.

Retain inactive records and their provenance for comparison.
Do not report inactive branch leaves as uncovered default requirements.
Apply an influence only when its target FR and source DP are active.
Expand a multi-source influence into one record per source DP.
Activate a module when at least one realized DP is active.
Restrict its assessed realization set to active DPs.
Apply a PV or attachment only when its subject is active.
Retain evidence only for its exact candidate version and operating range.

## Cell resolution

Resolve applicability before effects.
An unconditional record applies in every context.
A context-specific record applies only in that exact context.
A workload-specific record applies when the snapshot names that workload.
Missing context information leaves conditional applicability unresolved.
Never select mutually excluded contexts together.

For each applicable exact record, evaluate all `holds_if` premises.
An invalidated premise disables its claimed effect and leaves an unresolved obligation.
An assumed or unevaluated premise supports only a conditional effect.
A validated premise still requires applicable support for a supported conclusion.
DP premises qualify all control claims that depend on that DP.

Merge compatible exact records without discarding their sources.
Two known contradictory effects produce a conflict, regardless of their support levels.
An explicit unknown remains visible beside a known assertion.
It prevents supported classification until its uncertainty is resolved.
It does not erase the known assertion from structural reports.

Apply a `cells` default only when no applicable exact record exists.
An exact unknown therefore prevents a default zero.
Defaults never overwrite exact facts.
Conflicting applicable defaults produce a conflict.
With neither exact facts nor a default, resolve the cell as unknown.
Keep conditional effects, conflicts, disabled records, and support gaps in every projection.

## Pairing and classification

Use `controls` to build a bipartite graph between sibling FRs and their DPs.
A pairing assigns each FR a distinct controlling DP.
Use it only when exactly one complete pairing exists.
Multiple complete pairings produce `ambiguous_pairing`.
No complete pairing produces `uncontrolled_requirement` or `redundant_control`, as applicable.
Never select a pairing because its matrix looks simpler.

Classify a square mapping only when every paired diagonal has a material effect.
A zero diagonal is an ineffective control.
An unknown diagonal leaves classification unresolved.
Rectangular mappings retain their full axes and coverage findings.
Do not remove rows or columns to obtain a square mapping.

An uncoupled mapping has material diagonal cells and justified zero off-diagonal cells.
A decoupled mapping admits a triangular order with at least one material off-diagonal cell.
Reorder paired rows and columns together, retaining their labels.
For each off-diagonal material effect from DP A to the FR paired with DP B, require A before B.
A cycle in these precedence relations establishes structural coupling when all required effects are known.
Unknown cells prevent a complete classification, even when a known cycle is reported.
Use label order only to display otherwise equivalent valid sequences.
An upstream change invalidates affected downstream conclusions.
A design sequence does not automatically specify runtime execution order.

## Hierarchy and support

The master axes contain every active leaf FR and every distinct active leaf DP.
A DP that controls several FRs still occupies one column.
Retain exact cross-branch effects on these axes.
Do not expand parent material effects or parent zeros into leaf facts.
An apparent ancestor disagreement creates `unresolved_refinement`.
Report a contradiction only when an applicable outcome argument proves incompatible claims.

An outcome argument is a claim-specific support record.
It identifies parent and child criteria, the allocation rule, premises, operating range, and source revisions.
For version 1, record these arguments in a separate review document linked through `source` and `cites`.
No new core argument block is introduced.
A citation alone does not establish that an argument exists or is sound.

Distinguish provenance from support.
A source citation identifies where a statement came from.
Qualitative support requires an applicable analytical, contractual, or observed argument for the exact claim.
Empirical probability evidence remains subject to the separate trial contract.
A supported conclusion requires human or external review of substantive arguments.
The analyzer can report structural completeness without claiming that it proves argument truth.
Changed claims, premises, criteria, workloads, or cited revisions invalidate dependent support.
The source profile preserves support gaps as warnings.
The architecture profile requires complete criteria and contracts, but completeness alone does not establish support.

## Feasibility and selection

Assess each candidate before comparing information content.
Report `infeasible` when a required constraint or criterion demonstrably fails.
Report `unresolved` when feasibility lacks evidence, coverage, or an operational criterion.
Report `feasible` only when all required constraints and criteria have applicable success evidence.
List the reasons and affected references beside the result.
An unresolved independence result blocks a supported Information Axiom recommendation.

Compare candidates against identical required FRs, criteria, contexts, workloads, and horizons.
Different acceptance ranges define different comparison problems.
Keep cost and user preferences separate from information content.
A selected candidate can remain provisional while evidence is missing.

Trials must be positive integers.
Failures must be integers from zero through trials.
Confidence must be strictly between zero and one.
Use the two-sided Wilson score interval without continuity correction.
Let n be trials, p the observed success fraction, and z the standard normal quantile at (1 + confidence) / 2.
The center is (p + z²/(2n)) / (1 + z²/n).
The half-width is z sqrt(p(1-p)/n + z²/(4n²)) / (1 + z²/n).
Clip bounds to [0,1] only for numerical roundoff.
All-success and all-failure samples retain their Wilson uncertainty.
Do not pool separate evidence blocks automatically.
Report each compatible block separately unless a reviewed joint sampling argument authorizes pooling.
In machine-readable output, represent infinite information as null with `status = "infinite"`.
Represent missing information as null with `status = "unknown"`.
Never emit nonfinite JSON numbers.

## Identity and operation results

Core-only input selects core version 1.
Future core versions require an explicit manifest selection.
Record source identity separately from semantic identity.
Source identity includes relative paths and exact source bytes.
Semantic identity includes admitted values, typed references, and versioned contracts.
Exclude whitespace, comments, file order, and source positions from semantic identity.
A file move changes source identity but preserves semantic identity when references still resolve identically.
A semantic change invalidates dependent assessments and evidence applicability.
Do not specify a hash algorithm until the machine-readable interchange contract defines canonical encoding.

Publish separate statuses for core assessment, each owner, composition, and rendering.
An owner failure cannot erase independent core findings.
Missing external observations produce unknown owner results.
Invalid required attachments make the requested project operation fail.
The selected profile determines diagnostic severity, not the truth of a claim.
No report can promote conditional support to established independence.
