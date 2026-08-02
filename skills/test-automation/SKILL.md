---
name: test-automation
description: Use when building or improving automated test suites, establishing testing strategies, or implementing TDD — making testing fast, reliable, and developer-owned
---

# Test Automation

## DORA Research Context

DORA research across multiple reports (2014, 2016, 2018, 2019) consistently shows that when developers primarily create and maintain tests and can easily fix test failures, delivery performance improves. Test automation drives improved software stability, reduced burnout, and lower deployment pain across organizations of all sizes.

## What It Is

The key to building quality into software — getting fast feedback on changes through reliable automated test suites run as part of continuous delivery pipelines. Test automation spans unit tests, integration tests, acceptance tests, and performance tests, all owned primarily by developers.

## Problem Solved

- Bugs found late in the cycle are expensive to fix
- Manual testing creates a bottleneck before every release
- Tests are flaky, slow, and maintained by a separate QA team
- Fear of changing code because you might break something

## Key Practices

1. **Allow testers to work alongside developers:** Testers should be embedded throughout the entire development and delivery process, not siloed at the end.
2. **Perform manual testing throughout:** Exploratory, usability, and acceptance testing happen continuously, not just before release.
3. **Continuously curate test suites:** Review and improve test suites to find defects effectively while keeping costs under control.
4. **Practice test-driven development (TDD):** Write unit tests before production code. This enforces testability and clarifies design intent.
5. **Keep the test suite fast:** Feedback should return in less than 10 minutes on both workstations and CI.
6. **Follow the test automation pyramid:** Most errors caught by fast unit tests, fewer by slower acceptance tests, and the least by manual exploratory testing.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Developers not involved in testing | Code is hard to test; tests are frequently broken | Developers are primary authors of tests; testability is a design concern |
| Wrong unit/acceptance test proportions | Slow feedback; errors found late | Catch errors at fastest/cheapest level; add a unit test for each acceptance test failure |
| Flaky (unreliable) tests | Teams lose trust; failures get ignored | Test failures must always indicate real defects; quarantine or remove flaky tests |
| Not curating test suites | Tests accumulate cruft and slow down over time | Continuously review and improve; remove redundant or low-value tests |

## How to Measure

- **Percentage of tests written by developers:** Goal is for developers to be primary authors
- **Change in proportion of bugs found in cheaper test phases over time:** Trend toward earlier detection
- **Test suite runtime:** Goal is under 10 minutes
- **Whether all test suites run on every pipeline trigger:** Full coverage on every change

## Coaching Patterns

1. **Build a skeleton pipeline:** One unit test, one acceptance test, one automated deploy — threaded together end-to-end. Expand from there.
2. **Require tests for all new/changed code:** Don't try to retrofit. Grow coverage incrementally with each change.
3. **Prune unreliable suites:** Ten reliable tests beat hundreds of untrustworthy ones. Remove or rewrite flaky tests immediately.

## Related Skills

- [`test-driven-development`](../test-driven-development/): The TDD workflow in detail
- [`test-data-management`](../test-data-management/): Managing test data to support automated suites
- [`continuous-integration`](../continuous-integration/): Running tests automatically on every change
- [`continuous-delivery`](../continuous-delivery/): Extending test automation through to deployment

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | — |

## Test-Driven Development (RED-GREEN-REFACTOR)

### When to Use TDD
- Implementing any new feature, however small
- Fixing a bug — write a test that reproduces the bug first
- Refactoring — existing tests must already cover the code being restructured
- Integrating with an external dependency — write tests against the expected contract first

### When NOT to Use
- Pure UI layout and styling where behavior is visual and subjective
- Exploratory spikes written to learn an API or architecture — delete the spike, then TDD the real implementation
- Auto-generated code (migrations, serializers) where the generator provides the test

### The Cycle
1. **RED:** Write a failing test that describes one behavior. Run it — confirm it fails for the right reason (not a syntax error).
2. **GREEN:** Write the minimum code that makes the test pass. No extra logic, no "while I'm here" additions.
3. **REFACTOR:** Clean up the implementation without changing behavior. Tests stay green throughout.
4. **Repeat** for the next behavior.

### Anatomy of a Good Failing Test

```
GIVEN:  a specific, controlled starting state
WHEN:   one action or call is made
THEN:   one observable outcome is asserted

test("rejects transfer when balance is insufficient") {
  account = Account(balance: 50)           // GIVEN
  result  = account.transfer(amount: 100)  // WHEN
  assert result.error == "insufficient_funds"  // THEN
}
```

One assertion per test. If a test can fail for two different reasons, split it.

### Code Pattern — Before (No Test Exists)

```
1. Write implementation until it "feels right"
2. Open a test file
3. Try to test the implementation
4. Discover the implementation is hard to isolate → patch it
5. Write tests that match what the code already does (not what it should do)
6. Ship code and tests together

Result: tests verify the implementation, not the requirement.
        Coverage exists, but wrong behavior is also covered.
```

### Code Pattern — After (Test First)

**TypeScript (vitest/jest):**
```typescript
import { describe, it, expect } from 'vitest'
import { calculateTotal } from './pricing'

describe('calculateTotal', () => {
  it('returns item price when no discount applies', () => {
    expect(calculateTotal({ price: 100, discount: null })).toBe(100)
  })
  it('applies percentage discount', () => {
    expect(calculateTotal({ price: 100, discount: { type: 'percent', value: 20 } })).toBe(80)
  })
  it('clamps total to zero when discount exceeds price', () => {
    expect(calculateTotal({ price: 50, discount: { type: 'flat', value: 75 } })).toBe(0)
  })
})
```

**Python (pytest):**
```python
from pricing import calculate_total

def test_returns_price_when_no_discount():
    assert calculate_total(price=100, discount=None) == 100

def test_applies_percentage_discount():
    assert calculate_total(price=100, discount={"type": "percent", "value": 20}) == 80

def test_clamps_total_to_zero():
    assert calculate_total(price=50, discount={"type": "flat", "value": 75}) == 0
```

**Example cycle — a price calculation function:**

```
Cycle 1 — basic case
  RED:    test("returns item price when no discount applies")
  GREEN:  function totalPrice(item) { return item.price }
  REFACTOR: nothing to clean yet

Cycle 2 — discount case
  RED:    test("applies percentage discount when item is on sale")
  GREEN:  add discount branch to totalPrice
  REFACTOR: extract discount logic to named helper

Cycle 3 — edge case
  RED:    test("returns zero when item price is negative")
  GREEN:  add guard clause
  REFACTOR: consolidate guard clauses
```

Each cycle takes 2–5 minutes. The function grows only as far as the tests demand.

### TDD Quick Reference

| Rule | Guidance |
|------|----------|
| Test first | No implementation line exists before its corresponding failing test |
| Minimum green | Write exactly enough code to pass the test; no more |
| One cycle at a time | Finish RED-GREEN-REFACTOR before adding the next test |
| Test the behavior | Assert outcomes visible to callers, not internal state |
| Bug fix entry point | Reproduce the bug in a failing test before touching the fix |

### TDD Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Writing multiple tests before any implementation | Skips the feedback of watching each one fail and pass | One test, one cycle |
| Writing tests that always pass | Tests that cannot fail give no information | Run the test before writing implementation; confirm it is red |
| Testing internal implementation details | Tests break on every refactor even when behavior is unchanged | Assert only on public outputs and side effects |
| Skipping the refactor step | Code passes tests but accumulates complexity | Treat refactor as mandatory; tests are the safety net for it |
| Writing the implementation "temporarily" before the test | The test is retrofitted; intent is lost | Commit to test-first on every cycle, including small ones |
| Large test setups shared across many tests | A change to setup breaks unrelated tests | Keep each test's setup local and minimal |