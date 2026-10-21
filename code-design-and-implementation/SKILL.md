---
name: code-design-and-implementation
description: Analyze code, discuss alternatives, review implementations, or implement agreed designs involving behavior, responsibilities, interfaces, concurrency, or lifecycle, including comment tasks that require judging these behaviors or contracts. Reviews are static and read-only. Standalone unit-test design and authoring use unit-testing when available. Skip syntax-only explanations, cosmetic wording or formatting, spelling checks, routine renames, simple descriptive comments, and mechanical edits.
---

# Code design and implementation

Align code analysis, design discussions, reviews, and implementation with the user's intended behavior and confirmed decisions. Surface consequential assumptions before they become implementation policy. Apply the relevant guidance at the depth the task needs; do not impose a planning template or a new approval stage on every increment.

Read-only analysis, design discussion, and code review can be complete tasks: explain the relevant behavior and ownership, assess the concern or alternatives, and identify consequential open questions. They do not require an implementation plan or later edits. Simple symbol lookup does not require this workflow. Honor explicit invocation within the requested scope, including comment tasks that require judging behavior or contracts.

Feature implementation and production-code repair retain responsibility for necessary tests and permitted verification. Use `unit-testing`, when available, as the primary workflow for standalone unit-test design or authoring, or consult it for substantive test-design choices within an implementation. Do not force a separate testing task or TDD sequence. Test-code review keeps the review mode below; execution-only verification does not automatically become test authoring or repair.

In a code review task, use code reading and static reasoning only; do not modify files or run builds, tests, previews, apps, or other runtime verification. Earlier modification or runtime-verification authorization does not carry into a current review task. Ground findings in inspected code and a concrete failure scenario or responsibility or contract mismatch. Explain the impact and recommendation, distinguish actionable defects from optional design preferences, and say when no actionable issue is found. A finding does not itself authorize a fix.

## Establish the current task and baseline

Reuse the goal, authorized scope, and confirmed decisions from the available task context. Follow-ups refine that baseline unless the user changes it; do not replace the overall agreement with the latest local suggestion or ask the user to repeat settled decisions.

Read the related implementation before assessing its design. Use relevant formal references for confirmed contracts and the user's requirements for the intended change. Respect task-specific reading exclusions. Incomplete scaffolding, deferred integration, and legacy code do not themselves authorize migration or completion.

Where it affects the decision, distinguish required guarantees and confirmed responsibility agreements from current implementation choices, derived mechanisms, proposals, and unresolved choices. An existing mechanism does not establish an additional requirement; a confirmed responsibility agreement remains binding until its adjustment is authorized. Distinguish a confirmed but unimplemented target from an outdated description when code and documentation differ. Identify consequential discrepancies, recover missing decisions from available context, and seek clarification under the decision rules below when needed.

## Assess structure and coordination across the affected flow

When a task concerns unclear code structure, relationships, boundaries, responsibilities, or lifecycles, inspect the related callers, dependencies, data flow, state owners, and completion and cleanup paths before recommending a change. Evaluate the user's local ideas against the overall goal and confirmed constraints, then recommend a coherent approach that resolves the original concern, including keeping the current design when appropriate. Distinguish necessary corrections, structural improvements justified by current needs, and optional preferences. Necessary analysis may cross files; it does not authorize broader edits or a project-wide audit.

Before introducing state, abstractions, or compensating mechanisms such as retries, state-chasing loops, synchronization barriers, history records, or repeated validation, establish the concrete scenario, required guarantee, and confirmed requirement. Explain why existing owners, inputs, or results cannot meet the need directly; identify who owns, changes, and consumes the information and when it becomes invalid. Do not turn an unchosen strategy or hypothetical future requirement into implementation policy.

Compare coordination costs across the affected flow, rather than judging only local code length, type count, or duplication. If a local simplification needs additional state, forwarding, or synchronization, first compare simplifying ownership and data flow with maintaining that compensation. Preserve coordination needed for confirmed guarantees and explain its basis; fewer layers alone are not a goal. Apply the decision rules below if an alternative requires changing confirmed behavior or responsibilities.

When concurrency, interacting states, state sources, or versions affect the decision, assess the conceptual model, main flow, and tradeoffs. Explain relevant state meanings, owners, and validity scopes, including whether versions identify values or establish ordering. Distinguish authoritative state, cached views, operation inputs, and delivered results where needed. Use relevant interleavings to explain input selection and the boundaries governing execution, commit, and result delivery.

When concurrency or lifecycle affects the decision, distinguish a current execution slot from work still running or finishing, cancellation of one waiter from cancellation of shared work, and operation completion from result delivery. Explain where the relevant invariant is enforced. Preserve necessary safeguards without spreading the same policy across multiple owners.

For structural analysis that remains inconclusive, local changes that repeatedly shift coordination costs elsewhere, or designs that are difficult to compare, consider bounded independent multi-agent cross-analysis as an optional escalation. First explain the unresolved disagreement, proposed analysis scopes, expected outputs, and anticipated benefit. Ask for authorization before delegation if it has not been given; reuse existing authorization within its scope without asking again. Do not start subagents by default.

Give agents the shared requirements, confirmed constraints, and necessary source material, with independent questions rather than a preferred answer. Bound local analysis to relevant types and their direct callers and consumers, and end-to-end analysis to the affected business flow and necessary adjacent contracts. Either perspective may recommend local changes or restructuring. The main agent reconciles evidence and disagreements into one recommendation rather than deciding by majority vote. Do not automatically expand scope or launch further rounds. Delegation does not resolve missing business decisions or change the current task's read-only, modification, or verification boundaries.

## Align understanding and resolve consequential decisions

Proactively identify consequential uncertainties about behavior, responsibilities, inputs and outputs, failure handling, and lifecycle. Describe concrete scenarios and ownership differences while assessing the related flow; do not wait for the user to discover contradictions. Silence, pending answers, omitted details, and agreement on a broad direction do not confirm specific choices.

When an unresolved interpretation or proposed design adjustment would materially change behavior, responsibilities, dependency direction, inputs or outputs, failure handling, lifecycle, scope, or implementation approach, or introduce a policy or guarantee neither confirmed nor directly required by established rules, explain the consequences and recommendation and obtain the missing decision before treating it as selected or implementing dependent changes. Raise conflicts with confirmed boundaries, inability to meet the goal, or substantial simplifications that require changing an agreement. Pause only the dependent decision and implementation. Continue read-only comparison with explicit assumptions and continue independent work already authorized. Resolve clear typos and low-impact details from context; routine names, helper methods, and mechanisms that realize confirmed rules do not require additional approval. Carry earlier answers forward.

Compare viable approaches against the same requirements and explain meaningful costs and limits. Maintain an evidence-based assessment when a suggestion conflicts with it. When changing a recommendation, identify the changed requirement, new fact, or correction to the earlier assessment and explain what that changes.

## Implement within the agreed scope

Keep read-only analysis and design discussion requests read-only, including temporary files. Start implementation only within the current authorized scope and applicable task-mode restrictions; do not ask again merely because the conversation began as a discussion. Keep necessary dependent changes within the task. Authorization does not independently extend to an unrequested design artifact, unrelated configuration, or verification beyond the task's permissions.

Implement the requested increment within confirmed behavior and responsibility boundaries, keeping the main behavior understandable. Choose routine implementation details yourself and apply the decision rules above if an unresolved choice or a new policy or guarantee is uncovered. New code or state alone does not require confirmation.

## Verify the affected chain and report evidence

Before declaring implementation complete, statically inspect the saved changes and actual diff against the authorized scope and confirmed decisions. Check for unintended changes or compensation without a confirmed basis. Inspect affected callers, state owners, result consumers, and relevant comments to verify their contracts still agree; modification scope does not limit inspection to edited lines. After changing responsibilities, ownership, data flow, or synchronization, check for obsolete state, helpers, compensation, and repeated checks. Apply the same [structure and coordination criteria](#assess-structure-and-coordination-across-the-affected-flow) to the resulting flow without expanding into unrelated cleanup. This self-check is part of implementation.

Check relevant success and failure paths. For asynchronous work, trace interleavings that can change the outcome, including cancellation, state changes, delayed notifications, and late completion. Check where stale work loses mutation or delivery rights and who completes each result. Review the whole affected path rather than only the edited method.

Use only checks permitted by the project and current task. During implementation, correct in-scope errors found by self-checking and recheck the affected path; apply the decision rules above if resolution requires an unconfirmed choice. Static self-checking does not make implementation a separate code-review task; standalone verification does not authorize repairs. Static reasoning, including event-sequence analysis, does not establish runtime correctness.

Report what changed, consequential decisions or remaining questions, checks actually performed, and relevant unverified behavior. Judge convergence by whether the original concern is resolved while preserving confirmed constraints, not by the number of edits. Once that condition holds, another viable arrangement alone is not unfinished work or a reason to continue structural refactoring.

Discussion can remain inline. When the user requests a design manuscript or formal reference, use the appropriate document workflow if available; this skill does not require creating either artifact.
