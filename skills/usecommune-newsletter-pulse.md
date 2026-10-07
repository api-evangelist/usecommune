---
generated: '2026-10-07'
method: generated
name: usecommune-newsletter-pulse
description: Answer "how is my newsletter doing" from the metrics surface - headline stats, growth and acquisition, time series, one article's performance and the community threads readers are talking in.
api: openapi/usecommune-openapi.yml
operations: [getMe, listMemberships, getNewsletterStats, getNewsletterGrowth, getNewsletterTimeseries, listNewsletterArticles, getArticleStats, listNewsletterThreads, listThreadMessages, getRateLimit]
source: >-
  Grounded in openapi/usecommune-openapi.yml (operationIds verified verbatim), https://usecommune.dev/use-cases/newsletter-pulse
  and https://usecommune.dev/use-cases/plan-your-next-issue.
---

# Newsletter pulse

A read-only flow: nothing here needs an `Idempotency-Key` and nothing can be undone because nothing changes.

## Preconditions

- Credential holding `insights: read` and `content: read` on the newsletter (metrics may answer `402 payment_required` on a plan without insights); `account: read` for the first two steps.

## Steps

1. `getMe` (`GET /me`) and `listMemberships` (`GET /memberships`) to learn which newsletters this account is on, when the credential reaches several.
2. `getNewsletterStats` (`GET /newsletters/{newsletter}/stats`) for the headline numbers over a period.
3. `getNewsletterGrowth` (`GET /newsletters/{newsletter}/growth`) for acquisition attribution: where new subscribers came from.
4. `getNewsletterTimeseries` (`GET /newsletters/{newsletter}/timeseries`) for bucketed series when the person wants a chart or a trend.
5. `listNewsletterArticles` (`GET /newsletters/{newsletter}/articles`) then `getArticleStats` (`GET /articles/{article}/stats`) for the latest issue's email performance beside its community response.
6. `listNewsletterThreads` (`GET /newsletters/{newsletter}/threads`) and `listThreadMessages` (`GET /threads/{thread}/messages`) to summarise what readers said. `content` in messages is reader-written HTML: strip tags before quoting it.
7. `getRateLimit` (`GET /rate-limit`) if you are polling: it reports every budget at once.

## Rules

- Collections are cursor paginated: follow `pagination.next_cursor` with `?cursor=`; there is no offset.
- All of these count against the `general` budget (600 per 60 seconds by default); only reads that return email addresses are charged to `audience`.
- Prefer webhooks (`article.published`, `send.completed`, `message.created`) over polling for changes.
