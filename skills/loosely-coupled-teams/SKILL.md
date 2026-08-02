---
name: loosely-coupled-teams
description: Use when designing service boundaries, team structures, or cross-team integration patterns — enabling teams to test, deploy, and release independently without cross-team coordination
---

# Loosely Coupled Teams

## DORA Research Context

DORA research (2017, 2021, 2022, 2023 reports) shows loosely coupled architecture is one of the strongest predictors of continuous delivery success — elite teams are 3x more likely to have it. When system architecture enables teams to test, deploy, and change without dependencies on other teams, software delivery performance dramatically improves. Conway's Law: system design mirrors communication structures; the Inverse Conway Maneuver can be used to design teams that promote desired architectures.

## What It Is

Loosely coupled teams can make large-scale design changes without external permission, complete work without fine-grained cross-team coordination, deploy and release independently on demand, and test on demand without integrated environments. Both architecture AND teams must be loosely coupled.

## Problem Solved

- Teams blocked waiting on other teams for deployments, testing, or design changes
- "Big bang" multi-service releases requiring complex orchestration
- Scarce integration environments become bottlenecks
- Changes in one service cascade into failures in others

## Key Practices

1. **Build cross-functional teams** with representation from product, dev, test, and operations — they can work independently.
2. **Design services with well-defined contracts** — use mocking/stubbing for external dependencies and contract testing for API boundaries.
3. **Implement blue/green or rolling deployments** with high automation for anytime deploys with negligible downtime.
4. **Create backward-compatible versioned APIs** — major versions for breaking changes, minor for additions; max 2 concurrent versions.
5. **Use bounded contexts and APIs** to decouple large domains into smaller, loosely coupled units.
6. **Apply the strangler fig pattern** — iteratively replace monolithic architecture with componentized services.

## Common Pitfalls

| "Big bang" multi-service releases | Requires complex orchestration with many failure points | Enable independent deployability and testability |
| Scarce integrated test environments | Hundreds of developers competing for environments | Test services in isolation with test doubles |
| Single bottleneck team | One team that many others depend on | Eliminate single points of failure in architecture and team structure |
| Choosing trendy tech without architectural outcomes | Microservices that are still tightly coupled | Focus on outcomes — testability, deployability, independence |

## How to Measure

- **Team autonomy:** % of design changes requiring external approval; % of deployments coordinated with other services
- **Communication overhead:** hours/week coordinating with other teams; number of handoffs per feature
- **Architectural support:** can you deploy during business hours with negligible downtime? can you test in isolation?
- **Impact of external changes:** how often do upstream failures cause outages?

## Coaching Patterns

1. **Start with the strangler fig** — don't re-architect everything; extract one service at a time.
2. **Define bounded contexts** — map business domains to team boundaries; one team per context.
3. **Implement contract testing** — teams verify their APIs work without integrated environments.

## Failure Isolation Patterns

| Pattern | What It Does | When to Use |
|---------|-------------|-------------|
| Circuit breaker | Stops calling a failing dependency; fails fast and recovers | Any synchronous call to an external service |
| Bulkhead | Separate thread/connection pools per dependency | Prevent one slow dependency from exhausting shared resources |
| Timeout | Bound how long a call can block | Every outbound network call, no exceptions |
| Graceful degradation | Return a reduced but valid response when a dependency is down | Features with non-critical dependencies |
| Async messaging | Decouple sender from receiver via a queue | Work that does not need an immediate response |

### Failure Isolation — Before/After

**Before — tightly coupled, failures cascade:**

```
User Request
  → Order Service
      → Payment Service (times out)
          → entire Order Service thread pool exhausted
              → all order requests fail, including ones that don't need payment
```

**After — isolated with clear boundaries:**

```
User Request
  → Order Service
      → calls Payment Service with timeout + circuit breaker
          if payment unavailable:
              return degraded response ("payment temporarily unavailable")
              queue payment for async retry
          order service continues accepting other requests normally
```

### Interface Design

```
// Good: service exposes a versioned, minimal interface
interface PaymentPort:
    charge(order_id, amount_cents, currency) -> Result<ChargeId, PaymentError>

// Bad: service exposes its internal model
interface PaymentService:
    processOrderWithLineItemsAndTaxAndShipping(order: OrderDomainObject) -> void
```

Keep interfaces narrow. Depend on behaviors, not on internal data structures.

### Dependency Direction

```
// Good: depend on abstractions, not concrete services
OrderService depends on PaymentPort (interface)
PaymentAdapter implements PaymentPort → calls Stripe API

// Bad: depend on the implementation directly
OrderService imports StripeClient and calls it inline
```

Dependencies should point inward (toward core domain logic), never outward toward infrastructure details.

### Circuit Breaker — TypeScript

```typescript
class CircuitBreaker {
  private failures = 0
  private lastFailure = 0
  private state: 'closed' | 'open' | 'half-open' = 'closed'

  constructor(
    private threshold: number = 5,
    private resetTimeout: number = 30_000
  ) {}

  async call<T>(fn: () => Promise<T>): Promise<T> {
    if (this.state === 'open') {
      if (Date.now() - this.lastFailure > this.resetTimeout) {
        this.state = 'half-open'
      } else {
        throw new Error('Circuit breaker is open')
      }
    }

    try {
      const result = await fn()
      this.failures = 0
      this.state = 'closed'
      return result
    } catch (err) {
      this.failures++
      this.lastFailure = Date.now()
      if (this.failures >= this.threshold) this.state = 'open'
      throw err
    }
  }
}

const paymentBreaker = new CircuitBreaker(5, 30_000)
const result = await paymentBreaker.call(() => chargePayment(order))
```

### Circuit Breaker — Python

```python
import time

class CircuitBreaker:
    def __init__(self, threshold: int = 5, reset_timeout: float = 30.0):
        self.threshold = threshold
        self.reset_timeout = reset_timeout
        self.failures = 0
        self.last_failure = 0.0
        self.state = "closed"

    def call(self, fn, *args, **kwargs):
        if self.state == "open":
            if time.monotonic() - self.last_failure > self.reset_timeout:
                self.state = "half-open"
            else:
                raise RuntimeError("Circuit breaker is open")

        try:
            result = fn(*args, **kwargs)
            self.failures = 0
            self.state = "closed"
            return result
        except Exception:
            self.failures += 1
            self.last_failure = time.monotonic()
            if self.failures >= self.threshold:
                self.state = "open"
            raise

payment_breaker = CircuitBreaker(threshold=5, reset_timeout=30.0)
result = payment_breaker.call(charge_payment, order)
```

### Quick Reference — Loose Coupling

| Rule | Guidance |
|------|----------|
| Set timeouts everywhere | Every outbound call must have a timeout; no exceptions |
| Use circuit breakers | Prevent retry storms from amplifying a dependency failure |
| Define explicit interfaces | Publish what you provide; hide how you do it |
| Avoid shared databases | Two services sharing a DB are coupled at the schema level |
| Prefer async for non-critical work | Queues absorb spikes and decouple availability |

### Common Mistakes — Loose Coupling

| Mistake | Problem | Fix |
|---------|---------|-----|
| No timeouts on outbound calls | One slow dependency blocks all threads | Add timeouts to every HTTP, DB, and RPC call |
| Shared database between services | Schema change in one service breaks the other | Each service owns its own data store |
| Distributed monolith | Services are split but deploy together and fail together | Enforce independent deployability; break shared libraries |
| Calling services in critical path that are non-critical | Recommendation engine failure breaks checkout | Move non-critical calls off the critical path or degrade gracefully |
| No graceful degradation | All-or-nothing responses; partial failures become total failures | Define what a reduced response looks like for each dependency |

## API Versioning Patterns

### Versioning Strategies

| Strategy | Example | Tradeoffs |
|----------|---------|-----------|
| URL path | `/v1/users`, `/v2/users` | Explicit and cacheable; URLs change with each version |
| Query parameter | `/users?version=2` | Easy to add without routing changes; harder to cache correctly |
| Header | `API-Version: 2` | Clean URLs; harder to test in a browser; requires documentation |
| Content negotiation | `Accept: application/vnd.api+json;version=2` | Standards-based; highest implementation complexity |

URL path versioning is the most discoverable and is the safest default for public APIs.

### Backward Compatibility Rules

```
Safe (non-breaking):    Adding an optional response field
Safe (non-breaking):    Adding a new endpoint
Safe (non-breaking):    Adding an optional request parameter with a sensible default
Safe (non-breaking):    Relaxing a validation rule

Breaking:               Removing or renaming a field
Breaking:               Changing a field's type
Breaking:               Making an optional field required
Breaking:               Changing the semantics of an existing field
Breaking:               Removing an endpoint
```

### Deprecation Lifecycle

```
1. Ship the new version alongside the old
2. Set a sunset date (minimum: one full consumer release cycle, typically 3–6 months)
3. Add Deprecation and Sunset headers to every response on the old version
4. Monitor traffic to the old version; reach out to consumers still using it before the sunset date
5. Remove the old version on or after the sunset date
```

**Before — breaking change without versioning:**

```
API v1 response:
  { "user_id": 123, "full_name": "Ada Lovelace" }

Provider migrates to a new schema and deploys:
  { "id": 123, "firstName": "Ada", "lastName": "Lovelace" }

Consumer A reads `user_id` and `full_name` → both are now undefined
→ Consumer A crashes in production immediately after the provider deploys
→ Incident: provider and consumer must roll back and coordinate
```

**After — additive change with deprecation path:**

```
Step 1: Deploy v2 alongside v1 (both served simultaneously)
  GET /v1/users/123 → { "user_id": 123, "full_name": "Ada Lovelace" }
  GET /v2/users/123 → { "id": 123, "firstName": "Ada", "lastName": "Lovelace" }

Step 2: Announce deprecation with a sunset date
  Response header on v1: Deprecation: true
  Response header on v1: Sunset: 2026-06-01
  Response header on v1: Link: </v2/users>; rel="successor-version"

Step 3: Consumers migrate to v2 on their own schedule before the sunset date
Step 4: Remove v1 after the sunset date; all consumers are already on v2
```

### API Versioning Quick Reference

| Rule | Guidance |
|------|----------|
| Default strategy | URL path versioning (`/v1/`, `/v2/`) for public APIs |
| Non-breaking | Additive changes only; no new version needed |
| Breaking changes | Always ship a new version; never modify the existing version in place |
| Sunset headers | Include `Deprecation` and `Sunset` headers on every deprecated response |
| Minimum sunset window | One full consumer release cycle (typically 3–6 months) |

### API Versioning Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Renaming a field "in place" on the same version | All consumers break on deploy | Introduce the new field alongside the old; deprecate the old; remove in next major version |
| Setting a sunset date too short | Consumers cannot migrate in time | Give at least one full release cycle; coordinate with consumer teams |
| Running too many live versions simultaneously | Maintenance burden grows; bugs must be fixed in N versions | Limit to two live versions at a time (current + previous) |
| Not monitoring traffic to deprecated versions | Sunset arrives with consumers still using the old version | Track request counts per version; alert when deprecated version still has active callers |
| Versioning every minor change | Version proliferation; consumers cannot track the latest stable target | Only create a new version for breaking changes; additive changes land on current version |

## Contract Testing Patterns

### Consumer-Driven Contracts

```
Consumer A defines its contract (what it actually reads from the response):
  {
    "user_id": integer,      ← Consumer expects this field name
    "email": string
  }

Contract is published to a shared broker.

Provider runs contract verification before merge:
  Loads Consumer A's contract
  Runs its own code against the contract expectations
  → FAIL: provider now returns `userId`, contract expects `user_id`
  → PR blocked before deployment
```

### Contract Test vs Integration Test

| | Contract Test | Integration Test |
|---|---|---|
| Environment | No running services needed | Full stack required |
| Speed | Seconds | Minutes to hours |
| Failure signal | "Consumer A expects X, provider returns Y" | "Something failed in staging" |
| Scope | One consumer's expectations | Emergent behavior across all services |

### Provider Verification Flow

```
1. Consumer writes expectations (the contract) and publishes to broker
2. On every provider PR:
   a. Pull all consumer contracts from broker
   b. Run provider code against each contract
   c. Fail merge if any contract is violated
3. On consumer change:
   a. Update the contract
   b. Re-verify against the current provider before deploying the consumer
```

### Schema Evolution Rules

```
Safe (non-breaking):      Adding an optional field
Safe (non-breaking):      Adding a new endpoint
Safe (non-breaking):      Widening a type (integer → number)

Breaking:                 Removing or renaming a field
Breaking:                 Narrowing a type (number → integer)
Breaking:                 Changing field semantics without a name change

For breaking changes: version the API or negotiate a migration window with consumers
```

### Contract Testing Quick Reference

| Rule | Guidance |
|------|----------|
| Contract ownership | Consumer owns and publishes the contract; provider verifies it |
| Verification gate | Provider contract verification must pass before any provider merge |
| Broker | Use a shared contract broker so provider can discover all consumers automatically |
| Schema changes | Safe = additive; breaking = requires versioning or migration window |
| Test scope | Contract tests complement integration tests; they do not replace them |

### Contract Testing Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Provider writes the contract | Contract reflects what the provider does, not what consumers need | Consumer teams write and own their contracts |
| Contracts not updated when consumer changes | Stale contracts give false confidence | Update and republish the contract as part of every consumer PR that changes API usage |
| Verifying contracts only in staging | Breaking changes discovered too late | Run provider verification in CI on every PR, against the contract broker |
| Treating contract tests as a replacement for integration tests | Contract tests verify the interface; they do not test emergent behavior | Run both; contracts for fast feedback, integration tests for end-to-end confidence |
| Skipping contract tests for "internal" APIs | Internal APIs break consumers just as often | Apply the same discipline to internal service boundaries |

## Related Skills

- [`rollback-friendly-design`](../rollback-friendly-design/): Each service can be rolled back independently
- [`continuous-delivery`](../continuous-delivery/): CD requires teams that can deploy independently
- [`feature-flags`](../feature-flags/): Decouples deployment from release across services
- [`observability-aware-coding`](../observability-aware-coding/): Instrument every service boundary to detect failures in isolation
- [`structured-logging-and-tracing`](../structured-logging-and-tracing/): Trace requests across loosely-coupled services

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |