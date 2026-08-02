---
name: continuous-integration
description: Use when setting up build pipelines, configuring automated tests on commit, or establishing merge frequency disciplines — rapid feedback on every code change.
---

# Continuous Integration

## DORA Research Context

The 2015 and 2016 State of DevOps Reports found that CI leads to higher deployment frequency, more stable systems, and higher quality software. The 2018 report established that test feedback should take no more than approximately 10 minutes, and teams perform better when developers merge into trunk at least daily. This is a [core model](/research/#core-model) capability.

## What It Is

CI is the practice of developers integrating all work into trunk/mainline at least daily, with automated builds and tests running on every commit to provide rapid feedback. It catches integration problems early, when they are cheapest to fix.

## Problem Solved

Symptoms when this capability is absent:

- Integration hell — merging weeks of divergent work is painful and error-prone
- Broken builds go unnoticed for hours or days
- Tests take so long that developers avoid running them
- "It works on my machine" — builds aren't reproducible

## Key Practices

1. **Every commit triggers a build** of the software and a series of automated tests.

2. **Build process is automated** — creates authoritative, numbered, repeatable packages used by all downstream processes.

3. **Tests provide feedback within minutes** — unit and acceptance tests covering high-value functionality.

4. **CI system runs on every check-in** with visible status (chat, physical indicators — not email).

5. **Broken build is highest priority** — fix immediately or revert the breaking change.

6. **Practice trunk-based development** — merge into trunk at least daily, work in small batches.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Not putting everything in version control | Builds aren't reproducible | Version control all scripts, configs, and dependencies |
| Tests taking too long (>10 min) | Developers stop running them or batch changes | Improve efficiency, parallelize, split into pipeline stages |
| Not fixing broken builds immediately | Compound failures; team loses trust in CI | Fix within minutes or revert |
| Having CI tools but no daily merge discipline | False confidence; integration still happens in big batches | Enforce small batches and daily trunk merges |

## How to Measure

- **Percentage of commits that trigger a build without manual intervention:** Measures automation coverage
- **Percentage of commits that trigger automated tests:** Measures test coverage in CI
- **Time between build break and fix (or revert):** Measures team discipline and CI health
- **Availability of builds to testers for exploratory testing:** Measures downstream value

## Coaching Patterns

1. **Get builds green and keep them green** — fix all existing failures before adding new tests. A red build loses all signal value.

2. **Speed up the build** — invest in test performance until feedback is under 10 minutes. Profile the slowest tests, parallelize where possible, and split into pipeline stages.

3. **Make CI status visible** — big screens, chat notifications; make failure impossible to ignore. If nobody sees a broken build, nobody fixes it.

## Related Skills

- [`trunk-based-development`](../trunk-based-development/): Enables daily integration discipline
- [`test-automation`](../test-automation/): Provides the tests that CI runs on every commit
- [`version-control`](../version-control/): Foundation for reproducible, automated builds
- [`continuous-delivery`](../continuous-delivery/): CI is the gateway practice for CD

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | — |