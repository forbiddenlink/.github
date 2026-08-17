# Shared CI hardening verification

This branch makes two existing reusable checks authoritative instead of advisory:

- TypeScript errors fail the reusable Next.js workflow.
- High-severity `pnpm audit` findings fail the reusable security workflow.

Before broad fleet rollout, validate the workflows from at least one representative consumer repository. If a consumer currently relies on ignored failures, fix that repository or add a narrow documented exception there rather than weakening the shared baseline.
