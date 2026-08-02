---
name: wip-limits
description: Use when setting up Kanban, managing team capacity, or addressing too much work in progress — expose bottlenecks and improve flow by limiting concurrent work
---

# WIP Limits (Work in Process Limits)

## DORA Research Context

DORA research shows WIP limits drive software delivery performance improvements, especially combined with visual displays and monitoring. Derived from lean manufacturing — producing shorter lead times, higher quality, lower costs, less waste.

## What It Is

WIP limits constrain how many work items can be in each workflow stage at one time, designed to expose bottlenecks and improve flow by focusing on completing work rather than starting it.

## Problem Solved

- Everything is in progress, nothing gets finished
- Bottlenecks are invisible — work just accumulates
- People split time across too many tasks
- Lead times are long and unpredictable

## Key Practices

1. **Use a storyboard** — write all work on cards on a board (visualizes invisible technology inventory).
2. **Ink a dot on a card for every day it's been worked on** — easily see blocked or slow work.
3. **For each column, specify the WIP limit** — how many cards can be there at once.
4. **Pull, don't push** — after WIP limit is reached, team must move a card before pulling the next.
5. **Determine limits by team capacity** — e.g., 4 pairs of developers = max 4 cards in "in development."
6. **When limits cause idle time, improve the constraint** — don't increase limits.
7. **After things feel comfortable, reduce WIP limits further** to expose the next bottleneck.
8. **Aim for single-piece flow** — work flows from idea to customer with minimal wait or rework.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Not counting invisible work | Only measuring part of the picture | Visualize the entire value stream |
| WIP limits too large | No constraint; no improvement | If team splits time across tasks, limits are too high |
| Relaxing WIP limits when people are idle | Missed opportunity to improve the system | Help other parts of the value stream |
| Quitting while you're ahead | Just making limits easy | Reduce limits to expose next obstacle |
| Too many columns | Process has too many handoffs | Simplify the delivery process |

## How to Measure

- **Metric:** Do you know mean lead time and variability for the entire value stream?
- **Metric:** Are WIP limits surfacing obstacles? Are you doing something about those obstacles?
- **Metric:** Is flow increasing and lead time decreasing?

## Coaching Patterns

1. **Make all work visible:** Physical or virtual board with every work item.
2. **Set initial WIP limits at team capacity:** Slightly below what feels comfortable.
3. **Reduce limits every time things get easy:** Expose the next bottleneck; improve; repeat.

## Related Skills

- [`visual-management`](../visual-management/): How it supports
- [`work-visibility-in-value-stream`](../work-visibility-in-value-stream/): How it supports
- [`working-in-small-batches`](../working-in-small-batches/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | — |
| Time to Restore Service | — |