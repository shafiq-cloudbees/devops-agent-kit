# Troubleshooting

## MCP Server Connection Issues

### CloudBees Unify MCP server won't start

**Symptom:** `npx -y @cloudbees/unify-mcp-server` fails or times out.

**Fixes:**
- Verify Node.js v18+: `node --version`
- Check that `CLOUDBEES_API_TOKEN` and `CLOUDBEES_ORG_ID` are set
- Test the token: the agent will show an auth error if the token is invalid or expired
- If behind a corporate proxy, set `HTTPS_PROXY` environment variable

### Jira MCP server won't start

**Symptom:** `uvx mcp-atlassian` fails.

**Fixes:**
- Install uv: `curl -LsSf https://astral.sh/uv/install.sh | sh`
- Verify `JIRA_URL` includes the protocol: `https://yourcompany.atlassian.net`
- Generate a new API token at https://id.atlassian.com/manage-profile/security/api-tokens
- `JIRA_USERNAME` should be your email, not your display name

### Slack MCP server won't start

**Symptom:** `npx -y @zencoderai/slack-mcp-server` fails.

**Fixes:**
- Verify `SLACK_BOT_TOKEN` starts with `xoxb-`
- Ensure the Slack app has required scopes: `chat:write`, `channels:read`, `channels:history`
- `SLACK_TEAM_ID` is the workspace ID (found in Slack app settings)

### GitHub MCP not available

**Symptom:** GitHub tools not showing up in the agent.

**Fixes:**
- In Claude Code: the GitHub MCP uses the HTTP transport to `https://api.githubcopilot.com/mcp/` — ensure GitHub Copilot is active
- In Cursor: the `mcp-remote` bridge is used — ensure `npx -y mcp-remote` works
- For standalone use: authenticate with `gh auth login`

## Agent Behavior Issues

### Agent gets stuck or produces unexpected output

**Fixes:**
- Start a new conversation — MCP server state may be stale
- Check that the correct org is set in `CLOUDBEES_ORG_ID`
- Run `demo/setup.sh` to validate all connections

### `logs_list` returns 500 error

**This is a known limitation.** The CloudBees Unify MCP server's log retrieval may fail for some runs. The agent is designed to fall back to analyzing step names, statuses, and durations instead. No action needed.

### Controller analytics widgets return empty data

**Known limitation.** Widgets ci5 (Completed Runs), ci6 (Usage Patterns), and ci7 (Project Activity) may return empty data. The agent skips them gracefully and calculates the CI Health Score from available data.

### Org-level security reports show "No Data Found"

**Known limitation.** Widgets s4 and s5 at the org level may not have data. The agent falls back to component-level `security_issues_all_get` which works reliably.

### Agent skips some runs (code_scan workflows)

**By design.** Runs with workflow names containing "code_scan" are infrastructure-managed security scans, not user CI pipelines. The agent filters these out to focus on user-relevant pipelines.

## Environment Issues

### .env file not loading

**Fix:** The setup script sources `.env` from the repo root. Ensure:
- The file is named `.env` (not `env` or `.env.local`)
- Values don't have quotes around them: `CLOUDBEES_API_TOKEN=abc123` not `CLOUDBEES_API_TOKEN="abc123"`
- No trailing whitespace in values

### Running behind a corporate proxy

Set these environment variables:
```bash
export HTTP_PROXY=http://proxy.company.com:8080
export HTTPS_PROXY=http://proxy.company.com:8080
export NO_PROXY=localhost,127.0.0.1
```

## Still stuck?

Open an issue at https://github.com/cloudbees/devops-agent-kit/issues with:
1. Which MCP server is failing
2. The error message
3. Output of `demo/setup.sh`
