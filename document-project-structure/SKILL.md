---
name: document-project-structure
description: Create or substantively maintain project-structure and code-placement guides that help readers navigate a repository and place new work. Do not use for ordinary code exploration, design documents, or minor wording edits.
---

# Document project structure

Produce a practical guide to the project's structure and placement conventions. Treat agents as a primary audience by default, while honoring the request and project conventions when the guide also or primarily serves people. Its purpose determines whether it emphasizes navigation, placement decisions, or both; do not assume every project needs the same outline or level of detail.

## Establish the evidence and scope

Read the request and applicable project guidance, then inspect the existing guide, relevant entry points, and only the directories, code, or documents needed for the task. Use the repository to establish what currently exists; use confirmed decisions and project guidance to establish intended responsibilities and placement rules. Do not infer a convention merely from a file's present location, or infer that a documented target is implemented.

Distinguish existing structure, confirmed placement rules for paths not yet present, and legacy or transitional arrangements when the distinction matters. If evidence conflicts or an agreement's status is unclear, report the discrepancy; do not invent a rule, discard a confirmed convention as stale, or silently make a new architectural decision. Ask a focused question when resolving the discrepancy is necessary to state a material rule, and continue independent work within scope.

## Select useful content

Help readers find relevant parts of the project and decide where new work belongs. Describe major directories or targets and their responsibilities, clarify commonly confused placement boundaries, and include important entry points or non-obvious connections when they help a task. For example, a small flat package may need little more than source and test locations plus an unusual test-host connection; a larger application may need more detail about neighboring ownership boundaries.

For agents, make it clear when the guide helps, where to start, what related locations may need coordinated changes, and which existing project rules or task constraints govern confirmation when relevant. Prefer stable, decision-useful information over inventories that ordinary searches can readily recover, a complete directory tree, or descriptions of every type and test. Include individual files when they are useful entry points or their role is otherwise hard to discover. State placement rules at the specificity supported by the project; avoid turning examples or current implementation details into mandatory conventions or inventing approval requirements.

Keep detailed architecture, behavioral contracts, and execution instructions with their existing primary sources. Explain the local boundary needed for placement and link to details where useful, without duplicating them. Preserve consequential project-specific rules and exceptions when reducing repetition. Attribute a rule to another document only when that source supports it.

## Write and check

Follow the requested language, format, destination, and existing project conventions. For a new guide without a specified destination, use the project's established documentation location; do not impose a directory layout or create an index by default. When discoverability matters, check whether existing project guidance tells agents when to consult the guide. Report a missing or unclear entry point when useful; update `AGENTS.md` only when authorized, and do not add a redundant instruction. A discussion or inline draft does not by itself authorize saving files, moving code, or changing other documentation.

When condensing a guide, check whether readers can still locate relevant code, decide where new files belong, identify non-obvious coordinated changes, and understand applicable rules for structure changes. Preserve consequential exceptions; do not add a confirmation rule merely to answer the question.

Keep the guide current at the level of responsibilities and placement decisions, rather than requiring updates for every routine file addition. After writing, inspect the result against the evidence and requested scope. Check destinations of added or modified links; when a document path or heading changes or is removed, find references to that affected path or anchor. Do not audit untouched links or recursively traverse references by default. Repair affected references only within the authorized scope and report remaining impact. Distinguish static inspection from any runtime verification performed.
