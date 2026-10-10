---
name: draft-software-design
description: Draft or revise working manuscripts for proposed software designs, architecture changes, and technical RFCs. Use when the user asks for a design manuscript, a proposal to discuss, or analysis of goals, constraints, options, and unresolved choices. Do not use for publishing settled design agreements, ordinary engineering questions, or routine wording edits.
---

# Draft software design

Produce a working manuscript that helps engineers discuss a change and decide how to proceed. Explain the target, the relevant current behavior, plausible choices, and what still needs a decision. Keep the depth proportional to the task.

## Purpose, placement, and reading role

This workflow develops a design for discussion. Writing a draft does not make its proposals accepted, turn it into a formal reference, or authorize implementation. Preserve accepted agreements as the baseline; identify proposed changes to them explicitly.

Publishing or maintaining confirmed design documentation is a separate workflow. Ordinary engineering discussion and small wording edits do not require a design-manuscript workflow. Honor an explicit invocation or delivery instruction without expanding the task merely to fit this skill.

When saving a new manuscript without a specified path, use a `drafts/` directory within the project's design-documentation area, for example `docs/design/drafts/`. Explicit destinations and applicable project layout take precedence. Keep an existing file in place unless moving it is authorized. The directory describes the artifact's role, not a deletion policy.

Drafts are not the default reading entry or authoritative contract for unrelated implementation tasks. A draft explicitly associated with an initial implementation or an active change may provide important direction. Its alternatives and unresolved details do not automatically become requirements.

Use code to establish current implementation facts and relevant formal documents to establish accepted concepts, responsibilities, and contracts. Requirements and confirmed design choices establish the intended change. If materials disagree, distinguish an unimplemented target from an outdated description; do not automatically treat either the code or document as correct. Follow the project's own reading rules.

## Establish and develop the proposal

Reuse the purpose, scope, constraints, and requested deliverable already supplied. Read only the related code and references needed for the proposal. Ask a focused question when missing information materially changes the design; leave genuine unresolved choices visible rather than inventing answers.

Ground current-behavior claims in inspected code or supplied material. Explain ownership, data relationships, dependency direction, and a representative flow where they affect the decision. Compare meaningful alternatives and explain reasons, costs, and limits. Do not manufacture options or introduce abstractions without a concrete need.

Verify external API capabilities and platform behavior that materially affect the proposal's feasibility or choice, using authoritative documentation or SDK declarations applicable to the target version. If verification is unavailable or inconclusive, mark the dependency as an unverified assumption and explain which choices or feasibility conclusions remain conditional. Keep research focused on those decision-relevant facts.

Expand interfaces, failure behavior, concurrency, lifecycle, migration, and verification only where they affect this proposal. Keep implementation plans, project-wide document reorganization, and unrelated code cleanup outside the requested scope.

Write in Chinese by default unless the request or existing artifact establishes another language. Preserve identifiers and existing useful format conventions. For a new manuscript, make its working-draft purpose clear; distinguish current facts, proposals, and accepted baseline agreements without labeling every paragraph.

## References when needed

- Before drafting a new structured standalone manuscript using this skill's default format, read the [metadata rules](references/design-guidelines.md#document-metadata-and-annotations). Keep requested or established formats during revisions; this new-manuscript requirement does not add metadata to existing manuscripts or short inline drafts.
- Read [design-guidelines.md](references/design-guidelines.md) for substantive proposal organization, detailed interface treatment, or metadata and decision annotations that the requested manuscript needs.
- Read [writing-style.md](references/writing-style.md) when a substantial prose revision or a formatting question needs additional guidance.
- Use [design-template.md](assets/design-template.md) only when a structured manuscript would help and no supplied or established format takes precedence. It illustrates a working draft; do not fill every section by default.

A short, clear proposal can use this entrypoint without loading every reference.

## Review and deliver

Check that the target, reasoning, ownership, important conditions, and unresolved choices are coherent and supported. Keep confirmed design separate from verified implementation progress. Remove accidental template scaffolding and unrelated material.

During discussion, respond inline. Save only when requested or already authorized, and inspect the saved content or diff. Do not silently promote a draft, overwrite a formal contract with an unaccepted proposal, move existing files, or implement the proposed change.

Report the requested draft, a usable link when saved, and the actual checks and remaining limits. Planned verification is not evidence that tests ran or that implementation exists.
