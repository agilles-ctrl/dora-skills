---
name: platform-engineering
description: Use when building or improving internal developer platforms, addressing "ticket-ops" bottlenecks, or designing self-service infrastructure — shifting complexity down so teams can focus on user value
---

# Platform Engineering

## DORA Research Context

2025: 90% of organizations use internal developer platforms; 76% have dedicated platform teams. When platform quality is high, AI adoption's effect on org performance becomes strong and positive. When low, AI's effect is negligible. 2024: developer independence resulted in 5% productivity improvement. This capability is part of the [AI model](/ai/#explore-the-model).

## What It Is

Platform engineering is a sociotechnical discipline where engineers design and build internal developer platforms — shared, self-service "golden paths" for building, testing, and deploying applications. It shifts cognitive load down so development teams can focus on delivering user value rather than infrastructure complexity.

## Problem Solved

- Developers wait days for environments, tickets, approvals
- Platform team is a bottleneck ("ticket-ops")
- Cognitive load on developers is too high — Kubernetes, cloud networking, security, all at once
- Individual developer productivity gains from AI are lost to downstream bottlenecks

## Key Practices

1. **Adopt a product management mindset:** Assign a PM focused on developer experience (DevEx).
2. **Map critical user journeys:** Spinning up a service, debugging production — to find friction.
3. **"Shift down" cognitive load:** Abstract Kubernetes, cloud networking, security into simple self-service paths.
4. **Start with a minimum viable platform:** Build just enough for the most common workflow.
5. **Design for extensibility:** Clear APIs and contribution models so other teams can contribute.
6. **Provide clear feedback on task outcomes:** The platform capability most correlated with positive UX.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| "Build it and they will come" | Platform nobody asked for | User research first |
| "Ivory tower" — dictating standards | Platform team seen as gatekeepers | Collaborate with users |
| "Ticket-ops" — reactive ticket mill | Same bottleneck, different name | Enable self-service |
| "Big bang" release | Building everything before shipping | MVP; iterate based on usage |
| "One-size-fits-all" | Rigid "golden cage" | Enabling constraints with flexibility |

## How to Measure

- **Software delivery performance:** Lead time, deployment frequency, failure recovery time
- **Developer satisfaction (DevEx):** CSAT or NPS surveys
- **Adoption:** H.E.A.R.T. framework — onboarding rate, continued usage
- **Task success:** Efficiency of developers completing key workflows

## Coaching Patterns

1. **Map developer journeys:** Identify the top 3 workflows that cause the most friction.
2. **Build an MVP platform:** Solve the most painful workflow first; make it self-service.
3. **Manage the J-curve:** Expect a dip as complexity increases before recovery at higher performance.

## Related Skills

- [`flexible-infrastructure`](../flexible-infrastructure/): How it supports
- [`teams-empowered-to-choose-tools`](../teams-empowered-to-choose-tools/): How it supports
- [`deployment-automation`](../deployment-automation/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |