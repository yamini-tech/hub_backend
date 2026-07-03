---
mode: agent
agent: backend-ci
name: backend-ci-prompt
description: "Prompt for the backend-ci agent. Creates and updates GitHub Actions CI workflows for backend linting, testing, and deployment."
---

### Requirements

1. **Workflow Triggers:** Push to `main`, pull requests, and `workflow_dispatch` with optional environment input.
2. **Jobs:** `lint` (`ruff check .`), `test` (`pytest -q`), `migration-check` (`alembic check`). Optionally include `security-scan` and `coverage`.
3. **Caching:** pip dependency caching and Python virtual environment caching.
4. **Python Version:** Use Python 3.10 (LTS). Support matrix build for 3.10, 3.11.
5. **Environment Variables:** Set `DATABASE_URL`, `SECRET_KEY` and other env vars from GitHub Secrets.
6. **Notifications:** Optional Slack notification on failure via `SLACK_WEBHOOK_URL`.

### Constraints

- GitHub Actions syntax — no third-party CI platforms
- Use `actions/setup-python@v5` for Python setup
- Use `actions/cache@v4` for dependency caching
- Secrets referenced as `${{ secrets.SECRET_NAME }}` — never hardcode values

### Success Criteria

- Workflow runs without syntax errors on push
- All core jobs (lint, test, migration-check) pass
- Cache is restored and saved correctly
- Notifications fire on failure if configured

### Usage Template

```
Create/update a backend CI workflow with:
- Python version: [version]
- Jobs: [lint, test, migration-check, security-scan, coverage]
- [Optional] Slack notifications via [secret name]
Show the diff and wait for my confirmation before applying.
```

### Chat Example

```
User: Create a backend-ci.yml workflow for lint, test, migration-check.
- Python 3.10, 3.11 matrix
- Cache dependencies
- Slack notifications on failure via SLACK_WEBHOOK_URL
```

Agent (expected):
- Scans repo for existing workflows and requirements.txt
- Drafts backend-ci.yml with requested jobs and caching
- Shows the diff and waits for confirmation before applying
