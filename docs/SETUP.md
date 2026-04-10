# Setup Guide

## Prerequisites

- [Node.js](https://nodejs.org/) v18+ (for `npx`)
- [uv](https://github.com/astral-sh/uv) (for `uvx` — Jira MCP server)
- [Claude Code](https://claude.ai/code) or [Cursor](https://cursor.com/)
- A CloudBees Unify account with API access

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/cloudbees/devops-agent-kit.git
cd devops-agent-kit

# 2. Copy the env template and fill in your values
cp demo/env.template .env

# 3. Run the setup check
bash demo/setup.sh

# 4. Launch the agent
claude .        # Claude Code
# or
cursor .        # Cursor
```

## Environment Variables

### CloudBees Unify (required)

| Variable | Description | How to get it |
|----------|-------------|---------------|
| `CLOUDBEES_API_TOKEN` | Personal access token | CloudBees Unify > User Settings > API Tokens |
| `CLOUDBEES_ORG_ID` | Organization ID | CloudBees Unify > Organization Settings |

### Jira (required for /file-ticket)

| Variable | Description | How to get it |
|----------|-------------|---------------|
| `JIRA_URL` | Your Jira instance URL | e.g., `https://yourcompany.atlassian.net` |
| `JIRA_USERNAME` | Your Jira email | The email you log in with |
| `JIRA_API_TOKEN` | API token | [Atlassian API Tokens](https://id.atlassian.com/manage-profile/security/api-tokens) |

### Slack (required for Slack notifications)

| Variable | Description | How to get it |
|----------|-------------|---------------|
| `SLACK_BOT_TOKEN` | Slack bot OAuth token | Slack App > OAuth & Permissions > Bot User OAuth Token |
| `SLACK_TEAM_ID` | Slack workspace ID | Slack App settings or workspace admin |

### GitHub

The GitHub MCP server uses the Copilot HTTP transport. If you're using Claude Code with GitHub Copilot, no additional env vars are needed. For standalone use, authenticate via `gh auth login`.

## Using Your Own Environment (BYOE)

The kit works with any CloudBees Unify environment. Set `CLOUDBEES_API_TOKEN` and `CLOUDBEES_ORG_ID` to point at your own org and the agent will work against your real data.

## Troubleshooting

See [TROUBLESHOOTING.md](TROUBLESHOOTING.md) for common issues.
