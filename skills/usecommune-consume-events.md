---
generated: '2026-10-07'
method: generated
name: usecommune-consume-events
description: Wire a webhook consumer to a Commune newsletter - open the delivery portal to register the endpoint, verify the Commune-Signature HMAC, dedupe on event id, audit delivery attempts and replay one that failed.
api: openapi/usecommune-openapi.yml
operations: [createPortalSession, listNewsletterDestinations, listNewsletterEvents, listNewsletterDeliveryAttempts, getDeliveryAttempt, replayDeliveryAttempt]
source: >-
  Grounded in openapi/usecommune-openapi.yml (operationIds verified verbatim), https://api-reference.usecommune.dev/group/webhook-webhooks
  and https://usecommune.dev/use-cases/react-in-real-time.
---

# Consume events

Commune publishes 23 event topics as HTTPS POSTs with one shared envelope. Destinations are managed in a delivery portal, not through a CRUD endpoint.

## Preconditions

- Credential holding `webhooks: write` (to mint a portal link) or `webhooks: read` (to audit); `sending: write` to replay an attempt.
- An HTTPS endpoint of your own that answers `200` fast and does the work afterwards.

## Steps

1. `createPortalSession` (`POST /newsletters/{newsletter}/portal-session`) mints a one-use portal URL. **The returned `url` is a credential**: redirect the person to it and never store or log it. In the portal, add the destination, choose topics and copy the `whsec_` signing secret. This is the only way to create or edit a destination.
2. `listNewsletterDestinations` (`GET /newsletters/{newsletter}/destinations`) to confirm the endpoint is registered and `enabled`, and which `topics` it receives.
3. On each delivery, verify before parsing: HMAC-SHA256 keyed with the secret (prefix included) over `<Commune-Timestamp as Unix seconds>.<raw body>`, lowercase hex, matched against any `v0=` digest in `Commune-Signature` (two during rotation). Reject stale timestamps, then dedupe on `Commune-Event-Id`. Delivery is at least once and unordered; `occurred_at` is the ordering field.
4. If your consumer also writes to the API, skip any event whose `idempotency_key` is one you issued, or you will answer your own echo.
5. `listNewsletterEvents` (`GET /newsletters/{newsletter}/events`) reads the raw event stream when you need to backfill (charged to the `audience` budget).
6. `listNewsletterDeliveryAttempts` (`GET /newsletters/{newsletter}/delivery-attempts`), filterable by `event_id`, and `getDeliveryAttempt` (`GET /delivery-attempts/{attempt}`) answer "did that event reach me".
7. `replayDeliveryAttempt` (`POST /delivery-attempts/{attempt}/replay`) re-delivers the event as a new attempt marked `manual: true`. Use it for a failure you have since fixed, not to catch up after an outage (automatic retries already run eleven attempts over about eight and a half hours).

## Rules

- A wrong signature should answer `401`; it is retried like any non-2xx.
- Replays, and automatic retries, are duplicates the consumer has to handle by `id`.
