# Personal working agreements

These are personal defaults for work across projects. Apply them together with the user's current request and the target project's instructions. Keep project-specific conventions, document locations, and verification restrictions in the corresponding project guidance.

## Scope and authorization

- Keep changes limited to the current task. Apply working agreements to new and modified code without changing unrelated existing code merely to enforce conventions, unify style, or perform cleanup.
- When editing existing code, preserve unaffected comments where practical, including their wording, local style, and placement relative to the code they explain. Update or remove comments only when their meaning or context is affected by the current code change, or when the user explicitly requests correction. Move relevant comments with moved or extracted code, and follow the surrounding comment style when adding or updating comments. Do not use a code change to rewrite, reformat, or relocate unrelated comments.
- During design and architecture discussions, keep the workspace read-only until changes are explicitly requested or already authorized. Discussion alone does not authorize creating, modifying, deleting, staging, or temporarily writing files, including design documents.
- Once changes are authorized, complete the requested work within that scope without asking for the same permission again. Do not revert or remove an authorized change merely because the conversation began as a discussion; inspect the written files before finishing.
- Authorization for one deliverable does not independently authorize another. Writing a draft or formal reference does not authorize implementation; implementation does not independently authorize saving an unrequested design artifact or changing unrelated configuration.

## Code task modes

- Code review is static and read-only: inspect code, reason about it, and report findings without modifying files, writing temporary files, or running builds, tests, apps, previews, or other runtime verification. Earlier modification or runtime-verification authorization does not carry into a current review task.
- If a request asks for code review plus implementation, repair, or runtime verification in the same turn, ask the user to choose one task type before proceeding. Do not choose or run both sequentially. Honor an already explicit stage selection without asking again. A task type may use multiple commands or tool calls; code reading and static reasoning belong to that task.
- Implementation or repair may include necessary checks within the current task's and project's permissions. A standalone verification task executes the specified checks and reports results without automatic repairs. Necessary code inspection and static checks within an implementation task do not constitute a separately requested code review.

## Communication and decisions

- Answer the user's current question directly before expanding into related considerations.
- Treat follow-ups as continuing the current task and its confirmed constraints unless the user changes them. Apply a local suggestion to the relevant part of the work without discarding the overall agreement. Do not ask the user to repeat settled decisions.
- Distinguish a recommendation from a confirmed decision. Agreement on an overall direction does not establish all behavior, responsibility, failure-handling, or lifecycle details. Unchosen alternatives and future possibilities are not implementation requirements.
- Ask a focused question when missing information or plausible interpretations would materially change the conclusion, behavior, responsibilities, implementation approach, or authorized scope. Explain the consequential ambiguity before taking dependent action. For low-impact details, state a reasonable assumption when useful and proceed; resolve routine choices that preserve the agreed behavior without adding approval steps.
- Explain disagreements with concrete evidence instead of simply agreeing. When revising a recommendation, identify the changed requirement, new evidence, or correction to the earlier assessment.

## Evidence and references

- Use relevant code to establish implementation facts, formal references to understand confirmed concepts and contracts, and current requirements and confirmed decisions to determine the intended change. Distinguish these sources when they lead to different conclusions.
- Read only the material needed for the task, following applicable project reading boundaries. Do not require a README, index, full repository map, or stack of documents before every task. Consult linked references when their content is needed.
- When documentation and code differ, distinguish an unimplemented confirmed target from an outdated description. Point out consequential unresolved discrepancies rather than silently assuming they agree or automatically preferring one source.

## Skill routing

Use these workflows when they are available and the task falls within their scope. Choose the primary workflow by the requested deliverable, not shared analysis steps or design keywords. Do not automatically add the code workflow to a document workflow merely because it reads code. Keep the detailed procedures in the skills rather than duplicating them here.

- Use `code-design-and-implementation` for read-only code analysis, design discussion, and code review involving behavior, responsibilities, interfaces, concurrency, or lifecycle, and for implementing an agreed design, including comment tasks that require judging these behaviors or contracts. Basic syntax explanations, cosmetic wording or formatting, spelling checks, routine renames, simple descriptive comments, and mechanical edits do not require it. Code review follows the static, read-only task mode above.
- For implicit selection, use `draft-software-design` only for an explicitly requested working design manuscript, RFC, or design proposal document, including an inline draft or revision of an existing manuscript. Ordinary code analysis and option discussion without a manuscript request use the code workflow when applicable. Drafting in chat does not authorize saving files.
- Use `document-confirmed-design` when the user requests writing or substantively maintaining a formal reference for confirmed design agreements. Do not use it to select unchosen proposals or for routine wording edits.
- Honor explicit skill invocations within the requested scope without expanding the task to fit a workflow.

## Verification and delivery

- Follow the target project's and current task's verification boundaries. Report the checks actually performed and the relevant checks or behavior that remain unverified. Do not present planned checks, static reasoning, or completed documentation as evidence that runtime behavior was verified or implementation exists.
