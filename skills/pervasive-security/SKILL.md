---
name: pervasive-security
description: Use when integrating security into the development lifecycle, conducting security reviews, or automating security testing — building security in from the start, not at the end
---

# Pervasive Security

## DORA Research Context

The 2016 State of DevOps Report found that high-performing teams spend 50% less time remediating security issues. Security must be everyone's daily work, not tested at the end of the delivery cycle. Integrating security into design and automating security tests reduces both cost and risk while improving overall delivery outcomes.

## What It Is

Security is everyone's responsibility — also known as "shifting left." Developers work with security experts throughout the product lifecycle in small batches, integrating security into daily development, QA, and operations. This replaces the traditional model where security review happens as a final gate before release.

## Problem Solved

- Security reviews happen after development, causing expensive rework
- Security team is a bottleneck — understaffed and overwhelmed
- Developers aren't aware of common security risks
- Security testing is manual and happens only before release

## Key Practices

1. **Get InfoSec involved in software design:** Add security review as a gating factor before development begins, not after.
2. **Develop security-approved tools:** Provide preapproved libraries, packages, toolchains, and processes so developers can move fast without compromising security.
3. **Develop automated security testing:** Build SAST, DAST, and dependency scanning into the CI pipeline. Run on every commit and fail builds on critical issues.
4. **Integrate InfoSec into every phase:** Design, development, testing, deployment, and operations all include security perspectives.
5. **Invite InfoSec to software demos:** They spot security weaknesses early when changes are cheap to fix.
6. **Conduct security reviews for all major features:** Make reviews lightweight and collaborative, not heavyweight and adversarial.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Failing to collaborate with InfoSec | Security issues found too late; adversarial relationship | Collaborate from the start; treat InfoSec as partners |
| Understaffing InfoSec | 1:10:100 ratio (InfoSec:infra:dev) is unsustainable | Scale through automation, not more reviewers |
| Engaging InfoSec too late | Changes are painful and expensive to remediate | Get them involved at the design phase |
| Developers unfamiliar with OWASP Top 10 | Common vulnerabilities aren't prevented | Train developers on security fundamentals |

## How to Measure

- **Percentage of features that undergo security review early in design:** Should increase over time
- **Time security review adds to development:** Should decrease as collaboration improves
- **Number of security requirements in automated testing:** Should increase
- **Number of InfoSec-approved libraries available and in use:** Should grow

## Coaching Patterns

1. **Invite InfoSec to design reviews:** Start with high-risk features. Build the relationship before there's a crisis.
2. **Build a preapproved library list:** Make the secure path the easy path. Curate and maintain a list of vetted dependencies.
3. **Automate security scanning:** Add SAST/DAST to the CI pipeline. Start with critical severity; fail builds and notify teams immediately.

## Related Skills

- [`streamlining-change-approval`](../streamlining-change-approval/): Reducing approval friction while maintaining security
- [`continuous-integration`](../continuous-integration/): Automating security checks in the CI pipeline

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | — |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |