# DevOps Agent Kit

Turn your AI coding assistant into a DevOps specialist. Clone this repo, open it in [Claude Code](https://claude.ai/code) or [Cursor](https://cursor.com/), and get a working DevOps agent that sees across all your CI/CD tools.

> **This is a community project maintained by CloudBees DevRel. It is not a CloudBees product and is not covered by CloudBees support.**

## What it does

The DevOps Agent connects to your CI/CD tools via [MCP](https://modelcontextprotocol.io/) and gives you:

- **Unified pipeline visibility** across Jenkins, GitHub Actions, and CloudBees Workflows
- **Build failure triage** with root cause classification
- **Security posture assessment** with remediation priorities
- **Release readiness checks** with go/no-go decisions
- **Feature flag management** from your IDE
- **CI health monitoring** with actionable scores
- **Cross-tool actions** — Jira tickets, Slack posts, GitHub PR comments

## Quick start

```bash
git clone https://github.com/cloudbees/devops-agent-kit.git
cd devops-agent-kit
cp demo/env.template .env
# Edit .env with your tokens
bash demo/setup.sh
claude .
```

## Skills (slash commands)

| Skill | What it does |
|-------|-------------|
| `/pipeline-overview` | Unified cross-tool CI/CD status dashboard |
| `/triage` | Analyze failed runs — root cause + classification |
| `/security-scan` | Security posture across components |
| `/release-status` | Release readiness with go/no-go verdict |
| `/flag-rollout` | List, enable, disable, or create feature flags |
| `/ci-health` | CI health score with controller analytics |
| `/file-ticket` | Create a Jira ticket from any finding |

## MCP servers

| Server | What it provides |
|--------|-----------------|
| [CloudBees Unify](https://www.cloudbees.com/) | CI runs, logs, components, security, analytics, workflows, flags |
| [GitHub](https://github.com/) | PRs, issues, code search, Actions status |
| [Jira](https://www.atlassian.com/software/jira) | Issue creation and management |
| [Slack](https://slack.com/) | Team notifications |

## Works with

- **Claude Code** — Full support via CLAUDE.md + .claude/skills/ + .claude/settings.json
- **Cursor** — Full support via .cursor/rules/ + .cursor/mcp.json

## Bring your own environment

The kit works with any CloudBees Unify environment. Set your `CLOUDBEES_API_TOKEN` and `CLOUDBEES_ORG_ID` to point at your own org.

## Documentation

- [Setup Guide](docs/SETUP.md) — Environment variables, prerequisites, configuration
- [Demo Scenarios](docs/SCENARIOS.md) — Four demo scripts with expected outputs
- [Troubleshooting](docs/TROUBLESHOOTING.md) — Common issues and fixes

## License

[Apache 2.0](LICENSE)
