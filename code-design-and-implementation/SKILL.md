---
name: code-design-and-implementation
description: Analyze code, discuss alternatives, review implementations, or implement agreed designs involving behavior, responsibilities, interfaces, concurrency, or lifecycle, including comment tasks that require judging these behaviors or contracts. Reviews are static and read-only. Skip syntax-only explanations, cosmetic wording or formatting, spelling checks, routine renames, simple descriptive comments, and mechanical edits.
---

# Code design and implementation

Align code analysis, design discussions, code reviews, and implementation with the user's intended behavior and confirmed responsibility boundaries. Surface consequential assumptions before they become implementation policy. Apply the relevant guidance at the depth the task needs; do not impose a planning template or a new approval stage on every increment.

Read-only code analysis, design discussion, and code review can be complete tasks: explain the relevant current behavior and ownership, assess the concern or alternatives, and identify consequential open questions. They do not require an implementation plan or later edits. Enter implementation only within the current authorized task scope, after applying any task-mode restrictions in the applicable guidance. Basic syntax explanations, cosmetic wording or formatting, spelling checks, routine renames, simple descriptive comments, mechanical edits, and simple symbol lookup do not require this workflow. Comment tasks requiring judgment about behavior or contracts still use the relevant analysis or review guidance; honor an explicit invocation at the depth the user's task needs.

In a code review task, use code reading and static reasoning only; do not modify files or run builds, tests, previews, apps, or other runtime verification. Ground findings in inspected code and a concrete failure scenario or responsibility or contract mismatch. Explain the impact and relevant recommendation; distinguish actionable defects from optional design preferences. If no actionable issue is found, say so. A review finding does not by itself authorize a fix.

## Establish the current task and baseline

Reuse the goal, authorized scope, and confirmed decisions from the available task context. Follow-ups refine that baseline unless the user changes it. Do not replace the overall agreement with the latest local suggestion or ask the user to repeat settled decisions.

Read the related implementation before assessing its design. Use relevant formal references for confirmed contracts and the user's requirements for the intended change. Respect task-specific reading exclusions. Recognize incomplete scaffolding, deferred integration, and legacy implementations; their presence or incompleteness does not authorize migration or completion.

Distinguish current facts, confirmed targets, proposals, and unresolved choices where they affect the task. Code may lag a confirmed target; a document may describe an outdated agreement. Identify a consequential discrepancy instead of silently treating either source as authoritative. Recover missing decisions from relevant available context; ask when they cannot be established and would change the work.

## Align understanding through concrete behavior

Proactively identify behavior, responsibilities, inputs and outputs, failure handling, and lifecycle boundaries that the current proposal depends on but that have not been established. Raise consequential questions during analysis, design, and implementation; do not wait for the user to discover contradictions or finish reading the code. Silence, omitted details, pending answers, and agreement on a broad direction do not confirm specific choices. Before committing to an interpretation, describe the concrete behavior and ownership where the alternatives would produce different outcomes.

When informal wording, omissions, or terminology admit plausible interpretations that would materially change behavior, responsibilities, dependency direction, inputs or outputs, failure handling, lifecycle, scope, or implementation approach, pause the design and edits that depend on that interpretation until the user confirms the decision. Explain the difference with a concrete scenario, give a recommendation when supported, and ask a focused question. Surface consequential assumptions even when one interpretation initially seems obvious. Resolve clear typos and low-impact details from context; state a reasonable assumption when useful and proceed within the authorized scope.

Keep questions proportional to the uncertainty. Do not require the user to approve local names, helper methods, or other routine choices that preserve the agreed behavior and boundaries. Carry earlier answers forward.

Compare viable approaches against the same requirements and explain meaningful costs and limits. Maintain an evidence-based assessment when a suggestion conflicts with it. When changing a recommendation, identify the changed requirement, new fact, or correction to the earlier assessment and explain what that changes.

If the agreed design conflicts with its responsibility boundaries, cannot meet the current goal, or could be substantially simplified by changing confirmed behavior or responsibilities, raise the issue before proceeding with dependent work. Explain the evidence, proposed adjustment, and consequences, then obtain the user's decision before treating the adjustment as selected or implementing it. Routine implementation improvements that preserve the confirmed behavior and boundaries remain within the assistant's judgment.

## Make coordination serve an explicit responsibility

Before introducing new state, abstractions, or compensating mechanisms such as retries, state-chasing loops, synchronization barriers, history records, or repeated validation, establish the concrete scenario, the guarantee being maintained, and the confirmed requirement that calls for it. Explain why the existing owners, inputs, or results cannot meet the need directly; identify who owns the information, who changes or consumes it, and how its lifecycle ends or becomes invalid. If introducing the mechanism would change confirmed behavior, responsibilities, or scope, or add a policy or guarantee that is neither already confirmed nor directly required by established rules, pause the dependent work and ask for the missing decision before implementing it. Choose ordinary implementation mechanisms that realize confirmed rules without further approval; new code or state alone does not trigger confirmation. Do not turn an unchosen strategy or a hypothetical future requirement into present implementation policy.

When a design involves concurrent operations, multiple interacting states or state sources, or multiple versions, assess the clarity of its conceptual model, main flow, and tradeoffs. Explain the meaning, ownership, and validity scope of the relevant states and versions, including whether versions identify values or establish ordering. Distinguish authoritative state, cached views, operation inputs, and delivered results only where those roles are necessary. Use relevant interleavings to explain how inputs are selected and where execution, commit, and result delivery are governed.

When concurrency or lifecycle affects the decision, distinguish a current execution slot from tasks still running or finishing, cancellation of one waiter from cancellation of shared work, and operation completion from result delivery. Explain the relevant interleaving and where the invariant is enforced. Preserve necessary safeguards without spreading the same policy across multiple owners.

Review the data flow before adding compensation for duplicate state or asynchronous notifications. Check whether coordination complexity serves confirmed requirements or arises from current implementation choices. If ownership or synchronization choices create extra bookkeeping, compare simplifying ownership and data flow with maintaining the compensation. Explain meaningful alternatives in terms of their guarantees, failure behavior, and coordination costs. Judge the design by whether the affected flow is understandable and required guarantees hold, rather than only by code length, type count, or local duplication. Apply the existing clarification and confirmation boundaries to decisions uncovered by this assessment.

## Implement within the agreed scope

Keep read-only analysis and design discussion requests read-only, including temporary files. Respect the current task mode before acting. A current code review task remains static and read-only even when earlier tasks authorized changes or runtime checks. Start implementation only within the current authorized scope; do not ask again merely because the conversation began as a discussion. Keep necessary dependent changes within the requested task. Authorization does not independently extend to saving an unrequested design artifact, unrelated configuration changes, or verification beyond the task's permissions.

Implement the requested increment within the confirmed behavior and responsibility boundaries. Choose routine implementation details and mechanisms that realize established rules yourself, without further confirmation. Apply the clarification, design-adjustment, and compensation confirmation rules above when implementation exposes an unresolved decision about changing confirmed behavior, responsibilities, or scope, or introducing an unconfirmed policy or guarantee that is not directly required by established rules. Pause only the dependent part until that decision is confirmed, and continue independent authorized work where appropriate.

Keep the main behavior understandable in the affected code.

## Verify the affected chain and report evidence

Before declaring an implementation complete, perform a static self-check of the saved changes and the affected flow against the authorized scope and confirmed decisions. Check the actual diff for unintended changes and for extra behavior or compensation without a confirmed basis. Inspect the affected callers, state owners, and result consumers, including relevant comments, sufficiently to verify their contracts still agree; modification scope does not limit this inspection to the edited lines. After changes to responsibilities, ownership, data flow, or synchronization, check for obsolete state, helpers, compensating mechanisms, or repeated checks. Keep this self-check within the affected flow and do not use it to justify unrelated cleanup. Apply the [coordination clarity and tradeoff criteria](#make-coordination-serve-an-explicit-responsibility) to the affected design. This necessary self-check is part of implementation.

Check the relevant success and failure paths. For asynchronous work, trace the interleavings that can change the outcome, including cancellation, state changes, delayed notifications, and late completion where applicable. Check where stale work loses mutation or delivery rights and who completes each result. Review the whole affected path rather than only the edited method, without expanding into a project-wide audit.

For code review, verify through code reading and static reasoning only. During implementation, correct in-scope implementation errors found by the self-check and recheck the affected path; if resolving a finding requires a new behavioral or responsibility decision, pause the dependent changes and ask. For implementation or a standalone verification task, use only checks permitted by the target project and current task. Static self-checking does not make an implementation request a separate code-review task; a standalone verification task does not authorize repairs. Static inspection may include event-sequence reasoning, but it does not establish runtime correctness.

Report what changed, any consequential design decisions or remaining questions, the checks actually performed, and relevant unverified behavior. Judge convergence by whether the original concern has been resolved while preserving confirmed constraints, not by how many edits were made.

Discussion can remain inline. When the user requests a design manuscript or a formal reference, use the appropriate document workflow if available; this skill does not require creating either artifact.
