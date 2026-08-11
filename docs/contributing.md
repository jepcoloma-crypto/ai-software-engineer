# Contributing to the Framework

This document explains how to contribute to the AI Software Engineer framework
itself — the guidance, structure, and conventions stored in this repository.
It complements the repository-level guidelines in `CONTRIBUTING.md`, which
remain authoritative.

Contributing to this framework is different from contributing to an
application: most contributions are content and structure, and they modify the
behavior of autonomous agents. That raises the bar for care. Framework changes
should be deliberate, verified, and consistent with the framework's own
principles.

## Understand the Architecture First

Before modifying anything:

1. Read `AGENTS.md` in full. It is the constitution: mission, principles,
   lifecycle, safety, and source of truth.
2. Read `docs/architecture.md` to understand the layers (constitution,
   agents, skills, rules, workflows, templates, knowledge, commands,
   documentation) and how they relate.
3. Inspect the target directory and existing content to follow its
   conventions.
4. Check for existing content on the topic to avoid duplication.

## Avoid Unnecessary Changes

The framework's own principles apply to contributions:

- Keep changes focused on the requested task.
- Prefer small changes over large rewrites.
- Do not bundle unrelated edits into one contribution (per `CONTRIBUTING.md`).
- Preserve existing functionality unless a change is intentional.
- Do not add layers, abstractions, or content without a concrete need.

## Add Specialized Knowledge to Skills Rather Than AGENTS.md

`AGENTS.md` is the constitution. It should stay focused on mission,
principles, lifecycle, and safety. Specialized, task-area knowledge belongs in
skills under `.opencode/skills/` (see `docs/skills.md`), in domain knowledge
under `knowledge/`, or in the domain rules under `rules/` — not padded into
`AGENTS.md`. Keeping the constitution small keeps it authoritative.

## Add Processes to Workflows Rather Than Rules

Rules are guardrails; workflows are procedures. If a process with an ordered
sequence, responsible agents, and gates is needed, add or extend a workflow in
`workflows/` rather than encoding the process into a rule file. Rules should
state constraints; workflows should orchestrate the steps, agents, skills,
gates, and approvals.

## Keep Rules Focused

Rules should state a single, focused constraint and stay consistent with
`AGENTS.md`. When a rule is added, make its purpose and scope clear and
consistent with the existing rule files in `rules/`. Prefer refining an
existing rule over adding overlapping ones.

## Keep Templates Reusable

Templates under `templates/` are generic, reusable starting points for
artifacts. Keep them free of project-specific assumptions, technology
assumptions, and concrete details that do not belong to every task. When you
change a template, check the workflows that produce that artifact so they
stay consistent.

## Keep Knowledge Evidence-Based

Knowledge under `knowledge/` must be accurate and verifiable:

- Follow the rigor defined in `knowledge/research/README.md`: prefer official
  documentation, cite sources, record evidence and uncertainty, and distinguish
  verified facts from unverified claims.
- Follow `knowledge/lessons-learned/README.md` for lessons: record the
  situation, what happened, the cause, and the recommended change.
- Never fabricate sources, quotes, versions, APIs, or results.
- Never document features or behavior that do not exist.

## Propose Framework Improvements Instead of Silently Changing Core Behavior

The framework has a continuous improvement loop (see `docs/architecture.md`):
reflect, record, propose, verify, approve. Core behavior — rules, workflows,
principles, and other governing behavior — must not be changed silently.
Record the lesson and the proposed improvement, and get explicit human
approval before applying changes to core framework behavior.

## Validate Changes

- Ensure contributions are complete and not placeholders or stubs.
- Check grammar, spelling, and formatting against surrounding content.
- Confirm that references to agents, skills, rules, workflows, templates, and
  directories point to things that actually exist.
- Keep documentation synchronized with the repository structure; update
  related documentation when you add or relocate content.
- Confirm no fabrications: nothing is documented that does not exist.

## Avoid Secrets

- Never commit credentials, tokens, keys, or private data.
- Check diffs and staged content for secrets before committing (per
  `rules/git.md`).
- Treat a committed secret as compromised: rotate it, then remove history
  responsibly.

## Avoid Destructive Git Operations

- Never force-push, reset, or rewrite shared history (per `rules/git.md`).
- Prefer reversible operations and `revert` over `reset`.
- If a destructive command is truly necessary, state what it will do before
  running it.

## Never Commit or Push Without Authorization

- Do not commit, push, or merge unless explicitly asked (per `rules/git.md`).
- Make changes on a branch and integrate through review where the project uses
  that flow.
- Prepare and verify changes, then report them for approval.