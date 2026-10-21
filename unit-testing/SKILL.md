---
name: unit-testing
description: Design, write, or improve unit tests that protect observable behavior and contracts, including boundary cases, dependency substitution, and deterministic async testing. Use when unit-test design or test code is the main deliverable. General code review and execution-only verification keep their own task modes. TDD is optional.
---

# Unit testing

Write focused tests that detect concrete regressions, explain intended behavior, and remain useful when implementation details change. Match the effort to the behavior and risk; a test count or coverage target does not establish test quality.

## Choose the task and preserve its boundaries

Use this workflow as the primary skill when the requested deliverable is unit-test design, new tests, or improvements to existing tests. Test-design discussion stays read-only until file edits are authorized.

For feature implementation or production-code repair, keep the code workflow in charge of the task, including necessary tests and verification. Consult this skill when test design needs its guidance; do not force a separate testing task, handoff, or phase for every implementation. Reading production code to write tests does not by itself require an additional code-design workflow.

Reviewing test code remains a static, read-only code-review task. Prefer `code-design-and-implementation` when available; explicit invocation of this skill still honors that mode, with no edits, temporary files, or runtime verification. If a request combines review with edits or execution, obtain the chosen task mode first unless it is already explicit. A request only to run specified checks is verification: execute within its permissions and report results without automatically writing tests or repairing code.

Independent test authoring authorizes test code and necessary test helpers within the requested scope. It does not independently authorize production-code fixes, interface changes, framework migration, dependency installation, or test-infrastructure redesign. If a useful test needs a production change outside existing authorization, explain the concrete obstacle and proposed change before proceeding with that part; continue independent testing work. Reuse authorization already given.

TDD is optional. Follow the user's or project's chosen development approach. Existing implementations and newly added tests that pass immediately are valid starting points; do not delete, rewrite, or deliberately break production code merely to obtain an initial failing test.

## Establish behavior and existing facilities

Read the relevant implementation, callers, existing tests, and runner configuration only as needed to understand the requested behavior and testing conventions. Reuse the project's framework, fixtures, dependency seams, and commands. For Swift tasks, read [Swift testing guidance](references/swift-testing.md) for framework-specific choices and semantics.

Derive expected behavior from requirements, confirmed contracts, and relevant accepted references. Implementation establishes what the code currently does, not whether that behavior is correct. Existing tests are evidence of expectations, not automatic authority over an explicit requirement. Clarify consequential disagreements or missing behavior instead of silently encoding a choice in a test. Pause only cases that depend on the missing decision and continue independent work.

When the request is to characterize legacy behavior, identify that purpose and distinguish observed behavior from confirmed intended behavior. Do not silently preserve a known defect as the desired contract.

Choose a narrow behavior boundary with useful observable results. It may include several small cooperating in-process types; do not impose one test per method or require every collaborator to be mocked. If the important risk depends on real infrastructure or broader integration, explain that limitation and propose the appropriate test level without expanding the task automatically.

## Select cases and independent expectations

For each case, identify the behavior it protects and a plausible defect that would make it fail. Cover meaningful input partitions, threshold boundaries, failures, side effects, and state transitions relevant to this task. Include concurrency and lifecycle cases only when they affect the contract. Prefer a small set of discriminating cases over exhaustive combinations or tests of trivial forwarding with no independent behavior.

Build expected results independently of the code under test and its helpers. Use explicit values, hand-checked fixtures, or independently justified properties. Do not copy the production algorithm into the assertion or call the same implementation to compute both actual and expected values.

Exercise the real unit through its supported interface and assert the result, externally meaningful state change, or required side effect. A mock configured to return a value and then queried directly is not a test of the consuming unit. Avoid assertions on private structure, incidental call sequences, or source text as substitutes for behavior. Structural checks can serve a separate purpose; report them as such.

Prefer result and state assertions. Assert dependency calls, arguments, counts, or ordering when they represent a necessary contract, such as preventing duplicate sends or redundant work. Verify only the interactions needed to establish that behavior; interaction checks do not prove the real dependency works.

## Keep fixtures, dependencies, and timing controlled

Prefer real, lightweight, deterministic collaborators when practical. Use a fake, stub, or spy to isolate external resources, trigger relevant failure paths, or control time and completion. Preserve the dependency semantics the unit relies on, including relevant errors and side effects. Avoid reproducing an entire dependency or inventing interfaces merely to make mocking convenient. Identify integration assumptions the substitute cannot establish.

Keep each test independent of execution order and other tests' mutable state. Give fixtures clear ownership and cleanup, including tasks, observers, and resources created by the test. Helpers should reveal setup and remove distracting repetition without hiding expected values or reproducing production logic. Do not move test-only lifecycle methods into production types for test convenience.

For asynchronous behavior, control the event or completion that creates the relevant ordering using existing test facilities, gated dependencies, or controllable clocks. Await the result being asserted and settle test-owned work before the test exits, including on failure. Use bounded waits to diagnose a missing event; arbitrary sleeps, repeated retries until green, and globally serializing tests do not establish the required ordering. Distinguish cancelling one waiter, ending shared work, and suppressing late effects when those meanings differ in the contract.

## Write readable tests and assess their strength

Name tests after the scenario and expected behavior using local conventions. Keep setup, action, and assertions easy to distinguish; Arrange–Act–Assert is useful without requiring three comment labels. Keep one coherent behavior per case, with as many assertions as that behavior needs. Parameterize cases when inputs and expected outcomes vary over the same behavior; keep different setup or failure semantics separate when that improves clarity.

Before finishing, reason through representative mistakes: a wrong boundary comparison, ignored failure, missing state change, duplicate side effect, or late completion. Check whether the assertions would detect the relevant error. This is static reasoning, not a claim that mutation tests ran. Do not add tests solely to exercise language syntax, framework internals, or coverage counters.

## Verify within permission and report evidence

Inspect the saved tests and diff against the requested scope. Run only commands permitted by the current task and target project. Writing tests does not override a project rule requiring an explicit request before builds or test execution. When execution is allowed, start with the relevant target or cases and broaden to required or justified checks. Do not impose a full-suite run on every task.

Classify failures using the contract and observed evidence: a test mistake, production defect, environment problem, or unresolved requirement. Correct in-scope test mistakes. Report production defects outside authorization and retain a meaningful regression test when appropriate; do not weaken its expected result, silently disable it, or change production behavior merely to make the run green. Do not repair unrelated failures automatically.

Report behaviors covered, relevant files, commands actually run and observed results, and remaining limitations. Distinguish written tests, static inspection, executed tests, and integration assumptions. If execution was prohibited, unavailable, or blocked, say so; a runnable-looking test or planned command is not evidence of a pass.

## Background sources

These sources informed the guidance above; they are not additional workflows to load or adopt wholesale.

- [Software Engineering at Google: Unit Testing](https://abseil.io/resources/swe-book/html/ch12.html) and [Test Doubles](https://abseil.io/resources/swe-book/html/ch13.html): behavior-focused tests, maintainability, and dependency tradeoffs.
- [Microsoft: Unit testing best practices](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices): readable structure, repeatability, and coverage limitations; framework-specific naming is not prescribed here.
- [Superpowers: Writing Good Tests](https://github.com/obra/superpowers/blob/main/skills/test-driven-development/writing-good-tests.md): independent expectations and reasoning about defects a test detects. Its mandatory TDD and production-rewrite policies are not adopted.
- [Swift Testing Agent Skill](https://github.com/AvdLee/Swift-Testing-Agent-Skill): framework-specific topics, adapted in the local Swift reference without imposing migration.
- [OpenAI: Testing Data Visualizations](https://github.com/openai/plugins/blob/main/plugins/build-web-data-visualization/skills/testing-data-visualizations/SKILL.md): selecting test levels from concrete risks; visualization-specific procedures are outside this skill.
