---
name: continuous-delivery
description: Use when designing deployment pipelines, reducing release friction, or implementing practices that keep software in a deployable state — making deployments safe, reliable, and on-demand.
---

# Continuous Delivery

## DORA Research Context

The 2016, 2018, and 2021 DORA reports consistently show that continuous delivery reduces deployment pain and burnout while improving delivery performance. The 2021 report found that loosely coupled architecture is one of the strongest predictors of CD success — elite teams are 3x more likely to practice it. This is a [core model](/research/#core-model) capability.

## What It Is

Continuous delivery is the ability to release changes of all kinds on demand — quickly, safely, and sustainably — keeping software in a deployable state throughout its lifecycle. It applies to all software contexts, not just web services.

## Problem Solved

Symptoms when this capability is absent:

- Releases are risky, infrequent events that cause anxiety
- Manual deployment processes cause errors and delays
- Software sits undeployed for weeks, accumulating integration risk
- Emergency changes require entirely different (and scary) processes

## Key Practices

1. **Build comprehensive test automation** — reliable suites created and maintained by developers; only pass releasable code.

2. **Fully automate deployments** with no manual intervention, using the same process for all environments.

3. **Practice trunk-based development** — fewer than 3 active branches, branches live less than a day.

4. **Integrate security throughout** — security reviews at design time, pre-approved libraries, automated security tests in CI.

5. **Make teams loosely coupled** — teams can test and deploy independently without cross-team orchestration.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Mistaking CD for "deploy more often with the same broken process" | Automation amplifies existing problems | Implement the technical capabilities that drive CD first |
| Adopting tools without process/architecture changes | Tools alone don't make delivery reliable | Use value stream mapping; redesign processes |
| Hitting the J-curve and giving up | Initial automation increases visible work | Invest in relentless improvement and simplification |

## How to Measure

- **The four DORA metrics:** deployment frequency, lead time, change failure rate, time to restore
- **Whether emergency changes use the same process as regular changes:** Measures process consistency
- **Deployment pain:** Fear and anxiety when pushing to production, measured via survey
- **Whether deployments happen during normal business hours:** Indicates confidence in the process

## Coaching Patterns

1. **Map the value stream** to discover bottlenecks before automating. Have the team draw the path from commit to production and annotate every wait state and handoff.

2. **Start with version control + CI + automated tests** — the gateway practices. Don't automate deployment until these foundations are solid.

3. **Gradually automate deployments** — one environment at a time, until production is push-button. Each environment you automate builds confidence for the next.

## Related Skills

- [`continuous-integration`](../continuous-integration/): Prerequisite for reliable delivery pipelines
- [`deployment-automation`](../deployment-automation/): Enables push-button, repeatable deployments
- [`trunk-based-development`](../trunk-based-development/): Keeps software in a deployable state
- [`test-automation`](../test-automation/): Provides the safety net for frequent releases
- [`pervasive-security`](../pervasive-security/): Integrates security into the delivery pipeline

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |

## Deployment Safety Patterns

### Rollback-Friendly Design

**When to use:** Planning a database schema change alongside a code change, releasing to production without a maintenance window, adding a new field/endpoint/behavior that callers might not immediately support, evaluating whether a proposed change is a "one-way door."

**When NOT to use:** Prototype code not going to production, batch migration jobs with system offline, internal tools with a single caller updated atomically.

**Before — deploy that cannot be rolled back:**

```
Version 2 of the API changes the response format:
  GET /orders → { "items": [...] }         (v1)
  GET /orders → { "order_items": [...] }   (v2)

Deploy v2 code. Mobile clients still expect "items" field.
  → rollback to v1 code
  → but v1 config was overwritten by v2 deploy
  → rollback fails, both versions are broken
```

**After — deploy where old and new code coexist:**

```
Phase 1 (expand):
  Deploy code that returns BOTH fields:
    { "items": [...], "order_items": [...] }
  Old and new clients both work.

Phase 2 (migrate):
  Update clients to read "order_items"
  Monitor: are any clients still reading "items"?

Phase 3 (contract):
  Remove "items" field once no client reads it

Rollback is safe at any point in Phase 1 or 2 —
old code only added a field, never removed one.
```

**Expand-Contract Pattern:**

```
// Any schema or interface change follows three phases:

EXPAND   → add the new thing alongside the old thing
MIGRATE  → move traffic/data to the new thing gradually
CONTRACT → remove the old thing once nothing depends on it
```

This pattern applies to: columns, tables, API endpoints, queue topics, config keys.

**Rollback strategies:**

| Strategy | How It Works | Rollback Speed |
|----------|-------------|----------------|
| Blue-green | Two identical environments; traffic switches between them | Instant (DNS/load balancer) |
| Canary | New version receives a small percentage of traffic | Instant for affected % |
| Feature flag | Logic change hidden behind a flag | Instant (toggle flag) |
| Versioned endpoints | Old endpoint kept alive during transition | Gradual (deprecate later) |

**Identifying one-way doors:**

A change is a one-way door if rolling back the code would break the running system. Ask:

```
If I deploy this and immediately roll back the code:
  - Does the old code still read the data correctly?
  - Does the old code still call the APIs correctly?
  - Can both old and new instances run simultaneously?

If any answer is NO → apply expand-contract before deploying.
```

**Rollback quick reference:**

| Rule | Guidance |
|------|----------|
| Never rename or drop in the same deploy as code | Schema change and code change must be independently rollback-safe |
| Test rollback before going to production | Run the rollback in staging; confirm data integrity |
| Use feature flags for behavioral changes | Separate the code deploy from the feature activation |
| Keep deploys small | A one-line change is trivially rollback-safe; a 2,000-line change is not |
| Version APIs | Old callers must continue working when the server is rolled back |

**Rollback common mistakes:**

| Mistake | Problem | Fix |
|---------|---------|-----|
| Rename column in same deploy as code change | Old code cannot read renamed column after rollback | Use expand-contract: add new column, migrate, drop old |
| New code writes format that old code cannot read | Rollback corrupts data or causes crashes | Ensure old code can safely ignore or parse new fields |
| No rollback plan documented | Incident pressure leads to improvised rollback that causes more damage | Write rollback steps before the deploy, not during the incident |
| Blue-green with shared database | Schema change makes old environment invalid | Make schema changes backward-compatible before switching traffic |
| Feature flag not tested in OFF state | Rollback (flag OFF) hits untested code paths | CI must test both flag states |

### Feature Flags

**When to use:** A feature is not yet ready for all users but code needs to reach production; a risky change needs an instant off-switch; rolling out to a subset of users before full release; A/B testing; guarding incomplete work merged to main in trunk-based development.

**When NOT to use:** Security fixes — ship them immediately; simple low-risk changes; as a substitute for proper environment promotion.

**Before — incomplete feature blocks deployment:**

```
feature branch lives for 3 weeks
  → painful merge to main
  → either delay release or ship broken UX
  → no safe rollback path
```

**After — feature behind a flag, shipped safely:**

```typescript
const isEnabled = (flags, flag, userId) => {
  const f = flags[flag]
  if (!f) return false
  if (f.allowlist && userId) return f.allowlist.includes(userId)
  return f.enabled
}

if (isEnabled(featureFlags, "new_checkout", user.id)) {
  return renderNewCheckout(cart)
}
return renderLegacyCheckout(cart)
```

Deploy to production with the flag OFF. Enable for internal users, validate, then roll out progressively. If something goes wrong, flip the flag — no redeploy required.

**Flag lifecycle:**

```
1. CREATE  — add flag, default OFF, merge to main
2. ENABLE  — turn ON for a test cohort (internal, beta, 5% of traffic)
3. VALIDATE — monitor metrics, error rates, user signals
4. RELEASE — enable for 100% of users
5. REMOVE  — delete the flag and dead code path (do not skip this step)
```

**Flag types:**

| Type | Purpose | Example |
|------|---------|---------|
| Release | Hide incomplete work | `new_checkout_flow` |
| Experiment | A/B test a hypothesis | `checkout_single_page` |
| Ops | Kill switch for system behavior | `enable_rate_limiting` |
| Permission | Gate by user role or plan | `advanced_analytics` |

**TypeScript — feature flag check:**

```typescript
interface FeatureFlags {
  [key: string]: { enabled: boolean; allowlist?: string[] }
}

function isEnabled(flags: FeatureFlags, flag: string, userId?: string): boolean {
  const f = flags[flag]
  if (!f) return false
  if (f.allowlist && userId) return f.allowlist.includes(userId)
  return f.enabled
}

// Usage
if (isEnabled(flags, 'new_checkout_flow', user.id)) {
  return renderNewCheckout(order)
}
return renderLegacyCheckout(order)
```

**Python — feature flag check:**

```python
from dataclasses import dataclass

@dataclass
class FeatureFlag:
    enabled: bool = False
    allowlist: list[str] | None = None

def is_enabled(flags: dict[str, FeatureFlag], flag: str, user_id: str | None = None) -> bool:
    f = flags.get(flag)
    if not f:
        return False
    if f.allowlist and user_id:
        return user_id in f.allowlist
    return f.enabled

# Usage
if is_enabled(flags, "new_checkout_flow", user.id):
    return render_new_checkout(order)
return render_legacy_checkout(order)
```

**Feature flag quick reference:**

| Rule | Guidance |
|------|----------|
| Default state | New flags default OFF in production |
| Flag lifetime | Set a removal date when you create the flag |
| Cleanup | Remove flags within 1–2 sprints of full rollout |
| Nesting | Avoid flags inside flags; maximum 1 level deep |
| Testing | Test both flag ON and flag OFF paths in CI |

**Feature flag common mistakes:**

| Mistake | Problem | Fix |
|---------|---------|-----|
| Never removing flags | Code accumulates dead branches; logic becomes unreadable | Add a cleanup task when the flag is created |
| Nesting flags 2–3 levels deep | Combinatorial explosion of states to test | Flatten: one flag per concern |
| Using flags as environment config | Flags are for features, not for DB URLs or secrets | Use `configuration-as-code` for environment config |
| No flag inventory | Unknown flags linger for years | Maintain a registry with owner and target removal date |
| Testing only the ON path | OFF path breaks silently | CI must validate both paths |