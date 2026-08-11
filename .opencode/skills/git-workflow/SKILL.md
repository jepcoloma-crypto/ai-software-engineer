---
name: git-workflow
description: Use when planning or executing Git operations. Use for branching, commits, pull requests, conflict resolution, history quality, safe Git operations, and avoiding destructive operations.
---

# Git Workflow

## When to use

Use whenever you create branches, make commits, open or update pull requests, merge, rebase, resolve conflicts, or otherwise touch repository history. Consult the workflow sections before any destructive or interactive Git command.

## Process

1. **Start from a clean, current base**: Before branching or committing, inspect `git status` and your current branch. Update from the shared branch before starting work to minimize conflicts.
2. **Branch with intent**: Create a short-lived branch per piece of work, named after the change. Keep the branch's commits focused and small.
3. **Write clear commits**: Stage only the intended files — never `git add -A` blindly. Craft a concise message in the repo's style that states what changed and why. Separate one concern per commit.
4. **Inspect before committing**: Review `git diff` (and staged vs unstaged) to confirm exactly what will be recorded. Never commit secrets, build artifacts, or unrelated files.
5. **Open pull requests deliberately**: Build the PR from the finished branch, keep it reviewable (small diffs, one purpose), and link it to the issue/requirement it resolves.
6. **Resolve conflicts with understanding**: On conflict, read both sides before choosing. Merge or rebase per the project's convention; verify the result builds and tests pass afterward.
7. **Keep history clean but honest**: Prefer non-interactive operations. Once a commit is pushed and shared, do not rewrite it unless explicitly requested — avoid force-push, rebase of shared history, and destructive resets.

## Important checks

- Am I on the right branch, against the right base?
- Is everything I am staging intended and free of secrets?
- Is the commit small and its message accurate about the change?
- Is this operation reversible, and do I understand its effect on shared history?
- Does the branch still build and pass tests before a PR or merge?

## Common mistakes

- Committing from the wrong branch or against an outdated base.
- Staging everything (`git add -A`) and sweeping secrets or junk into commits.
- Rewriting public history (rebase/force-push) without an explicit request.
- `git checkout`/`reset`/clean operations that destroy uncommitted work or data.
- Leaving merge conflicts half-resolved without verifying the build and tests.

## Completion

A focused branch built on a current base contains a clearly-messaged commit (or small set) with only intended changes, has been verified to build and pass tests, and exists as a reviewable PR. No destructive, rewrites, or history reordering were performed without explicit approval.