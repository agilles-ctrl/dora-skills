---
name: deployment-automation
description: Use when building CI/CD pipelines, automating release processes, or reducing manual steps between commit and production — making deployments push-button and repeatable.
---

# Deployment Automation

## Configuration as Code Patterns

- Version ALL configuration files alongside application code
- Separate configuration from packages — same artifact for all environments, config injected at deploy time
- Environment-specific values via env vars or config files, never hardcoded
- Secrets referenced by name, never stored as values in config files

Before:
```javascript
const API_URL = "http://localhost:3000/api";
const DB_HOST = "localhost";
```

After:
```javascript
const API_URL = process.env.API_URL ?? "http://localhost:3000/api";
const DB_HOST = process.env.DB_HOST ?? "localhost";
```

## DORA Research Context

DORA research shows automation is essential for reducing deployment risk and enabling fast feedback through comprehensive testing. Deployments should be fully automated without manual intervention, and the same process should work for every environment including production. This is a [core model](/research/#core-model) capability.

## What It Is

Deployment automation enables deploying software to testing and production environments with the push of a button, reducing the risk of production deployments and providing fast feedback on software quality. It eliminates manual toil and variability from the release path.

## Problem Solved

Symptoms when this capability is absent:

- Manual deployment steps cause errors and variability
- Deployments take hours and require multiple people
- Production deploys use a different (more risky) process than staging
- Rollbacks are complex and unpredictable

## Key Practices

1. **Use the same deployment process for every environment**, including production.

2. **Use the same packages for every environment** — keep environment-specific configuration separate.

3. **Store deployment scripts and configuration in version control** — everything needed to recreate any environment.

4. **Make deployment steps idempotent** — repeatable without side effects.

5. **Design services to be independently deployable** — no orchestration required between services.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Automating a complex, fragile manual process | Produces a complex, fragile automated process | Re-architect for deployability first |
| Deployment requiring orchestration | Multiple services must be deployed in order | Design services for independent deployability |
| Components not designed for automation | Require GUI interaction to configure | Use APIs; replace tools that lack APIs |

## How to Measure

- **Count the number of manual steps in the deployment process** — reduce systematically toward zero
- **Measure time spent on delays in the deployment pipeline:** Identifies bottlenecks to automate next
- **Level of automation in the deployment pipeline** — increase continually until fully automated

## Coaching Patterns

1. **Document the current deployment process** — every manual step and handoff. Map it visually and count the human touchpoints.

2. **Automate the most painful step first** — usually environment provisioning. Pick the step that takes the most time or causes the most errors and eliminate it.

3. **Make deployments self-service** — anyone with credentials should be able to deploy any version on demand. Production deploys stop being special events and become routine operations.

## Related Skills

- [`continuous-delivery`](../continuous-delivery/): Deployment automation is the engine of CD
- [`configuration-as-code`](../configuration-as-code/): Separates environment config from build artifacts
- [`version-control`](../version-control/): Stores deployment scripts and configuration alongside code

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |