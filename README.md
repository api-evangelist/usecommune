# Commune

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Commune turns newsletters into communities: each newsletter has an archive of articles and every article carries a threaded chat, with engagement insights, subscriber analytics, growth tracking and superfan identification on top. The Commune API (63 operations, 23 webhook topics, contract version 2026-08-26) exposes newsletters, articles, threads, messages, subscribers, tags, senders, domains, metrics, sends and event delivery over a cursor-paginated REST surface at api.usecommune.com, authenticated with bearer API keys or OAuth 2.1 (PKCE, dynamic client registration, RFC 9728 protected-resource metadata), versioned by a Commune-Version date header, with a required Idempotency-Key on every write and a hosted MCP server at api.usecommune.com/mcp.

**Areas:** Newsletters · Email · Community · Publishing · Creator Economy · Subscribers · Webhook · MCP · Analytics · Content

## Commune on APIs.io

Everything profiled for Commune is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/usecommune/](https://apis.io/providers/usecommune/)** — or go straight to one of the APIs or properties below.

### APIs (18)

- [Commune Articles API](https://apis.io/apis/usecommune/usecommune-articles-api/) — An article is one thing a newsletter published: written in Commune and sent, or imported from the newsletter's provider. Two rules gate every article read…
- [Commune Engagement API](https://apis.io/apis/usecommune/usecommune-engagement-api/) — What Commune knows about one subscriber that a newsletter's email provider cannot answer: engagement scored across the inbox and the community together, and…
- [Commune Event delivery API](https://apis.io/apis/usecommune/usecommune-event-delivery-api/) — Where a newsletter's events go, and how a creator changes it. Commune hands every event it publishes to a delivery service that owns fan out, retries,…
- [Commune Highlights API](https://apis.io/apis/usecommune/usecommune-highlights-api/) — A highlight is a passage of an article a reader marked. It anchors a comment to the exact sentence that prompted it.
- [Commune Messages API](https://apis.io/apis/usecommune/usecommune-messages-api/) — A message is a reply inside a thread, up to two levels deep. Reactions hang off a message.
- [Commune Metrics API](https://apis.io/apis/usecommune/usecommune-metrics-api/) — The rolled up numbers for a newsletter and for one article: headline stats for a period, acquisition attribution, bucketed series for charting, and one…
- [Commune Newsletters API](https://apis.io/apis/usecommune/usecommune-newsletters-api/) — A newsletter is the top level object in Commune. It owns its articles, its chat, its subscribers and its team. Everything else in this API hangs off one.
- [Commune Platform API](https://apis.io/apis/usecommune/usecommune-platform-api/) — The API's own machinery rather than any newsletter's data: the readiness probe, what a credential has left of its rate limit budgets, what its newsletter's…
- [Commune Search API](https://apis.io/apis/usecommune/usecommune-search-api/) — One query across newsletters, articles, people and chat. Where a reader starts who does not yet have an identifier for any of them.
- [Commune Senders API](https://apis.io/apis/usecommune/usecommune-senders-api/) — The addresses a newsletter sends from, and the state of the DNS that has to be in place for them to work. The sending half of the pair; Website domains is…
- [Commune Sends API](https://apis.io/apis/usecommune/usecommune-sends-api/) — A send is one dispatch of one article to a newsletter's list: when it started, when it finished, and the three numbers it finished on. Not to be confused…
- [Commune Subscriber tags API](https://apis.io/apis/usecommune/usecommune-subscriber-tags-api/) — A tag segments a newsletter's audience. Sending an article to a tag stamps that article with an audience, which is what makes it invisible to everyone…
- [Commune Subscribers API](https://apis.io/apis/usecommune/usecommune-subscribers-api/) — Who receives a newsletter. Needs `audience`, and never a public surface: a newsletter's list belongs to its creator. `GET /subscriptions` is that edge read…
- [Commune Team API](https://apis.io/apis/usecommune/usecommune-team-api/) — Who may act on behalf of a newsletter: its owner, plus the members the owner added as admins, editors or guests. Both sides of that edge are here. A…
- [Commune Threads API](https://apis.io/apis/usecommune/usecommune-threads-api/) — A thread is a conversation inside a newsletter's community. Commune has no separate posts or comments stack: a creator's broadcast, a reader's question and…
- [Commune Users API](https://apis.io/apis/usecommune/usecommune-users-api/) — A person with a Commune account: the readers who join a community and the writers who are credited on an article. Looked up by identifier or by username,…
- [Commune Webhooks API](https://apis.io/apis/usecommune/usecommune-webhooks-api/) — The events Commune pushes to a consumer, rather than the resources a consumer pulls. Commune publishes state changes on 23 topics, each delivered as one…
- [Commune Website domains API](https://apis.io/apis/usecommune/usecommune-website-domains-api/) — A creator's own domain pointed at their Commune site, so their community lives at their address rather than at ours. The same prove you own this hostname…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Usecommune Webhooks](https://apis.io/asyncapis/usecommune/usecommune-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [commune](https://apis.io/servers/usecommune/commune/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Usecommune Agentic Access](https://apis.io/agentic-access/usecommune/usecommune-agentic-access/)

#### JSON Schema (6)

The data models the API reads and writes.

- [ApiKey](https://apis.io/schemas/usecommune/usecommune-api-key/)
- [Article](https://apis.io/schemas/usecommune/usecommune-article/)
- [ArticlePerformance](https://apis.io/schemas/usecommune/usecommune-article-performance/)
- [DeliveryAttempt](https://apis.io/schemas/usecommune/usecommune-delivery-attempt/)
- [NewsletterStats](https://apis.io/schemas/usecommune/usecommune-newsletter-stats/)
- [Send](https://apis.io/schemas/usecommune/usecommune-send/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Usecommune Context](https://apis.io/jsonld/usecommune/usecommune-context/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Usecommune Openapi Overlay](https://apis.io/overlays/usecommune/usecommune-openapi-overlay/)

#### Governance rules (1)

Spectral rulesets for the provider's contracts.

- [Commune API Rules](https://apis.io/rules/usecommune/usecommune-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Usecommune Authentication](https://apis.io/security/usecommune/usecommune-authentication/)
- [Usecommune Domain Security](https://apis.io/security/usecommune/usecommune-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Usecommune Scopes](https://apis.io/scopes/usecommune/usecommune-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Usecommune Plans Pricing](https://apis.io/plans/usecommune/usecommune-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Usecommune Rate Limits](https://apis.io/rate-limits/usecommune/usecommune-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://usecommune.com)
- [Documentation](https://usecommune.dev/guides)
- [Getting started](https://usecommune.dev/guides/getting-started)
- [API reference](https://api-reference.usecommune.dev/)
- [Pricing](https://usecommune.com/pricing)
- [Sign up](https://usecommune.com/register)
- [Changelog](https://api-reference.usecommune.dev/changes)
- [Terms of service](https://usecommune.com/terms)
- [Privacy policy](https://usecommune.com/privacy)

## API Evangelist rating

**Kin Score 64.2** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 75.2 |
| Contract governance | 22.0 |
| Operational transparency | 55.3 |
| Developer ergonomics | 56.5 |
| Access clarity | 76.3 |

**Agent readiness 61.6** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | documented (partial credit) |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | verified |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 35.0** — Telecommunications

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/usecommune/](https://apis.io/providers/usecommune/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Commune: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/usecommune/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
