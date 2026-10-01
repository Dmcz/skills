# Skills repository maintenance

These instructions apply when creating or maintaining skills in this repository. A skill's execution rules belong inside its own directory so it can be used in another project.

## Organization and language

- Keep each skill in an independent directory at the repository root. Match the directory name to the frontmatter `name`; use lowercase letters, digits, and hyphens, and keep names unique within this repository.
- Write Agent instructions, reference guidance, and evaluation procedures in English. Write maintainer-facing README files in Chinese. Literal labels and input examples may use the language required by their task.
- Choose template and output languages according to the skill's workflow and user requirements; the authoring language does not determine the output language.
- Require `SKILL.md` for each skill. Add references, scripts, assets, or evaluation cases only when they serve a concrete need; avoid empty resource directories and unfinished scaffolds.

## Editing and delivery

- Inspect the affected skill and relevant callers before changing shared definitions or removing resources. Preserve unrelated instructions, supported metadata, and invocation policies.
- Keep execution rules in `SKILL.md` or linked resources within the skill. Do not require the repository's root README or `AGENTS.md` for execution in another project.
- Define a rule in one authoritative execution source. A template illustrates its use; a maintainer README may explain it without adding separate execution requirements. Check affected examples and explanations when changing a rule.
- Update the root README's catalog when adding, renaming, removing, or changing the purpose of a skill. Keep internal file inventories in a skill's own documentation when useful.
- Inspect saved files after edits. Check affected frontmatter, local file links, and reference anchors using available tooling or static inspection, and fix issues within the requested scope.
- For changes to selection or workflow behavior, consider relevant cases that inspect actual actions and outputs. Keep structural validation and behavioral evaluation results separate, and report what was performed and any remaining limits.
