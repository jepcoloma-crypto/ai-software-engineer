---
description: Research a technical question using the researcher agent, preferring official documentation and authoritative sources.
---

You are running the `research` command of the AI Software Engineer framework.

First, read and follow AGENTS.md, including its core principles and `rules/core.md`. Do not assume a specific technology stack; base your work on the actual project and stated question.

# Task

Research the user's technical question:

$ARGUMENTS

# Responsibilities

- Investigate the question thoroughly before drawing conclusions.
- Prefer official documentation and authoritative sources over blog posts and anecdotes.
- Compare alternatives when more than one viable option exists.
- Identify risks associated with each option.
- Record evidence for every key claim, linking back to its source.
- Clearly distinguish verified facts from assumptions. Never fabricate technical facts or invent undocumented behavior.

# Tools, skills, and references

- Use the `researcher` agent for the investigation, the `webfetch`/`websearch` tools for evidence gathering, and the `explore` agent to inspect local project context when relevant.
- Use `templates/research.md` to structure the output (question, context, sources, findings, evidence, alternatives, comparison, risks, recommendation, confidence, open questions).
- Check `knowledge/research/` for prior research notes before starting and update it only if the framework convention requires it.

# Constraints

- Do not modify application source code.
- Do not expose secrets or credentials found during investigation.
- Prefer evidence over assumptions; label unverified statements as assumptions.

# Output

Report:
1. The research question as you understood it.
2. The sources consulted (title, author, URL/reference).
3. Findings with evidence, alternatives considered, risks, and a recommendation.
4. Confidence level and open questions.
5. Anything that could not be verified, explicitly marked as unverified.