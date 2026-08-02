---
name: documentation-quality
description: Use when creating, reviewing, or improving internal documentation — ensuring documentation is clear, findable, reliable, and amplifies every other engineering practice.
---

# Documentation Quality

## DORA Research Context

The 2022 DORA report found that documentation quality underpins ALL technical capabilities. The lift to organizational performance from technical capabilities is massively amplified for teams with above-average documentation quality. For example, trunk-based development's impact on organizational performance is 36% for teams with below-average docs versus 1525% for teams with above-average docs. This is a [core model](/research/#core-model) capability.

## What It Is

Documentation quality measures how clear, findable, and reliable internal documentation is. It underpins the implementation of every single technical practice DORA studied, acting as a force multiplier for all other engineering capabilities.

## Problem Solved

Symptoms when this capability is absent:

- Information is tribal knowledge — new team members take months to become productive
- Documentation exists but is outdated, contradictory, or unfindable
- Every technical capability is harder to implement without good docs

## Key Practices

1. **Actively create and maintain documentation** — it takes sustained work, not one-time effort.

2. **Follow the 8 quality attributes:** clarity, findability, reliability, and others from the 2022 DORA survey.

3. **Follow established style guides** such as the Google developer documentation style guide.

4. **Leverage technical writers or documentation champions** within the organization.

5. **Treat documentation as code** — version it, review it, maintain it as systems evolve.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Treating documentation as low-priority, non-technical work | Docs rot and become useless | Recognize it as technical work with proven performance impact |
| Letting documentation rot after initial creation | Becomes untrustworthy | Actively maintain alongside code changes |

## How to Measure

- **Eight quality attributes:** clarity, findability, reliability, and 5 others from the 2022 survey
- **Whether documentation is current and reflects the actual system state:** Surveys and spot-checks
- **Time to onboard new team members; time to find answers to technical questions:** Direct measure of findability

## Coaching Patterns

1. **Audit existing documentation** against the 8 quality attributes. Pick 5 key documents and score each one — clarity, findability, accuracy, etc. Share the results with the team.

2. **Treat docs as code** — version in the same repo, review in PRs, update with every feature. Add a documentation checkbox to your PR template.

3. **Invest in technical writing** — hire or train documentation champions. Give one person per team explicit responsibility for documentation quality and the time to maintain it.

## Related Skills

- [`ai-accessible-internal-data`](../ai-accessible-internal-data/): Quality docs make internal data AI-accessible
- [`code-maintainability`](../code-maintainability/): Good docs make the codebase more maintainable

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |