---
name: proactive-failure-notification
description: Use when configuring alerts, setting up monitoring thresholds, or reducing alert fatigue — detecting and acting on problems before they become outages
---

# Proactive Failure Notification

## DORA Research Context

DORA's 2014 State of DevOps Report identifies proactive monitoring as a significant predictor of software delivery performance. When failures are primarily reported by customers rather than internal monitoring, performance suffers.

## What It Is

Proactive failure notification generates notifications when monitored values approach known failure thresholds, rather than waiting for systems to fail or customers to report outages.

## Problem Solved

- Customers report outages before the team knows about them
- Alerts fire only when systems are already down, not when approaching thresholds
- Alert fatigue — too many alerts, most are noise
- Irrelevant alerts get disabled entirely, losing signal with the noise

## Key Practices

1. **Generate failure notifications using specific alerting rules** that define conditions and channels.
2. **Set thresholds for metrics that indicate real trouble** — alert before user-facing impact occurs.
3. **Monitor in at least two ways:** threshold-based (value over/under) and rate-of-change-based (changing faster/slower than expected).
4. **Hold incident postmortems** and determine which indicators could have predicted the incident.
5. **Plan a notification strategy** — if a notification always requires the same action, automate the response.
6. **Configure alerts to notify the people who can actually fix the problem.**
7. **Regularly review notifications** — delete those that cannot be acted upon.
8. **Prevent alert fatigue** — during incidents, a deluge of notifications is distracting.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Reactive monitoring only | Alerting only when systems are already down | Set thresholds that predict failures |
| Alert fatigue | Desensitization leads to ignored alerts | Prune irrelevant alerts; only generate actionable ones |
| Disabling all alerts | Throwing out signal with noise | Selectively disable irrelevant; keep relevant |
| Not reviewing and pruning | Unactionable alerts accumulate | Regular review cycles |

## How to Measure

- **Metric:** Are failure alerts from logging/monitoring systems captured and used?
- **Metric:** Is system health proactively monitored using threshold warnings?
- **Metric:** Is system health proactively monitored using rate-of-change warnings?
- **Metric:** False positive rate; false negative rate

## Coaching Patterns

1. **Audit current alerts:** How many fire? How many are acted on? Delete unactionable ones.
2. **Set thresholds before failure:** Identify the value that causes user impact; alert at 70-80% of that.
3. **Automate no-decision responses:** If the response is always the same, script it.

## Related Skills

- [`monitoring-and-observability`](../monitoring-and-observability/): How it supports
- [`monitoring-systems`](../monitoring-systems/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | — |
| Lead Time for Changes | — |
| Change Failure Rate | X |
| Time to Restore Service | X |