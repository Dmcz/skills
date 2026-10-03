---
name: write-code-design
description: Draft, revise, or organize software design documents and technical RFCs grounded in requirements, existing code, and constraints. Use when explaining a proposed code or architecture change, or clarifying the structure and scope of related design documents.
---

# Write code design documents

Produce a document that lets an engineer understand the proposed change, assess its consequences, and identify what still needs a decision. Keep the depth proportional to the change and the reader's needs.

## Language and resources

Write the document in Chinese by default. Follow an explicitly requested language or the language of an existing document. Preserve code identifiers, API names, and source titles.

Explicit user requirements take precedence over this skill's defaults. Follow applicable project conventions and preserve the existing document's format conventions. Use the skill's default metadata and annotation format when no requested or established convention exists. A narrow edit does not justify reformatting unrelated content or adding metadata.

Agent instructions and references in this skill are maintained in English. The Chinese README explains the skill to maintainers; it is not an additional source of execution rules.

- Read [design-guidelines.md](references/design-guidelines.md) when developing or revising the substance of a design, organizing its sections or related files, or defining document metadata and decision or evidence annotations. It defines the organization criteria, labels, and fields; the template only illustrates their use.
- Read [writing-style.md](references/writing-style.md) when drafting or editing document prose. Apply its Markdown conventions using the project's markdownlint configuration when available, and use the language-neutral principles from Writing Clearly and Concisely while keeping Chinese prose natural and accurate.
- For a new document without an established format, adapt [design-template.md](assets/design-template.md). The Chinese template is a starting point, not a list of mandatory sections. Preserve a supplied template or an existing document's useful structure.

## Establish the brief

Identify the intended readers, problem, desired behavior, scope, constraints, and requested deliverable from the conversation and available material. Reuse information already provided.

Ask a focused question when missing information would materially change the recommendation or prevent a useful draft. Continue independent work where possible. For gaps that can remain open, state the uncertainty and its effect on the design instead of filling it with invented detail. Avoid fixed question counts and routine confirmations between sections.

Follow the requested delivery mode: respond inline during discussion; create or update a document when the user asks to save or edit it. Use the requested destination or the repository's document conventions. Treat documentation, product implementation, runtime verification, and Git operations as separate actions; perform each only within the user's authorized scope and applicable project instructions.

## Ground the proposal

For an existing codebase, inspect the files, interfaces, and project guidance that affect the change. Establish current responsibilities, dependencies, and behavior before describing proposed changes. A wording-only edit usually needs only its affected context.

Tie important claims about current behavior to inspected code or supplied material. Clearly distinguish current behavior, proposed behavior, assumptions, and unresolved decisions where confusing them would affect implementation. If code is unavailable, describe the limits of the available evidence.

Check authoritative external sources when a design depends on uncertain or changing APIs or platform behavior. Link relevant evidence without turning every writing task into a broad research exercise.

## Develop and write the design

Use the [document organization criteria](references/design-guidelines.md#document-structure-and-file-responsibilities) to choose or revise the outline and file boundaries within scope. Revisit the organization when new material changes the reader's path through the design.

Explain what changes and why. Connect the recommended approach to the stated goals and constraints. Compare plausible alternatives when a meaningful choice exists, including keeping the current approach when relevant. Describe costs and limitations as well as benefits; do not manufacture alternatives to satisfy a quota.

Make component ownership, dependency direction, and the important execution or data flow understandable. Add detail about state, lifecycle, interfaces, failures, or migration only where it affects correctness or a design decision. Use a small example or diagram when it resolves a concrete ambiguity.

When metadata or annotations are needed, follow their definitions in the design guidelines and the document's applicable format. Keep preparation and update dates accurate and distinguish document state from implementation status.

A recommendation remains a proposal until explicit user agreement or a still-applicable accepted project decision establishes it. Describe proposed verification separately from checks actually performed.

## Review and deliver

Review the document as an engineer who has not read the conversation:

- Can the reader explain the problem, the proposed behavior, and the reason for the choice?
- Can the reader navigate from the overview to relevant details and locate authoritative shared definitions?
- Are component responsibilities and interactions consistent across prose, tables, diagrams, and examples?
- Are important assertions supported, and do open questions identify what they block?
- Did rewriting preserve conditions, guarantees, limitations, and uncertainty?
- Does every remaining section help evaluate or implement this design?

Fix issues within scope. Remove template instructions and accidental placeholders from a finished document; retain genuine unresolved questions as explicit open questions. Preserve established decisions during a narrow edit, and surface substantive changes rather than silently presenting them as wording fixes.

After saving a new document or a substantial rewrite, inspect the saved artifact to confirm its destination and final content. For a partial edit, inspect the diff or compare the affected context with the original to confirm the requested change and preservation of unrelated content. If saving or inspection fails, report the limitation instead of claiming a completed delivery.

Return the requested document or revision, with a link when saved, and a short account of material changes, outstanding decisions, and the verification actually performed. Do not claim approval, runtime success, or independent reader testing without evidence.
