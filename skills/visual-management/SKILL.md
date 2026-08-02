---
name: visual-management
description: Use when setting up team dashboards, Kanban boards, CI monitors, or information radiators — creating shared, visible understanding of operational effectiveness
---

# Visual Management

## DORA Research Context

DORA's 2015 State of DevOps Report identifies visual management displays combined with WIP limits and production feedback as contributors to higher delivery performance. This practice is foundational to lean development.

## What It Is

Visual management displays key information about team processes where everybody can see it, creating shared understanding of operational effectiveness.

## Problem Solved

- Team members don't know what others are working on
- Build/test failures go unnoticed
- Status is buried in tools nobody checks
- No shared view of progress toward goals

## Key Practices

1. **Use card walls, storyboards, or Kanban boards** — physical or virtual — with cards representing in-progress work.
2. **Use dashboards and visual indicators** — CI monitors with traffic lights showing build status.
3. **Use burn-up/burn-down charts** (cumulative flow diagrams) showing progress against backlog.
4. **Use deployment pipeline monitors** showing the latest deployable build and failing stages.
5. **Use production telemetry monitors** — request counts, latency, errors, popular pages.
6. **Combine visual management with WIP limits and production feedback.**
7. **Create, update, and discard displays** in response to current team concerns.
8. **Involve the team in selecting goals and metrics** (e.g., via OKRs).

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Selecting metrics without team involvement | Displays get ignored | Teams with input into metrics are more motivated |
| Creating displays that are complex or not actionable | Information overload; no action | Simple whiteboard updated daily can beat elaborate dashboards |
| Not evolving visual displays | Displays become irrelevant | Change as team context evolves |
| Managing the metric, not the problem | Quick fixes to make display "green" | Fix root cause, not the indicator |

## How to Measure

- **Metric:** Do displays give you the information you need? Is it up to date?
- **Metric:** Are people acting on this information?
- **Metric:** Is the information contributing to measurable improvement toward team goals?
- **Metric:** Does everyone know what the goals are?

## Coaching Patterns

1. **Start simple:** A whiteboard with key information updated daily.
2. **Make displays glanceable:** Information should be understandable from across the room.
3. **Review displays in retrospectives:** Change, discard, or create new ones as needed.

## Related Skills

- [`wip-limits`](../wip-limits/): How it supports
- [`work-visibility-in-value-stream`](../work-visibility-in-value-stream/): How it supports
- [`monitoring-systems`](../monitoring-systems/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | — |
| Time to Restore Service | — |