---
name: streamlining-change-approval
description: Use when designing change management processes, replacing CABs with automation, or implementing peer review workflows — making approvals fast without sacrificing safety
---

# Streamlining Change Approval

## Code Review Discipline

### What to Review
- **Correctness:** Does the code do what it says? Are edge cases handled?
- **Security:** Input validation, auth checks, data exposure
- **Maintainability:** Is it clear? Would someone new understand it?
- **Test coverage:** Do tests cover the change? Are they meaningful?

### Review Patterns
- Review within 4 hours of request — small PRs enable fast review
- Start with tests to understand expected behavior
- Ask questions, don't dictate — "What happens if X is null?" not "Add a null check"
- Approve or request changes; never "looks good but..." — be decisive
- If changes are needed, re-review only the diff, not the whole PR

## DORA Research Context

DORA's 2019 State of DevOps Report found that peer review during development combined with automation is the most effective change approval approach. Formal external review processes such as Change Advisory Boards have a negative impact on delivery performance with no evidence of reducing change failure rates.

## What It Is

Change approvals are best implemented through peer review during development, supplemented by automation to detect, prevent, and correct bad changes early. This replaces heavyweight external CAB meetings with continuous, lightweight validation built into the development workflow.

## Problem Solved

- Change Advisory Board (CAB) meetings slow everything down
- Every change requires the same heavy process regardless of risk
- Emergency changes use a different (and scarier) process
- Adding more process when stability problems occur creates a vicious cycle

## Key Practices

1. **Use peer review to meet segregation of duties:** Reviews should be captured in the development platform (pull requests, merge requests) with clear audit trails.
2. **Employ CI, continuous testing, and comprehensive monitoring:** Rapidly detect and correct bad changes through automation rather than manual gates.
3. **Shift the CAB to a strategic role:** Focus on facilitating coordination between teams and helping with process improvement, not approving individual changes.
4. **Make the regular change process fast enough for emergencies:** If every deployment is routine and well-tested, there's no need for a separate "fast track."
5. **Implement security controls at the platform layer:** Embed controls in the toolchain rather than relying on manual review.
6. **Analyze to detect and flag high-risk changes early:** Not all changes are equally risky. Apply additional scrutiny proportionally, not uniformly.

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Centralized CAB catching errors | People far from the change don't understand its implications | Peer review by those who understand the context + automation |
| Treating all changes equally | Low-risk changes wait behind high-risk ones | Differentiate by risk profile; automate low-risk approvals |
| Adding process when stability problems occur | Increases batch sizes, lead times, and actual risk | Invest in making changes quicker and safer, not slower |

## How to Measure

- **Percentage of changes requiring manual approval for production:** Track by risk profile and drive this number down
- **Time changes spend waiting for approval from external bodies:** Identify and eliminate bottlenecks
- **Team confidence that changes can get through approval in a timely manner:** Survey the team; low confidence signals process problems

## Coaching Patterns

1. **Map the current approval process end-to-end:** Identify every step, every handoff, and every wait state. Visualize the pain.
2. **Start with low-risk changes:** Automate their approval path first. Prove the model works before expanding to higher-risk changes.
3. **Redefine CAB's role:** Transition from gatekeepers approving individual changes to strategic coordinators improving the overall process.

## Related Skills

- [`continuous-integration`](../continuous-integration/): Automated validation that enables lightweight approvals
- [`test-automation`](../test-automation/): Building the confidence needed to reduce manual gates
- [`pervasive-security`](../pervasive-security/): Integrating security into the approval pipeline
- [`code-review-discipline`](../code-review-discipline/): Effective peer review practices

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | — |