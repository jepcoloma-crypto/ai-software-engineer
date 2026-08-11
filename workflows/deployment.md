# Workflow: Deployment

## 1. Purpose

Release a verified build to a target environment (staging or production)
safely, with validated configuration, managed secrets, executed migrations,
observable rollout, verified health, and a known rollback path. The workflow is
`VALIDATE → BUILD → TEST → SECURITY CHECK → DEPLOY → VERIFY → DOCUMENT` and
reuses the framework's deployment, testing, security, and documentation
capabilities.

## 2. When to use

Use when moving software from code to a running environment, including
releases, database migrations in the release, environment configuration, and
post-deploy verification. Use when reviewing an existing deployment process.
Do not use for code that has not passed its preceding change workflow
(`feature-development.md`, `database-change.md`, `api-change.md`, or
`bug-fix.md`).

## 3. Preconditions

- The change to be released has passed its change workflow and validation
  gates.
- A target environment and an intended artifact (commit/tag) are identified.
- The project's release, health-check, and rollback procedure exists or is
  established.
- Human approval is required before any production deployment.

## 4. Workflow steps

1. **Validate the change** — **Lead agent / Tester agent.**
   Confirm the changes scheduled for release completed their change workflows
   and passed their gates: tests executed, review resolved, security review
   clean. Use the `deployment` skill and `rules/testing.md`.
   **Gate G1:** nothing is deployed that has failed or skipped its preceding
   validation gates.
2. **Build the artifact** — **Developer agent.**
   Produce a reproducible, versioned build of the intended commit or tag in the
   deployment environment. Confirm no gate-test failures block the release.
   Use the `deployment` skill and `rules/coding.md`.
   **Gate G2:** the build succeeds and is the verified build of the intended
   revision.
3. **Run the release test suite** — **Tester agent.**
   Run the relevant suite against the artifact. Report actual results only.
   Use the `testing` skill and `rules/testing.md`.
   **Gate G3:** the executed suite passes for the artifact to be released.
4. **Perform a security check** — **Security agent.**
   Verify no blocking vulnerabilities, no exposed secrets, correct secure
   defaults for the target environment, and sound dependency status. Use the
   `security-review` skill and `rules/security.md`.
   **Gate G4:** the deployment is free of blocking security issues.
5. **Confirm environment and configuration** — **Lead agent / Developer agent.**
   Confirm the deployment targets the intended environment with the correct
   configuration and dependency wiring. Ensure environment-specific settings
   and secrets come from the platform's secret management, never from version
   control. Use the `deployment` skill and `rules/security.md`.
   **Gate G5:** configuration is verified against the target environment and
   free of secrets in code.
6. **Deploy and run migrations** — **Lead agent (with human approval).**
   Apply database migrations in order with backward/forward compatibility and a
   known rollback path. Release with an observable method (rolling, canary, or
   blue-green where available). Migrations to staging or production require
   prior human approval per `rules/database.md`.
   **Gate G6:** deployment proceeds only after approval; migrations are safe
   and reversible.
7. **Verify after deployment** — **Tester agent / Lead agent.**
   Check the health endpoint, key business flows, response codes, error rates,
   and logs for a defined period. Confirm migrations completed and feature
   behavior matches expectations. Use the `deployment` skill.
   **Gate G7:** post-deployment success signals are observed, not assumed.
   **Gate G7b:** if health checks fail, roll back using the documented
   procedure rather than debugging in production.
8. **Document the release** — **Documentation agent.**
   Record the release, version, environment, migration status, verification
   results, and any rollback actions. Update deployment and changelog
   documentation per `rules/documentation.md`.

## 5. Responsible agents

| Task | Agent |
| --- | --- |
| Release validation | Lead agent / Tester agent |
| Build | Developer agent |
| Release test suite | Tester agent |
| Security check | Security agent |
| Environment and configuration | Lead agent / Developer agent |
| Deployment and migrations | Lead agent (with human approval) |
| Post-deployment verification | Tester agent / Lead agent |
| Release documentation | Documentation agent |

## 6. Relevant skills and rules

- **Skills:** `deployment`, `testing`, `security-review`,
  `database-design`, `git-workflow`.
- **Rules:** `rules/core.md`, `rules/testing.md`, `rules/security.md`,
  `rules/database.md`, `rules/documentation.md`, `rules/git.md`,
  `rules/architecture.md`.
- **Framework:** the safety and before-completion checks in `AGENTS.md`.

## 7. Required artifacts

- Record of the completed change workflows and their passed gates.
- Reproducible build artifact tied to a commit or tag.
- Actual test results for the release candidate.
- Security check results for the deployment.
- Verified environment and configuration details, free of secrets.
- Deployment and migration execution record.
- Post-deployment health and verification results.
- Rollback plan and any execution notes.
- Release documentation and changelog entry.

## 8. Validation gates

- **G1:** preceding change workflows complete and their gates passed.
- **G2:** build succeeds and matches the intended revision.
- **G3:** release suite executed and passes.
- **G4:** no blocking security issues for the target environment.
- **G5:** configuration correct for the target environment and secret-free.
- **G6:** deployment and migrations approved and executed safely.
- **G7:** post-deployment health and behavior verified with observed evidence.
- **G7b:** health-check failure triggers the documented rollback.

## 9. Approval requirements

- Human approval is required before any production deployment.
- Human approval is required before applying migrations to staging or
  production, and before any destructive or irreversible operation on
  production data.
- Human approval is required before a rollback that involves history
  rewriting or destructive data operations per `rules/git.md` and
  `rules/database.md`.
- Secrets must never be committed to the repository; configuration must not be
  deployed from version control.

## 10. Completion criteria

Completion requires verified evidence of all of the following:

- The released change passed its preceding validation gates.
- The artifact is a reproducible build of the intended revision.
- The release test suite was executed and passed.
- No blocking security issue remains and no secrets were exposed.
- Environment configuration is correct and secret-free.
- Migrations ran in order and are reversible with a known rollback path.
- Post-deployment health and success signals were observed for the defined
  period.
- Rollback procedure exists and was followed if health checks failed.
- Release and deployment documentation is updated and accurate.

Do not claim completion without running the verification steps described
above.