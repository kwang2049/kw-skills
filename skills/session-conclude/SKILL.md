---
name: session-conclude
description: Summarize the current coding-agent session, inspect and stage relevant git changes, create an appropriate git commit, then either ask what remote action to take or finish with git push or pull request creation when the user includes the keyword "push" or "pr". Use at the end of a work session when the user wants completed work packaged into version control.
---

# Session Conclude

Conclude a coding session by producing a concise session summary, committing the relevant work, and handling the final remote step requested by the user.

## Invocation Modes

- `$session-conclude`: commit the relevant work, then ask whether to push or open a PR.
- `$session-conclude push`: commit the relevant work, then push the current branch.
- `$session-conclude pr`: commit the relevant work, push the current branch if needed, then open a pull request.

## Workflow

1. Inspect the repository state:
   - Run `git status --short`.
   - Review relevant diffs with `git diff` and, when needed, `git diff --staged`.
   - Identify untracked files that belong to the session.
2. Summarize the session before committing:
   - State the meaningful changes made.
   - Mention validation or tests run, including anything that could not be run.
   - Call out unrelated dirty worktree changes that should not be included.
3. Stage only the changes that belong to the completed session:
   - Prefer explicit paths with `git add <path>...`.
   - Do not use broad staging such as `git add .` when unrelated changes are present.
   - If ownership of a change is unclear, ask the user before staging it.
4. Commit the staged changes:
   - Re-check the staged diff before committing.
   - Use a concise imperative commit message that reflects the session outcome.
   - Run `git commit -m "<message>"`.
   - Do not create an empty commit unless the user explicitly asks.
5. Finish according to the invocation mode:
   - No keyword: stop after the commit and ask whether to push or open a PR.
   - `push`: push the current branch after the commit.
   - `pr`: push the current branch if needed, then open a pull request.

## Guardrails

- Treat the exact invocation keywords `push` and `pr` as explicit user confirmation for that final action.
- Never push or open a PR without either an invocation keyword or explicit user confirmation after the commit.
- Never enable auto-merge or merge without explicit user confirmation after the PR exists.
- Never rewrite history with amend, rebase, reset, or force push unless explicitly requested.
- Preserve unrelated user changes, even if they are in the same worktree.
- If there are no relevant changes to commit, report that clearly and ask what the user wants to do next.
- If the commit fails, report the exact blocker and leave the repository state unchanged except for any staging already performed.
- If `push` or `pr` is requested but the branch has no upstream, set the upstream with the normal `git push -u origin <branch>` flow when the remote is clear.
- If `pr` is requested, use the repository's available GitHub tooling and include the PR URL in the final response.

## Final Response

After finishing, include:

- the commit SHA and commit title,
- a short summary of what was committed,
- whether the branch was pushed,
- the PR URL when one was opened,
- validation performed,
- any remaining uncommitted changes,
- a direct question asking whether the user wants a push or PR next only when no invocation keyword was provided.
