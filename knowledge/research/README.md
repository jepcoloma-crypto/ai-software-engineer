# Research

## Purpose

This directory stores technical research produced before and during
software tasks. It captures the evidence behind technical decisions so
that reasoning, sources, and uncertainties remain traceable after the
work is done.

Research here supports the RESEARCH step of the development lifecycle
defined in `AGENTS.md`.

## What Belongs Here

- Findings from investigating technologies, libraries, tools, or APIs
  before adoption.
- Comparisons of alternatives with documented trade-offs.
- Verification notes confirming whether a claim or API is real.
- Answers to technical questions that required external sources.
- Records of uncertainty and open questions that were not fully resolved.

Research that is no longer current should be marked outdated (see
below) rather than deleted silently.

## Source Verification Requirements

- Every claim sourced from external material must cite where it came
  from (official documentation, source code, published specification,
  or a specific page/version).
- Distinguish between verified facts and unverified claims.
- If a source cannot be located or accessed, record that the claim is
  unverified rather than presenting it as fact.
- Do not copy copyrighted material verbatim. Record findings in your
  own words and cite the source.

## Preference for Official Documentation

- Prefer official documentation, published specifications, and original
  source code over blog posts, forum answers, or secondary summaries.
- When official and secondary sources conflict, treat official sources
  as authoritative and note the discrepancy.
- If only secondary sources exist, say so explicitly.

## Recording Sources and Evidence

Each research entry should record:

- The research question or decision under investigation.
- The conclusion reached, if any.
- The sources used, with URLs or file references and version/date.
- The evidence supporting the conclusion.
- Any contradicting evidence.
- The date the research was performed.

Use a format that makes the chain from question to evidence to
conclusion explicit.

## Recording Uncertainty

- Explicitly state when a conclusion is uncertain, incomplete, or
  based on assumptions.
- Record the level of confidence and what would resolve the remaining
  uncertainty.
- Never present speculation as verified fact.

## Identifying Outdated Research

- Record the date and the technology version at research time so
  staleness can be detected.
- Mark entries as outdated when a referenced version is superseded or
  when official documentation changes contradict the entry.
- An outdated entry must state what changed and, when possible, link to
  or point toward current information.

## Promoting Research into Verified Reusable Knowledge

Research becomes reusable knowledge only after it has been verified and
accepted. A promotion should include:

- Confirmation that every claim is verified against an authoritative
  source.
- A review of the conclusion for correctness and safety.
- An explicit decision to accept it as reusable knowledge.
- Recording the promotion decision and the verification evidence.

Promoted knowledge should be stored in the appropriate knowledge
directory so it can be reused by future tasks.

## Fabricated Information Is Prohibited

- Fabricating sources, quotes, versions, APIs, or results is forbidden.
- Never invent documentation, specifications, or behavior to support a
  conclusion.
- Research that cannot be verified against a real source must be
  recorded as unverified or unresolved, not as fact.
