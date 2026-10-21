# Swift testing guidance

Read this reference for Swift test authoring or test-design questions. The main skill defines task scope, test quality, and execution permissions; this reference adds Swift-specific choices.

## Preserve the project's framework and targets

Inspect the relevant test target and Swift/Xcode constraints. Extend an existing XCTest or Swift Testing suite using its conventions. Do not migrate frameworks simply because Swift Testing is available. If a new target needs a framework choice, consider toolchain support and project conventions; Swift Testing is an option for supported Swift unit tests, while UI automation and XCTest performance metrics have their own framework requirements and are outside this skill's default scope.

Keep testing-framework imports and test helpers in test targets. Prefer existing dependency injection and supported module visibility. Do not expose private production members or introduce protocols and wrappers solely to satisfy a testing pattern without considering the task's authorization and the actual obstacle.

## Express outcomes and prerequisites

In Swift Testing, use `#expect` for outcomes. Use `try #require(...)` when further assertions depend on a condition or an unwrapped optional; an ordinary expectation failure allows the test to continue. In XCTest, use the corresponding assertions and throwing prerequisites such as `XCTUnwrap` when needed. An early return must not silently turn a failed prerequisite into a passing test.

Use parameterized tests for the same behavior with multiple input/expected-result pairs. Keep the expected results explicit and independently derived. Swift Testing forms a Cartesian product when given multiple argument collections; use paired cases or `zip` when inputs and expectations belong together rather than testing every combination.

## Isolate concurrent tests and await their work

Swift Testing runs tests in parallel by default. Avoid shared mutable singleton fixtures, shared persistent stores, and assumptions about suite execution order. First examine whether the test can own an isolated instance or resource. Do not add blanket `@MainActor` annotations or weaken concurrency checking to silence errors; match the isolation of the API being exercised.

Use `.serialized` only for an identified need within its scope. On a suite, it serializes contained tests and sub-suites; on a parameterized function, it serializes that function's cases. It does not coordinate with unrelated suites or tests, and has no effect on a non-parameterized test function. It is not a global lock for shared resources.

Prefer awaiting async APIs directly. For callback APIs, use the project's established bridge or expectation facilities while respecting completion and cancellation semantics. Swift Testing `confirmation` checks that the required events occur within its operation; it does not independently suspend until an event arrives. Ensure the operation awaits the work producing the event before returning. In XCTest async tests, use supported asynchronous fulfillment APIs rather than blocking the executor.

When testing late completion or cancellation, arrange the necessary suspension and release explicitly with a controlled dependency. Keep test-owned tasks and callback registration scoped to the test and handle failure cleanup. Avoid using `Task.sleep` or repeated `Task.yield` as evidence that another operation has reached a required state.

## Authoritative API references

Check API availability against the target project's toolchain when it affects the test. These links support the framework semantics above; they do not authorize a build or test run.

- [Apple: Expectations and confirmations](https://developer.apple.com/documentation/testing/expectations)
- [Apple: Implementing parameterized tests](https://developer.apple.com/documentation/testing/parameterizedtesting)
- [Apple: Running tests serially or in parallel](https://developer.apple.com/documentation/testing/parallelization)
- [Apple: Migrating a test from XCTest](https://developer.apple.com/documentation/testing/migratingfromxctest)
