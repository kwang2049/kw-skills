# AGENTS.md

## Project Overview

This repository stores workspace-level coding-agent skills. The canonical skill source is `skills/`; agent-specific directories are lightweight adapters that point back to that shared directory.

Important paths:

- `skills/`: canonical shared skills directory.
- `.codex/skills`, `.kiro/skills`, `.claude/skills`, `.agents/skills`: relative symlinks to `../skills`.
- `skills/<skill-name>/SKILL.md`: primary instructions and metadata for an individual skill.
- `skills/<skill-name>/agents/`: optional agent-specific metadata, such as `openai.yaml`.

## Setup and Validation

There is no package manager, build system, or test runner configured in this repository. Validate changes with shell checks:

```sh
find . -maxdepth 3 -type l -ls
find skills -maxdepth 3 -type f | sort
```

When modifying symlinks, confirm the expected relative targets:

```sh
ls -la .codex .kiro .claude .agents
```

## Skill Authoring

- Before creating or editing skills, check the official guidelines for the target agent surfaces:
  - Kiro CLI skills: https://kiro.dev/docs/cli/skills/
  - Claude Code skills: https://code.claude.com/docs/en/skills
  - OpenAI Codex skills: https://developers.openai.com/codex/skills
- Treat the shared `SKILL.md` shape as the portable baseline, then add agent-specific metadata only when the target agent's documentation supports it.
- Keep portable skill content under `skills/` whenever possible.
- Each skill should have a `SKILL.md` with YAML frontmatter including at least `name` and `description`.
- Put detailed workflow instructions in the skill body, not in the repository README.
- Use `agents/` inside a skill only for compatibility metadata that is specific to one agent or interface.
- Document compatibility caveats in the skill's own README or metadata when a skill is not portable across all supported agents.
- Keep the main `SKILL.md` concise and actionable. Put large examples, templates, scripts, and reference material in supporting files such as `references/`, `scripts/`, or `assets/` when the relevant agent supports those paths.

## Repository Conventions

- Preserve the relative symlink layout described in `README.md`; it lets the repository move between workspace paths without rewriting links.
- Do not replace symlinked agent skill directories with copied directories unless the repository strategy changes.
- Keep root documentation focused on repository usage. Put agent-facing operational guidance in this file and skill-specific behavior in the relevant `SKILL.md`.
- Avoid committing generated system files such as `.DS_Store`; `.gitignore` already ignores `.DS_Store`.

## Agent Notes

- `skills/agents-md/` is currently untracked in git. Treat it as user work unless asked to commit or reorganize it.
- If adding build, lint, or test tooling later, update this file with the exact supported commands.
- Closest `AGENTS.md` files take precedence for files below their directory. Add nested files only when a subproject needs different instructions.
