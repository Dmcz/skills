# Swift project working agreements

These are reusable Swift engineering defaults. Keep project architecture, documentation entry points, product choices, and business contracts in the target project's own guidance, and preserve that guidance when adopting these defaults.

## Project context

- Follow the target project's documentation locations, structure conventions, and task-specific reading boundaries; do not assume a directory layout or named architecture component.
- Keep migrations, moves, and renames within the authorized task. Routine additions within established boundaries do not need separate approval; material changes to responsibility or module boundaries follow the task's decision rules.

## Code design principles

- Prefer the simplest idiomatic design that meets confirmed behavior and responsibility boundaries. Keep edits within the authorized scope; this does not require preserving the current decomposition.
- Always access instance properties and instance methods through `self.`, even when Swift permits the qualifier to be omitted. Parameters and local variables may share names with instance members; distinguish them using `self.member` and `member`.
- Use extensions only for focused protocol conformances, genuinely universal protocol default implementations, constrained generic behavior, and framework-required integration points. Do not use them to add responsibilities or hide an oversized implementation by distributing it across declarations or files; an extension is not an architectural, ownership, or dependency boundary.
- Consider extracting a dedicated project-owned type when it gives related behavior, state, or lifecycle a clear owner, or establishes a dependency boundary needed by the current task. Compare the complexity it removes with the assembly, forwarding, and coordination it adds; a distinct concept or dependency alone does not establish the need for a new type.
- Do not extend standard-library or framework-owned types with application-specific or domain-specific behavior. Prefer a wrapper, adapter, service, or standalone function.
- Do not provide empty protocol default implementations unless ignoring that requirement is explicitly safe and semantically valid.
- Do not use force unwrapping (`value!`), forced casts (`as!`), `try!`, or implicitly unwrapped optionals (`Type!`). Prefer optional binding, explicit initialization, and error propagation rather than assuming failure is impossible.
- Prefer optional element access (`first`, `last`) and iteration over manual indexing. Before array subscript or range access, explicitly validate all indices and bounds against the same stable data; caller contracts and index calculations alone are insufficient.
- Handle failures explicitly through error propagation, ending the current operation, or a semantically valid fallback. Do not replace failure handling with `fatalError`, `precondition`, or `preconditionFailure`, or hide failures through silent returns, arbitrary defaults, or ignored errors.

## Visual review

- If a conclusion requires visual judgment, use screenshots already provided by the user. If those screenshots are insufficient or unavailable, describe the specific screenshots needed and wait for the user to provide them.
- Do not open previews, simulators, or capture screenshots unless the user explicitly asks.

## Verification

- By default, perform static inspection only. Do not build, run tests, launch the app, or perform runtime verification unless the user explicitly asks.
