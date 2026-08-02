# DORA Skills — Full Capability Coverage

**Date:** 2026-08-01
**Status:** Approved

## Goal

Update the dora-skills repo to cover all 34 DORA capabilities from https://dora.dev/capabilities/, adding ~25 new capability skills and updating existing practice skills with DORA research citations.

## Architecture: Two-Tier Skill System

```
dora-overview (router — updated)
├── Capability skills (NEW: mirror dora.dev articles)
│   ├── continuous-delivery, continuous-integration, ...
│   └── working-in-small-batches
│
└── Practice skills (EXISTING: engineering how-tos)
    ├── test-driven-development, small-incremental-commits, ...
    └── stop-and-clarify
```

**Capability skills:** Deep reference + actionable. Each mirrors a dora.dev capability article with research evidence, key practices, pitfalls, coaching patterns, and cross-references to practice skills.

**Practice skills:** Existing engineering how-tos. Stay unchanged in function but get DORA research citations added to Impact sections.

## New Capability Skills (25 needed)

Capabilities not yet covered by existing practice skills:

| # | Capability | Category | New skill name |
|---|-----------|----------|---------------|
| 1 | AI-accessible internal data | AI | `ai-accessible-internal-data` |
| 2 | Clear and communicated AI stance | AI | `clear-and-communicated-ai-stance` |
| 3 | Code maintainability | Core | `code-maintainability` |
| 4 | Continuous delivery | Core | `continuous-delivery` |
| 5 | Continuous integration | Core | `continuous-integration` |
| 6 | Customer feedback | Lean | `customer-feedback` |
| 7 | Deployment automation | Core | `deployment-automation` |
| 8 | Documentation quality | Core | `documentation-quality` |
| 9 | Empowering teams to choose tools | Core | `teams-empowered-to-choose-tools` |
| 10 | Flexible infrastructure | Core | `flexible-infrastructure` |
| 11 | Generative organizational culture | Core | `generative-organizational-culture` |
| 12 | Healthy data ecosystems | AI | `healthy-data-ecosystems` |
| 13 | Job satisfaction | Core | `job-satisfaction` |
| 14 | Learning culture | Core | `learning-culture` |
| 15 | Monitoring systems (business decisions) | Supporting | `monitoring-systems` |
| 16 | Pervasive security | Core | `pervasive-security` |
| 17 | Platform engineering | AI | `platform-engineering` |
| 18 | Proactive failure notification | Supporting | `proactive-failure-notification` |
| 19 | Streamlining change approval | Core | `streamlining-change-approval` |
| 20 | Team experimentation | Lean | `team-experimentation` |
| 21 | Test data management | Core | `test-data-management` |
| 22 | Transformational leadership | Core | `transformational-leadership` |
| 23 | User-centric focus | AI | `user-centric-focus` |
| 24 | Version control | Core+AI | `version-control` |
| 25 | Visibility of work in the value stream | Lean | `work-visibility-in-value-stream` |
| 26 | Visual management | Lean | `visual-management` |
| 27 | Well-being | Core | `well-being` |
| 28 | Work in process limits | Lean | `wip-limits` |
| 29 | Working in small batches | Core+AI | `working-in-small-batches` |

## Capability Skills to Update/Remap (5)

Existing practice skills that directly map to DORA capabilities:

| DORA Capability | Existing Skill | Action |
|---|---|---|
| Trunk-based development | `trunk-based-development` | Add research citations, expand with DORA evidence |
| Loosely coupled teams | `loose-coupling` | Rename to `loosely-coupled-teams`, add research |
| Database change management | `backward-compatible-migrations` (partial) | Create new `database-change-management` capability skill; add cross-ref from existing |
| Test automation | `test-driven-development` (partial) | Create new `test-automation` capability skill; add cross-ref from existing |
| Monitoring & observability | `observability-aware-coding` + `structured-logging-and-tracing` (partial) | Create new `monitoring-and-observability` capability skill; add cross-refs from existing |

## Practice Skills to Cite-Update (12)

Skills that remain unchanged but need DORA research citations added to their Impact sections:

- `small-incremental-commits`, `small-pull-requests`, `code-review-discipline`, `type-safety-and-linting`, `contract-testing`, `dependency-management`, `api-versioning`, `rollback-friendly-design`, `feature-flags`, `configuration-as-code`, `stop-and-clarify`

## Skill Format (Capability Skills)

Each capability skill follows this structure:

1. YAML frontmatter (name, description matching repo conventions)
2. DORA Research Context (key findings, report year, model category)
3. What It Is (concise definition)
4. Problem Solved (symptoms when this capability is absent)
5. Key Practices (research-backed, numbered, actionable)
6. Common Pitfalls (what teams get wrong)
7. How to Measure (specific metrics)
8. Coaching Patterns (how to introduce/improve in an org)
9. Related Skills (cross-references to practice skills)
10. DORA Metrics Impact table

Target: ~150-300 lines per capability skill.

## Updated Router (dora-overview)

Add capability skills to the router table. Map activities to both capability and practice skills where relevant.

## What Won't Change

- Existing practice skill content (add citations only)
- Agents (dora-review, dora-health-check, dora-improve)
- Hooks and CLI integration
- CLAUDE.md structure (add rows for new capabilities)
- The dora-devops skill at ~/.claude/skills/ (separate artifact)

## Implementation

Highly parallelizable — all 34 capability article fetches are independent. Use parallel agents to fetch articles and draft skills concurrently. Update existing skills in batch.