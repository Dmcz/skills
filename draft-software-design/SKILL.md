---
name: draft-software-design
description: Draft or revise explicitly requested working software-design manuscripts, RFCs, or design proposal documents, including inline drafts. Do not trigger for ordinary code analysis or option discussion without a manuscript request, confirmed design references, or routine wording edits.
---

# Draft software design

Produce a working manuscript that helps engineers discuss a change and decide how to proceed. Explain the target, the relevant current behavior, plausible choices, and what still needs a decision. Keep the depth proportional to the task.

## Purpose, placement, and reading role

This workflow develops a design for discussion. Writing a draft does not make its proposals accepted, turn it into a formal reference, or authorize implementation. Preserve accepted agreements as the baseline; identify proposed changes to them explicitly.

Publishing or maintaining confirmed design documentation is a separate workflow. Select this workflow for a requested manuscript, RFC, or design proposal document, including an inline draft or revision of an existing manuscript. Ordinary code analysis and option discussion without a manuscript request do not require it; discussing goals or constraints alone does not imply a manuscript deliverable. Use the appropriate code workflow for such tasks when available and applicable. Do not ask whether to write a manuscript merely because the discussion involves design. This workflow already includes the code inspection and option analysis needed for its manuscript; those supporting steps do not by themselves require another workflow. Honor an explicit invocation or delivery instruction within its requested scope without manufacturing a manuscript requirement.

When saving a new manuscript without a specified path, use a `drafts/` directory within the project's design-documentation area, for example `docs/design/drafts/`. Explicit destinations and applicable project layout take precedence. Keep an existing file in place unless moving it is authorized. The directory describes the artifact's role, not a deletion policy.

Drafts are not the default reading entry or authoritative contract for unrelated implementation tasks. A draft explicitly associated with an initial implementation or an active change may provide important direction. Its alternatives and unresolved details do not automatically become requirements.

Use code to establish current implementation facts and relevant formal documents to establish accepted concepts, responsibilities, and contracts. Requirements and confirmed design choices establish the intended change. If materials disagree, distinguish an unimplemented target from an outdated description; do not automatically treat either the code or document as correct. Follow the project's own reading rules.

## Establish and develop the proposal

Reuse the purpose, scope, constraints, and requested deliverable already supplied. Read only the related code and references needed for the proposal. Ask a focused question when missing information materially changes the design; leave genuine unresolved choices visible rather than inventing answers.

Ground current-behavior claims in inspected code or supplied material. Explain ownership, data relationships, dependency direction, and a representative flow where they affect the decision. Compare meaningful alternatives and explain reasons, costs, and limits. Do not manufacture options or introduce abstractions without a concrete need.

Verify external API capabilities and platform behavior that materially affect the proposal's feasibility or choice, using authoritative documentation or SDK declarations applicable to the target version. If verification is unavailable or inconclusive, mark the dependency as an unverified assumption and explain which choices or feasibility conclusions remain conditional. Keep research focused on those decision-relevant facts.

Expand interfaces, failure behavior, concurrency, lifecycle, migration, and verification only where they affect this proposal. Keep implementation plans, project-wide document reorganization, and unrelated code cleanup outside the requested scope.

Write in Chinese by default unless the request or existing artifact establishes another language. Preserve identifiers and existing useful format conventions. For a new manuscript, make its working-draft purpose clear; distinguish current facts, proposals, and accepted baseline agreements without labeling every paragraph.

## Cross-references and change impact

- Keep the document understandable within its own scope. Maintain detailed definitions in one primary source per topic; state the boundary this document relies on without mirroring another document's internal structure, detailed rules, or progress.
- Add body links where the reader needs a specific external contract, evidence, or background, and make that purpose clear in the sentence. Use an existing index for broad navigation.
- Record document-level state and implementation progress centrally in the source document and, when useful, its existing index. Avoid routinely copying these mutable facts into inbound link labels or summaries; note a limitation at the point of use only when it affects interpretation.
- State the accepted baseline needed for the proposal and preserve its confirmation basis. Linking another draft or deprecated record does not establish agreement; keep proposed changes distinct from effective contracts.
- Prefer stable document paths or contract sections. Reciprocal navigation is acceptable when each document owns its definitions; do not pass a key definition around a reference cycle.
- Read only the linked material needed for the task. A cross-reference does not require reading the whole target document or recursively following its links.

Maintain related documents according to actual impact, within the authorized scope:

- Wording, internal details, or progress updates normally affect only the edited document.
- When a path or referenced anchor changes, repair the directly affected links.
- When an effective contract changes or is retired, check the documents that actually depend on it and update affected statements. Report needed changes outside the authorized file scope instead of expanding the task.

Write project-local document links relative to the document being edited; crossing directory levels is valid. Avoid machine-specific absolute paths and local targets outside the project.

Link to external material only when it provides a key basis for the design or the user explicitly requests it; do not add it as routine navigation.

## References when needed

- Before drafting a new structured standalone manuscript using this skill's default format, read the [metadata rules](references/design-guidelines.md#document-metadata-and-annotations). Keep requested or established formats during revisions; this new-manuscript requirement does not add metadata to existing manuscripts or short inline drafts.
- Read [design-guidelines.md](references/design-guidelines.md) for substantive proposal organization, detailed interface treatment, or metadata and decision annotations that the requested manuscript needs.
- Read [writing-style.md](references/writing-style.md) when a substantial prose revision or a formatting question needs additional guidance.
- Use [design-template.md](assets/design-template.md) only when a structured manuscript would help and no supplied or established format takes precedence. It illustrates a working draft; do not fill every section by default.

A short, clear proposal can use this entrypoint without loading every reference.

## Review and deliver

Check that the target, reasoning, ownership, important conditions, and unresolved choices are coherent and supported. Keep confirmed design separate from verified implementation progress. Remove accidental template scaffolding and unrelated material.

An inline draft can be a complete deliverable. Drafting in chat or choosing this workflow does not by itself authorize saving files. Save only when the current task requests or authorizes file output, and inspect any saved content or diff. Do not silently promote a draft, overwrite a formal contract with an unaccepted proposal, move existing files, or implement the proposed change.

Report the requested draft, a usable link when saved, and the actual checks and remaining limits. Planned verification is not evidence that tests ran or that implementation exists.
