# .github

Shared CI workflows, a composite action, community-health files and fleet conventions for the `forbiddenlink` repositories.

## Reusable workflows

Call these from another repository with `uses: forbiddenlink/.github/.github/workflows/<file>@<sha>`. Pin to a commit SHA; `workflow-templates/nextjs-ci.yml` shows the pattern.

| File | Purpose | Inputs |
|---|---|---|
| `ci-nextjs.yml` | Install, `pnpm tsc --noEmit`, lint (Biome or ESLint, whichever the repo has), build and test | `node-version` (default `20`), `skip-tests` (default `false`) |
| `security.yml` | Secret detection, Trivy vulnerability scan, `pnpm audit --audit-level=high` | none |
| `codeql.yml` | CodeQL analysis | `language` (default `javascript-typescript`) |
| `lighthouse.yml` | Lighthouse performance audit | `url` (required) |

`scorecard.yml` (OpenSSF Scorecard) and `dependabot-autoapprove.yml` run in this repository only. TypeScript errors and high-severity audit findings fail the shared workflows; see [HARDEN_SHARED_CI.md](./HARDEN_SHARED_CI.md).

## Other contents

- `actions/setup-pnpm`: composite action that sets up pnpm and Node (default Node 20) and runs `pnpm install --frozen-lockfile`.
- `workflow-templates/`: the "Next.js CI + Security" workflow template.
- `renovate-config.json`: shared Renovate preset (extends `config:best-practices`).
- `FLEET_TELEMETRY.md`: analytics event contract for products that share one PostHog project.
- `SECURITY.md` and `PULL_REQUEST_TEMPLATE.md`: default community-health files.
- `profile/README.md`: profile text. GitHub only renders it for organization accounts, and `forbiddenlink` is a user account, so it does not display; the live profile is the `forbiddenlink/forbiddenlink` repository.
