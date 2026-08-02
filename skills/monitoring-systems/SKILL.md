---
name: monitoring-systems
description: Use when sharing operations data with product and business teams, or using monitoring insights beyond incident response — turning ops data into strategic decisions.
---

# Monitoring Systems to Inform Business Decisions

## DORA Research Context

DORA positions monitoring as enabling rapid feedback and cross-team knowledge transfer. Operations data shared across the organization helps people and systems improve. Supporting practices model category.

## What It Is

Monitoring is the process of collecting, analyzing, and using information about applications and infrastructure to guide business decisions — not just incident response. It turns operational telemetry into strategic insight.

## Problem Solved

- Operations data stays in ops; product and business teams never see it
- Decisions are made without data on actual system behavior
- Monitoring is reactive — only used when things break
- No shared understanding between technical and business teams about system health

## Key Practices

1. **Collect data from key areas throughout the value chain** — application performance and infrastructure.
2. **Choose metrics appropriate for function and for the business.**
3. **Transform and visualize data** to make it accessible to different audiences.
4. **Share operations data upstream** to development and product management.
5. **Provide context with data** — help non-experts understand if values are high/low, expected, changing.
6. **Choose the right medium per audience** — real-time dashboards for DevOps, regular reports for longer-period metrics.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Monitoring reactively | Only alerts when down; no leading indicators | Monitor thresholds and trends |
| Monitoring too small a scope | Focusing on one or two areas | Cover the full development and delivery pipeline |
| Monitoring everything | Alert fatigue; drowning in data | Thoughtful selection; focus on key areas |
| Focusing on local optimizations | Optimizing one service without broader context | Evaluate across the full infrastructure |

## How to Measure

- Data from application performance monitoring is used to make business decisions
- Data from infrastructure monitoring is used to make business decisions
- Is monitoring data shared, discussed, and acted upon outside the ops team?

## Coaching Patterns

1. **Share one ops dashboard with product** — pick a metric that matters to both teams.
2. **Include monitoring data in business reviews** — system performance alongside business metrics.
3. **Start simple** — a shared spreadsheet is better than nothing.

## Related Skills

- [`monitoring-and-observability`](../monitoring-and-observability/): How it supports
- [`proactive-failure-notification`](../proactive-failure-notification/): How it supports
- [`work-visibility-in-value-stream`](../work-visibility-in-value-stream/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | — |
| Lead Time for Changes | — |
| Change Failure Rate | X |
| Time to Restore Service | X |