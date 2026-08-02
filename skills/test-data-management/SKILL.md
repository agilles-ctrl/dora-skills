---
name: test-data-management
description: Use when managing test environments, test data, or testing strategies — ensuring adequate, on-demand test data that doesn't constrain automated testing
---

# Test Data Management

## DORA Research Context

DORA analysis shows that successful teams ensure adequate test data is available for full test suites, data can be acquired on demand, and data availability doesn't limit the tests teams can run. Over-reliance on external data makes tests brittle; copying production data introduces security and compliance risks.

## What It Is

Good test data management lets teams validate user journeys, test edge cases, reproduce defects, and simulate errors without being constrained by data availability or quality. It covers how data is created, refreshed, masked, and made available to automated and manual testing workflows.

## Problem Solved

- Tests can't run because test data isn't available
- Production data copies are too large, slow, and contain sensitive information
- Tests are brittle because they depend on data defined outside the test scope
- Teams spend excessive time managing test data instead of writing tests

## Key Practices

1. **Favor unit tests:** Unit tests should be independent of external data. This is the majority of tests per the test automation pyramid.
2. **Tests should create their own state via application APIs:** Don't depend on pre-existing data. Each test sets up exactly what it needs.
3. **Minimize reliance on test data:** Data requires ongoing maintenance as APIs evolve. Prefer tests that don't need it.
4. **Favor in-memory databases for tests:** Faster execution and better isolation than persistent databases shared across test runs.
5. **Make test data readily available:** Identify relevant production data subsets; export regularly and make available on demand.
6. **Mask or hash sensitive data:** Never use raw production data in test environments. Always anonymize PII, credentials, and secrets.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Over-reliance on data in testing | Tests are brittle; high maintenance overhead | Unit tests independent of external data; tests create their own state |
| Using full production DB copies | Slow, large, exposes sensitive data | Extract only relevant sections; always mask sensitive information |
| Relying on outdated test data | Tests don't reflect current reality | Keep test data refreshed regularly; let tests create their own state |

## How to Measure

- **Time developers/testers spend managing test data:** Should decrease as processes improve
- **Percentage of key data sets available on demand:** Should approach 100%
- **Number of automated tests that can run without additional data acquisition:** Should increase over time

## Coaching Patterns

1. **Increase unit test coverage:** Minimize reliance on data-dependent higher-level tests. Shift testing left.
2. **Tests create their own state:** Each test sets up what it needs via application APIs. No data dependencies between tests.
3. **Export production data subsets:** Export regularly rather than full copies. Always mask sensitive data before use in any non-production environment.

## Related Skills

- [`test-automation`](../test-automation/): The testing strategy this capability supports
- [`test-driven-development`](../test-driven-development/): Writing tests that don't depend on external data

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | — |