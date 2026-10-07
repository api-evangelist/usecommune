---
generated: '2026-10-07'
method: generated
name: usecommune-segment-subscribers
description: Find a newsletter's most engaged or drifting readers from engagement insights, then tag them into a segment (or remove them), remembering that a tag grants access to every article addressed to it.
api: openapi/usecommune-openapi.yml
operations: [listNewsletterSubscribers, listNewsletterInsights, listNewsletterTags, createTag, addTagSubscribers, addSubscriberTag, removeSubscriberTag, deleteTag]
source: >-
  Grounded in openapi/usecommune-openapi.yml (operationIds verified verbatim), https://usecommune.dev/use-cases/win-back-readers,
  https://usecommune.dev/use-cases/reward-your-superfans and https://usecommune.dev/errors/rate_limited.
---

# Segment subscribers

Turn engagement scores into a tagged segment that an article can be addressed to.

## Preconditions

- Credential holding `audience: write` (tags and tagging) and `insights: read` (engagement) on the newsletter. Insights reads may answer `402 payment_required` on a plan that excludes them.
- `Idempotency-Key` on every write; `Commune-Version: 2026-08-26` on every request.

## Steps

1. `listNewsletterInsights` (`GET /newsletters/{newsletter}/insights`) to read per-subscriber engagement. This read returns email addresses, so it is charged to the `audience` budget (60 per 60 seconds by default): page with `limit=100` and cache.
2. `listNewsletterSubscribers` (`GET /newsletters/{newsletter}/subscribers`) when you need the full roster rather than scored rows. Same budget.
3. `listNewsletterTags` (`GET /newsletters/{newsletter}/tags`) to reuse an existing segment, or `createTag` (`POST /newsletters/{newsletter}/tags`) to make one.
4. `addTagSubscribers` (`POST /tags/{tag}/subscribers`) tags up to 500 subscribers in one request; use it instead of looping `addSubscriberTag` (`POST /subscribers/{subscriber}/tags/{tag}`), which is one subscriber per call and counts against the `write` budget (60 per 60 seconds).
5. To undo, `removeSubscriberTag` (`DELETE /subscribers/{subscriber}/tags/{tag}`). It works even on a retired tag, and succeeds silently when the subscriber did not hold it.
6. `deleteTag` (`DELETE /tags/{tag}`) removes a tag outright only if no article was ever addressed to it; otherwise it is retired and everyone holding it keeps reading what it was addressed to. Read `outcome` in the answer.

## Rules

- A tag is an access grant: addressing an article to a tag makes the article invisible to everyone outside it, and tagging a subscriber grants them every article that segment was addressed to.
- Route on `tag_id`, not the tag name, which a creator can rename.
- `subscriber.tagged` fires with `direction: added|removed`; skip the ones carrying your own `idempotency_key`.
