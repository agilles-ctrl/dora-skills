---
name: work-visibility-in-value-stream
description: Use when mapping delivery processes, identifying bottlenecks, or understanding how work flows from idea to customer — making invisible work visible.
---

# Visibility of Work in the Value Stream

## DORA Research Context

Part of lean product management. Teams must understand how work moves from business to customer, have visibility into the flow, see it on visual displays, and have flow info available. Predicts both software delivery and organizational performance. Lean product management model category.

## What It Is

Visibility of work represents how well teams understand and see the flow of work from the business all the way through to customers, including the status of products and features. It surfaces bottlenecks and exposes handoff friction.

## Problem Solved

- No one knows where work is stuck or why lead times are so long
- The organization has no shared understanding of the end-to-end delivery process
- Improvements target local optimizations that don't help overall flow
- Handoffs between teams are invisible and unmeasured

## Key Practices

1. **Use value stream mapping (VSM)** — gather stakeholders from every part of the delivery value stream.
2. **Break the stream into 5-15 process blocks** recording activity and responsible team.
3. **For each block, measure:** Lead time (accept to handoff), Process time (uninterrupted completion time), % Complete and Accurate (%C/A — usable without rework).
4. **Identify blocks with poor quality downstream** (low %C/A) and long lead times relative to process time.
5. **Create a future-state map** reflecting the optimal state 6 months to 2 years out.
6. **Re-run VSM regularly** (every 6 months).

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Overestimating organizational knowledge | Nobody has the full picture; surprises are common | Map the entire stream; involve people from every part |
| Failing to map the entire value stream | Local optimizations; missed opportunities | Map from idea through IT operations and support |
| Focusing on non-bottleneck areas | No impact on overall lead time | Improve the constraint first |
| No authority to make changes | Maps are interesting but nothing changes | Involve people with decision authority |

## How to Measure

- Is there a current or recent value stream map available to anyone?
- Does everyone have access to a visual display of their work and status?
- Are statistics on lead time and %C/A available to the team?

## Coaching Patterns

1. **Run a VSM workshop** — 1-2 days, all stakeholders, map the current state.
2. **Measure the top 3 process blocks** — lead time, process time, %C/A.
3. **Make metrics visible** — visual displays showing flow; update regularly.

## Related Skills

- [`visual-management`](../visual-management/): How it supports
- [`wip-limits`](../wip-limits/): How it supports
- [`monitoring-systems`](../monitoring-systems/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | — |
| Time to Restore Service | — |