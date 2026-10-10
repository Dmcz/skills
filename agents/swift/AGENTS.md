# Project Working Agreements

## Scope of changes

- Keep changes limited to what the current task requires. Apply these agreements to new and modified code, without proactively changing unrelated existing code solely to enforce these agreements, unify style, or perform cleanup.

## Documentation and reusable workflows

- Keep this file self-contained for team-wide working agreements, critical repository-specific constraints, directory purposes, and task-specific reading boundaries. Store detailed designs, engineering conventions, and task procedures under `docs/`.
- Read relevant code to establish current implementation facts. Use formal documents to understand confirmed concepts, responsibilities, contracts, and rationale; use current requirements and explicitly confirmed decisions to determine intended changes.
- Use `docs/design/`, outside `drafts/`, for formal design references. Distinguish implemented behavior from confirmed targets that are not yet implemented.
- Use `docs/design/drafts/` for working design manuscripts covering goals, constraints, proposals, alternatives, and unresolved choices. Consult a relevant draft during its associated discussion, initial implementation, or ongoing implementation task; do not make drafts the default reading focus for unrelated tasks or treat unchosen options as requirements. The directory does not imply automatic deletion.
- Use `draft-software-design` to develop or revise working manuscripts, and `document-confirmed-design` to record or maintain confirmed formal designs. Ordinary engineering questions and minor wording edits do not automatically require either workflow. Honor explicit skill invocations within the requested scope.
- Use `docs/conventions/` for detailed engineering agreements and examples.
- Use `docs/workflows/` for reusable task procedures.
- Read only documents and sections needed for the current task, and follow applicable engineering conventions and workflows. README files and indexes are not mandatory first steps; use the [design document index](docs/design/README.md) when needed to locate a relevant reference. Follow document links only when their content is needed for the task.
- When locating related implementation, creating files, deciding file placement, or changing directory structure, consult [Project Structure](docs/project-structure.md) as needed. It defines directory organization, file placement, and related naming rules. If a placement convention is unclear or there is a concrete reason to adjust it, explain the issue, rationale, and proposed change, then confirm with the user before making the related decision or adjustment.
- When understanding component responsibilities, dependencies, assembly, or ownership, consult [Application Architecture](docs/design/application-architecture.md) and the relevant specialist designs as needed.
- Give each document a clear scope and keep one primary source per topic. When documentation and code differ, distinguish an unimplemented confirmed target from an outdated description; point out unresolved discrepancies rather than silently assuming they agree.
- Documentation and workflows must respect the change authorization and verification boundaries in this file. Writing a draft or formal document does not authorize implementation or other file changes.
- Use `.agents/skills/<skill-name>/SKILL.md` for formal Codex Skills. Ordinary documents under `docs/` are reference material and are not automatically discovered as Skills; consider packaging a workflow as a Skill once it is stable and repeatedly used.

## Design and architecture discussions

- During design and architecture discussions, stay in discussion mode and keep the workspace read-only until the user explicitly asks to modify, fix, implement, or save something.
- While discussion remains read-only, do not create, modify, delete, stage, or temporarily write any files. Detailed design discussion alone is not authorization to save a design document.
- Once the user explicitly authorizes file changes, make the changes required by the task within its authorized scope. Do not revert or remove an authorized change merely because the conversation originally started as a discussion; verify the written files before finishing.
- Answer the user's current question directly before expanding into related considerations.
- Read the relevant code first to understand the existing design, layout, and constraints.
- If a conclusion requires visual judgment, use screenshots already provided by the user. If those screenshots are insufficient or unavailable, describe the specific screenshots needed and wait for the user to provide them.
- Do not open previews, simulators, or capture screenshots unless the user explicitly asks.
- When multiple approaches are viable, explain the meaningful trade-offs and give a recommendation without treating it as a settled decision.
- Ask a focused question only when missing information would materially change the conclusion; otherwise, state a reasonable assumption.
- If the user's reasoning conflicts with the current assessment, explain the disagreement with concrete evidence instead of simply agreeing.
- Treat follow-up messages as continuing the current task and its confirmed constraints, updating them when the user clearly changes the goal or authorization scope. If a follow-up makes the intended goal or authorization scope materially unclear, ask a focused question before taking action that depends on the answer. Revise earlier conclusions when appropriate.

## Code design principles

- Prefer the simplest idiomatic design that preserves clear responsibilities and dependency boundaries.
- Apply established best practices and clean-architecture principles pragmatically, introducing abstractions only when they serve a concrete current need.
- Favor designs that keep changes local and make ownership, data flow, and dependencies easy to understand.
- Always access instance properties and instance methods through `self.`, even when Swift permits the qualifier to be omitted. Parameters and local variables may share names with instance members; distinguish them using `self.member` and `member`.
- Do not use extensions to add new responsibilities to a type or to hide an oversized implementation by distributing it across multiple declarations or files. An extension is not an architectural, ownership, or dependency boundary.
- Prefer extracting a dedicated project-owned type when behavior represents a separate domain concept, policy, dependency, side effect, or lifecycle.
- Extensions are permitted only for focused protocol conformances, genuinely universal protocol default implementations, constrained generic behavior, and framework-required integration points.
- Do not extend standard-library or framework-owned types with application-specific or domain-specific behavior. Prefer a wrapper, adapter, service, or standalone function.
- Do not provide empty protocol default implementations unless ignoring that requirement is explicitly safe and semantically valid.

## UI copy and accessibility

- Write all new or updated user-facing UI copy in English. Do not translate unrelated existing copy unless requested.
- Do not add accessibility-specific Swift code by default, including SwiftUI `.accessibility*` modifiers, accessibility environment values, and `UIAccessibility` APIs. Add it only when explicitly requested.

## Verification

- By default, perform static inspection only.
- Do not build, run tests, launch the app, or perform runtime verification unless the user explicitly asks.
- When finishing, state which checks were actually performed and which relevant verification steps were not performed.
