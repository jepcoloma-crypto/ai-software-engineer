---
name: deployment
description: Use when releasing software to any environment. Use for build validation, environments, configuration, secrets, migrations, deployment checks, health checks, rollback, and post-deployment verification.
---

# Deployment

## When to use

Use when moving software from code to a running environment — staging or production — including releases, database migrations, environment configuration, and post-deploy verification. Also use when reviewing an existing deployment process.

## Process

1. **Validate the build first**: Ensure the artifact builds cleanly in the deployment environment — reproducible build, correct version/tag, no test failures that gate the release. Never deploy a broken or unverified build.
2. **Confirm the target environment and configuration**: Deploy the intended artifact to the intended environment. Check that environment-specific configuration points at the right dependencies (databases, services, feature flags) and that no local or wrong-environment settings leak in.
3. **Handle secrets separately from the repository**: Secrets come from the platform's secret management — never from code or version control. Confirm the deploy reads the correct secret set for the target environment.
4. **Run migrations safely**: Apply database migrations as part of the release in the correct order, backward/forward compatibly with the running application. Ensure migrations are reversible or have a known rollback path before executing them on production data.
5. **Perform pre-deployment checks**: Verify the deploy prerequisites — connectivity to dependencies, required storage, health-check endpoint defined, rollback plan known, and release notes/runbook for the change.
6. **Deploy and health-check**: Release with a method that can be observed (blue-green, canary, or rolling where available). Immediately check the health endpoint, key business flows, and logs for startup errors.
7. **Have a rollback path**: Know exactly how to return to the previous release before you start. Prefer an image/version rollback over code-level patching; roll back quickly when health checks fail rather than debugging in production.
8. **Verify after deployment**: Check success signals — response codes, error rates, key user journeys, migrations completed, and feature behavior — for a defined period, not just "it started".

## Important checks

- Is the artifact the verified build of the intended commit/tag?
- Is the configuration correct for this environment and free of secrets?
- Will migrations run safely, in order, and reversibly against production data?
- Is the health check defined and does it pass after deploy?
- Is the rollback procedure known, tested, and fast to execute?
- Are post-deploy success signals observed before declaring success?

## Common mistakes

- Deploying an unverified build and discovering the failure in production.
- Baking secrets into the repo or the image instead of the secrets manager.
- Running migrations that are irreversible or incompatible with the current running app version.
- Skipping the health check and declaring success on process start alone.
- Having no tested rollback, then improvising during an incident.
- Confusing environment configuration: deploying staging settings to production.

## Completion

The verified build is deployed to the correct environment with proper configuration and platform-managed secrets, migrations ran safely, health checks pass, the rollback path is understood and available, and post-deployment verification confirms the release behaves correctly.