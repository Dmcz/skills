---
name: document-confirmed-design
description: Write or maintain formal software-design references from confirmed decisions and relevant current facts. Use when the user asks to document settled concepts, relationships, responsibilities, contracts, and future directions, consolidate an agreed working draft, or substantively update an existing formal design reference. Do not use to develop unchosen proposals, compare architecture options, or answer ordinary engineering questions. Routine wording edits alone should not trigger this skill. Honor explicit invocation while keeping the edit within the requested scope.
---

# Document confirmed design

Produce a formal reference that faithfully states the effective agreements and can be understood without the original conversation. Formal describes the document's role as a confirmed reference, not its length or proof that implementation is complete. A source comment, a short note, or a detailed specification can serve this role.

## Select and explain the content

- Start from the user's latest clarified purpose, supplied summary, explicit agreements, and still-valid accepted records. Earlier proposals, abandoned approaches, examples, and arguments are background rather than a transcript to preserve.
- Organize the reference around the reader's design questions: the problem being addressed, agreed concepts and data relationships, ownership and responsibility boundaries, capabilities and contracts, and reasons for confirmed decisions. Include identified future directions at the requested level. Use code to verify facts rather than following a traversal of types, methods, fields, or execution branches. Add the context needed for an independent reader without introducing new decisions or inferring unconfirmed rationale.
- Preserve conditions, exceptions, timing, and limits. Do not strengthen a general goal into a specific execution contract, select an unstated strategy, or turn an assistant recommendation into an agreement.
- Distinguish current behavior, confirmed targets, and unresolved scope where confusion would change the meaning. Confirmed goals may be unimplemented. A deferred possibility is not a commitment to implement it.
- Select details that explain responsibility boundaries, contracts readers need to rely on, or consequential confirmed design choices. Express execution behavior through its meaning, guarantees, and ownership of actions and outcomes. Agreement on a mechanism does not by itself justify documenting its full execution sequence. Retain relevant mechanisms and concurrency guarantees without expanding every discussion into exhaustive implementation details.
- Handle new conflicts, missing decisions, or substantive concerns through the [clarification rules](#clarify-conflicts-before-continuing).

As a selection test, ask: if the internal implementation changed but responsibilities and behavior stayed the same, would this passage still be useful? If so, it usually belongs in the main design explanation. If not, assess whether it explains a key implementation choice the reader needs to understand; do not include it merely because the current code does it or it was discussed. Leave details that add no design understanding in source; mention identifiers or locations only when they help the reader.

## Placement and reading role

Formal documentation is for looking up effective concepts, responsibilities, contracts, and design rationale. When working on existing implementation, related code establishes actual structure and behavior; relevant formal documents establish the agreements the change must respect. Requirements and confirmed choices establish the intended change. Distinguish an unimplemented target from an outdated description instead of automatically preferring code or prose.

Working manuscripts belong in the project's design-area `drafts/` directory and are read for explicitly associated discussion or implementation work. They are not automatically formal references. Extract the confirmed content when asked to consolidate a manuscript; retain only the unresolved boundaries needed to explain the effective agreement.

For a new formal file, use the project's formal-documentation location outside `drafts/`, unless the user specifies another destination. Follow project layout and preserve existing paths. Source comments stay in the requested source file. Do not move, delete, or archive a manuscript or reorganize indexes unless authorized.

## Verify and write at the requested level

Use the discussion and provided materials first. When a current-code claim needs checking, read the relevant declarations or affected context. Follow repository instructions; do not perform a project-wide review or load broad references merely to make the document more comprehensive.

Verify external API or platform facts used as design evidence against authoritative documentation or SDK declarations for the applicable version, and retain their source and relevant version context. A confirmed design choice does not verify the external facts it relies on. If evidence is unavailable or inconclusive, identify the gap without presenting the fact as verified. Keep checked facts and their provenance even when they disagree with an agreement; follow the [clarification rules](#clarify-conflicts-before-continuing) when uncertainty or a discrepancy affects how that agreement should be stated. Limit checking to evidence needed for the requested record.

Write in Chinese by default unless the request or existing artifact establishes another language. Preserve identifiers and terminology. State the data relationships and component responsibilities directly.

Follow the requested format and useful existing conventions. Short records do not need full-specification scaffolding; detailed accepted designs may need more explanation. Do not add dates, status taxonomies, fixed sections, examples, or checklists by default. Mark approval and implementation status only as needed to preserve meaning.

Use links in the document body by default for cross-references to directly relevant documents within the current project that provide the needed responsibilities, contracts, or background. Write these links relative to the document being edited; crossing directory levels is valid when the reference is relevant and stays within the project. Mention type names and source locations as plain text by default, rather than linking each symbol. Avoid machine-specific absolute paths and local targets outside the project.

Link to external material only when it provides a key basis for the design or the user explicitly requests it; do not add it as routine navigation.

Save only when requested or already authorized, and update only the requested artifact. Preparing a formal reference does not confer new approval or authorize implementation.

## Clarify conflicts before continuing

When a conflict, missing decision, or substantive concern makes it unclear how an effective agreement should be stated, explain the checked facts or evidence gap, identify the affected agreement, and ask a focused question about what the record should say. Pause drafting and saving the affected content until the user clarifies. If the issue affects the document's central agreement or purpose, pause the whole artifact. Preserve existing content while waiting; independent inspection and unaffected preparation may continue.

Do not silently change an agreement's status or select a replacement design. When the supplied material already clearly distinguishes an unimplemented confirmed target from current behavior, record that distinction without asking again. An explicitly unresolved implementation detail or evidence limit can likewise be recorded without a question when the agreement's meaning is clear.

Once the user clarifies, resume the requested work within its existing authorized scope and inspect any saved changes.

## Check the result

Compare the record with the final agreements and intended reader. Check that its main line explains the design and its reasons rather than paraphrasing code execution, and consolidate repeated explanations of the same concept. Remove material retained only because it appeared earlier in the discussion. Verify that ownership, guarantees, decision status, and implementation status did not change through rewriting.

After saving, inspect the affected content or diff and report the actual change and checks. Identify remaining uncertainty briefly; do not claim implementation or runtime verification from completing the document.

Maintenance [behavior evaluation cases](evals/behavior-cases.md) are available for requested evaluations; do not load them during ordinary documentation work.
