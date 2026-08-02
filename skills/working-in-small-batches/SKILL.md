---
name: working-in-small-batches
description: Use when decomposing features, planning sprints, or implementing AI coding practices — breaking work into independently completable units that can ship in hours to days.
---

# Working in Small Batches

## DORA Research Context

2025 State of AI-assisted Software Development: small batches amplify AI's positive impact on product performance. Critical countermeasure to AI-generated instability. Foundational to both CI and trunk-based development. Part of lean product management and core model categories.

## What It Is

Working in small batches breaks down work into independently completable units finished in hours to a couple of days, enabling rapid hypothesis testing and fast feedback loops. Each batch is deployed independently for immediate learning.

## Problem Solved

- Work sits in progress for weeks, accumulating integration risk
- Feedback on whether the right thing was built arrives too late
- AI accelerates code generation but review can't keep up with large batches
- Failed features represent weeks of wasted investment

## Key Practices

1. **Break features into work units completable in hours to a couple of days.**
2. **Apply INVEST:** Independent, Negotiable, Valuable, Estimable, Small, Testable.
3. **Check code into trunk at least once per day** — multiple small releasable changes.
4. **Use dark launching** — deploy behind feature toggles without making it visible to users.
5. **Use feature toggles** to enable/disable functionality at deploy or runtime.
6. **Consider batches incomplete until deployed to production** and feedback has begun.
7. **When using AI coding assistants, enforce small batches** — shift focus from code generation to thoughtful decomposition.

## Commit and PR Patterns

### Small Incremental Commits

- One logical change per commit — if the message needs "and", split it
- Commit after every passing change; push immediately
- Each commit should be independently deployable and revertable
- Write descriptive commit messages: what changed and why (not how)

Good: `feat: add discount calculation for premium users`
Bad: `fixed stuff` or `WIP`

### Small Pull Requests

- Under 400 lines changed; under 10 files touched
- Single purpose — one PR = one feature, bugfix, or refactor
- Open the PR as soon as there's something to review (not when "done")
- Draft PRs for early feedback; mark ready when tests pass
- Keep PRs small by stacking — `feat/module-a` → `feat/module-b` targeting module-a

Before (bad): PR with 1200 lines, 25 files, 3 unrelated changes
After (good): 3 stacked PRs, each ~300 lines, single concern

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Not breaking work small enough | >1 week batches have too much risk | Any batch >1 week is too big |
| Small batches but regrouping before deploying | Delays feedback on defects and correctness | Deploy each batch independently |
| AI generating large, complete features | Higher cognitive load per line to review; instability | Enforce small batch discipline; AI-generated code needs more verification |

## How to Measure

- How often are releases possible? How does cadence differ across teams?
- What proportion of features can be completed in ≤1 week?
- Can changes be committed and released before feature completion?
- Are MVPs defined as goals?

## Coaching Patterns

1. **Set a batch size limit** — no task > 3 days; decompose anything larger.
2. **Use feature toggles** — deploy incomplete features dark; complete them incrementally.
3. **Pair AI with small batches** — use AI for one small unit, review, commit, repeat.

## Related Skills

- [`trunk-based-development`](../trunk-based-development/): How it supports
- [`continuous-integration`](../continuous-integration/): How it supports
- [`feature-flags`](../feature-flags/): How it supports
- [`wip-limits`](../wip-limits/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |