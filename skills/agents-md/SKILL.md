---
name: agents-md
description: Create, edit, or memorize instructions in an AGENTS.md file for the current workspace following the official AGENTS.md guide at https://agents.md/. Use when the user invokes the skill by itself to create AGENTS.md, provides an accompanying instruction to modify AGENTS.md content, or includes the keyword "memorize" with instructions/rules that should be added to the corresponding AGENTS.md section if not already present.
---

# AGENTS.md

Create or edit project-specific `AGENTS.md` instructions for coding agents. Treat the file as a concise, practical README for agents: repository context, commands, conventions, and gotchas that help future agents work correctly.

Default behavior:

- If the user invokes this skill without additional editing instructions, create an `AGENTS.md` file for the current workspace.
- If the user provides an editing instruction along with the skill invocation, edit the relevant existing `AGENTS.md` file according to that instruction.
- If the user includes the keyword `memorize` followed by instructions or rules, add those instructions or rules to the corresponding section of the relevant `AGENTS.md` file only when they are not already present.
- If the requested edit targets a missing `AGENTS.md`, create it and apply the requested guidance.

## Workflow

1. Inspect the current workspace before writing:
   - Read existing `AGENTS.md` files, if any.
   - Read `README*`, contribution docs, package manifests, build files, test configs, CI workflows, and obvious project metadata.
   - Use `rg --files` first to identify relevant files quickly.
2. Derive instructions from the repository rather than inventing them.
   - Include commands only when they are supported by scripts, configs, docs, or clear project conventions.
   - If a command cannot be verified, either omit it or label it as a project-specific assumption only when the user requested best-effort output.
3. Create or edit `AGENTS.md` at the current workspace root unless the user specifies another directory.
   - If a root `AGENTS.md` already exists, update it in place and preserve accurate existing guidance.
   - When editing, make the requested change directly while keeping unrelated accurate guidance intact.
   - When memorizing, place the new instruction under an existing matching section when possible. If the user names a section, use that section. Otherwise infer the best section from the content, such as `Build, Test, and Lint`, `Code Style`, `Testing Instructions`, `Security and Configuration`, `PR and Commit Notes`, or `Agent Notes`.
   - If no matching section exists during memorize mode, create the most appropriate concise heading and add the rule there.
   - Do not duplicate existing guidance. Treat a rule as already present when the same instruction is stated exactly or clearly covered by existing wording.
   - In a monorepo, create nested `AGENTS.md` files only when the user asks or when a subproject clearly needs different instructions.
4. Keep the output standard Markdown. The format has no required fields; choose headings that fit the project.
5. Validate that the final file is actionable and not just descriptive.

## Recommended Sections

Use only sections that are useful for the discovered project:

- `Project Overview`: brief purpose, main languages/frameworks, important directories.
- `Setup Commands`: dependency installation and local setup.
- `Build, Test, and Lint`: exact commands future agents should run.
- `Code Style`: formatting, typing, architecture, naming, and dependency conventions.
- `Testing Instructions`: where tests live, how to run focused tests, fixtures, coverage expectations.
- `Security and Configuration`: secrets handling, environment files, generated files, network or data cautions.
- `PR and Commit Notes`: title format, required checks, changelog or review expectations.
- `Agent Notes`: project-specific pitfalls, expensive commands, generated artifacts, or files to avoid editing.

## Official Guide Constraints

Follow these points from the official guide:

- Prefer the repository root file name `AGENTS.md`.
- Use standard Markdown with whatever headings make sense.
- Put agent-focused context here instead of cluttering human-facing `README.md`.
- Closest-file precedence matters: nested `AGENTS.md` files override broader instructions for files under their directory.
- Explicit user chat instructions override `AGENTS.md`.
- Treat `AGENTS.md` as living documentation and update it when repository workflows change.
