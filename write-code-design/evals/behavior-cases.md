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

## B09: Reorganize one cohesive design and preserve references

Input artifact: `docs/cancellation.md`.

```markdown
# 取消设计

文档状态：设计讨论记录
实现情况：未核实

## 清理

> 状态：已确认

Repository 负责丢弃尚未持久化的结果，Worker 通过 Repository 接口请求清理。

## 补充笔记

取消发生在持久化完成前时丢弃待写结果；持久化完成后不回退已写结果。
用户希望取消操作不会留下尚未写入的中间结果。

## 重复调用

> 状态：建议

重复取消同一个任务不产生额外副作用，具体去重方式待定。

## 总体方案

Worker 接收取消请求并通知 Repository，Repository 根据持久化状态处理结果。

## 验证

需要分别检查持久化完成前后取消，以及同一任务重复取消。

## 又一条补充

持久化完成后不回退已写结果。
```

Input artifact: `docs/README.md`.

```markdown
# 设计入口

[重复取消的方案](cancellation.md#重复调用)
```

User request:

> 用 $write-code-design 整理 docs/cancellation.md 的章节，把问题、总体方案和局部规则组织清楚，合并重复说明。可以调整标题和顺序；如改动锚点，同步修复 docs/README.md。保留已有决定和未决事项，只改文档。

Expected results:

- Select the skill, inspect both supplied files, and reorganize around the problem, overall approach, and relevant detail. Keep this small, cohesive design in one file rather than mechanically creating overview and module files.
- Preserve the confirmed cleanup ownership, cancellation timing, persisted-result guarantee, proposed repeated-cancellation behavior, and undecided deduplication mechanism. Do not promote repeated cancellation to a confirmed decision.
- Consolidate the duplicated post-persistence statement without dropping its condition. Preserve the established metadata and annotation conventions; do not claim verified implementation or execution of the proposed checks.
- Keep the inbound link valid, whether by retaining its target heading or repairing the link after a heading change. Inspect the saved changes and report the material reorganization and actual checks.

## B10: Organize related files around an authoritative shared contract

Input artifact: `docs/design/README.md`.

```markdown
# 任务执行设计

Worker 调度任务，Repository 持有待写结果并负责持久化。
共享取消规则以 [契约](contracts.md#取消) 为准。
其他说明：[Worker](worker.md)，[已接受的归属决定](adr-001.md)。
```

Input artifact: `docs/design/contracts.md`.

```markdown
# 共享契约

## 取消

> 状态：已确认

取消发生在持久化完成前时丢弃待写结果；完成后不回退已写结果。
```

Input artifact: `docs/design/worker.md`.

```markdown
# Worker 设计

## 共享规则

取消发生在持久化完成前时丢弃待写结果；完成后不回退已写结果。

## 局部流程

> 状态：建议

Worker 把取消请求交给 Repository。等待清理完成后，才开始下一条队列任务。
```

Input artifact: `docs/design/adr-001.md`.

```markdown
# 结果归属

Status: Accepted
Date: 2025-11-03

Repository 持有待写结果并负责持久化；Worker 只调用它的接口。
这让多个 Worker 使用同一个持久化生命周期。
```

User request:

> 整理 docs/design/ 这组软件设计文档，修改现有文件，明确总览、共享契约、Worker 局部设计和历史 ADR 的职责，减少重复并检查相互引用。保留所有设计状态和历史信息，不修改代码。

Expected results:

- Select the skill through normal discovery and inspect the relevant entry point, all four files, and their links before editing. The request itself supplies enough scope to proceed with ordinary organizational choices.
- Keep `contracts.md` authoritative based on the inspected entry document. Replace the redundant contract definition in the Worker design with a usable link while retaining its distinct proposed sequencing requirement and its state.
- Make the overview useful for navigation and retain enough overall context to explain how Worker and Repository relate. Make the connection between the Worker details and the shared contract understandable.
- Preserve the ADR's accepted status, date, ownership decision, and rationale as history. Do not convert it into a current task list or delete it as a duplicate. Distinguish document roles without requiring extra empty files or levels.
- Inspect actual saved contents and links, preserve code, and report only completed organizational changes and verification. No Markdown wording or fixed heading count is required for a pass.

## B11: Map proposed code responsibilities and dependency direction

Input artifact: `src/worker.py`.

```python
import json
import sqlite3


def run_job(raw, database_path):
    job = json.loads(raw)
    with sqlite3.connect(database_path) as connection:
        connection.execute(
            "INSERT INTO jobs (id, payload) VALUES (?, ?)",
            (job["id"], job["payload"]),
        )
    return job["id"]
```

Input artifact: `src/cli.py`.

```python
import sys
from .worker import run_job


def main(database_path):
    print(run_job(sys.stdin.read(), database_path))
```

User request:

> 用 $write-code-design 为这个 Worker 起草重构设计，保存到 docs/worker-design.md。后续命令行和后台入口都需要复用任务解析；测试中需要替换 SQLite 存储。说明拟议模块或文件分别负责什么、接口如何衔接及允许的依赖方向，保持当前写入后返回任务 ID 的行为。只写设计，不改代码，不引入新框架。

Expected results:

- Inspect both source files before describing current behavior. Identify the existing mixture of JSON parsing, persistence, and orchestration, and distinguish the planned background entry point from an implemented one.
- Map important proposed responsibilities to concrete module or file locations and explain their relevant interfaces. Show how entry points reuse parsing and how the orchestration can consume a replaceable storage contract; explain changes from the current locations.
- Explain state and side-effect ownership and the allowed dependency direction. Any architectural layers or abstractions must serve the stated reuse and storage-substitution requirements and respect the small existing package; do not impose a framework or a fixed layer-directory template.
- Preserve the required return-after-write behavior in the proposal and planned verification. Mark unresolved interface details as proposals or open choices rather than inventing accepted decisions or runtime guarantees.
- Save and inspect the document, leave both source files unchanged, and distinguish suggested checks from checks actually performed. Do not write a task-by-task implementation plan or claim that a storage-substitution test ran.

## B12: Structural revision within a fixed outline and one-file scope

Input artifact: `docs/worker-rfc.md`.

```markdown
# Worker RFC

Status: Draft

## Context

The worker parses a job and writes it to SQLite. Keep returning the job ID after the write.
Proposed: share parsing with a future background entry point.

## Proposal

Tests currently cannot substitute storage independently of parsing.
Proposed: consume a replaceable storage interface.

## Consequences

The exact storage interface remains undecided.
```

Input artifact: `docs/README.md`.

```markdown
# Designs

[Worker proposal](worker-rfc.md#proposal)
```

User request:

> 用 $write-code-design 整理 docs/worker-rfc.md 的内容归属，让现状、方案和后果更清楚，但保持英文、三个章节标题及顺序，只修改这个文件，不新增或拆分文件。这是待评审方案。

Expected results:

- Reassign misplaced current limitations, proposed changes, and required behavior within the supplied outline. Honor the explicit headings, order, language, and file scope despite the permission to organize content.
- Preserve the return-after-write requirement, proposed shared parsing and replaceable storage, undecided interface, and Draft status. Do not add the skill's default metadata or present the design as accepted.
- Leave `docs/README.md` and its link unchanged and valid. Do not create extra document levels, split files, restructure code, or require routine approval to make these authorized edits.
- Inspect the saved difference and report actual changes and checks. A structural revision is successful only if the meaning and scoped artifacts are preserved, not merely because the outline looks tidy.
