# StayingAPI

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

Unified accommodation-data API returning live search, availability, price, cross-OTA price comparison, and normalized reviews across Airbnb, Booking.com, Vrbo, and Google Hotels via a single normalized JSON schema, so one integration covers four platforms. Delivered over a nine-operation REST API, a hosted MCP server with seven read-only tools, and a typed TypeScript SDK, all drawing on one shared credit balance. Live calls are asynchronous — a scrape returns HTTP 202 with a jobId to poll — while a deterministic stay_test_ sandbox answers synchronously at zero credits. Failed, empty and blocked calls are never billed. Launched July 2026 with a published stability policy, a locked 35-code error catalog, an llms.txt, an RFC 9727 api-catalog and fourteen installable agent skills.

**Areas:** Travel · Hospitality · accommodation-data · hotel-api · Vacation Rentals · Short-Term Rental · Airbnb · Booking.com · Vrbo · google-hotels · cross-ota-price-comparison · Availability

## StayingAPI on APIs.io

Everything profiled for StayingAPI is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/stayingapi/](https://apis.io/providers/stayingapi/)** — or go straight to one of the APIs or properties below.

### APIs (5)

- [StayingAPI MCP Server](https://apis.io/apis/stayingapi/stayingapi-mcp-server/) — Hosted MCP server (Streamable HTTP, OAuth 2.1/PKCE) exposing 7 read-only tools mapping 1:1 to the REST endpoints: search_stays, check_availability,…
- [StayingAPI Agent Skills](https://apis.io/apis/stayingapi/stayingapi-agent-skills/) — Published portable SKILL.md agent skill in the stayingapi/travel-skills GitHub repo, referenced from the SDK docs, plus n8n workflow recipes.
- [StayingAPI Account API](https://apis.io/apis/stayingapi/stayingapi-account-api/) — Account, plan and credit balance
- [StayingAPI Data API](https://apis.io/apis/stayingapi/stayingapi-data-api/) — Accommodation data endpoints
- [StayingAPI Jobs API](https://apis.io/apis/stayingapi/stayingapi-jobs-api/) — Async job polling

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Arazzo workflows (2)

Multi-step workflows that chain operations into a business task.

- [StayingAPI — check availability, then price the stay](https://apis.io/arazzos/stayingapi/stayingapi-availability-then-price/)
- [StayingAPI — cross-OTA price comparison](https://apis.io/arazzos/stayingapi/stayingapi-cross-ota-price-comparison/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [StayingAPI](https://apis.io/servers/stayingapi/stayingapi/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Stayingapi Agentic Access](https://apis.io/agentic-access/stayingapi/stayingapi-agentic-access/)

#### Collections (3)

Postman and Open Collection request collections.

- [Staying Account API](https://apis.io/collections/stayingapi/open-stayingapi-account-api/)
- [Staying Data API](https://apis.io/collections/stayingapi/open-stayingapi-data-api/)
- [Staying Jobs API](https://apis.io/collections/stayingapi/open-stayingapi-jobs-api/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Stayingapi Openapi Overlay](https://apis.io/overlays/stayingapi/stayingapi-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Stayingapi Authentication](https://apis.io/security/stayingapi/stayingapi-authentication/)
- [Stayingapi Domain Security](https://apis.io/security/stayingapi/stayingapi-domain-security/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Stayingapi Scopes](https://apis.io/scopes/stayingapi/stayingapi-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Stayingapi Plans](https://apis.io/plans/stayingapi/stayingapi-plans/)

#### Rate limits (1)

Published request limits.

- [Stayingapi Rate Limits](https://apis.io/rate-limits/stayingapi/stayingapi-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.stayingapi.com/)
- [Documentation](https://stayingapi.com/docs)
- [Getting started](https://stayingapi.com/docs/quickstart)
- [API reference](https://stayingapi.com/docs/endpoints/search)
- [Pricing](https://stayingapi.com/pricing)
- [Sign up](https://stayingapi.com/signup)
- [Support](https://stayingapi.com/contact)
- [Changelog](https://stayingapi.com/changelog)
- [Terms of service](https://stayingapi.com/terms)
- [Privacy policy](https://stayingapi.com/privacy)
- [GitHub](https://github.com/stayingapi)
- [Status](https://status.stayingapi.com)

## API Evangelist rating

**Kin Score 64.9** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 85.0 |
| Contract quality | 51.4 |
| Contract governance | 4.5 |
| Operational transparency | 73.7 |
| Developer ergonomics | 76.2 |
| Access clarity | 76.3 |

**Agent readiness 60.2** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | verified |
| Event Surface Described | — |
| Agent Skills | yes |
| Well Known Catalog | yes |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 34.3** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/stayingapi/](https://apis.io/providers/stayingapi/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for StayingAPI: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/stayingapi/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
