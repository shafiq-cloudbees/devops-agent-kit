# Demo Scenarios

Four scenarios that demonstrate the DevOps Agent's capabilities. Each builds on the previous one, but they can also be run independently.

---

## Scenario 1: "What's happening across my pipelines?"

**The hero demo.** Shows unified cross-tool pipeline visibility — the heterogeneous CI story that no single-tool vendor can replicate.

### Setup
- Meridian demo org with 4 components across Jenkins, GitHub Actions, and CloudBees Workflows

### Script

```
You: Show me what's happening across all our pipelines.
```

The agent runs `/pipeline-overview all` and:

1. Discovers all 4 components
2. Pulls workflows and recent runs per component
3. Checks Jenkins controller status
4. Pulls security findings and feature flag state
5. Presents a unified dashboard table

**Expected output:**
- Dashboard showing all 4 components across 3 CI tools
- GitHub Actions: mostly passing (85-93%)
- CloudBees Workflows: failing on all service components (common config bug)
- Jenkins: mixed results on account-service
- 7 HIGH security findings across 2 components
- 1 feature flag (instant-transfers, OFF)

### Follow-up

```
You: Triage the payment-api failures.
```

The agent runs `/triage meridian-payment-api` and identifies the root cause (e.g., `path` vs `folder-name` config bug), classifies as CONFIG, and recommends a fix.

### Cross-tool actions

```
You: File a Jira ticket for this and post to Slack.
```

The agent creates a structured Jira ticket and posts a summary to the specified Slack channel.

**Why it's compelling:** One question gives you a cross-tool picture that would take 15 minutes of clicking through three separate dashboards. The agent spots patterns across components that a human checking one at a time might miss.

---

## Scenario 2: "Are we secure?"

**The DevSecOps demo.** Shows security posture assessment with cross-reference to CI status and feature flags.

### Script

```
You: Give me the security posture across all our components.
```

The agent runs `/security-scan all` and:

1. Pulls all open security issues
2. Gets severity breakdowns per component
3. Checks scanner coverage and SLA status
4. Cross-references with feature flag state

**Expected output:**
- Security dashboard with 7 HIGH findings across 2 components
- All Gitleaks (exposed secrets) — Stripe token, API keys, private key
- All within SLA (due Apr 14)
- Scanner coverage: 50% components, 33% workflows, SAST only
- Feature flag check: no active rollouts affected

### Follow-up

```
You: File tickets for the critical findings.
```

The agent creates structured Jira tickets with severity, file paths, SLA dates, and remediation steps.

**Why it's compelling:** Combines security scanning data with CI status, feature flags, and project management in one view.

---

## Scenario 3: "Ship the release"

**The progressive delivery demo.** Shows release orchestration + feature flags + security gates.

### Script

```
You: Is the release candidate ready? Walk me through the deployment.
```

The agent runs `/release-status` and:

1. Checks all components: CI status, security findings, flag states
2. Identifies the release orchestration workflow
3. Generates a go/no-go report

**Expected output:**
- Release readiness report with BLOCKED verdict
- Per-component status with specific blockers
- Action items checklist

### After resolving blockers

```
You: Blockers are fixed. Enable the instant-transfers flag in production.
```

The agent runs `/flag-rollout instant-transfers enable production`:
- Shows current state (OFF)
- Warns about production impact
- Waits for confirmation
- Enables the flag
- Offers to post to Slack

**Why it's compelling:** Progressive delivery end-to-end — release orchestration + feature flags + security gates, all from the IDE.

---

## Scenario 4: "Morning standup briefing"

**The full-breadth demo.** Chains all skills into one synthesized output.

### Script

```
You: Give me the morning briefing — what do I need to know?
```

The agent chains multiple skills:

1. **Pipeline status** — `/pipeline-overview all` (quick summary)
2. **Security update** — `/security-scan all` (changes since last check)
3. **CI health** — `/ci-health org` (health score, controller status)
4. **Release status** — `/release-status` (blockers, readiness)
5. **Feature flags** — current flag states

**Expected output:**

A synthesized briefing with:
- CI Health Score (e.g., 62/100)
- Per-tool pass rates
- Security findings summary
- Release blockers
- Recommended focus items for the day

### Follow-up

```
You: Post the briefing to the #engineering Slack channel.
```

**Why it's compelling:** Shows the agent as a true DevOps copilot that synthesizes across all tools, not a single-purpose utility.
