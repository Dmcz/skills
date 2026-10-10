# Writing style

Apply these rules to the document's requested language. Preserve its technical meaning before improving its presentation.

Follow explicit user requirements, applicable project conventions, and the existing document's format before using the skill's defaults. Keep formatting changes within the requested scope.

## Reference material and Chinese adaptation

Use these two sources for their respective purposes:

- [markdownlint](https://github.com/DavidAnson/markdownlint): Markdown formatting conventions and configurable static checks. Use the project's existing configuration to determine which rules apply.
- [Writing Clearly and Concisely](https://github.com/obra/the-elements-of-style/blob/main/skills/writing-clearly-and-concisely/SKILL.md): Language-neutral principles such as clear subjects, concrete statements, coherent paragraphs, and concise wording.

Keep design documents in Chinese by default, as specified in the skill. Apply Chinese grammar and punctuation; do not import English spelling, possessive forms, comma rules, or sentence patterns as requirements. Preserve necessary qualifications and uncertainty while making prose concise.

Use the local guidance below for routine writing. Consult the relevant source sections when a rule needs clarification, rather than reading both sources in full for every task. These are reference sources, not a requirement to install or invoke a separate writing skill.

## Meaning and certainty

- Distinguish existing behavior, a proposal, a requirement, and a possibility. Do not rewrite an assumption as a fact or an intended outcome as an established guarantee.
- Preserve the scope of statements: conditions, exceptions, timing, cardinality, and failure behavior. A shorter sentence is not an improvement if it changes the contract.
- Name the component that acts or owns state when that matters. Replace ambiguous pronouns and broad labels such as "the system" with the relevant component.
- Define a specialized term at its first relevant use, then use it consistently. Match terminology to actual code and project vocabulary.

## Structure and expression

Lead a section with its conclusion or purpose, then explain the evidence and implications. Give each paragraph one central point. Use connected prose for reasoning and lists for parallel items or sequences.

Prefer concrete behavior to evaluative adjectives. Replace claims such as "clean," "robust," or "flexible" with the responsibility, constraint, or change they describe. Remove repeated summaries, generic benefits, and background that the intended reader does not need.

Describe conditions before the behavior they control when this makes the relationship clearer. Use an active subject where it identifies responsibility. Preserve necessary technical terms rather than replacing them with a vague simplification.

Keep distinctions that help a decision, including genuine scope exclusions. Avoid rhetorical oppositions that add no design information.

## Markdown and examples

When project tooling is available and applicable project instructions permit it, run the configured markdownlint check on the changed Markdown documents. Treat the project configuration as the source of rule choices, including line-length limits. Fix relevant formatting issues while preserving meaning and the document's status annotations.

If the tool is unavailable, apply the local formatting checks and do not claim that markdownlint ran. Tool installation and lint-configuration changes must be within the user's requested scope. Do not silently change configuration to suppress a conflict with the requested format.

- Use one document title and a consistent heading hierarchy. Give headings descriptive names.
- Follow the definitions and format precedence in the [design guidelines](design-guidelines.md#document-metadata-and-annotations) for metadata and decision or evidence annotations. In the default format, put annotations in a blockquote below the relevant heading, with blank lines around it, and keep status tags out of heading text. Preserve an existing annotation format during a narrow edit.
- Separate headings, paragraphs, lists, and fenced blocks with blank lines. Use numbered lists for ordered steps and bullets for parallel points.
- Use tables for comparable options, responsibilities, or mappings when they are easier to read than prose.
- Format identifiers, paths, commands, and literal values as inline code. Label fenced code blocks with the appropriate language.
- Use descriptive link labels. Keep links portable for the document's destination.
- Keep examples small and label illustrative code as illustrative when it is not verified implementation. Introduce a diagram with the question it answers and check its consistency with the prose.

## Revision check

Compare a rewritten passage with its source for changed meaning. For example:

Original: "If cancellation arrives before persistence completes, the worker discards the pending result."

Unsafe rewrite: "Cancellation discards the result."

The rewrite loses both the timing condition and the distinction between a pending and persisted result. Preserve those distinctions while removing unnecessary wording.

When editing a document, keep facts and decisions outside the requested change stable. Surface any proposed change to the design itself.
