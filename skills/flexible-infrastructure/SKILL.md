---
name: flexible-infrastructure
description: Use when provisioning infrastructure, migrating to cloud, or building self-service platforms — ensuring teams can rapidly adapt infrastructure to changing needs
---

# Flexible Infrastructure

## DORA Research Context

The Accelerate State of DevOps 2023 report found that flexible infrastructures lead to 30% higher organizational performance. The 2019 report showed that elite performers were more than 23x more likely to meet all 5 NIST cloud characteristics than low performers. Meeting all NIST characteristics correlates with 2.6x better cost estimation.

## What It Is

Flexible infrastructure allows teams to rapidly and reliably adapt to changing business needs without being bottlenecked by hardware procurement or manual provisioning, typically through cloud that meets all five NIST essential characteristics.

## Problem Solved

- Provisioning new environments takes days or weeks
- Infrastructure costs are invisible or unpredictable
- Cloud migration didn't improve speed or cost (lift-and-shift penalty)
- Systems can't auto-scale to meet demand

## Key Practices

1. **Meet all five NIST cloud characteristics:** On-demand self-service, broad network access, resource pooling, rapid elasticity, measured service.
2. **Adopt Infrastructure as Code (IaC):** Infrastructure config in version control; automated provisioning via cloud APIs.
3. **Implement segregation of duties through version control approvals:** Not manual change boards.
4. **Build an Internal Developer Platform (IDP):** That provides "paved roads" — abstract cloud resources with self-service and autonomy.
5. **Align incentives:** So system owners have both cost visibility and incentive to build efficient systems (e.g., chargeback models).

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| "Cloud penalty" (lift and shift) | Keeps traditional manual provisioning; negates cloud benefits | Radically transform applications and processes, or stay on-prem |
| Building gates instead of guardrails | IDP that requires manual tickets | Prioritize self-service and autonomy |
| Incentivizing migration volume over modernization | Teams bypass modernization to hit targets | Measure against NIST characteristics and business outcomes |
| Neglecting training | Cloud tools without cloud skills | Dedicated budget and time for continuous learning |

## How to Measure

- **Time to provision:** From developer request to ready-to-use resource
- **Self-service adoption rate:** % of infra requests fulfilled via APIs/IDP vs. manual tickets
- **Elasticity:** Can systems auto-scale without human intervention?
- **Cost transparency:** Can teams view and forecast their infrastructure costs?

## Coaching Patterns

1. **Assess against NIST characteristics:** Identify which of the 5 are missing.
2. **Start IaC:** Version control everything; pilot with one low-risk application.
3. **Build guardrails, not gates:** Automated compliance checks, not manual approval boards.

## Related Skills

- [`platform-engineering`](../platform-engineering/): Builds the self-service platform atop flexible infrastructure
- [`configuration-as-code`](../configuration-as-code/): Infrastructure as code is a prerequisite
- [`deployment-automation`](../deployment-automation/): Automating deploys onto flexible infra

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |