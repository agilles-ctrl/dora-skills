---
name: customer-feedback
description: Use when designing features, gathering user input, or validating product decisions — building feedback into the delivery process so teams build the right thing.
---

# Customer Feedback

## DORA Research Context

2016 State of DevOps: teams perform better when they collect customer satisfaction metrics regularly and use feedback to design products. 2019: increased customer engagement strengthens identification with organizational goals. Industry data (Kohavi, Microsoft): only ~1/3 of features improve business outcomes. Lean product management model category.

## What It Is

Customer feedback is the practice of regularly collecting satisfaction metrics, seeking out feedback on product quality, and using that feedback to design products and features. It closes the loop between building and learning.

## Problem Solved

- Features ship but don't solve real problems (2/3 deliver zero or negative outcomes)
- Feedback arrives too late to act on
- Success is measured by "delivered as specified" not "solved the customer's problem"
- Teams build what they were told to build, not what users need

## Key Practices

1. **Gather customer feedback first** — before defining any potential features.
2. **Validate you're solving a real problem before writing code** — hypothesis-driven development.
3. **Use A/B testing for user experiments** on live features.
4. **Track AARRR metrics:** Acquisition, Activation, Retention, Referral, Revenue.
5. **Build feedback gathering into the delivery process** — every significant feature starts with user research.
6. **For early-lifecycle products, validate the business model before code** (lean startup).

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Not gathering feedback at all | Building in a vacuum | Start with any feedback channel |
| Gathering feedback too late | Can't act on it within delivery cycle | Integrate feedback at feature planning stage |
| Dismissing inconvenient feedback as "scope creep" | Incomplete solutions that don't solve problems | Expect to discard 2/3 of proposed solutions |
| Measuring success by "delivered as specified" | Wrong thing, built well | Measure by customer outcomes |

## How to Measure

- Do you have customer satisfaction metrics? Are they updated regularly? Do you act on them?
- Do you validate features before building? Perform user research with prototypes?
- Do you make changes to features based on user research?
- Adoption, retention, CSAT, NPS

## Coaching Patterns

1. **Pick one feedback channel** — in-app survey, user interview, analytics — and start collecting.
2. **Require user validation before implementation** — every feature spec includes evidence of user need.
3. **Make feedback visible to the whole team** — dashboards, not reports buried in email.

## Related Skills

- [`user-centric-focus`](../user-centric-focus/): How it supports
- [`team-experimentation`](../team-experimentation/): How it supports
- [`working-in-small-batches`](../working-in-small-batches/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | — |