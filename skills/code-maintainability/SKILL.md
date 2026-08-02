---
name: code-maintainability
description: Use when making code searchable, reusable, or changeable across teams — implementing PR-based cross-team changes, managing dependencies at scale, or consolidating version control platforms.
---

# Code Maintainability

## Type Safety and Linting

- Enable strict mode in type checker (TypeScript `strict: true`, Python `mypy --strict`)
- Enforce linting in CI — no merge without passing lint
- Domain invariants encoded in types, not comments
- Infer types from usage; avoid redundant annotations

## Dependency Management

- Commit lockfiles to version control
- Automate dependency updates (Dependabot, Renovate)
- Scan for vulnerabilities in CI
- Define dependency versions in a single, version-controlled manifest
- Test new dependency versions for compatibility before merging

## DORA Research Context

The 2019 State of DevOps Report identified code maintainability as a key contributor to continuous delivery success. Google's monolithic code repository demonstrates the scale involved — approximately 1 billion files and 2 billion lines of code. DORA's research shows that teams need easy access to find, reuse, and change code across the organization for delivery performance to improve. This is a [core model](/research/#core-model) capability.

## What It Is

Code maintainability is the ability of teams to easily find, reuse, and change code across the organization's codebase, including code maintained by other teams. It ensures that the codebase remains a shared asset rather than a collection of siloed repositories.

## Problem Solved

Symptoms when this capability is absent:

- Can't find or reuse existing code across the organization
- Making changes to code owned by other teams requires manual coordination
- Dependencies are outdated, unmanaged, or untraceable

## Key Practices

1. **Use a single version control platform** with default open access across the organization.

2. **Enable cross-team changes** through PR/code review mechanisms with automated owner approval routing.

3. **Keep dependencies up-to-date** using automated CI that tests compatibility and vulnerabilities of new versions.

4. **Ensure traceability** from any deployment back to the exact version of every dependency.

5. **Ensure reproducibility** by making build processes as deterministic as possible.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Multiple VCS platforms or restrictive access | Code becomes invisible across teams, duplicating effort | Single VCS platform with default open access |
| No process for cross-team code changes | Changes require manual coordination and wait time | PR-based mechanism with automated approval routing |
| Ad-hoc dependency management per team | Security vulnerabilities, version sprawl | Organization-wide standards, automated CI testing |

## How to Measure

- **Percentage of codebase that is searchable:** What fraction of the org's code can any developer discover and read
- **Median lead time to make a change to code you don't have write access to:** Measures cross-team friction
- **Percentage of duplicate code; percentage of unused code:** Signals wasted effort and maintainability debt
- **Number of different library versions in production; how many are over 1 year old:** Measures dependency sprawl

## Coaching Patterns

1. **Audit current state:** Measure searchability, dependency sprawl, and cross-team change latency. Walk through a real cross-team change end-to-end and time every step.

2. **Consolidate:** Move to a single VCS platform with default open access. Start with the most fragmented teams and migrate their repos first.

3. **Automate:** Build CI infrastructure that tests new dependency versions for compatibility. Set up automated owner routing so cross-team PRs reach the right reviewers without manual coordination.

## Related Skills

- [`version-control`](../version-control/): Foundation for a single, accessible codebase
- [`continuous-integration`](../continuous-integration/): Automates dependency testing and reproducibility

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |