---
name: user-centric-focus
description: Use when designing features, gathering user feedback, or ensuring AI-accelerated development stays aligned with real user needs — preventing the "feature factory" trap
---

# User-Centric Focus

## DORA Research Context

Teams with strong user focus have 40% higher organizational performance. AI amplifies this: with strong user focus, AI grows performance; without it, AI can harm performance by accelerating production of low-value software ("feature factory" trap). 2023, 2024, 2025 DORA reports. This capability is part of the [AI model](/ai/#explore-the-model).

## What It Is

A measurable capability defined by how well teams understand user needs, prioritize user experience, and leverage feedback to continuously reprioritize work. It ensures that software delivery velocity translates to actual user value, not just more features shipped.

## Problem Solved

- Features ship but nobody uses them (2/3 of features deliver zero or negative business outcomes)
- AI accelerates feature output without validation — more wrong things, faster
- Developers are disconnected from users; product decisions happen in a black box
- Success is measured by output (features shipped) not outcomes (user value)

## Key Practices

1. **Integrate user feedback loops:** Low-latency channels (in-app surveys, direct observation); feedback immediately available to teams.
2. **Make user metrics visible:** Display CSAT, task completion, H.E.A.R.T. metrics alongside technical metrics.
3. **Involve engineering in user research:** Invite developers to observe user testing directly.
4. **Leverage Spec-Driven Development (SDD):** Refine user needs into detailed specs before code; specs constrain AI-generated code.
5. **Continuously reprioritize based on user feedback:** Be willing to discard features that don't solve real problems.
6. **Measure outcomes, not output:** Shift from velocity/features shipped to user value delivered.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Feature factory mindset | Measuring output instead of outcomes | AI exacerbates this; more code solving fewer problems |
| Resume-driven development | Adopting tech for its own sake (solutionism) | Focus on user problems, not technology choices |
| Organizational silos | Policies disconnect developers from users | Remove gatekeepers between developers and user feedback |

## How to Measure

- **Product performance:** Adoption, retention, CSAT
- **Feedback integration:** How often feedback leads to reprioritization
- **Team alignment:** "We have a clear understanding of what users want to accomplish"

## Coaching Patterns

1. **Create direct user feedback channels:** In-app surveys, observation sessions; make results visible.
2. **Invite developers to user testing:** Observation creates empathy that reports can't.
3. **Adopt SDD:** User requirement specs become the constraint for AI-generated code.

## Related Skills

- [`customer-feedback`](../customer-feedback/): How it supports
- [`team-experimentation`](../team-experimentation/): How it supports
- [`working-in-small-batches`](../working-in-small-batches/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | — |
| Change Failure Rate | X |
| Time to Restore Service | — |