# kw-skills

Workspace-level agent skills for coding agents such as Codex, Kiro CLI, and Claude Code.

The repository keeps one canonical `skills/` directory. Agent-specific skill folders are symlinked to that shared directory so the same skill files can be used regardless of which workspace convention an agent expects.

## Layout

```text
skills/          # canonical skills directory
.codex/skills    -> ../skills
.kiro/skills     -> ../skills
.claude/skills   -> ../skills
.agents/skills   -> ../skills
AGENTS.md        # repository instructions for coding agents
work-logs/       # local daily work logs
```

## Usage

Clone this repository at the root of a workspace, or copy the symlink pattern into an existing workspace:

```sh
mkdir -p .codex .kiro .claude .agents
ln -s ../skills .codex/skills
ln -s ../skills .kiro/skills
ln -s ../skills .claude/skills
ln -s ../skills .agents/skills
```

Add shared skills under `skills/`. Each agent-specific path will resolve to the same files.

By default, add new skills through the corresponding agent-specific skills folder for the agent option in use, such as `.codex/skills`, `.kiro/skills`, `.claude/skills`, or `.agents/skills`. In this workspace, those paths are symlinks to the local `skills/` directory, so the skill remains versioned here and shared across agents.

## Included Skills

- `agents-md`: create, edit, or memorize rules in project-specific `AGENTS.md` files.
- `code-read`: analyze a code repository and write a Markdown understanding report with diagrams and code references.
- `implement`: develop feature ideas through proposal, feedback, approval, and implementation.
- `session-conclude`: summarize a coding session, check README freshness, commit relevant changes, and optionally push or open a PR.
- `work-logs`: set up dated workspace logs and summarize recent log status.

## Notes

- Keep portable skills in `skills/` whenever possible.
- If a skill needs agent-specific instructions, document the compatibility in that skill's own README or metadata.
- Symlinks are relative so the repository can be moved or cloned into different workspace paths.
