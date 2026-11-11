---
name: vcommit
description: Make and push commits that are easy to read.
---

# vcommit

## Goal

Make commits that are easy to read and review.

- Only the intended changes are included.
- Commits are logically scoped (split when required).
- Commit messages describe what changed and, when needed, why.

## Inputs to ask for (if missing)

- Single commit or multiple commits (default: multiple small commits when there are unrelated changes).
- Commit style: use the following priority order:
  - If `AGENTS.md` mentions a commit standard, follow it unconditionally.
  - Check the Git `pre-commit` and `commit-msg` hooks for rules.
  - Otherwise, read [references/commit-message-template.md](references/commit-message-template.md) for the default scoped-subject style.

## Workflow (checklist)

1. Inspect the working tree before staging
   - `git status`
   - `git diff` (unstaged)
   - For many changes: `git diff --stat`
2. Decide commit boundaries (split if needed)
   - Split by: feature vs. refactor, backend vs. frontend, formatting vs. logic, tests vs. production code, dependency bumps vs. behavior changes.
   - If changes are mixed in one file, plan to use patch staging.
3. Stage only what belongs in the next commit
   - Prefer patch staging for mixed changes: `git add -p`
   - To unstage a hunk or file: `git restore --staged -p` or `git restore --staged <path>`
4. Review what will actually be committed
   - `git diff --cached`
   - Sanity checks:
     - No secrets or tokens
     - No accidental debug logging
     - No unrelated formatting churn
5. Describe the staged change in 1-2 sentences (before writing the message)
   - "What changed?" + "Why?"
   - If you cannot describe it cleanly, the commit is probably too big or mixed; go back to step 2.
6. Write the commit message
   - Use the commit style defined by the rules.
   - Prefer an editor for multi-line messages: `git commit -v`
7. Run the smallest relevant verification
   - Run the repo's fastest meaningful check (unit tests, lint, or build) before moving on.
8. Repeat for the next commit until the working tree is clean
9. Since this skill is only run after human review, push to the remote (if a remote exists)

## When to use

Use this skill when it is invoked or the user says `commit`, `push`, or `vcommit` in the message. Do not run it if invoked by an agent or an autonomous process. Only manual invocation or specific wording triggers this skill.

## Deliverable

Provide:

- The final commit message(s).
- A short summary per commit (what/why).
- The commands used to stage and review (at minimum, `git diff --cached`, plus any tests run).
