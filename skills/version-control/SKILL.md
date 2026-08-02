---
name: version-control
description: Use when setting up repositories, defining commit practices, or expanding version control beyond code to configurations, scripts, AI prompts, and agent configs — the foundation of reproducible software delivery
---

# Version Control

## DORA Research Context

DORA research consistently shows comprehensive version control predicts continuous delivery. In the AI era, strong VC practices amplify AI's positive impact on individual effectiveness and team performance. Frequent commits + rollback capability create a safety net for AI experimentation. This capability is part of the [AI model](/ai/#explore-the-model).

## What It Is

Version control systems provide a logical means to organize files and coordinate their creation, access, updating, and deletion. Comprehensive use — beyond code to all artifacts — predicts continuous delivery. It is the foundation for reproducibility, traceability, and safe experimentation.

## Problem Solved

- Builds aren't reproducible because configs and scripts aren't versioned
- AI-generated code causes instability with no easy rollback
- On-call can't trace what changed when an incident occurs
- Disaster recovery requires manual reconstruction of environments

## Key Practices

1. **Version everything:** Not just app code but test/deployment scripts, infrastructure/config, libraries, packages.
2. **Store AI artifacts in version control:** AI prompts, agent configuration files (CLAUDE.md, GEMINI.md, copilot instructions).
3. **Bring small, frequent commits into the inner loop:** Commit at every clean state, not just when "ready."
4. **Ensure every commit triggers automated creation of deployable packages:** Using only version-controlled info.
5. **Make it possible to recreate production-like environments on demand:** From version-controlled scripts and config.
6. **Use version control to enable reproducibility, traceability, disaster recovery, auditability.**

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Limited application — only app code | Can't reproduce builds or environments | Version all configs, scripts, infra, dependencies |
| Neglecting the inner loop | Delaying commits until "perfect"; losing version safety | Commit small and often, especially with AI code |
| Merge conflicts from long-lived branches | High AI code volume exacerbates | Short-lived branches; frequent integration |

## How to Measure

- **Commit frequency:** High frequency = higher effectiveness, especially with AI
- **Rollback reliance:** Frequent use amplifies AI's positive impact
- **Scope:** % of app code, system configs, app configs, build scripts in version control
- **Recovery speed and reprovisioning speed**

## Coaching Patterns

1. **Expand scope:** Identify what's NOT in VC: configs, scripts, AI prompts, agent configs.
2. **Commit small and often:** Every clean state; treat commits like save points in a game.
3. **Make rollbacks a first-class capability:** Strong VC enables fast recovery.

## Related Skills

- [`trunk-based-development`](../trunk-based-development/): How it supports
- [`continuous-integration`](../continuous-integration/): How it supports
- [`continuous-delivery`](../continuous-delivery/): How it supports
- [`working-in-small-batches`](../working-in-small-batches/): How it supports

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |