# DORA Capabilities — Active Enforcement

This plugin enforces all 34 DORA capabilities. These are standing instructions — not suggestions. Each skill is comprehensive: research context, key practices, common pitfalls, coaching patterns, and concrete implementation code examples all in one place.

## Before Writing Code

1. **Load the relevant skill.** Check the router below and load the skill that matches your activity before touching any implementation file.
2. **Write the test first.** No implementation code exists before a failing test. This is non-negotiable — load `test-automation` and follow the RED-GREEN-REFACTOR cycle.
3. **Create a feature branch.** Never commit directly to main. Create a short-lived branch (e.g., `feat/add-shipping-calc`) before the first commit.
4. **Stop and ask if something is unclear.** If the requirements are ambiguous, the codebase contradicts what you expected, or the task is bigger than it seemed — stop implementing and ask for clarification before proceeding. A 30-second question saves hours of rework. Load `stop-and-clarify` when in doubt.

## After Each Passing Change

1. **Commit immediately.** One logical change per commit. If the message needs "and", split it. Load `working-in-small-batches` for commit discipline patterns.
2. **Push to the branch.** Keep the feedback loop tight.
3. **Run dora-review agent.** It checks your changes against DORA practices and fixes issues.
4. **Open a PR.** Do not ask the user — just open it. Use `gh pr create` with a clear title and description.
5. **Keep going.** Do not stop between modules. Create the next feature branch off the current one and continue working. PRs are merged bottom-up as they get approved.

## Stacked PR Workflow (Default for Multi-Module Tasks)

When a task involves multiple modules, features, or logical units of work, use stacked PRs — do not stop between them:

1. Create `feat/first-module` branch from main
2. TDD, implement, commit, push, dora-review, open PR
3. Create `feat/second-module` branch **off the current branch** (not main)
4. TDD, implement, commit, push, dora-review, open PR targeting the previous branch
5. Repeat until all modules are complete — never pause to wait for review

Each PR is small, focused, and independently reviewable. They merge bottom-up.

## Skill Router — Load Based on Activity

| You are about to... | Load this skill |
|---------------------|----------------|
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
| Write database migrations or schema changes | `database-change-management` |
| Improve code searchability or cross-team reuse | `code-maintainability` |
| Streamline change approval or CAB processes | `streamlining-change-approval` |
| Improve data quality or data governance | `healthy-data-ecosystems` |

## Parallel Agents

When a task involves independent pieces of work, use multiple agents to work in parallel. For example:
- Running `dora-review` on completed changes while starting TDD on the next module
- Loading and applying multiple skills simultaneously when they cover independent concerns (e.g., `monitoring-and-observability` for logging code while `loosely-coupled-teams` for API boundaries)
- Running `dora-health-check` in the background while beginning work on the first module

The key constraint: each agent must work on independent files/concerns. Do not parallelize work that has dependencies between agents.

## Agent Checkpoints

| When | Run this |
|------|----------|
| Start of a new project or major task | `dora-health-check` agent |
| After completing a set of changes | `dora-review` agent |
| When a specific DORA metric needs improvement | `dora-improve` agent with the metric name |

## Why This Matters

Teams that follow these capabilities deploy more frequently, with shorter lead times, lower failure rates, and faster recovery. Speed and stability are not tradeoffs — the research shows elite teams achieve both. Each skill provides the complete picture: DORA research evidence for why the capability matters, plus concrete implementation patterns for how to apply it.
