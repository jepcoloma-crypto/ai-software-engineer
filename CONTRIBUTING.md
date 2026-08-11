# Contributing to AI Software Engineer

Thank you for helping improve this framework. This repository is a reusable,
guidance-centric project — it is not a business application — and most
contributions involve content, structure, and conventions rather than code.

## Ground Rules

- Respect the framework's own core principles as defined in `AGENTS.md`,
  especially: understand before changing, keep changes simple and focused,
  follow existing conventions, and never invent undocumented behavior.
- Preserve the existing mission and philosophy. Substantive changes to the
  framework's principles or lifecycle must be proposed first.
- Keep changes focused. Do not bundle unrelated edits into a single
  contribution.

## What Can Be Contributed

- Improvements and additions to `knowledge/` reference material.
- New or refined engineering `rules/`.
- New `templates/` for reusable artifacts.
- New or improved `workflows/` for repeatable procedures.
- Content in `docs/`, including architectural decisions and rationale.
- Fixes to grammar, unclear phrasing, or broken links.

## Before You Start

1. Read `AGENTS.md` in full.
2. Inspect the existing directory structure and follow its conventions.
3. Check existing content for the topic to avoid duplication.
4. For significant changes, describe your proposal before writing it.

## Making a Change

1. Create a branch for your change.
2. Make focused edits that follow the conventions of the target directory.
3. If your change introduces a new rule or workflow, make sure its purpose
   and scope are stated clearly and consistently with existing content.
4. Update the `README.md` layout section or related documentation when you
   add or relocate content.

## Verification

This repository contains no build tooling or automated test suite. Before
submitting, verify as applicable:

- All contributions are complete and not placeholders or stubs.
- Accidental artifacts (editor files, secrets, temp files) are not included.
- Grammar, spelling, and formatting are consistent with the rest of the
  repository.
- No credentials or secrets are introduced.

## Commit Guidelines

- Write concise commit messages that describe the change in the imperative
  mood (for example, "Add database design template").
- Never commit credentials, secrets, or unrelated personal files.
- Never push or create pull requests without being asked to do so.

## Proposing Improvements

This project values continuous improvement. If you identify something that
worked, failed, or was difficult, or you believe a rule, skill, or workflow
is missing, propose it. Suggest concrete changes rather than abstract
criticism.
## OpenCode Runtime Layer

The `.opencode/` directory is the OpenCode-specific runtime integration layer.
It is intentionally Markdown-only and host-bound.

Do not introduce package scaffolding, npm dependencies, JavaScript/TypeScript
runtime code, plugins, or other executable tooling under `.opencode/` unless a
separate architectural proposal explicitly requires it and the change is
approved.

Portable engineering guidance belongs in the root-level framework layers such
as `AGENTS.md`, `rules/`, `workflows/`, `templates/`, and `knowledge/`.
OpenCode-specific syntax and runtime behavior should remain inside `.opencode/`.
