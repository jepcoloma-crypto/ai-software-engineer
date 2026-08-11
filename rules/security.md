# Security Rules

Constraints that apply to every feature and system boundary.

## Least Privilege

- Grant the minimum permissions and data access a component needs to function.
- Scope service accounts, tokens, and roles to their specific purpose.
- Default to deny; grant only what is required.

## Secrets

- Never hardcode credentials, tokens, or keys in code or configuration.
- Load secrets from environment or a dedicated secrets store.
- Never log, echo, or expose secrets in output or error messages.

## Authentication

- Authenticate every request that reaches protected resources.
- Use established, maintained authentication mechanisms; do not invent schemes.
- Fail closed when authentication state is missing or unverifiable.

## Authorization

- Enforce authorization per resource and per action, not only at the route level.
- Never derive authorization from unverified client-supplied values.
- Reject access when the decision cannot be made confidently.

## Input Validation

- Treat every external input as untrusted: bodies, params, headers, files, URLs.
- Validate type, length, range, and allowed values at the boundary.
- Reject malformed input explicitly instead of sanitizing it into correctness.

## Injection Prevention

- Use parameterized queries or the framework's query builder; never string-concatenate SQL.
- Escape or use safe builders for all dynamic query, shell, and template contexts.
- Do not evaluate user input as code or structured data.

## XSS

- Escape or encode all user-controlled content before rendering.
- Prefer framework-safe rendering and strict CSP over ad hoc mitigation.
- Do not disable built-in browser protections.

## CSRF

- Protect state-changing requests against cross-site request forgery.
- Use origin checks and validated CSRF tokens; reject mismatched requests.
- Do not rely on cookies alone for CSRF safety.

## Dependency Security

- Keep direct dependencies current and track security advisories.
- Do not add dependencies for features already available or supported.
- Pin and review dependencies that carry a security boundary.

## File Handling

- Validate file type and size against declared limits before processing.
- Store files by generated identifiers, never by user-provided names or paths.
- Prevent path traversal and execution of uploaded content.

## Rate Limiting

- Rate limit sensitive, expensive, and public endpoints.
- Apply limits per audience (user, IP, token) as appropriate to the threat.
- Make the limit explicit in the response when it is enforced.

## Session Security

- Issue session tokens with appropriate expiry and rotation.
- Invalidate sessions on logout, password change, and suspected theft.
- Use secure, HttpOnly, SameSite attributes for cookies; never accept session tokens from untrusted input.

## Logging

- Log security-relevant events: authentication, authorization, and permission changes.
- Never include secrets, tokens, or personal data in logs.
- Keep logs tamper-evident enough to support investigation.

## Secure Configuration

- Disable debug modes, verbosity, and insecure defaults in production.
- Set secure defaults for CSP, headers, and transport.
- Audit configuration changes that relax security controls.