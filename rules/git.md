# Git Rules

Safe use of version control.

## Meaningful Commits

- Write concise, descriptive commit messages that state what and why.
- Match the repository's commit message style.
- Do not squash multiple unrelated changes into one commit.

## Branching

- Make changes on a branch and integrate through review where the project uses that flow.
- Keep branches short-lived and named for their purpose.
- Never work directly on a protected branch.

## Reviewable Changes

- Keep each change small enough to review in one sitting.
- Include tests and documentation that belong to the change in the same commit.
- Split unrelated work into separate commits.

## Avoid Destructive Commands

- Never run force-push, reset, or history-rewriting commands without explicit instruction.
- Prefer reversible operations.
- If a destructive command is truly necessary, state what it will do before running it.

## Avoid Secrets

- Never commit credentials, tokens, or private keys.
- Check diffs and staged content for secrets before committing.
- Treat a committed secret as compromised: rotate it, then remove history responsibly.

## Safe History Operations

- Do not rewrite shared history.
- Prefer `revert` over `reset` for removing merged work.
- When rewriting local-only history, verify nothing has been pushed.

## Never Push or Commit Without Explicit Instruction

- Under this framework, do not commit, push, or merge unless the user explicitly asks.
- Prepare and verify changes, then report them for approval.
- Confirm the branch and remote before any push.