---
name: code-design-and-implementation
description: Analyze code, discuss designs, review implementations, or implement changes involving behavior, responsibilities, interfaces, concurrency, or lifecycle. Includes comments requiring judgment about these contracts. Reviews are static and read-only. Skip syntax-only explanations, cosmetic edits, routine renames, simple descriptive comments, and mechanical edits. Standalone unit-test authoring uses unit-testing when available.
---

# Code design and implementation

Resolve the user's original concern within confirmed behavior, responsibility boundaries, and authorized scope. Apply the guidance at the depth the task needs; it is not a required report template or an additional approval stage.

Read-only analysis and design discussion can be complete tasks. Explain the relevant behavior, assess the concern, and identify consequential open questions without requiring an implementation plan or later edits. Honor explicit invocation within its requested scope.

Establish deliverable permissions from the current request, still-valid same-task authorization, and project requirements. A production-code request covers production changes and directly related necessary comments; test code and standalone documentation need their own authorization. Selecting a skill, reading related material, or finding an issue does not expand scope. Complete authorized deliverables together without routinely asking to add others.

Use `unit-testing`, when available, for standalone unit-test design or authoring, or consult it when substantive test work is also authorized. Do not force a separate testing phase or TDD sequence. Test-code review follows the review mode below; execution-only verification does not authorize test authoring or repair.

Code review is static and read-only, including no temporary files, builds, tests, apps, previews, or other runtime verification. Earlier edit or execution authorization does not carry into review. If review is combined with edits or execution, obtain the task-mode choice unless already explicit. Ground findings in inspected code and a concrete failure scenario or contract mismatch; explain impact and distinguish defects from preferences. Say when no actionable issue is found. Findings do not authorize fixes.

## Establish the task and constraints

Carry forward the original goal, confirmed behavior and responsibility boundaries, and explicit user constraints. Follow-ups refine that baseline rather than replacing it with the latest local suggestion. Separate required guarantees from current implementation choices: an existing mechanism is not an additional requirement, and approval to try it does not make every incidental detail permanent. Re-evaluate a mechanism that obstructs the goal while respecting explicitly selected designs.

Read the related implementation for current facts and relevant references for confirmed contracts. Requirements and confirmed decisions establish the intended change. Respect reading exclusions; distinguish an unimplemented target from an outdated description when sources disagree. Scaffolding, deferred integration, and legacy code do not authorize migration or completion.

Ask when an unresolved choice materially affects the conclusion or would change confirmed behavior, responsibility or dependency boundaries, externally relied-on interfaces, lifecycle guarantees, explicit design constraints, or authorized scope. Explain the consequences and recommendation before dependent action; continue independent authorized work and read-only comparisons with explicit assumptions. Resolve equivalent internal details yourself and reuse earlier answers. Silence or approval of a broad direction does not select consequential missing details.

## Compare the affected design

For structural or simplification questions, inspect the affected callers, dependencies, state owners, and relevant completion paths. Compare viable approaches against the same requirements, including retaining the current design. Analysis may cross files without authorizing broader edits or a project-wide audit. For an explicitly limited increment, respect that limit and report any broader change needed to resolve the original concern.

Before calling a change a simplification, identify the complexity it removes and the state, indirection, assembly, or coordination it introduces across the affected flow. Merely relocating complexity is a tradeoff, not an established simplification. Distinguish necessary corrections, improvements justified by current needs, and optional preferences. A required correction may add complexity; explain the guarantee that requires it.

Before adding state, abstraction, forwarding, waiting, or synchronization, establish the concrete need and why existing owners, inputs, or results cannot meet it directly. Determine whether the addition represents an independent required fact or compensates for a chosen mechanism. In the latter case, reconsider that mechanism and its ownership or data flow before adding another layer. Preserve safeguards required by confirmed guarantees; do not invent future requirements or judge simplicity by line or type counts alone.

Analyze concurrency, state validity, or lifecycle only where they can change the outcome. Establish which state is authoritative, who can change it, and when results remain valid. Derive waiting and cleanup from the confirmed contracts. Use relevant interleavings to assess the required guarantees without treating every risk category as a requirement for a new mechanism.

Explain evidence-based disagreements and identify the changed requirement, new fact, or correction when revising a recommendation. Do not present another arrangement as an improvement without showing how it addresses the original concern.

Consider bounded independent multi-agent cross-analysis only when an unresolved structural tradeoff would benefit from it. Explain the scopes, expected outputs, and benefit, and delegate only with authorization; reuse existing authorization within scope. Provide shared requirements, constraints, and source material with independent questions. Bound analysis to the affected types and flow, reconcile evidence rather than votes, and do not launch further rounds automatically. Delegation does not resolve missing business decisions or expand permissions.

## Implement and check the result

Keep analysis and discussion read-only, including temporary files, until edits are authorized. Once authorized, complete the requested increment without redundant approval merely because the task began as discussion. Keep changes within the authorized deliverables and task mode.

Inspect saved changes and the actual diff before declaring completion. Check the affected callers, owners, consumers, and relevant comments for agreement with the confirmed contracts. Check that the original concern is resolved and obsolete state, helpers, forwarding, or repeated checks have been removed within scope. Reuse the design criteria above on the resulting flow; static self-checking is part of implementation, not a separate review or permission to expand cleanup. Correct in-scope errors and recheck affected paths, asking only when resolution needs a consequential new decision.

Use only permitted checks. Tests need explicit execution authorization; implementation or test authoring alone does not grant it. Establish environment and scope before any run; a known command alone is not a default scope. If the request or project has not selected one, or a consequential choice remains unresolved, ask before any target or preliminary subset. Run agreed checks after changes, reusing authorization for necessary same-task reruns unless revoked or superseded by a task-mode change; confirm expansions. Otherwise finish static inspection without routinely asking to run tests.

Report changes, consequential decisions, actual checks, and remaining limits. Claim a command-based check passed only when its output and exit status confirm success; distinguish static reasoning from runtime results. Completion means resolving the original concern while preserving confirmed constraints. Once that holds, another viable arrangement is not a reason to continue refactoring.

Discussion can remain inline. When the user requests a design manuscript or formal reference, use the appropriate document workflow if available; this skill does not require creating either artifact.
