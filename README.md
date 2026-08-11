# AI Software Engineer

A reusable AI Software Engineering Framework that turns software ideas and
requirements into production-quality software with consistent, senior-level
engineering discipline.

## What Is This?

This repository is an operating framework for autonomous software engineering
agents. It codifies how an agent should behave when asked to design, build,
test, review, and improve software. It is **not** a business application —
it is a set of reusable guidance, rules, knowledge, templates, and workflows.

## What It Provides

- **Mission & Principles** — a defined role and seventeen core engineering
  principles that govern every task (`AGENTS.md`).
- **Development Lifecycle** — a repeatable process from `REQUIREMENTS` through
  `COMPLETE` (running `RESEARCH → ANALYSIS → ARCHITECTURE → PLAN → IMPLEMENT →
  TEST → REVIEW → SECURITY REVIEW → DOCUMENT` in between).
- **Rules** — enforceable guardrails for safety, change management, and
  engineering quality (`rules/`).
- **Knowledge** — reference material, research, and lessons learned organized
  under `knowledge/`.
- **Templates** — reusable starting points for common artifacts (`templates/`).
- **Workflows** — repeatable procedures for recurring tasks (`workflows/`).
- **Documentation** — architectural decisions and guidance (`docs/`).

## Repository Layout

```
├── AGENTS.md        # Mission, principles, lifecycle, safety, source of truth
├── docs/            # Additional documentation and decisions
├── knowledge/       # Domain reference material
│   ├── architecture/
│   ├── backend/
│   ├── databases/
│   ├── devops/
│   ├── frontend/
│   ├── security/
│   ├── research/
│   └── lessons-learned/
├── rules/           # Enforceable engineering and safety rules
├── templates/       # Reusable artifact templates
├── workflows/       # Repeatable procedures
└── .opencode/       # OpenCode agents, commands, and skills
    ├── agents/      # OpenCode agent definitions
    ├── commands/    # OpenCode project commands
    └── skills/      # OpenCode skill definitions
```

## Getting Started

For agents, start by reading `AGENTS.md` before undertaking any task. It
defines the operating instructions, the development lifecycle, and the
guardrails that must not be broken.

For humans, browse the `rules/`, `knowledge/`, `templates/`, and `workflows/`
directories to reuse the framework's practices in your own engineering work,
or fork this repository to create a framework tuned to your team.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on improving this
framework.

## License

Licensed under the MIT License. See [LICENSE](LICENSE).