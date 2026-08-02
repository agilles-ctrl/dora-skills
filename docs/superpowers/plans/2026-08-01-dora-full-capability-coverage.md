# DORA Full Capability Coverage — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use `subagent-driven-development` or `dispatching-parallel-agents` to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add 29 new capability skills and update all 17 existing skills to cover the full 34-capability DORA catalog from dora.dev.

**Architecture:** Two-tier skill system. Capability skills mirror dora.dev articles (deep reference + actionable). Practice skills remain as engineering how-tos with added DORA citations. Skills cross-reference each other via the Related Skills section.

**Tech Stack:** Markdown SKILL.md files with YAML frontmatter. Parallel agent dispatch for article fetching and skill drafting.

## Global Constraints

- Each new capability skill: 150-300 lines, YAML frontmatter, follows template below
- Each updated practice skill: add DORA research citations to Impact table, add cross-refs
- Existing practice skill content and agents must not be altered beyond citation additions
- Skill names use kebab-case, match dora.dev URL slugs
- Router (dora-overview) must include all new skills
- README must document all new skills
- All capability articles are at `https://dora.dev/capabilities/<capability-slug>/`

---

## File Structure

### New files (29 capability skills):
```
skills/ai-accessible-internal-data/SKILL.md
skills/clear-and-communicated-ai-stance/SKILL.md
skills/code-maintainability/SKILL.md
skills/continuous-delivery/SKILL.md
skills/continuous-integration/SKILL.md
skills/customer-feedback/SKILL.md
skills/database-change-management/SKILL.md
skills/deployment-automation/SKILL.md
skills/documentation-quality/SKILL.md
skills/teams-empowered-to-choose-tools/SKILL.md
skills/flexible-infrastructure/SKILL.md
skills/generative-organizational-culture/SKILL.md
skills/healthy-data-ecosystems/SKILL.md
skills/job-satisfaction/SKILL.md
skills/learning-culture/SKILL.md
skills/monitoring-and-observability/SKILL.md
skills/monitoring-systems/SKILL.md
skills/pervasive-security/SKILL.md
skills/platform-engineering/SKILL.md
skills/proactive-failure-notification/SKILL.md
skills/streamlining-change-approval/SKILL.md
skills/team-experimentation/SKILL.md
skills/test-automation/SKILL.md
skills/test-data-management/SKILL.md
skills/transformational-leadership/SKILL.md
skills/user-centric-focus/SKILL.md
skills/version-control/SKILL.md
skills/work-visibility-in-value-stream/SKILL.md
skills/visual-management/SKILL.md
skills/well-being/SKILL.md
skills/wip-limits/SKILL.md
skills/working-in-small-batches/SKILL.md
```

### Modified files:
```
skills/trunk-based-development/SKILL.md        — add research citations, cross-refs
skills/backward-compatible-migrations/SKILL.md — add cross-ref to database-change-management
skills/observability-aware-coding/SKILL.md     — add cross-ref to monitoring-and-observability
skills/structured-logging-and-tracing/SKILL.md — add cross-ref to monitoring-and-observability
skills/test-driven-development/SKILL.md        — add cross-ref to test-automation
skills/dora-overview/SKILL.md                  — add all new capability skills to router
skills/loose-coupling/SKILL.md                 — rename to loosely-coupled-teams, add research
README.md                                       — document all new skills
```

### Citation updates only (12 practice skills):
```
skills/small-incremental-commits/SKILL.md
skills/small-pull-requests/SKILL.md
skills/code-review-discipline/SKILL.md
skills/type-safety-and-linting/SKILL.md
skills/contract-testing/SKILL.md
skills/dependency-management/SKILL.md
skills/api-versioning/SKILL.md
skills/rollback-friendly-design/SKILL.md
skills/feature-flags/SKILL.md
skills/configuration-as-code/SKILL.md
skills/stop-and-clarify/SKILL.md
```

---

## Capability Skill Template

Every new capability skill follows this exact structure:

```markdown
---
name: <capability-slug>
description: <problem-oriented trigger — when to load>
---

# <Capability Title>

## DORA Research Context

What DORA's research found about this capability. Cite the specific report year and any key statistics. Note whether this is part of the [core model](/research/#core-model) or [AI model](/ai/#explore-the-model).

Key finding: <1-2 sentence summary with data>

## What It Is

<2-4 sentences defining the capability>

## Problem Solved

Symptoms when this capability is absent:

- <symptom 1>
- <symptom 2>
- <symptom 3>

## Key Practices

1. **<Practice name>:** <1-2 sentences of research-backed guidance>

2. **<Practice name>:** <1-2 sentences of research-backed guidance>

3. **<Practice name>:** <1-2 sentences of research-backed guidance>

4. **<Practice name>:** <1-2 sentences of research-backed guidance>

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| <pitfall> | <reason> | <better approach> |
| <pitfall> | <reason> | <better approach> |

## How to Measure

- **<metric name>:** <what to track and why>
- **<metric name>:** <what to track and why>

## Coaching Patterns

How to introduce or improve this capability in an organization:

1. **<Phase name>:** <concrete action, not abstract advice>
2. **<Phase name>:** <concrete action, not abstract advice>
3. **<Phase name>:** <concrete action, not abstract advice>

## Related Skills

- [`<skill-name>`](../<skill-name>/): <how it supports this capability>
- [`<skill-name>`](../<skill-name>/): <how it supports this capability>

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | <X / —> |
| Lead Time for Changes | <X / —> |
| Change Failure Rate | <X / —> |
| Time to Restore Service | <X / —> |
```

---

## Phase 1: Fetch All Capability Articles

### Task 1: Fetch Core Model Capabilities (batch 1)

**Files:**
- Fetch only (no writes yet)

**Approach:** Dispatch parallel agents, each fetches one article and returns structured content.

- [ ] Fetch https://dora.dev/capabilities/code-maintainability/
- [ ] Fetch https://dora.dev/capabilities/continuous-delivery/
- [ ] Fetch https://dora.dev/capabilities/continuous-integration/
- [ ] Fetch https://dora.dev/capabilities/database-change-management/
- [ ] Fetch https://dora.dev/capabilities/deployment-automation/
- [ ] Fetch https://dora.dev/capabilities/documentation-quality/
- [ ] Fetch https://dora.dev/capabilities/teams-empowered-to-choose-tools/
- [ ] Fetch https://dora.dev/capabilities/flexible-infrastructure/
- [ ] Fetch https://dora.dev/capabilities/generative-organizational-culture/

### Task 2: Fetch Core Model Capabilities (batch 2)

- [ ] Fetch https://dora.dev/capabilities/job-satisfaction/
- [ ] Fetch https://dora.dev/capabilities/learning-culture/
- [ ] Fetch https://dora.dev/capabilities/loosely-coupled-teams/
- [ ] Fetch https://dora.dev/capabilities/monitoring-and-observability/
- [ ] Fetch https://dora.dev/capabilities/pervasive-security/
- [ ] Fetch https://dora.dev/capabilities/streamlining-change-approval/
- [ ] Fetch https://dora.dev/capabilities/test-automation/
- [ ] Fetch https://dora.dev/capabilities/test-data-management/
- [ ] Fetch https://dora.dev/capabilities/trunk-based-development/

### Task 3: Fetch AI Capabilities

- [ ] Fetch https://dora.dev/capabilities/ai-accessible-internal-data/
- [ ] Fetch https://dora.dev/capabilities/clear-and-communicated-ai-stance/
- [ ] Fetch https://dora.dev/capabilities/healthy-data-ecosystems/
- [ ] Fetch https://dora.dev/capabilities/platform-engineering/
- [ ] Fetch https://dora.dev/capabilities/user-centric-focus/
- [ ] Fetch https://dora.dev/capabilities/version-control/

### Task 4: Fetch Lean Product Management + Supporting Capabilities

- [ ] Fetch https://dora.dev/capabilities/customer-feedback/
- [ ] Fetch https://dora.dev/capabilities/team-experimentation/
- [ ] Fetch https://dora.dev/capabilities/working-in-small-batches/
- [ ] Fetch https://dora.dev/capabilities/work-visibility-in-value-stream/
- [ ] Fetch https://dora.dev/capabilities/visual-management/
- [ ] Fetch https://dora.dev/capabilities/wip-limits/
- [ ] Fetch https://dora.dev/capabilities/monitoring-systems/
- [ ] Fetch https://dora.dev/capabilities/proactive-failure-notification/
- [ ] Fetch https://dora.dev/capabilities/transformational-leadership/
- [ ] Fetch https://dora.dev/capabilities/well-being/

---

## Phase 2: Create New Capability Skills

### Task 5: Create Core Technical Capability Skills (batch 1)

**For each:** Create directory under `skills/`, write SKILL.md using the template, filling in content from the fetched article.

- [ ] Create `skills/code-maintainability/SKILL.md`
- [ ] Create `skills/continuous-delivery/SKILL.md`
- [ ] Create `skills/continuous-integration/SKILL.md`
- [ ] Create `skills/database-change-management/SKILL.md`
- [ ] Create `skills/deployment-automation/SKILL.md`
- [ ] Create `skills/documentation-quality/SKILL.md`

### Task 6: Create Core Cultural + Infrastructure Capability Skills

- [ ] Create `skills/teams-empowered-to-choose-tools/SKILL.md`
- [ ] Create `skills/flexible-infrastructure/SKILL.md`
- [ ] Create `skills/generative-organizational-culture/SKILL.md`
- [ ] Create `skills/job-satisfaction/SKILL.md`
- [ ] Create `skills/learning-culture/SKILL.md`

### Task 7: Create Core Operations Capability Skills

- [ ] Create `skills/monitoring-and-observability/SKILL.md`
- [ ] Create `skills/pervasive-security/SKILL.md`
- [ ] Create `skills/streamlining-change-approval/SKILL.md`
- [ ] Create `skills/test-automation/SKILL.md`
- [ ] Create `skills/test-data-management/SKILL.md`

### Task 8: Create AI Capability Skills

- [ ] Create `skills/ai-accessible-internal-data/SKILL.md`
- [ ] Create `skills/clear-and-communicated-ai-stance/SKILL.md`
- [ ] Create `skills/healthy-data-ecosystems/SKILL.md`
- [ ] Create `skills/platform-engineering/SKILL.md`
- [ ] Create `skills/user-centric-focus/SKILL.md`
- [ ] Create `skills/version-control/SKILL.md`

### Task 9: Create Lean Product Management + Supporting Skills

- [ ] Create `skills/customer-feedback/SKILL.md`
- [ ] Create `skills/team-experimentation/SKILL.md`
- [ ] Create `skills/working-in-small-batches/SKILL.md`
- [ ] Create `skills/work-visibility-in-value-stream/SKILL.md`
- [ ] Create `skills/visual-management/SKILL.md`
- [ ] Create `skills/wip-limits/SKILL.md`
- [ ] Create `skills/monitoring-systems/SKILL.md`
- [ ] Create `skills/proactive-failure-notification/SKILL.md`
- [ ] Create `skills/transformational-leadership/SKILL.md`
- [ ] Create `skills/well-being/SKILL.md`

---

## Phase 3: Update Existing Skills

### Task 10: Rename and Expand `loose-coupling` → `loosely-coupled-teams`

**Files:**
- Create: `skills/loosely-coupled-teams/SKILL.md`
- Remove: `skills/loose-coupling/` (or rename directory)

**Approach:** Copy existing loose-coupling content, rename to match DORA capability name, add research citations from the dora.dev article, add cross-refs to related capability skills.

- [ ] Create `skills/loosely-coupled-teams/SKILL.md` with DORA research context added
- [ ] Verify loose-coupling is removed/replaced

### Task 11: Expand `trunk-based-development` with DORA Research

**Files:**
- Modify: `skills/trunk-based-development/SKILL.md`

**Approach:** Add DORA Research Context section at top, add key statistics from the dora.dev article, add Related Skills cross-refs. Keep existing actionable content intact.

- [ ] Read existing `skills/trunk-based-development/SKILL.md`
- [ ] Add DORA Research Context section after frontmatter
- [ ] Add key stats: branch lifetime <1 day, <3 active branches
- [ ] Add Related Skills section cross-referencing working-in-small-batches, continuous-integration, version-control
- [ ] Commit

### Task 12: Add Cross-References to Related Existing Skills

**Files:**
- Modify: `skills/backward-compatible-migrations/SKILL.md`
- Modify: `skills/test-driven-development/SKILL.md`
- Modify: `skills/observability-aware-coding/SKILL.md`
- Modify: `skills/structured-logging-and-tracing/SKILL.md`

**Approach:** Add Related Skills section (if absent) or append to existing. Cross-reference the new capability skills.

- [ ] Add cross-ref to `database-change-management` in backward-compatible-migrations
- [ ] Add cross-ref to `test-automation` in test-driven-development
- [ ] Add cross-refs to `monitoring-and-observability` in observability-aware-coding and structured-logging-and-tracing
- [ ] Commit

---

## Phase 4: Add Research Citations to Practice Skills

### Task 13: Add DORA Citations to 12 Practice Skills

**Files:**
- Modify: `skills/small-incremental-commits/SKILL.md`
- Modify: `skills/small-pull-requests/SKILL.md`
- Modify: `skills/code-review-discipline/SKILL.md`
- Modify: `skills/type-safety-and-linting/SKILL.md`
- Modify: `skills/contract-testing/SKILL.md`
- Modify: `skills/dependency-management/SKILL.md`
- Modify: `skills/api-versioning/SKILL.md`
- Modify: `skills/rollback-friendly-design/SKILL.md`
- Modify: `skills/feature-flags/SKILL.md`
- Modify: `skills/configuration-as-code/SKILL.md`
- Modify: `skills/stop-and-clarify/SKILL.md`

**Approach:** Find the DORA Impact table in each skill. Add a reference line below the table citing which DORA capability this practice supports and a relevant research stat if available. Do not change existing content.

For each skill, add this block after the DORA Metrics Impact table:

```markdown
## DORA Research Basis

This practice supports the [<capability-name>](../<capability-slug>/) capability. <optional: one DORA stat if applicable>
```

- [ ] Add research basis to `small-incremental-commits` → supports `working-in-small-batches`
- [ ] Add research basis to `small-pull-requests` → supports `working-in-small-batches`
- [ ] Add research basis to `code-review-discipline` → supports `streamlining-change-approval`
- [ ] Add research basis to `type-safety-and-linting` → supports `code-maintainability`
- [ ] Add research basis to `contract-testing` → supports `loosely-coupled-teams`
- [ ] Add research basis to `dependency-management` → supports `code-maintainability`
- [ ] Add research basis to `api-versioning` → supports `loosely-coupled-teams`
- [ ] Add research basis to `rollback-friendly-design` → supports `continuous-delivery`
- [ ] Add research basis to `feature-flags` → supports `continuous-delivery`, `working-in-small-batches`
- [ ] Add research basis to `configuration-as-code` → supports `deployment-automation`
- [ ] Add research basis to `stop-and-clarify` → supports `learning-culture`
- [ ] Commit

---

## Phase 5: Update Router and Documentation

### Task 14: Update dora-overview Router

**Files:**
- Modify: `skills/dora-overview/SKILL.md`

**Approach:** Add all new capability skills to the Practice-to-Metric Mapping table, the Self-Assessment section, and the Skill Router table.

- [ ] Read existing `skills/dora-overview/SKILL.md`
- [ ] Add new skills to Practice-to-Metric Mapping table (mark which metrics each impacts)
- [ ] Add new skill sections to Self-Assessment questions
- [ ] Add new capability skills to Skill Router table (map to appropriate activities)
- [ ] Add capability skills to "How Skills Compose" section
- [ ] Commit

### Task 15: Update README.md

**Files:**
- Modify: `README.md`

- [ ] Add Capability Skills section to README skill index
- [ ] List all 29 new capability skills with descriptions
- [ ] Update total skill count
- [ ] Commit

---

## Phase 6: Verify and Commit

### Task 16: Final Verification

- [ ] Verify all 34 capability skills exist (29 new + 5 updated)
- [ ] Verify all 12 practice skills have research citations
- [ ] Verify dora-overview router references all new skills
- [ ] Verify no existing skill content was removed/altered beyond citations
- [ ] Verify README lists all skills
- [ ] Commit with message: "feat: add full DORA capability coverage — 29 new skills"

---

## DORA Metrics Impact for New Capability Skills

These impact assignments should be used when filling in the DORA Metrics Impact table for each capability skill:

| Capability | Freq | Lead Time | Fail Rate | MTTR |
|---|---|---|---|---|
| ai-accessible-internal-data | — | X | X | — |
| clear-and-communicated-ai-stance | — | X | — | — |
| code-maintainability | — | X | X | — |
| continuous-delivery | X | X | X | X |
| continuous-integration | X | X | X | — |
| customer-feedback | — | — | X | — |
| database-change-management | X | X | X | X |
| deployment-automation | X | X | X | X |
| documentation-quality | — | X | X | — |
| teams-empowered-to-choose-tools | — | X | — | — |
| flexible-infrastructure | X | X | — | X |
| generative-organizational-culture | X | X | X | X |
| healthy-data-ecosystems | — | X | X | — |
| job-satisfaction | X | — | — | — |
| learning-culture | — | X | X | — |
| loosely-coupled-teams | X | X | — | X |
| monitoring-and-observability | — | — | X | X |
| monitoring-systems | — | X | X | X |
| pervasive-security | — | — | X | X |
| platform-engineering | X | X | X | X |
| proactive-failure-notification | — | — | — | X |
| streamlining-change-approval | X | X | — | — |
| team-experimentation | X | X | — | — |
| test-automation | — | X | X | — |
| test-data-management | — | X | X | — |
| transformational-leadership | X | X | X | X |
| user-centric-focus | X | — | X | — |
| version-control | X | X | X | X |
| work-visibility-in-value-stream | X | X | — | — |
| visual-management | X | X | — | — |
| well-being | X | — | — | — |
| wip-limits | X | X | — | — |
| working-in-small-batches | X | X | X | — |