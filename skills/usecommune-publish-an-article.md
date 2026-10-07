---
generated: '2026-10-07'
method: generated
name: usecommune-publish-an-article
description: Draft an article on a Commune-published newsletter, send yourself a test copy, then schedule or send it to the list, with the idempotency and reversibility rules that keep an agent from emailing real people twice.
api: openapi/usecommune-openapi.yml
operations: [listNewsletters, createArticle, updateArticle, sendArticleTest, scheduleArticle, unscheduleArticle, sendArticle, getSend]
source: >-
  Grounded in openapi/usecommune-openapi.yml (every operationId verified verbatim), the Writes section of the
  contract's info.description, https://usecommune.dev/guides/getting-started and
  https://usecommune.dev/use-cases/publish-from-anywhere.
---

# Publish an article

Write in Commune, rehearse with a test send, then put the article on the schedule or send it now.

## Preconditions

- A bearer credential (API key `cmn_sk_...` or OAuth access token) holding `content: write` and `sending: write` on the newsletter.
- The newsletter's `esp` is `commune`; articles can only be created or edited on a newsletter Commune publishes itself (`not_commune_newsletter`, 422, otherwise).
- Pin the contract with `Commune-Version: 2026-08-26` on every request.
- Every POST/PATCH/DELETE carries an `Idempotency-Key` you generated. Reuse the same key only when retrying the same request; a different request under a used key answers `409 conflict`.

## Steps

1. `listNewsletters` (`GET /newsletters`) to find the newsletter the credential reaches and confirm `esp` is `commune`.
2. `createArticle` (`POST /newsletters/{newsletter}/articles`) with the Markdown body. The article is a draft and is invisible to readers.
3. `updateArticle` (`PATCH /articles/{article}`) for edits. Each edit is its own write with its own `Idempotency-Key`.
4. `sendArticleTest` (`POST /articles/{article}/test-send`) with no body to mail a copy to the credential's owner, or `to` (up to 5 addresses). Nobody on the list receives anything, the article status does not move and no event is published. Limit: 50 test sends per credential per day.
5. Either:
   - `scheduleArticle` (`POST /articles/{article}/schedule`) with a future `scheduled_for`. Every gate the real send runs is run now (verified sender, non-empty body, reachable images, footer). Scheduling an already scheduled article moves it.
   - `sendArticle` (`POST /articles/{article}/send`). **Cannot be undone.** Answers `202` before the article has gone out. Confirm with the person before calling it.
6. To take a scheduled article back, `unscheduleArticle` (`POST /articles/{article}/unschedule`) before dispatch; an article that already went out answers `422` and cannot be recalled.
7. Watch `send.completed` / `send.failed` webhooks, or read `getSend` (`GET /sends/{send}`) for the outcome counts.

## Rules

- Sends and schedules share a daily cap of 25 dispatches per newsletter; a schedule counts as a send, a refused send counts for nothing.
- A `429 rate_limited` on a send carries `Retry-After` in hours; on other calls, seconds. Retry with the same `Idempotency-Key`.
- The event your write publishes is delivered back to any webhook you run; skip events whose `idempotency_key` you issued.
