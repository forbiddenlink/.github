# Fleet Telemetry Contract

Use this contract for serious personal/product repos that send analytics to the shared PostHog project. The goal is comparable product evidence without coupling products together.

## Required context

Every custom product event should include:

- `app_id`: stable repository/product slug, e.g. `finance-quest`, `hire-ready`, `myaqualog`
- `environment`: `production`, `preview`, `development`, or `test`
- `event_version`: integer schema version, starting at `1`

When relevant also include:

- `feature`: stable feature slug
- `plan`: product plan/tier, never a secret or payment credential
- `source`: acquisition or workflow source
- `is_internal`: boolean for owner/test traffic when known

Do not send secrets, access tokens, raw payment data, sensitive prompts, or unnecessary PII.

## Canonical product lifecycle events

Projects do not need every event, but when the concept exists prefer these names instead of inventing variants:

- `signup_completed`
- `onboarding_started`
- `onboarding_completed`
- `activation_completed`
- `feature_used`
- `upgrade_started`
- `purchase_completed`
- `subscription_started`
- `subscription_canceled`
- `feedback_submitted`

Product-specific events are encouraged when they describe the core value loop, for example `portfolio_generated` or `interview_completed`.

## Viability evidence

Each revenue/flagship product should define:

1. one activation event;
2. one repeat-value/retention event;
3. one conversion event when monetized;
4. the primary feature(s) represented through `feature_used` or equivalent product-specific events.

The Audit Pack viability pass should use these live signals when available rather than relying only on qualitative judgment.

## Shared-project rules

Because multiple apps share one PostHog project:

- queries over custom events should filter or break down by `app_id`;
- hostname may be used as a compatibility fallback for historical events, not as the long-term product identity;
- development/preview/test traffic must not be mixed into product KPIs;
- event names and meanings should remain stable once dashboards depend on them;
- schema-breaking meaning changes increment `event_version`.

## Division of responsibility

- PostHog: product behavior, activation, retention, funnels, experiments, and feature adoption.
- Vercel/Sentry/Axiom or equivalent runtime tooling: production failures and operational health.
- Audit Pack: decides which evidence is required and interprets it during viability/quality reviews.
- HQ (the shared fleet command/orchestration tool): orchestrates access to these providers; it does not duplicate their telemetry stores.

## Adoption order

Adopt first in revenue/flagship apps, then public utilities with real users. Do not instrument parked demos merely for consistency.