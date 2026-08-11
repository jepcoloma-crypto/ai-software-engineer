# Workflow: Security Review

## 1. Purpose

Identify and remediate security vulnerabilities in a codebase or design from
attack-surface mapping through verified fixes and documentation. The workflow
is `IDENTIFY ATTACK SURFACE → ANALYZE VULNERABILITIES → TEST → FIX → VERIFY →
DOCUMENT` and reuses the framework's security, testing, and review
capabilities.

## 2. When to use

Use before merging security-sensitive changes, when introducing
authentication or authorization, when handling secrets or user files, when
auditing an existing codebase, endpoint, or dependency set, or when a security
incident or concern is reported. Also use as the security stage of
`new-project.md`, `feature-development.md`, and `api-change.md`.

## 3. Preconditions

- The code or design under review is accessible and the review scope is
  stated.
- The trust boundaries of the system are identifiable.
- Fixing a blocking vulnerability may require human approval for any
  destructive or scope-changing remediation.

## 4. Workflow steps

1. **Identify the attack surface** — **Security agent.**
   Map trust boundaries and entry points: HTTP requests, file uploads,
   webhooks, third-party data, and any public surface. Identify what each
   boundary can reach. Use the `security-review` skill and `rules/security.md`.
   **Gate G1:** the attack surface and trust boundaries are mapped before
   analysis begins.
2. **Analyze vulnerabilities** — **Security agent.**
   Review authentication, authorization, secrets, input validation, injection
   (SQL, command, template), XSS, CSRF, SSRF, file handling, rate limiting,
   session handling, dependencies, and security configuration. Use the
   `security-review` skill and `rules/security.md`.
   **Gate G2:** findings are recorded with severity, exploitability, impact,
   and remediation.
3. **Test the findings** — **Security agent / Tester agent.**
   Confirm exploitable findings where possible with the project's tools and
   test commands. Verify claims against actual behavior; never report an
   untested finding as confirmed. Use the `testing` skill and
   `rules/testing.md`.
   **Gate G3:** findings are classified as confirmed or theoretical with
   evidence.
4. **Fix the vulnerabilities** — **Developer agent.**
   Implement focused fixes for approved findings. Do not disable security
   controls to make tests pass. Apply the minimal change that removes the
   vulnerability. Use `rules/security.md`, `rules/coding.md`.
   **Gate G4:** fixes are scoped to the finding and do not weaken other
   controls.
5. **Verify the fixes** — **Security agent / Tester agent.**
   Re-run the tests and any security checks to confirm the vulnerability is
   removed and no regression was introduced. Use the `testing` skill and
   `rules/security.md`.
   **Gate G5:** the executed suite passes and the confirmed finding is no
   longer exploitable.
6. **Document the outcome** — **Documentation agent / Security agent.**
   Record the findings, severity, fixes, and residual risk. Update security
   documentation where it describes the affected surface. Use
   `rules/security.md` and `rules/documentation.md`.
7. **Confirm completion** — **Lead agent.**
   Confirm no blocking vulnerability remains and all gates have observed
   evidence before declaring completion.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Attack-surface mapping and analysis | Security agent |
| Finding validation | Security agent / Tester agent |
| Fix implementation | Developer agent |
| Fix verification | Security agent / Tester agent |
| Documentation | Documentation agent / Security agent |
| Coordination and approval | Lead agent |

## 6. Relevant skills and rules

- **Skills:** `security-review`, `testing`, `code-review`,
  `backend-development`, `frontend-development`, `api-design`.
- **Rules:** `rules/security.md`, `rules/core.md`, `rules/testing.md`,
  `rules/coding.md`, `rules/api.md`, `rules/documentation.md`, `rules/git.md`.
- **Framework:** the safety and secrets guidance in `AGENTS.md`.

## 7. Required artifacts

- Attack-surface map and trust-boundary description.
- Security findings with severity, exploitability, impact, and remediation.
- Evidence of finding confirmation from actual testing.
- Fixes applied for approved findings.
- Verification results showing the vulnerabilities are removed.
- Security report and documentation of residual risk.

## 8. Validation gates

- **G1:** attack surface and trust boundaries mapped.
- **G2:** findings recorded with severity and remediation.
- **G3:** findings confirmed or classified with evidence.
- **G4:** fixes scoped to findings and other controls intact.
- **G5:** executed suite passes and confirmed findings are no longer
  exploitable.

## 9. Approval requirements

- Human approval is required before remediating a vulnerability in a way that
  changes behavior, disables a control, or affects production data.
- Human approval is required for any destructive action, secret rotation, or
  history rewriting performed as part of remediation per `rules/security.md`
  and `rules/git.md`.
- A blocking vulnerability must not be left unresolved without explicit
  approval and a documented risk decision.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- The attack surface and trust boundaries are mapped.
- Findings are recorded with severity, exploitability, impact, and
  remediation.
- Blocking vulnerabilities are fixed and verified as no longer exploitable.
- The executed test suite passes; no security regression was introduced.
- No secrets were exposed during the review or remediation.
- Findings and residual risk are documented.

Do not claim completion without running the verification steps described
above.