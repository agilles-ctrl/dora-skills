---
name: well-being
description: Use when addressing burnout, deployment anxiety, or excessive rework — creating a work environment where people can do their best work sustainably
---

# Well-Being

## DORA Research Context

DORA studies well-being through deployment pain, rework, and burnout. 2016: high performers spend 49% time on new work vs. 38% for low performers. 2018: elite performers spend 50% on new work and 19.5% on rework. Continuous delivery predicts lower rework. Burnout research draws on Maslach's six organizational risk factors.

## What It Is

Well-being reflects happiness and job satisfaction and predicts both organizational performance and employee tenure. It is studied through deployment pain (fear of deploying), rework (unplanned work indicating poor quality), and burnout.

## Problem Solved

- Deployments cause fear and anxiety; people dread pushing to production
- Excessive unplanned work and rework steal time from value creation
- Burnout causes turnover, disengagement, and poor performance
- Work environment problems are blamed on individuals

## Key Practices

1. **Reduce deployment pain by implementing continuous delivery** — the same practices that improve speed and stability also reduce stress.
2. **Build quality in from the start** to minimize rework and unplanned work.
3. **Address Maslach's six organizational risk factors for burnout:** work overload, lack of control, insufficient rewards, breakdown of community, absence of fairness, value conflicts.
4. **Fix the work environment, not the person** — organizational changes have higher success likelihood.
5. **Track proportion of time on new/proactive work vs. unplanned/reactive work.**
6. **Use continuous delivery to drive higher quality and lower unplanned work.**

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Fixing the person instead of the environment | Wellness programs don't address root causes | Change organizational risk factors (management controls all of them) |
| Ignoring deployment pain | Painful deploys → fear → less frequent deploys → more pain | Implement CD technical practices |
| Not tracking new work vs. rework | Can't quantify how much value time is being lost | Measure and make visible the split |

## How to Measure

- **Metric:** Deployment pain: fear/anxiety when pushing code to production
- **Metric:** Rework: % of time on new work vs. unplanned work/rework
- **Metric:** Burnout: assess through the 6 organizational risk factors (overload, control, rewards, community, fairness, values)

## Coaching Patterns

1. **Measure deployment pain:** Anonymous survey; track over time as CD practices improve.
2. **Track the new-work/rework split:** Make it visible to the team and leadership.
3. **Address the risk factor with the lowest score:** Start with one; management owns all six.

## Related Skills

- [`continuous-delivery`](../continuous-delivery/): How it supports
- [`deployment-automation`](../deployment-automation/): How it supports
- [`job-satisfaction`](../job-satisfaction/): How it supports
- [`generative-organizational-culture`](../generative-organizational-culture/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |