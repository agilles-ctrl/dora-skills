---
name: monitoring-and-observability
description: Use when setting up production monitoring, alerting, dashboards, or incident debugging tooling — understanding and debugging systems through metrics, logs, and traces
---

# Monitoring and Observability

## DORA Research Context

DORA's 2018 Accelerate State of DevOps Report identified comprehensive monitoring and observability as a positive contributor to continuous delivery. Monitoring configuration should be treated as code, deployed through automation and versioned alongside the application. All developers should be proficient with monitoring — the practice must not be confined to a single specialist.

## What It Is

Monitoring is watching system state via predefined metrics and logs. Observability is actively debugging by exploring undefined patterns. Together they provide leading indicators of outages, detect degradations before customers notice, and help teams diagnose issues quickly. This capability spans metrics, logging, distributed tracing, alerting, and dashboarding.

## Problem Solved

- Outages are discovered by customers, not internal systems
- Debugging production issues requires the one monitoring specialist
- Alert fatigue — too many alerts, most are noise
- Can't trace requests across services to find root cause

## Key Practices

1. **Report on overall system health:** Are systems functioning? Are sufficient resources available? Surface CPU, memory, disk, and network saturation.
2. **Report on system state as experienced by customers:** Would they know it's down? Use error rates, latency percentiles, and throughput as primary signals.
3. **Monitor key business and systems metrics:** Track business KPIs (signups, checkouts, API usage) alongside technical metrics for context during incidents.
4. **Implement blackbox and whitebox monitoring:** Use synthetic probes from the outside (blackbox) and internal metrics, logs, and traces (whitebox).
5. **Instrument code to expose inner state:** Expose connection pool sizes, queue depths, cache hit rates, and custom counters/gauges.
6. **Keep monitoring configuration in version control:** Treat dashboards, alert rules, and SLO definitions as code — deploy through automation.
7. **Empower all developers to be proficient with monitoring:** Don't confine it to one person. Every team member should know how to query metrics, view logs, and trace requests.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Single monitoring person or dedicated team | Knowledge bottleneck; slow response during incidents | Build monitoring into baseline knowledge of all developers |
| Cause-based alerting | Enumerating all possible error conditions is impossible | Symptom-based alerting on user-facing symptoms (error rate, latency) |
| Poor alert delivery (email to team DL) | Diffusion of responsibility; no one owns the page | Multiple pathways; route to the right people via paging/chat |
| Alarm fatigue | Too many alerts, most are unactionable | Ensure alerts are actionable; track and prune stale alerts regularly |
| Curating the "Perfect Dashboard" | Endless tweaking with diminishing returns | Focus on team's ability to quickly create dashboards when needed |

## How to Measure

- **MTTD (Mean Time to Detect):** Time from incident start to detection
- **MTTR (Mean Time to Resolve):** Time from detection to resolution
- **False positives:** Alerts that triggered but required no action
- **False negatives:** Failures that occurred with no alert
- **Alert silencing/suppression metrics:** Are any alerts silenced indefinitely?
- **Percentage of out-of-hours alerts:** Measure toil and burnout risk

## Coaching Patterns

1. **Instrument for metrics, logs, and traces:** Adopt OpenTelemetry or similar frameworks. Start with the RED method (Rate, Errors, Duration) for every service.
2. **Write a postmortem after every outage:** Include corrective actions for improved monitoring. Track alert-toil and time spent on-call.
3. **Treat monitoring config as code:** Version dashboards, alert rules, and SLOs in the same repository as the application. Deploy through CI/CD.

## Related Skills

- [`proactive-failure-notification`](../proactive-failure-notification/): Alerting and notification patterns that pair with monitoring
- [`monitoring-systems`](../monitoring-systems/): System-level monitoring infrastructure guidance
- [`observability-aware-coding`](../observability-aware-coding/): Writing code that exposes observable state
- [`structured-logging-and-tracing`](../structured-logging-and-tracing/): Log and trace instrumentation best practices

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | — |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |

## Instrumentation Patterns

### Observability-Aware Coding

**When to use:** Designing a new service, adding an external dependency integration, reviewing hard-to-debug code, building background jobs or async workers with no user-facing output.

**When NOT to use:** Prototype/throwaway code, unit test helpers or fixtures, one-off manually-supervised migration scripts.

**Instrument boundaries — measure every call that crosses a process or network boundary:**

```
// 1. Instrument every external boundary
result = call_database(query)
record_histogram("db.query.duration_ms", elapsed, tags=["query:user_lookup"])
increment_counter("db.query.total", tags=["status:success"])

// 2. Enrich errors with context
if error:
    increment_counter("db.query.total", tags=["status:error", "error:timeout"])
    raise EnrichedError(
        message="user lookup failed",
        context={user_id: id, query: query, elapsed_ms: elapsed}
    )

// 3. Expose health and readiness
GET /health   → {status: "ok"}
GET /ready    → {status: "ok", checks: {db: "ok", cache: "ok"}}
GET /metrics  → Prometheus-format counters, gauges, histograms
```

**What to instrument:**

| Boundary | What to Measure |
|----------|----------------|
| Inbound requests | Count, duration, status code |
| Outbound calls (DB, API, queue) | Count, duration, error rate |
| Business decisions | Event count per outcome (e.g., `payment.result: success/decline`) |
| Background jobs | Start, finish, duration, items processed, errors |
| Queue consumers | Queue depth, processing lag, DLQ size |

**Metric types:**

| Type | Use For | Example |
|------|---------|---------|
| Counter | Things that happen | `requests.total`, `errors.total` |
| Gauge | Current state | `queue.depth`, `connections.active` |
| Histogram | Distributions | `request.duration_ms` (enables p50/p95/p99) |

**TypeScript example — instrument an external API call:**

```typescript
async function fetchUserProfile(userId: string): Promise<UserProfile> {
  const start = performance.now()
  const labels = { service: 'user-service', operation: 'get_profile' }

  try {
    const response = await fetch(`${USER_SERVICE_URL}/users/${userId}`)
    const elapsed = performance.now() - start

    metrics.histogram('external_call_duration_ms', elapsed, labels)
    metrics.increment('external_call_total', { ...labels, status: 'success' })

    return response.json()
  } catch (error) {
    metrics.increment('external_call_total', { ...labels, status: 'error' })
    metrics.histogram('external_call_duration_ms', performance.now() - start, labels)
    throw new Error(`User profile fetch failed for ${userId}: ${error.message}`)
  }
}
```

**Python example — instrument an external API call:**

```python
import time
from metrics import histogram, increment

def fetch_user_profile(user_id: str) -> dict:
    labels = {"service": "user-service", "operation": "get_profile"}
    start = time.monotonic()

    try:
        response = requests.get(f"{USER_SERVICE_URL}/users/{user_id}", timeout=5)
        response.raise_for_status()
        elapsed_ms = (time.monotonic() - start) * 1000

        histogram("external_call_duration_ms", elapsed_ms, labels)
        increment("external_call_total", {**labels, "status": "success"})

        return response.json()
    except Exception as err:
        elapsed_ms = (time.monotonic() - start) * 1000
        increment("external_call_total", {**labels, "status": "error"})
        histogram("external_call_duration_ms", elapsed_ms, labels)

        raise RuntimeError(f"User profile fetch failed for {user_id} after {elapsed_ms:.0f}ms: {err}")
```

**Observability quick reference:**

| Rule | Guidance |
|------|----------|
| Instrument boundaries | Measure every call that crosses a process or network boundary |
| Use histograms for latency | Averages hide tail latency; use p95/p99 |
| Enrich errors with context | Log what the code was trying to do, not just the exception class |
| Health vs. readiness | `/health` = process alive; `/ready` = safe to receive traffic |
| Tag consistently | Establish a team convention for tag names before shipping |

**Common mistakes:**

| Mistake | Problem | Fix |
|---------|---------|-----|
| Logging only on error | No baseline; can't distinguish degradation from silence | Log success and failure at every boundary |
| Using averages for latency | p99 slowdowns are invisible in the average | Use histograms; alert on p95/p99 |
| Missing context in errors | "database error" is not actionable | Include query, input IDs, elapsed time, and error code |
| No readiness endpoint | Load balancer routes to an unready service | Add `/ready` that checks all dependencies |
| Instrumenting inside loops | Counter increments per item, not per operation | Measure at the boundary of the operation, not each iteration |

### Structured Logging and Tracing

**When to use:** Implementing log output in any service, adding a service to a distributed system, designing cross-service request flows, investigating slow or error-prone incidents.

**When NOT to use:** Simple single-process scripts read by a human, locally-supervised batch jobs, replacing an existing structured logging library that works — extend it instead.

**Before — unstructured logs:**

```
[INFO] Processing order 12345
[ERROR] Payment failed!!! retry #2
[INFO] Done
```

These cannot be queried by order ID, cannot be correlated across services, and contain no timing information.

**After — structured JSON logs with correlation:**

```json
{
  "timestamp": "2026-03-21T14:02:33.412Z",
  "level": "info",
  "service": "order-service",
  "version": "1.4.2",
  "trace_id": "4bf92f3577b34da6a3ce929d0e0e4736",
  "span_id": "00f067aa0ba902b7",
  "message": "payment attempted",
  "context": {
    "order_id": "12345",
    "amount_cents": 4999,
    "payment_provider": "stripe",
    "duration_ms": 143
  }
}
```

**Trace context propagation — W3C Trace Context:**

```
// On every outbound HTTP call, inject W3C headers:
traceparent: 00-{trace_id}-{span_id}-01

// On every inbound request, extract before logging:
incoming_trace_id = request.header("traceparent").trace_id OR generate_new()
attach trace_id to all logs and outbound calls for this request
```

A single `trace_id` threads through every service. Search any log store for that ID and see every log line, in order, across all services.

**Log levels guidance:**

| Level | When to Use |
|-------|------------|
| debug | Internal state useful during development; off in production by default |
| info | Normal operations — request received, job started, significant state changes |
| warn | Unexpected but recoverable — retry succeeded, degraded mode active |
| error | Operation failed and action is required — alert on this level |

**TypeScript (pino):**

```typescript
import pino from 'pino'

const logger = pino({ level: 'info' })

function handleOrder(orderId: string, traceId: string) {
  const log = logger.child({ trace_id: traceId, order_id: orderId })

  log.info({ action: 'order_processing_started' }, 'Processing order')

  try {
    const result = chargePayment(orderId)
    log.info({ action: 'payment_charged', duration_ms: result.elapsed }, 'Payment successful')
  } catch (err) {
    log.error({ action: 'payment_failed', error: err.message }, 'Payment failed')
    throw err
  }
}
```

**Python (structlog):**

```python
import structlog

logger = structlog.get_logger()

def handle_order(order_id: str, trace_id: str) -> None:
    log = logger.bind(trace_id=trace_id, order_id=order_id)

    log.info("order_processing_started")

    try:
        result = charge_payment(order_id)
        log.info("payment_charged", duration_ms=result.elapsed)
    except Exception as err:
        log.error("payment_failed", error=str(err))
        raise
```

**What NOT to log:**

| Category | Risk | Alternative |
|----------|------|-------------|
| Passwords, API keys, tokens | Credential exposure in log stores | Log that auth was attempted, not the credential |
| PII (email, SSN, address) | Privacy / compliance violation | Log a user ID or hashed identifier |
| Full request/response bodies | Large volume, may contain secrets | Log size, content-type, and status — sample bodies only in debug |
| Credit card numbers | PCI violation | Log last 4 digits or a token reference |

**Structured logging quick reference:**

| Rule | Guidance |
|------|----------|
| Always emit JSON | Use a logging library; never build log strings by hand |
| Include trace_id on every line | Without it, cross-service correlation is impossible |
| Use W3C Trace Context | Standard header: `traceparent` — compatible with all major tracing systems |
| Log at boundaries | Request in/out, external calls, significant decisions |
| Propagate context, don't re-create | Pass the trace ID through; never generate a new one mid-request |

**Common mistakes:**

| Mistake | Problem | Fix |
|---------|---------|-----|
| String concatenation for logs | Not machine-parseable; breaks search | Use a structured logging library that emits JSON |
| No trace_id in logs | Cannot correlate across services | Inject trace context on every inbound request and pass it forward |
| Generating a new trace_id per service | Breaks the trace chain | Extract the incoming `traceparent` header; only generate if absent |
| Logging everything at INFO | Signal buried in noise | Use DEBUG for detail; INFO for events that matter |
| Logging secrets or PII | Compliance and security exposure | Scrub sensitive fields before the log call |