# Behavior evaluation cases

These cases evaluate the content selection, fidelity, and file operations of `document-confirmed-design`. They are maintenance material, not instructions to load during ordinary documentation work. The existing cross-skill selection cases remain in [the working-draft evaluation suite](../../draft-software-design/evals/behavior-cases.md); their criteria are not duplicated here.

## Evaluation method

- Run each case in a fresh conversation with normal agent instructions and an isolated disposable workspace. Populate only the listed artifacts and supplied material. Keep the skill's execution resources unchanged and available through normal discovery; do not preload its body for an implicit-selection case.
- Give the executing model the user request and raw material, without the expected results, other cases, or earlier evaluation conclusions. The evaluator retains the criteria below. An independent model or a human may evaluate the results; delegation is not required.
- For staged cases, send only the current stage's request and material. Inspect that stage's response and file operations before sending the listed follow-up in the same conversation; do not reveal future clarification in advance.
- Inspect the actual answer, skill selection, tool actions, saved files, and differences from the input. Judge design meaning and scope rather than exact wording, heading counts, or the presence of particular keywords. Record selection separately from output quality and file operations.
- Record the skill revision, model and configuration, case ID, observed selection, actions, artifact locations, outcome, and evidence for failures. Use pass, fail, or not run. Keep structural checks separate from behavioral results; reading these cases is not an execution of them.
- Generated artifacts must stay outside the skills repository. These cases permit only local reading, drafting, and requested document edits. Do not build, run tests, install tools, perform Git operations, or use external services. If execution is unavailable, report the limitation rather than simulating a pass.

## C01: The final agreement replaces earlier proposals

Input artifacts: none.

Supplied material:

> 早期讨论中，助手建议 TTL 为 30 秒，也比较过由 Worker 持有缓存的做法。用户没有接受这些建议。
> 用户最后确认：Repository 是缓存的唯一所有者；Worker 只通过 Repository 接口访问缓存。当前采用按 key 手动失效，不采用 TTL。
> 已确认的理由：数据更新入口由 Repository 掌握，把缓存失效责任放在同一处，避免调用方分别维护失效规则。
> 没有提供当前实现情况。

User request:

> 用 $document-confirmed-design 把最终约定整理成简短正式说明，先在对话中给出，让没参与讨论的人也能理解职责和理由。

Expected results:

- Honor the explicit invocation. Explain Repository ownership, Worker access, manual invalidation, and the supplied rationale as the effective agreement.
- Do not preserve the old TTL value or Worker ownership as effective requirements, an alternatives section, or a discussion transcript. Mention superseded ideas only if needed to explain the final agreement; do not invent additional rationale.
- Keep implementation progress unknown rather than claiming the agreed behavior exists. A short reference needs no default dates, status taxonomy, or full-specification template.
- Respond inline without creating files, implementing invalidation, or asking for routine approval to state the supplied agreement.

## C02: Goals do not establish stronger execution guarantees

Input artifacts: none.

Supplied material:

> 已确认目标：尽量减少取消后的无效工作；没有确认具体响应时限。
> 已确认契约：Repository 观察到取消时，如果持久化尚未完成，就丢弃待写结果；持久化已经完成时，不回退已写结果。
> 已确认：重复取消同一任务不产生额外副作用。具体去重机制未选定。
> 发出取消请求不代表执行已经停止。没有确认强制中断、锁或轮询策略。

User request:

> 把这些已确认的取消语义整理成正式说明，保存到 docs/design/cancellation.md。保留条件和限制，不补实现方案。

Expected results:

- Select `document-confirmed-design` through normal discovery. Keep the general goal distinct from a latency or interruption guarantee.
- Preserve the observation condition, persistence boundary, pending/persisted distinction, and repeated-cancellation guarantee. Do not turn request submission into immediate termination or promise rollback after persistence.
- Leave deduplication and interruption mechanisms unselected. Do not prescribe locks, polling frequency, retries, or an exhaustive execution sequence as accepted design.
- Save and inspect only the requested document. Report actual checks without claiming implementation, runtime success, or new approval.

## C03: Extract a formal reference from a mixed manuscript

Input artifact: `docs/design/drafts/cache-options.md`.

```markdown
# 缓存方案手稿

## 缓存归属

已确认：Repository 是缓存的唯一所有者，Worker 只通过其接口访问。

## 单键失效

已确认：提供 invalidate(key)，不存在的 key 没有副作用。
待定：返回值是否需要说明本次有没有删除条目。

## TTL

建议：每个条目在 30 秒后过期。尚未决定是否采用。

## 后续可能性

批量失效暂缓，只有出现具体需求才重新讨论，没有承诺实施。
```

Input artifact: `src/cache.py`.

```python
class Cache:
    def __init__(self):
        self.items = {}

    def get(self, key):
        return self.items.get(key)

    def put(self, key, value):
        self.items[key] = value
```

Input artifact: `docs/design/README.md`.

```markdown
# 设计文档

正式设计说明保存在本目录，讨论手稿放在 drafts/。
[缓存方案讨论](drafts/cache-options.md)
```

User request:

> 用 $document-confirmed-design 把缓存手稿中已确认的内容保存为正式说明。记录与接口有关的未决边界和已提到的后续方向，核对单键失效的实现情况，只新增正式说明文件。

Expected results:

- Extract confirmed ownership and absent-key semantics into a coherent formal reference outside `docs/design/drafts/`, following the supplied project layout. Do not promote the whole manuscript as an accepted specification.
- Retain the unresolved return-value boundary without choosing a result type. Keep batch invalidation as a deferred possibility, not a commitment. Do not carry the unaccepted TTL proposal into the effective agreement or invent another policy.
- Inspect `src/cache.py` before reporting implementation facts. Distinguish existing `get`/`put` from the confirmed but unimplemented `invalidate` target; the source does not independently prove the ownership agreement is implemented.
- Create and inspect only the new formal file. Preserve the manuscript, index, and code byte-for-byte; do not move, archive, delete, or relabel the draft.

## C04: A code discrepancy does not authorize a new decision

Input artifact: `docs/design/cache.md`.

```markdown
# 缓存设计

## 已接受的约定

Repository 是缓存的唯一所有者。Worker 只通过 Repository 接口访问缓存。
这个边界让多个 Worker 使用同一个缓存生命周期。

## 实现情况

尚未核对。
```

Input artifact: `src/cache.py`.

```python
class Cache:
    pass
```

Input artifact: `src/worker.py`.

```python
from .cache import Cache


class Worker:
    def __init__(self):
        self.cache = Cache()
```

User request:

> 根据这两个源文件维护 docs/design/cache.md 的实现情况，保留已接受的设计约定。代码与约定的差异还没决定如何处理，只改这份说明，并单独指出需要讨论的问题。

Expected results:

- Select the formal-reference workflow and inspect the two source files. Describe the observed per-Worker cache construction accurately without claiming unseen Repository integration or runtime behavior.
- Preserve the accepted ownership and shared-lifecycle rationale. Make the discrepancy visible; do not silently replace the agreement with Worker ownership, assert that the document is obsolete, or present the code as approval of a changed design.
- The request already specifies that the accepted design stays and only implementation status changes. Record the observed discrepancy and flag the unresolved reconciliation without a clarification gate. Do not choose a migration, redesign ownership, modify source code, or turn an implementation note into an accepted solution.
- Inspect the saved change, preserve unrelated text and the existing format, and distinguish static inspection from runtime verification.

## C05: Explain design meaning without transcribing execution

Input artifact: `src/executor.py`.

```python
import asyncio


class Executor:
    def __init__(self):
        self._locks = {}

    async def run(self, key, operation):
        lock = self._locks.setdefault(key, asyncio.Lock())
        async with lock:
            return await operation()
```

Supplied material:

> 已确认：调用方提供实体 key 和操作；Executor 拥有按 key 控制并发的状态。
> 同一个 key 的操作不能同时执行，前一个操作完成或失败退出后才允许另一个进入；不同 key 允许并发。不承诺相同 key 的固定执行顺序。
> 已选择按 key 使用异步锁的机制，以防止同一实体的操作重叠，同时保留不同实体的并发机会。
> 内部字典布局、变量名和每一步方法调用不是需要依赖的契约。

User request:

> 用 $document-confirmed-design 写一段可独立理解的正式设计说明，解释 Executor 的职责、并发保证和采用该机制的理由。结合源码核对，先在对话中给出。

Expected results:

- Inspect the supplied source and explain the caller/Executor responsibility boundary, same-key exclusion, operation-lifetime boundary, and cross-key concurrency in terms of their meaning.
- Retain the confirmed per-key asynchronous-lock mechanism and its supplied rationale. Do not strengthen exclusion into FIFO ordering or drop a concurrency guarantee merely to simplify prose.
- Make the explanation understandable without a line-by-line walkthrough. Incidental dictionary operations, imports, local variables, and method inventories need not become design sections. Identifiers may be mentioned where they help the reader.
- Keep the response inline and proportional to the requested paragraph. Do not create files, implement a different locking strategy, or claim runtime verification.

## C06: Relevant references remain portable and within scope

Input artifact: `docs/design/storage/ownership.md`.

```markdown
# Storage Ownership

The Repository owns pending results and persistence. Workers access it through its interface.
```

Input artifact: `docs/design/tasks/execution.md`.

```markdown
# Task Execution

## Responsibilities

TaskRunner receives tasks and delegates persistence to the Repository.
The storage ownership reference provides the agreed responsibility boundary.

## Implementation location

TaskRunner is declared in src/task_runner.py. Its implementation has not been verified here.
```

User request:

> 用 $document-confirmed-design 完善 docs/design/tasks/execution.md 中对 docs/design/storage/ownership.md 的正文引用，让读者能查到职责约定。保留英文、已有格式和源码位置，只修改 execution.md。

Expected results:

- Honor the explicit invocation within the narrow requested scope. Add a usable document-body link to the relevant ownership reference, relative to `execution.md`; crossing to the sibling storage directory is valid.
- Preserve the stated responsibilities and unverified implementation status. Keep `TaskRunner` and `src/task_runner.py` as plain-text/code identifiers unless the request provides a reason to link them; the source path is mentioned material, not a supplied file to verify in this case.
- Do not add machine-specific absolute paths, outside-project local references, external navigation, dates, or a new status format. Do not modify the ownership document or create an index.
- Inspect the saved content and verify the relative target. Report only the actual document edit and checks.

## C07: External evidence does not follow from design confirmation

Input artifact: `vendor/taskkit-2.4/task.pyi`. This is an authoritative SDK declaration fixture for the fictitious TaskKit 2.4; evaluate only the supplied material, without external services.

```python
class Task:
    def cancel(self) -> None:
        """Request cancellation. The task may continue running after return.
        This method does not wait for pending writes to finish.
        """
        ...
```

Supplied material:

> 已确认：Repository 统一负责发起取消，Worker 只通过 Repository 的接口访问任务。
> 已确认目标：调用方能够区分取消请求已发出和写入已经停止。实现尚未核对。
> 讨论时曾假设 TaskKit 2.4 的 cancel() 返回就表示写入停止，但没有核实该依据。完成通知能力也没有资料，尚未选择收敛机制。

User request:

> 用 $document-confirmed-design 把取消职责和目标保存到 docs/design/cancellation.md，核对作为依据的 SDK 事实并保留来源及版本。发现依据有疑点时单独指出，不改变已确认约定，也不补实现方案。

Expected results:

- Inspect the supplied declaration and preserve the confirmed Repository/Worker responsibility boundary and target. Explain that design confirmation does not establish implementation progress or validate the SDK assumptions.
- Record the checked cancellation semantics with the declaration source and TaskKit 2.4 context. Do not repeat the contradicted return-means-stopped assumption as a verified fact or effective guarantee.
- The confirmed responsibilities and target are explicit, and the contradicted SDK premise is only an unverified assumption. Record the checked facts and their impact without asking again about those clear agreements. Keep completion-notification capability unverified and the mechanism undecided; do not change the agreement's status, invent an SDK method, or select polling, locks, or a replacement design.
- Save and inspect only the requested formal reference. Leave the SDK fixture unchanged and report static checks without claiming runtime verification or using external services.

## C08: Clarify a central agreement conflict before saving, then resume

Input artifact: the authoritative fictitious TaskKit 2.4 declaration `vendor/taskkit-2.4/task.pyi` from C07.

Input artifact: `docs/design/cancellation.md`.

```markdown
# Cancellation

## Confirmed contract

The Repository owns cancellation; Workers use its interface.
Repository.cancel() only forwards the call to TaskKit 2.4 Task.cancel().
Returning from Repository.cancel() means the task has stopped and pending writes are complete.

## Implementation status

Not checked.
```

Initial user request:

> 用 $document-confirmed-design 核对 SDK 依据，更新 docs/design/cancellation.md，写清目前有效的取消契约。保留英文和已有格式，只改这份说明，不改代码，不自行选择机制。

Expected results before clarification:

- Inspect the declaration and document. Retain the checked SDK fact that cancellation may return before execution or pending writes finish, with its TaskKit 2.4 source context; do not relabel this fact as unverified merely because it conflicts with the record.
- Explain the conflict between forwarding the SDK call and promising stopped execution on return. Ask a focused question about whether the stopping guarantee remains an unimplemented confirmed target or the effective contract needs clarification; do not silently pick an interpretation or propose a replacement mechanism as accepted.
- Pause the whole artifact because its central contract is affected. Keep `docs/design/cancellation.md` byte-for-byte unchanged, leave the SDK fixture unchanged, and do not save an assumed resolution or report the update complete.

Follow-up user clarification, supplied only after inspecting the initial response and actions:

> SDK cancel() 只发出请求是当前事实；Repository 对外“停止且写入结束后才返回”保留为尚未实现的目标。旧文中的“只转发 SDK 调用”不是最终实现约定，等待机制未决。按这个澄清继续更新这份说明。

Expected results after clarification:

- Continue the authorized document update without asking again for permission to save. Use the clarification to distinguish the checked SDK behavior, the confirmed but unimplemented Repository target, and the undecided waiting mechanism.
- Preserve the Repository/Worker responsibility boundary, language, and useful format. Remove the superseded forwarding-only statement as an effective implementation agreement; do not invent an SDK completion API, waiting strategy, or runtime-success claim.
- Save and inspect only the requested document. Preserve the SDK fixture, include its source and version context, and report the completed record and actual checks.
