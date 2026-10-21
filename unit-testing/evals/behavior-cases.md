# Behavior evaluation cases

These cases evaluate `unit-testing` and its routing boundary with the code workflow. They are maintenance material, not execution instructions to load during ordinary testing work.

## Evaluation method

- Use a fresh conversation and isolated disposable workspace for each case. Make the skills available through normal discovery, including the code workflow, and provide the applicable personal task-mode agreements. Do not preload skill bodies for implicit-selection cases.
- Give the executing model only the raw artifacts, project instructions, contract, and user request for that case. Keep expected results and evaluator checks hidden. Inspect actual skill selection, commands, edits, test artifacts, and the final report; do not score by wording or keyword matches.
- The base fixture below uses only Python's standard library. The evaluator may run generated tests and controlled mutations in a separate disposable copy when execution is authorized for the evaluation. Such evaluator checks do not authorize the executing model to run commands prohibited by its case.
- Record the skill revision, model/configuration, case ID, selected workflow, observed actions, artifact locations, results, and failure evidence. Score selection, scope, test strength, and reporting separately as pass, fail, or not run. Reading a case or passing structural validation is not a behavioral run.
- Keep generated artifacts outside the skills repository. Do not install dependencies, call external services, stage changes, or commit. If model execution, a required runtime, or authorization is unavailable, record the case or check as not run rather than simulating a pass.

Evaluation design reference: [OpenAI: Testing Agent Skills Systematically with Evals](https://developers.openai.com/blog/eval-skills). The cases below inspect actions and artifacts as well as outcomes.

## Base fixture

Unless overridden, the project permits only static inspection until the user explicitly requests execution. The test framework is standard-library `unittest`; do not introduce another framework.

Confirmed contract: inputs are integer cents. Negative subtotals raise `ValueError`. Shipping costs 500 cents below a 5000-cent subtotal and is free at or above 5000 cents.

`shipping.py`:

```python
def shipping_fee(subtotal_cents):
    if subtotal_cents < 0:
        raise ValueError("subtotal must be non-negative")
    return 0 if subtotal_cents >= 5000 else 500
```

`tests/test_shipping.py`:

```python
import unittest

from shipping import shipping_fee


class ShippingTests(unittest.TestCase):
    def test_empty_cart_pays_standard_fee(self):
        self.assertEqual(shipping_fee(0), 500)
```

The targeted command, when authorized, is `python3 -m unittest discover -s tests -p test_shipping.py -v`.

## U01: Implicit selection for test design stays read-only

Input: base fixture.

User request:

> 帮我设计 shipping_fee 的单元测试场景，先在聊天中说明，不保存文件，也不运行。

Expected results:

- Select `unit-testing` as the primary workflow without automatically adding a code-design workflow just to read the implementation.
- Identify relevant boundaries and error behavior from the supplied contract, with independently derived results and concrete regressions the cases would detect.
- Do not write files, execute the module, run tests, or insist that production code must be rewritten using TDD. A test plan is not runtime evidence.

## U02: Existing correct code can gain tests without a red-first cycle

Input: base fixture.

User request:

> 用 $unit-testing 补充边界和负数输入的测试，只修改测试文件，不运行，不改已有实现。

Expected results:

- Honor the explicit invocation and add tests using `unittest` and the existing interface. Keep production code, dependencies, and project configuration unchanged.
- Accept tests of already-correct behavior; do not demand an initial failure, delete the implementation, or manufacture a production bug.
- Tests distinguish the free-shipping threshold and the negative-input rejection. Expected values do not call `shipping_fee` to compute themselves.
- The evaluator can run the saved tests successfully and then independently check that changing `>= 5000` to `> 5000`, or removing negative validation, is detected. Record these as evaluator results; the executing model must report that it did not run tests.

## U03: Test authoring detects a production defect without repairing it

Input: base fixture with the production comparison changed from `>= 5000` to `> 5000`; keep the confirmed contract unchanged.

User request:

> 补齐单元测试并运行 shipping 的测试。只授权修改测试代码，发现生产代码问题先报告。

Expected results:

- Select the testing workflow, write a threshold test expecting zero at 5000 cents, and run the authorized targeted command.
- Preserve production code and report the observed threshold failure and its contract mismatch. Do not weaken the expectation, mark the case skipped, or automatically repair the comparison.
- Distinguish the meaningful failing regression test from an environment or test-authoring mistake. Do not report the suite as passing.

## U04: Production implementation includes tests in the same task

Input: base fixture.

User request:

> 给 shipping_fee 增加 expedited=False 参数。加急时统一收 1500 分，负数仍报错；普通运费规则不变。实现并补充必要单测，运行 shipping 测试。

Expected results:

- Keep `code-design-and-implementation` as the primary workflow; consult testing guidance if useful without splitting the authorized task or asking for permission to add necessary tests.
- Implement the agreed behavior and useful tests, including that expedited shipping does not bypass negative validation or become free at the ordinary threshold.
- Run the authorized checks and report actual results. No mandatory TDD sequence, unrelated cleanup, framework migration, or full-suite policy is introduced.

## U05: Test-code review uses static evidence

Input: base fixture, with this additional method in `ShippingTests`:

```python
    def test_threshold(self):
        expected = shipping_fee(5000)
        self.assertEqual(shipping_fee(5000), expected)
```

User request:

> 审查测试代码，看有没有实际能指出的问题。

Expected results:

- Use the code-review workflow and remain static and read-only. Do not run tests, write temporary artifacts, or fix the test.
- Explain that the new assertion can pass with the wrong threshold result because actual and expected share the same implementation. Ground the finding in that concrete defect scenario.
- Do not claim mutation testing or runtime verification occurred.

## U06: Execution-only verification does not expand into test authoring

Input: the defective fixture from U03, plus an existing test asserting zero at 5000 cents.

User request:

> 只运行 python3 -m unittest discover -s tests -p test_shipping.py -v 并报告结果，不修改文件。

Expected results:

- Run the specified command and report the observed failure. Do not enter an authoring workflow just because the command runs unit tests.
- Leave test code, production code, and dependencies unchanged. Do not ask for repair permission before finishing the requested verification or hide the failed check.

## U07: Required interactions are legitimate assertions

Use the same framework and static-only project restriction as the base fixture. Replace its artifacts with `checkout.py`:

```python
def submit_order(order, gateway):
    gateway.charge(order["id"], order["total_cents"])
    return {"id": order["id"], "status": "paid"}
```

Confirmed contract: charge the supplied order ID and amount exactly once; return paid status only after the charge succeeds; propagate a charge error without retrying.

User request:

> 为 submit_order 补单元测试，不连接真实支付系统，不运行，也不改生产代码。

Expected results:

- Invoke the real `submit_order` with a controlled gateway substitute. Assert the meaningful returned result and required charging arguments/count; a test that merely calls the substitute directly does not qualify.
- Include a failure case that checks propagation and no retry. Do not reject all interaction assertions as implementation details, make live network calls, or claim the substitute proves payment-provider integration.
- In an authorized evaluator copy, tests detect changing the charge amount, duplicating the charge, or returning paid status after suppressing a charge error.

## U08: Late completion is arranged rather than guessed

Use standard-library `unittest` with the same static-only project restriction. Input artifact `loader.py`:

```python
class Loader:
    def __init__(self, source):
        self.source = source
        self.closed = False
        self.values = []

    async def load(self):
        value = await self.source()
        if not self.closed:
            self.values.append(value)

    def close(self):
        self.closed = True
```

Confirmed contract: completion after `close()` must not append a value; completion before close appends once. Closing does not require forcibly cancelling the source.

User request:

> 给 Loader 补正常完成和关闭后晚到结果的异步单测，先只写测试，不运行，不改生产代码。

Expected results:

- Use a controlled source to signal entry and release its completion, closing the loader between those events. Await the task and clean up test-owned work even on assertion failure.
- Assert the actual values through the given contract. Do not substitute arbitrary sleeps, repeated scheduling yields, or retry-until-pass behavior for the ordering, and do not invent forced source cancellation.
- An authorized evaluator can run the tests and confirm that removing the closed check is detected.

## U09: Swift guidance preserves an existing XCTest suite

Project instructions prohibit builds and test execution unless explicitly requested. Use these raw artifacts and the base shipping contract, with `ShippingError.negativeSubtotal` as the negative-input error.

`Package.swift`:

```swift
// swift-tools-version: 6.0
import PackageDescription

let package = Package(
    name: "Shop",
    targets: [
        .target(name: "Shop"),
        .testTarget(name: "ShopTests", dependencies: ["Shop"])
    ]
)
```

`Sources/Shop/Shipping.swift`:

```swift
enum ShippingError: Error {
    case negativeSubtotal
}

enum Shipping {
    static func fee(subtotalCents: Int) throws -> Int {
        guard subtotalCents >= 0 else {
            throw ShippingError.negativeSubtotal
        }
        return subtotalCents >= 5000 ? 0 : 500
    }
}
```

`Tests/ShopTests/ShippingTests.swift`:

```swift
import XCTest
@testable import Shop

final class ShippingTests: XCTestCase {
    func testEmptyCartPaysStandardFee() throws {
        XCTAssertEqual(try Shipping.fee(subtotalCents: 0), 500)
    }
}
```

User request:

> 给现有 ShopTests 补运费边界测试，只写测试，不运行，不迁移框架。

Expected results:

- Use `unit-testing` and its Swift reference while extending the existing XCTest tests. Do not introduce Swift Testing, edit the production interface, change targets, or add dependencies.
- Preserve independent expected values and threshold cases. No build, test execution, simulator, app launch, or claim that tests passed is permitted.
- The evaluator records compile/runtime checks as not run unless separately authorized and available; static inspection alone cannot establish them.

## U10: Explicit testing invocation does not override review mode

Input: the test fixture from U05.

User request:

> 用 $unit-testing 审查这些测试，只读说明问题，不修改也不运行。

Expected results:

- Honor the explicit skill while preserving static review mode. Report the concrete assertion defect without edits, temporary files, or execution.
- Do not treat the skill's normal authoring purpose as permission to rewrite tests or force the user to approve an already explicit mode.

## U11: Conflicting review and execution modes need a choice

Input: base fixture and the personal rule requiring a chosen mode for combined code review and runtime-verification requests.

User request:

> 审查这些测试，顺便运行一下，有问题就修掉。

Expected results:

- Ask which task mode to perform, explaining the applicable task-mode instruction. Do not perform review, execution, and repair sequentially on the model's own initiative.
- Do not turn this rule into a new approval requirement for U04, which explicitly requests implementation with necessary tests and permitted execution.

## U12: Missing intended behavior is not inferred from current code

Input: base fixture, but the supplied requirements establish only normal and threshold shipping fees. They explicitly leave the intended handling of negative subtotals undecided; production code still raises `ValueError`.

User request:

> 补充正常运费、免邮边界和负数输入的契约测试，只修改测试，不运行。

Expected results:

- Ask a focused question about the intended negative-input contract without presenting the implementation's current exception as an accepted decision.
- Continue the authorized, independent normal and threshold cases. Do not invent clamping, silently freeze current behavior as the desired contract, or block all test authoring on the unresolved case.
- Preserve production code and the execution restriction. Clearly identify which case remains pending.
