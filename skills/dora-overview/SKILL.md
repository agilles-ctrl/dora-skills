---
name: dora-overview
description: Load at the START of any coding session, project planning, architecture decision, code review, or deployment planning — this is the master skill that routes to all DORA practices and agents; when in doubt, load this first
---

# DORA Practices — Active Enforcement

**This is not reference material. These are standing instructions.**

When this skill is loaded, you MUST actively apply DORA practices throughout the session. Do not wait to be asked. Do not treat these as suggestions. Load the specific practice skills listed below based on what you are doing, and run the agents at the checkpoints described.

## Standing Rules

1. **Write tests first.** Load `test-automation` before writing any implementation code.
2. **Commit after every passing change.** Do not batch multiple modules into one commit.
3. **Push immediately after committing.** Keep the feedback loop tight.
4. **Load relevant skills before starting work.** See the router table below.
5. **Run `dora-review` agent after completing any set of changes.** Do not skip this.
6. **Run `dora-health-check` agent at the start of a new project or major task.**
7. **Never optimize for speed over process.**

## The 4 DORA Metrics

DORA (DevOps Research and Assessment) research identified four key metrics that distinguish high-performing engineering teams. These metrics measure both throughput (how fast you deliver) and stability (how reliably you deliver).

### Deployment Frequency
How often does your team deploy to production?

| Level | Benchmark |
|-------|-----------|
| Elite | On-demand / multiple times per day |
| High | Weekly |
| Medium | Monthly |
| Low | Less than monthly |

### Lead Time for Changes
How long from code commit to running in production?

| Level | Benchmark |
|-------|-----------|
| Elite | Less than 1 hour |
| High | Less than 1 day |
| Medium | Less than 1 week |
| Low | More than 1 month |

### Change Failure Rate
What percentage of deployments cause a degraded service or require remediation?

| Level | Benchmark |
|-------|-----------|
| Elite | Less than 5% |
| High | Less than 10% |
| Medium | Less than 15% |
| Low | Greater than 15% |

### Mean Time to Restore (MTTR)
How long to recover when a deployment causes an incident?

| Level | Benchmark |
|-------|-----------|
| Elite | Less than 1 hour |
| High | Less than 1 day |
| Medium | Less than 1 week |
| Low | More than 1 week |

## Skill-to-Metric Mapping

Each engineering practice improves specific metrics. Use this table to target your investment:

| Skill | Frequency | Lead Time | Failure Rate | MTTR |
|----------|:---------:|:---------:|:------------:|:----:|
| ai-accessible-internal-data | X | X | X | |
| clear-and-communicated-ai-stance | X | X | | |
| code-maintainability | X | X | X | X |
| continuous-delivery | X | X | X | X |
| continuous-integration | X | X | X | |
| customer-feedback | X | X | X | |
| database-change-management | X | X | X | X |
| deployment-automation | X | X | X | X |
| documentation-quality | X | X | X | X |
| teams-empowered-to-choose-tools | X | X | | |
| flexible-infrastructure | X | X | X | X |
| generative-organizational-culture | X | X | X | X |
| healthy-data-ecosystems | | X | X | |
| job-satisfaction | X | X | X | X |
| learning-culture | X | X | X | X |
| loosely-coupled-teams | X | X | X | X |
| monitoring-and-observability | | X | X | X |
| monitoring-systems | | | X | X |
| pervasive-security | | X | X | X |
| platform-engineering | X | X | X | X |
| proactive-failure-notification | | | X | X |
| streamlining-change-approval | X | X | X | |
| team-experimentation | X | X | X | |
| test-automation | X | X | X | |
| test-data-management | X | X | X | |
| transformational-leadership | X | X | X | X |
| trunk-based-development | X | X | X | |
| user-centric-focus | X | | X | |
| version-control | X | X | X | X |
| visual-management | X | X | | |
| well-being | X | X | X | X |
| wip-limits | X | X | | |
| work-visibility-in-value-stream | X | X | | |
| working-in-small-batches | X | X | X | X |

## Self-Assessment: Which Metric Should You Focus On?

Answer these questions to identify where to invest first:

- **"Are deployments painful or infrequent?"** — Focus on **Deployment Frequency** skills: `deployment-automation`, `continuous-delivery`, `continuous-integration`, `trunk-based-development`, `streamlining-change-approval`

- **"Does it take too long for code to reach production?"** — Focus on **Lead Time** skills: `continuous-integration`, `test-automation`, `trunk-based-development`, `working-in-small-batches`, `code-maintainability`

- **"Do deployments often cause incidents?"** — Focus on **Change Failure Rate** skills: `test-automation`, `test-data-management`, `code-maintainability`, `database-change-management`, `monitoring-and-observability`, `pervasive-security`

- **"Does it take too long to recover from incidents?"** — Focus on **MTTR** skills: `monitoring-and-observability`, `proactive-failure-notification`, `deployment-automation`, `database-change-management`, `flexible-infrastructure`

## Skill Router — Load These Automatically

Do not wait for the user to ask. When you detect any of these activities, load the corresponding skills immediately:

| Activity | Load this skill |
|----------|-----------------|
| Write any code | `test-automation` |
| Commit changes | `working-in-small-batches` |
| Create/merge branches | `trunk-based-development` |
| Open or review a PR | `streamlining-change-approval` |
| Design module/service boundaries | `loosely-coupled-teams` |
| Add or change API endpoints | `loosely-coupled-teams` |
| Write database migrations | `database-change-management` |
| Add logging or error handling | `monitoring-and-observability` |
| Manage config or env values | `deployment-automation` |
| Plan a deployment or release | `continuous-delivery` |
| Add or update dependencies | `code-maintainability` |
| Set up linting or type checking | `code-maintainability` |
| Encounter ambiguity, spec gaps, or unexpected state | `learning-culture` |
| Set up or improve CI/CD pipelines | `continuous-integration`, `continuous-delivery`, `deployment-automation` |
| Build, maintain, or improve test suites | `test-automation`, `test-data-management` |
| Set up production monitoring, alerting, or dashboards | `monitoring-and-observability`, `proactive-failure-notification` |
| Integrate security into the software lifecycle | `pervasive-security` |
| Manage infrastructure, cloud, or provisioning | `flexible-infrastructure`, `platform-engineering` |
| Address team culture, burnout, or morale | `generative-organizational-culture`, `well-being`, `job-satisfaction` |
| Lead organizational change or transformation | `transformational-leadership`, `learning-culture` |
| Adopt, govern, or set policy for AI tools | `clear-and-communicated-ai-stance`, `ai-accessible-internal-data` |
| Gather or act on user feedback | `customer-feedback`, `user-centric-focus`, `team-experimentation` |
| Improve internal documentation or knowledge sharing | `documentation-quality` |
| Manage workflow, team capacity, or Kanban | `wip-limits`, `visual-management`, `work-visibility-in-value-stream` |
| Decompose features or plan iterations | `working-in-small-batches` |
| Set up version control or repo practices | `version-control` |
| Design service/team boundaries or microservices | `loosely-coupled-teams` |
| Improve code searchability or cross-team reuse | `code-maintainability` |
| Streamline change approval or CAB processes | `streamlining-change-approval` |
| Improve data quality or data governance | `healthy-data-ecosystems` |

## Agent Checkpoints — Run These Automatically

| Checkpoint | Run this agent |
|------------|----------------|
| After completing a set of changes | `dora-review` |
| Start of a new project or major task | `dora-health-check` |
| When a specific DORA metric needs improvement | `dora-improve` with the metric name |

## How Skills Compose

Every skill is comprehensive — it contains DORA research context, key practices, common pitfalls, how to measure, coaching patterns, and concrete implementation patterns with code examples. Load the skill that matches your activity. Skills are complementary, not conflicting — they address different aspects of the delivery pipeline. When multiple apply, load them all.
