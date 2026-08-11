---
name: security-review
description: Use when auditing code or design for security vulnerabilities. Use for authentication, authorization, secrets, input validation, SQL injection, XSS, CSRF, API security, dependencies, file handling, rate limiting, and session security.
---

# Security Review

## When to use

Use before merging security-sensitive changes, when introducing authentication/authorization, handling secrets or user files, or when asked to audit a codebase, endpoint, or dependency set for vulnerabilities.

## Process

1. **Map trust boundaries**: Identify where untrusted input enters the system (HTTP requests, file uploads, webhooks, third-party data) and what it can reach. Review the boundary between authenticated and public surfaces.
2. **Review authentication**: Confirm identity is verified everywhere it is required, tokens/sessions are validated, passwords/credentials are hashed strongly, and default or hard-coded credentials do not exist.
3. **Review authorization — never just "is logged in"**: Verify each sensitive action checks the caller's permission for that specific resource (ownership, roles, scopes), on the server, every time. Watch for object references that let a user read someone else's data.
4. **Check input validation and injection**:
   - **SQL injection**: parameterized queries/prepared statements; no string-built SQL from user input.
   - **XSS**: user input is escaped on output; no `dangerouslySetInnerHTML`-style sinks fed by user data.
   - **CSRF**: state-changing requests are protected (CSRF tokens / SameSite / same-origin checks).
   - **Other injection**: command, path traversal, SSRF, template injection.
5. **Audit secrets**: No secrets in code, logs, error messages, or client bundles. Secrets come from environment/config with restricted access; do not log request bodies or tokens.
6. **Apply API and file-safety rules**: Rate limiting on sensitive/authenticated endpoints, size/type restrictions on uploads, safe file handling without path traversal, and access controls on file downloads.
7. **Review sessions and dependencies**: Secure cookie flags (`HttpOnly`, `Secure`, `SameSite`), session rotation on privilege change, logout invalidation, and known-vulnerable or outdated dependencies.
8. **Report findings by severity**: Explain the vulnerability, exploitability, impact, and a concrete remediation for each finding, ordered by risk.

## Important checks

- Is every protected route authenticated and every action authorized to the resource?
- Are all inputs validated and all output escaping in place to prevent injection?
- Does no code or log expose secrets, tokens, keys, or PII?
- Are API endpoints rate limited and uploads constrained?
- Are sessions and cookies configured securely?
- Are dependencies current and free of known vulnerabilities?

## Common mistakes

- Treating authentication as authorization: any logged-in user can act on any resource.
- Escaping in the wrong direction — SQL escaping for a database and HTML escaping before parsing — or escaping nowhere.
- Building SQL/HTML/shell strings by concatenation.
- Logging or returning full error detail / stack traces that leak internals or secrets.
- Relying on the frontend to enforce security rules.
- Using a framework's defaults blindly without checking them.

## Completion

Trust boundaries are mapped, authentication and authorization are verified on every sensitive path, input validation and output escaping prevent injection, secrets are never exposed, API/file/session/dependency risks are addressed, and remaining findings are reported with severity and remediation. Any blocking vulnerability is fixed.