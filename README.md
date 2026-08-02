# dora-skills

A collection of Claude Code skills and agents covering all 34 capabilities from the [DORA capability catalog](https://dora.dev/capabilities/). Each skill is comprehensive: DORA research evidence, key practices, common pitfalls, how to measure, coaching patterns, and concrete code examples — everything you need in one place.

---

## What Are DORA Metrics?

DORA (DevOps Research and Assessment) defines four key metrics that measure software delivery performance:

| Metric | What It Measures |
|---|---|
| **Deployment Frequency** | How often code ships to production |
| **Lead Time for Changes** | Time from commit to production |
| **Change Failure Rate** | Percentage of deploys that cause failures |
| **Mean Time to Restore (MTTR)** | Time to recover from a production failure |

High-performing teams deploy frequently, ship fast, break things rarely, and recover quickly. The skills in this repo target the specific practices that move those numbers.

## What Are DORA Capabilities?

DORA identifies **34 capabilities** — specific technical, process, and cultural practices — that drive software delivery and organizational performance. These span 6 categories:

| Category | Count | Examples |
|---|---|---|
| **Core Model** | 21 | Continuous delivery, continuous integration, test automation, version control, trunk-based dev, loosely coupled teams, monitoring & observability |
| **AI Model** | 6 | AI-accessible internal data, clear AI stance, healthy data ecosystems, platform engineering, user-centric focus |
| **Lean Product Management** | 6 | Customer feedback, team experimentation, working in small batches, WIP limits, visual management |
| **Supporting** | 2 | Proactive failure notification, monitoring for business decisions |
| **Cross-cutting** | (+ Transformational leadership, well-being, job satisfaction, learning culture, generative culture) |

This repo covers all 34. Each skill is self-contained: research context for the "why," implementation patterns for the "how," and coaching guidance for introducing the capability in your organization.

---

## Skill Index

These 34 skills mirror every article in the [DORA capability catalog](https://dora.dev/capabilities/). Each provides research context, key practices, common pitfalls, how to measure, coaching patterns, and cross-references.

| # | Skill | Description |
|---|---|---|
| 1 | `ai-accessible-internal-data` | Connect AI to internal docs and codebases — from generic assistant to specialized expert |
| 2 | `clear-and-communicated-ai-stance` | AI usage policy using the three-bucket framework: prohibited, permitted, allowed |
| 3 | `code-maintainability` | Make code searchable, reusable, changeable across the organization |
| 4 | `continuous-delivery` | Keep software in a deployable state — safe, reliable, on-demand releases |
| 5 | `continuous-integration` | Automated build and test on every commit with rapid feedback |
| 6 | `customer-feedback` | Gather and act on customer input to validate features before building |
| 7 | `database-change-management` | Integrate database changes into CD — zero-downtime schema migrations |
| 8 | `deployment-automation` | Push-button deployments — same process for every environment |
| 9 | `documentation-quality` | Clear, findable, reliable docs that amplify every other practice |
| 10 | `teams-empowered-to-choose-tools` | Balance autonomy with standards — teams choose tools, accept support burden |
| 11 | `flexible-infrastructure` | Cloud infrastructure meeting all 5 NIST characteristics — self-service, elastic, measured |
| 12 | `generative-organizational-culture` | High-trust, blameless culture that optimizes information flow |
| 13 | `healthy-data-ecosystems` | High-quality, accessible, unified internal data — foundation for AI success |
| 14 | `job-satisfaction` | Meaningful work, proper tools, valued expertise — drives performance |
| 15 | `learning-culture` | Training, safe-to-fail experimentation, knowledge sharing — learning as investment |
| 16 | `loosely-coupled-teams` | Teams that test, deploy, and release independently — no cross-team orchestration |
| 17 | `monitoring-and-observability` | Metrics, logs, and traces — understand and debug production systems |
| 18 | `monitoring-systems` | Use ops data to inform business decisions, not just incident response |
| 19 | `pervasive-security` | Security integrated into design and CI — shift left, not test at end |
| 20 | `platform-engineering` | Internal developer platforms with self-service golden paths |
| 21 | `proactive-failure-notification` | Detect and act on problems before they become outages |
| 22 | `streamlining-change-approval` | Peer review + automation replaces heavyweight CABs |
| 23 | `team-experimentation` | Teams work on new ideas without permission — hackathons, exploration |
| 24 | `test-automation` | Fast, reliable automated test suites — developers own quality |
| 25 | `test-data-management` | Adequate test data on demand — no constraints on automated testing |
| 26 | `transformational-leadership` | Five-dimension leadership model that enables technical capability adoption |
| 27 | `trunk-based-development` | Merge to trunk daily — short-lived branches, no code freezes |
| 28 | `user-centric-focus` | Understand user needs, leverage feedback — 40% higher org performance |
| 29 | `version-control` | Version everything — code, configs, scripts, AI prompts, agent configs |
| 30 | `visual-management` | Card walls, dashboards, CI monitors — shared visibility of work |
| 31 | `well-being` | Reduce deployment pain, rework, and burnout — fix the environment |
| 32 | `wip-limits` | Constrain concurrent work to expose bottlenecks and improve flow |
| 33 | `work-visibility-in-value-stream` | Value stream mapping — understand flow from idea to customer |
| 34 | `working-in-small-batches` | Independently completable units — hours to days, not weeks |

---

## Installation

### Option 1: Install as a plugin locally (recommended)

```bash
git clone https://github.com/agilles-ctrl/dora-skills ~/dora-skills
claude plugin install ~/dora-skills --scope user
```

Skills are namespaced automatically (e.g., `/dora-skills:continuous-integration`).

For development/testing, run with the plugin directory:

```bash
claude --plugin-dir ~/dora-skills
```

### Option 2: Reference via CLAUDE.md

Add this line to your project's `CLAUDE.md`:

```
@~/dora-skills/skills/
```

---

## Usage

Once installed, invoke skills by name in Claude Code:

```
/dora-skills:dora-overview
/dora-skills:continuous-integration
/dora-skills:test-automation
```

Start with `dora-overview` if you're unsure where to begin — it routes you to the most relevant skill based on your activity. Each skill is comprehensive, covering both strategic context and concrete implementation patterns.

---

## Agents

In addition to skills (which provide guidance), this plugin includes **agents** — autonomous workers that analyze your codebase against DORA capability standards.

| Agent | What It Does |
|---|---|
| `dora-review` | Reviews working tree changes against DORA capability standards, fixes issues, outputs a report |
| `dora-health-check` | Audits the repo, scores each capability area, makes safe additive improvements |
| `dora-improve` | Given a DORA metric, targets capability gaps to improve that metric |

### Running Agents

```
/agents dora-review
/agents dora-health-check
/agents dora-improve mttr
```

- **dora-review** operates on your current working tree (staged + unstaged changes). It leaves its fixes unstaged so you can review them with `git diff`.
- **dora-health-check** scans the full repo and produces a scorecard across all 34 DORA capabilities.
- **dora-improve** takes one of four metrics as input: `frequency`, `lead-time`, `failure-rate`, or `mttr`.

---

## Project Purpose

This repo exists to make the full DORA capability catalog accessible and actionable through Claude Code. Each skill is comprehensive — research context, implementation patterns, code examples, and coaching guidance — so you get everything you need in one place. Agents actively review and improve your code against these standards.

The skills and agents are designed for personal use but written to be shareable. Contributions and forks welcome.

## Related

- [DORA capability catalog](https://dora.dev/capabilities/) — the source material for every capability skill
- [DORA Quick Check](https://dora.dev/quickcheck/) — benchmark your team against the 4 key metrics
- [DORA research](https://dora.dev/research/) — all DORA reports and publications
