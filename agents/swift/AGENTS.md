# Project Working Agreements

## Documentation and reusable workflows

- Keep this file focused on team-wide engineering agreements, critical project constraints, directory purposes, and task-specific reading boundaries. Store detailed designs, engineering conventions, and task procedures under `docs/`.
- Use `docs/design/`, outside `drafts/`, for formal design references. Distinguish implemented behavior from confirmed targets that are not yet implemented.
- Use `docs/design/drafts/` for working design manuscripts covering goals, constraints, proposals, alternatives, and unresolved choices. Read a relevant draft during its associated discussion, initial implementation, or ongoing implementation task; do not make drafts the default reading focus for unrelated tasks. The directory does not imply automatic deletion.
- Use `docs/conventions/` for detailed engineering agreements and examples, and `docs/workflows/` for reusable task procedures.
- Use the [design document index](docs/design/README.md) when needed to locate a relevant reference, and follow applicable engineering conventions and workflows.
- When locating related implementation, creating files, deciding file placement, or changing directory structure, consult [Project Structure](docs/project-structure.md) as needed. It defines directory organization, file placement, and related naming rules. If a placement convention is unclear or there is a concrete reason to adjust it, explain the issue, rationale, and proposed change, then confirm with the user before making the related decision or adjustment.
- When understanding component responsibilities, dependencies, assembly, or ownership, consult [Application Architecture](docs/design/application-architecture.md) and relevant specialist designs as needed.
- Give each document a clear scope and keep one primary source per topic.
- Keep project-owned Codex Skills in `.agents/skills/<skill-name>/SKILL.md`.

## Code design principles

- Prefer the simplest idiomatic design that preserves clear responsibilities and dependency boundaries. Apply established best practices and clean-architecture principles pragmatically, introducing abstractions only when they serve a concrete current need. Favor local changes and clear ownership, data flow, and dependencies.
- Always access instance properties and instance methods through `self.`, even when Swift permits the qualifier to be omitted. Parameters and local variables may share names with instance members; distinguish them using `self.member` and `member`.
- Use extensions only for focused protocol conformances, genuinely universal protocol default implementations, constrained generic behavior, and framework-required integration points. Do not use them to add responsibilities or hide an oversized implementation by distributing it across declarations or files; an extension is not an architectural, ownership, or dependency boundary.
- Prefer extracting a dedicated project-owned type when behavior represents a separate domain concept, policy, dependency, side effect, or lifecycle.
- Do not extend standard-library or framework-owned types with application-specific or domain-specific behavior. Prefer a wrapper, adapter, service, or standalone function.
- Do not provide empty protocol default implementations unless ignoring that requirement is explicitly safe and semantically valid.

## UI copy and accessibility

- Write all new or updated user-facing UI copy in English. Do not translate unrelated existing copy unless requested.
- Do not add accessibility-specific Swift code by default, including SwiftUI `.accessibility*` modifiers, accessibility environment values, and `UIAccessibility` APIs. Add it only when explicitly requested.

## Visual review

- If a conclusion requires visual judgment, use screenshots already provided by the user. If those screenshots are insufficient or unavailable, describe the specific screenshots needed and wait for the user to provide them.
- Do not open previews, simulators, or capture screenshots unless the user explicitly asks.

## Verification

- By default, perform static inspection only. Do not build, run tests, launch the app, or perform runtime verification unless the user explicitly asks.
