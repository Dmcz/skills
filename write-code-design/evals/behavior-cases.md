# Behavior evaluation cases

These cases are maintenance material for evaluating skill selection and observable behavior. They are not instructions to load during ordinary document work. Run them when behavioral evaluation is requested and within the authorized environment; reading this file or passing structural validation is not a behavioral test.

## Evaluation method

- Start each case in a fresh conversation with the normal agent instructions and an isolated disposable workspace. Populate only the listed input artifacts; keep the skill under evaluation available without changing it. Keep generated files out of the skills repository.
- For selection checks, expose the skill's name and description through normal discovery. Do not force invocation for cases without an explicit skill name, especially the negative case. Record whether the skill was selected separately from output quality.
- Give the executing model the user request and raw artifacts, not the expected results or earlier review conclusions. The evaluator uses the criteria below after the run. A human evaluator or an independent model can assess the result; delegation is not required by this file.
- Inspect the actual answer, actions, saved artifacts, and differences from the input. Judge meaning, evidence, scope, and delivery rather than matching generated wording or requiring a fixed section count.
- Record the skill revision, model and configuration, case ID, observed selection, actions, artifact locations, result, and evidence for any failure. Use pass, fail, or not run; report an unavailable capability as a limitation. A pass in one case does not establish performance in the others.
- Do not build the sample project, run its tests, install tools, or perform Git or external-service actions. The requests below need only reading, drafting, and authorized document or code edits in the disposable workspace.

## B01: Explicit creation and saved delivery

Input artifact: `cache.py`.

```python
class Cache:
    def __init__(self):
        self.items = {}

    def get(self, key):
        return self.items.get(key)

    def put(self, key, value):
        self.items[key] = value
```

User request:

> 用 $write-code-design 为这个缓存增加 invalidate(key) 起草中文设计文档，保存到 docs/cache-invalidation.md。删除不存在的键应当没有副作用。只写设计，不修改代码。

Expected results:

- Select the skill and inspect the supplied code before describing current behavior. Distinguish the existing `get` and `put` methods from the proposed `invalidate` method.
- Explain the ownership, invalidation behavior, and meaningful verification scenarios, including an absent key. Treat additional interface choices as proposals unless the request establishes them.
- Save the document at the requested path, inspect its final contents, and provide a usable link. For this new document with no established format, use accurate local dates and separate document state from implementation status.
- Leave `cache.py` unchanged. Do not claim that the proposed checks ran or that the implementation exists.

## B02: Narrow wording edit with existing status headings

Input artifact: `docs/cache-rfc.md`.

```markdown
# Cache RFC

- Updated: 2025-11-03

## [Accepted] Cancellation

If cancellation arrives before persistence completes, the worker discards the pending result.

## [Accepted] Ownership

The Repository owns the cache.
```

User request:

> 用 $write-code-design 只润色 docs/cache-rfc.md 的 Cancellation 段落，保持英文，保留所有技术条件和既有格式。

Expected results:

- Preserve the timing condition, the worker's responsibility, and the distinction between a pending and a persisted result.
- Keep both status headings, the date, and the Ownership section unchanged. Do not add default metadata, translate the document, or relocate status annotations.
- Inspect the saved difference or compare the affected context with the original. Report only the actual edit and checks performed. Leaving already-clear wording unchanged with an explanation is acceptable.

## B03: Explicit discussion without persistence

Input artifact: the `cache.py` supplied in B01.

User request:

> 用 $write-code-design 先讨论手动失效和 TTL 对这个缓存的取舍，在对话中给出建议，暂时不保存，也不实现。

Expected results:

- Select the explicitly requested skill, inspect current behavior, and give a proportionate comparison tied to the available requirements.
- Ask a focused question if a missing freshness requirement materially changes the recommendation, or make a conditional recommendation with the uncertainty visible.
- Keep the recommendation distinct from a confirmed decision. Do not create or edit files, implement either option, or require routine approval between sections.

## B04: Indirect request with an established English format

Input artifact: `docs/cache-rfc.md`.

```markdown
# Cache Invalidation RFC

Status: Draft

## Context

The cache currently provides get and put.

## Proposal

Add invalidate(key). A missing key must be a no-op.

## Consequences

Callers may invalidate cached values after an update.
```

User request:

> 补充这份 RFC 的接口取舍和验证思路，保持原来的英文和章节结构，修改 docs/cache-rfc.md。所有内容都是待评审的方案。

Expected results:

- Select the skill through normal discovery. Keep the established language, Draft status, and section structure.
- Explain relevant interface choices and verification scenarios inside the existing sections; do not introduce the Chinese template's fields, headings, or default annotations.
- Keep proposal claims separate from current behavior, inspect the saved result, and preserve unaffected content. Do not turn planned verification into reported success.

## B05: Missing code and incomplete evidence

Input artifacts: none. No queue source or documentation is available.

User request:

> 把现有队列模块的并发取消机制整理成设计文档草稿，说明当前哪个组件负责清理，以及取消发生在持久化前后分别会怎样。先在对话中给我。

Expected results:

- Select the skill, establish that the requested current behavior cannot be verified, and request the relevant source or material without a fixed questionnaire.
- A preliminary outline or proposed behavior is acceptable if its assumptions and evidence limits are explicit. Do not invent cleanup ownership, cancellation ordering, benchmarks, or test results.
- Explain which conclusions depend on the missing evidence. Do not save a document or build a prototype.

## B06: A proposal challenges an accepted decision

Input artifact: `docs/adr-001.md`.

```markdown
# Cache ownership

Status: Accepted

The Repository owns the cache. Workers use the Repository interface.
This keeps cache lifetime shared across workers.
```

User request:

> 为这份已接受的 ADR 补充一个评估 Worker 持有缓存的方案，先在对话中起草。新方案尚未决定，请说明它与现有生命周期约定的冲突和取舍。

Expected results:

- Preserve the accepted Repository ownership decision and its rationale as the baseline. Describe Worker ownership as a proposal and link the accepted record where useful.
- Explain the lifetime conflict and consequences. Identify what would need a decision before replacement, without presenting the ADR as already superseded.
- Do not edit the ADR, claim approval of the alternative, or silently reconcile incompatible ownership claims.

## B07: Prior assistant suggestions do not establish confirmation

Input material supplied with the request:

> 上次助手的建议草稿：可以把 TTL 设为 30 秒，并让 Worker 持有缓存。用户当时没有确认，项目也没有相关已接受决策。

User request:

> 用 $write-code-design 把这段材料整理成简短中文设计草稿，先在对话中给出，区分建议和已确认事项。

Expected results:

- Treat the TTL and Worker ownership as recommendations, not confirmed decisions. Identify any missing requirements that affect their suitability.
- Do not infer approval from the existence of the earlier draft or invent accepted records, decision-makers, implementation status, or research evidence.
- Keep the response small enough for the supplied material; a full document template is unnecessary.

## B08: Negative selection for a direct code fix

Input artifact: `cache.py`.

```python
class Cache:
    def __init__(self):
        self.items = {}

    def get(self, key):
        return slef.items.get(key)
```

User request:

> 修正 cache.py 中 get 方法的拼写错误。

Expected results:

- Do not select `write-code-design` merely because the request changes code. Make the requested small code correction through the normal coding workflow.
- Do not replace the fix with a design discussion, create an RFC, or introduce design-stage approval gates.
- Preserve unrelated code. A successful code fix does not excuse an incorrect skill selection; record both outcomes.
