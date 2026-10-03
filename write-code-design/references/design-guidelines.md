# Design content guidelines

Use these criteria to decide what a document needs. Adapt them to the project and the requested change; they do not prescribe an architecture or require every topic in every document.

## Problem, outcome, and scope

Describe the concrete behavior or limitation that motivates the change. Identify the desired outcome and the constraints that influence a choice. Make scope exclusions explicit when a reader could reasonably expect them to be included.

For a small change, a few connected paragraphs may cover the problem, proposed change, rationale, and verification. Expand a document when multiple components, shared contracts, or uncertain decisions need explanation. Link existing requirements instead of reproducing them.

## Document structure and file responsibilities

Review organization when drafting a new design, making a substantive revision, or organizing related design documents. Repeated content, mixed responsibilities, inconsistent detail levels, or growth that obscures a decision are reasons to adjust sections or file boundaries. Keep wording-only edits within their affected context. Honor a requested fixed outline or file layout and applicable project conventions.

Order sections around what readers need to understand and decide. Establish the problem and overall approach before details that depend on them; place prerequisites before their consumers where useful. Read the headings together as an outline, give each section a clear purpose, and move or combine material whose placement obscures the reasoning. Preserve requirements, evidence, qualifications, and decision states when regrouping content.

When several design files are involved, inspect their relevant entry point, contents, and inbound links before restructuring. Clarify each file's purpose, intended reader, and scope. Distinguish an overview, a change proposal, a shared contract, module details, and a historical decision record where those roles help readers. Select an authoritative location for shared definitions using project conventions and existing references; link to it from other files. Resolve conflicting definitions from evidence or record the unresolved decision instead of silently choosing one. Preserve the provenance and status of historical decisions.

Choose detail levels by design scope. For a design spanning several components, explain their overall boundaries and shared decisions in the overview, then expand the relevant modules and their local behavior. Make the connection between an expanded detail and its parent design explicit. Keep essential context and reasoning in the overview so it remains understandable when details live elsewhere. Explain how local choices satisfy shared contracts, and surface a proposed change to such a contract at the scope it affects. Document hierarchy and architectural layers serve different purposes; neither needs a fixed number of levels or empty intermediate headings.

Keep a small, cohesive design in one file. Split when distinct responsibilities, audiences, reusable contracts, or independent maintenance make separate files easier to use; length alone does not determine the split. Give the entry document a concise map of the related files and keep summaries distinct from authoritative definitions. Follow the requested delivery mode and file scope: propose any restructuring beyond that scope, and do not turn an inline discussion into saved files or a one-document edit into a repository-wide reorganization.

## Evidence and decision state

Separate observations about existing code from the proposed design. Reference inspected source files or supplied documents for claims that drive the recommendation. Use repository-relative links in saved repository documents where practical; include line numbers only when checked and useful.

Avoid invented benchmarks, compatibility guarantees, ownership assignments, dates, or approval status. Place consequential assumptions next to the decisions they affect. An open question should identify the missing information and whether it blocks the proposal, implementation, or a later refinement.

When a project already records architecture decisions, preserve their status and rationale. If new requirements challenge an established decision, explain the conflict and proposed reconsideration.

## Document metadata and annotations

This section defines the skill's default metadata, decision labels, and evidence annotations. Use their format for new documents without a requested or established convention. Preserve existing conventions during revisions, including status in headings when that is the document's convention. A narrow wording edit does not add metadata or relocate annotations.

For a new standalone design document using this default, include its initial preparation date, latest substantive update date, document state, and implementation status near the title.

Use these field names for the default format; translate them consistently for other document languages:

| Field | English | Chinese |
| --- | --- | --- |
| Initial preparation date | Preparation date | 整理日期 |
| Latest substantive update date | Updated date | 更新日期 |
| Document purpose or review state | Document state | 文档状态 |
| Verified implementation progress | Implementation status | 实现情况 |
| Decision state | Status | 状态 |
| Research evidence | Evidence | 依据 |

Use ISO dates (`YYYY-MM-DD`). Record actual document events using the user's local date; do not copy example dates. Preserve the original preparation date during revisions, and update the revision date when the design, decisions, or substantive explanations change. If a historical date is unavailable, leave it out or identify it as unknown.

Document state describes the document's purpose or review state, such as a design discussion record. Implementation status describes verified code progress: not implemented (`尚未实现`), partially implemented (`部分实现`), implemented (`已实现`), or unverified (`未核实`). Do not infer implementation status from a discussion, a recommendation, or the document's completion.

Use these decision labels, with their Chinese equivalents for Chinese output:

- **Confirmed (`已确认`):** A design agreement explicitly confirmed by the user or recorded in a still-applicable accepted project decision. This does not mean the behavior is implemented or verified.
- **Recommendation (`建议`):** A proposed approach that has not yet been selected or confirmed.
- **Undecided (`待定`):** An interface, behavior, or implementation choice that remains unresolved.
- **Deferred (`暂缓`):** Work excluded from the current stage; revisit the design when a concrete need arises. This is not a commitment to a future implementation.

An assistant's earlier recommendation, an unaccepted draft, or a superseded record does not establish confirmation. Where decision provenance matters, link the explicit confirmation or accepted record. If its status or continued applicability is unclear, surface that uncertainty without silently changing an existing decision's status. Existing code establishes current behavior, not approval of a proposed change.

**Research fact (`调研事实`)** is an evidence label, not a decision status. Use it for information checked against official documentation or declarations in a specified SDK version. Cite the relevant source and SDK version where applicable, and state only what that source establishes. A declared interface or documented platform behavior does not establish that the local package implements or has verified the corresponding behavior.

For the default format, place annotations in a Markdown blockquote directly below the relevant heading, with blank lines before and after the block; keep status labels out of heading text. A decision status and a research-evidence line may share one block. Evidence-only sections may use an evidence line without a decision status. The template illustrates this format and does not define additional rules.

Mark decisions and evidence where the distinction matters, rather than labeling every paragraph. If a section contains mixed states, annotate its narrower subsections or individual decision items. Apply each annotation only to the content it describes. Preserve a confirmed agreement unless new discussion or evidence actually changes it.

## Responsibilities and interactions

Describe who owns each significant behavior, state transition, or side effect. Explain how components communicate and which direction their dependencies point. File organization alone does not establish an ownership boundary.

Follow the relevant project conventions. Introduce an abstraction, service, protocol, or layer only when it solves a concrete problem in this design. Explain its responsibility and cost. Avoid expanding the task into unrelated cleanup.

When code organization affects the design, map the important responsibilities to inspected or proposed modules and files. Explain what each owns, its relevant interfaces and dependencies, and what changes from the current organization. Choose boundaries around coherent behavior, state ownership, and change needs while following established project patterns. For architectural layers, describe what each layer owns and the permitted dependency direction. If a file's mixed responsibilities obstruct the requested change, include a targeted split or relocation with its reason and cost. Keep unaffected code organization out of scope and leave incidental file details open when they do not affect a decision.

Trace a representative flow from trigger to result. Include inputs, important intermediate state, and output. Add failure, cancellation, repeated invocation, concurrent access, or cleanup behavior when those conditions materially change the outcome. State which component enforces an important invariant.

Describe interfaces at the level needed to review the contract: meanings of inputs and outputs, ownership, failure behavior, and compatibility obligations. Use short signatures or examples if prose leaves a real ambiguity; link full definitions instead of duplicating implementation code.

## Alternatives and consequences

Compare realistic options against the same relevant criteria. Explain why the recommendation fits current constraints, what it costs, and when another approach would become preferable.

Consider preserving existing behavior when it is a credible option. If requirements leave no meaningful alternative, explain the constraint instead of inventing a weak option. Avoid unsupported assertions that an approach is optimal, scalable, or future-proof.

Keep decision reasoning visible: the context that matters, the chosen approach, and its consequences. Separate a recommendation from a choice already made by the project.

## Change impact and verification

Identify the affected components and contracts. For a compatible change, explain the relevant compatibility reasoning rather than simply declaring compatibility. Discuss migration, rollout, rollback, or persistent data changes when the proposal actually involves them.

Include performance, security, privacy, and observability concerns where the design changes them or project requirements call for them. Do not add generic checklists detached from the proposed behavior.

Connect verification to the desired behavior and important invariants. Describe scenarios, expected results, and unresolved feasibility questions. Identify existing evidence and planned checks separately. A writing task does not itself justify building the project, running tests, or creating a prototype.

## Coherence check

Check that the overview, detailed flow, interface examples, and any diagrams describe the same design. A reader should be able to locate the owner of a behavior and follow how information reaches it.

After structural edits, check the affected outline, file navigation, links, and reference anchors. Confirm that shared definitions remain consistent and that moved content retains its requirements, evidence, and decision state. Update affected inbound links within scope; disclose any references that could not be checked or repaired.

Keep implementation sequencing at the level needed to understand dependencies or migration. A design document need not become a task-by-task implementation plan. Remove background tutorials and duplicated information that do not affect the decision.
