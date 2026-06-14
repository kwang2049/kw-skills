---
name: work-logs
description: Set up and manage workspace work logs. Use by default to create a local work-logs/ folder and ensure AGENTS.md records that each work log file is named YYYY-MM-DD.md and that work logs should be updated right after each task is handled. Use with the keyword "status" to read and summarize recent work logs, including recent progress, decisions, blockers, and next steps.
---

# Work Logs

Manage durable local work logs for a workspace. Default mode sets up the workspace convention; `status` mode summarizes recent entries.

## Modes

- `$work-logs`: set up `work-logs/` under the local workspace and ensure `AGENTS.md` contains the work-log naming rule.
- `$work-logs status`: summarize recent work logs without modifying them.

## Setup Workflow

1. Identify the local workspace root:
   - Use the current working directory unless the user specifies another workspace path.
   - If inside a git repository, prefer the repository root.
2. Create `work-logs/` under that workspace when it does not exist.
3. Ensure `AGENTS.md` contains these rules, adding them only if missing:
   - Work logs live under `work-logs/`.
   - Each work log must be named after the date in `YYYY-MM-DD.md` format.
   - Work logs should always be updated right after each task is handled.
4. If `AGENTS.md` does not exist, create a concise one with the work-log rules.
5. Report the paths created or confirmed.

## Writing Logs

- When asked to create or update a log, use the local date for the filename: `work-logs/YYYY-MM-DD.md`.
- Update the current day's work log right after each task is handled.
- If today's file exists, append the new entry under a timestamp or short heading instead of overwriting existing content.
- Keep entries concise and factual. Prefer sections such as:
  - `Summary`
  - `Changes`
  - `Decisions`
  - `Validation`
  - `Blockers`
  - `Next Steps`

## Status Workflow

1. Locate `work-logs/` in the workspace.
2. Read the most recent dated logs first, sorted by filename descending.
3. If the user gives a count or date range, use that scope. Otherwise summarize the most recent 7 logs, or all logs if fewer exist.
4. Summarize:
   - recent progress,
   - important decisions,
   - open blockers or risks,
   - validation or deployments mentioned,
   - likely next steps.
5. Include links to the referenced log files when reporting status.

## Guardrails

- Do not invent work-log content. Summaries must be grounded in existing log files.
- Do not overwrite existing logs.
- Do not rename existing logs unless the user explicitly asks.
- Do not include secrets or sensitive local configuration values in logs or summaries.
- Treat non-date Markdown files in `work-logs/` as auxiliary notes, not canonical daily logs.
