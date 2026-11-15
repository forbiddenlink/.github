# Shared CI hardening verification

Status as of 2026-11-15: both changes are on `main` (`.github/workflows/ci-nextjs.yml` runs `pnpm tsc --noEmit` and `.github/workflows/security.yml` runs `pnpm audit --audit-level=high`, with no `continue-on-error`).

These changes make two existing reusable checks authoritative instead of advisory:

- TypeScript errors fail the reusable Next.js workflow.
- High-severity `pnpm audit` findings fail the reusable security workflow.

Before broad fleet rollout, validate the workflows from at least one representative consumer repository. If a consumer currently relies on ignored failures, fix that repository or add a narrow documented exception there rather than weakening the shared baseline.
