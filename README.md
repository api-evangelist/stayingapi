# StayingAPI (stayingapi)

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

**APIs.json:** [https://stayingapi.apievangelist.com/apis.yml](https://stayingapi.apievangelist.com/apis.yml)

## Tags

- travel
- hospitality
- accommodation-data
- hotel-api
- vacation-rental
- short-term-rental
- airbnb
- booking.com
- vrbo
- google-hotels
- cross-ota-price-comparison
- availability
- reviews
- rest
- mcp
- agent-native
- openapi

## Timestamps

- **Created:** 2026-08-03
- **Modified:** 2026-08-09

## APIs

### StayingAPI MCP Server

Hosted MCP server (Streamable HTTP, OAuth 2.1/PKCE) exposing 7 read-only tools mapping 1:1 to the REST endpoints: search_stays, check_availability, get_listing, get_price, compare_prices, get_reviews, get_job.

- **Human URL:** [https://stayingapi.com/docs](https://stayingapi.com/docs)
- **Base URL:** `https://mcp.stayingapi.com/mcp`

#### Tags

- travel
- hospitality
- accommodation-data
- hotel-api
- vacation-rental
- short-term-rental
- airbnb
- booking.com
- vrbo
- google-hotels
- cross-ota-price-comparison
- availability
- reviews
- rest
- mcp
- agent-native
- openapi

#### Properties

- [M C P](https://mcp.stayingapi.com/mcp)
- [M C P Server](mcp/stayingapi-mcp.yml)
- [Tool Crosswalk](mcp/stayingapi-tool-crosswalk.yml)
- [Documentation](https://stayingapi.com/docs/mcp)
- [Postman Collection](collections/stayingapi-account-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-account-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/stayingapi-data-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-data-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/stayingapi-jobs-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-jobs-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### StayingAPI Agent Skills

Published portable SKILL.md agent skill in the stayingapi/travel-skills GitHub repo, referenced from the SDK docs, plus n8n workflow recipes.

- **Human URL:** [https://github.com/stayingapi/travel-skills](https://github.com/stayingapi/travel-skills)
- **Base URL:** `https://github.com/stayingapi/travel-skills`

#### Tags

- travel
- hospitality
- accommodation-data
- hotel-api
- vacation-rental
- short-term-rental
- airbnb
- booking.com
- vrbo
- google-hotels
- cross-ota-price-comparison
- availability
- reviews
- rest
- mcp
- agent-native
- openapi

#### Properties

- [Agent Skills](https://github.com/stayingapi/travel-skills)
- [Agent Skill](skills/_index.yml)
- [Postman Collection](collections/stayingapi-account-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-account-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/stayingapi-data-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-data-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Postman Collection](collections/stayingapi-jobs-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-jobs-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### StayingAPI Account API

Account, plan and credit balance

- **Human URL:** [https://stayingapi.com/docs/endpoints/search](https://stayingapi.com/docs/endpoints/search)
- **Base URL:** `https://api.stayingapi.com/v1`

#### Tags

- Account

#### Properties

- [OpenAPI](openapi/stayingapi-account-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/stayingapi-account-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-account-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Documentation](https://stayingapi.com/docs)
- [API Reference](https://stayingapi.com/docs/endpoints/search)

### StayingAPI Data API

Accommodation data endpoints

- **Human URL:** [https://stayingapi.com/docs/endpoints/search](https://stayingapi.com/docs/endpoints/search)
- **Base URL:** `https://api.stayingapi.com/v1`

#### Tags

- Data

#### Properties

- [OpenAPI](openapi/stayingapi-data-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/stayingapi-data-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-data-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Documentation](https://stayingapi.com/docs)
- [API Reference](https://stayingapi.com/docs/endpoints/search)

### StayingAPI Jobs API

Async job polling

- **Human URL:** [https://stayingapi.com/docs/endpoints/search](https://stayingapi.com/docs/endpoints/search)
- **Base URL:** `https://api.stayingapi.com/v1`

#### Tags

- Jobs

#### Properties

- [OpenAPI](openapi/stayingapi-jobs-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/stayingapi-jobs-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/stayingapi-jobs-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Documentation](https://stayingapi.com/docs)
- [API Reference](https://stayingapi.com/docs/endpoints/search)

## Common Properties

- [Domain Security](security/stayingapi-domain-security.yml)
- [Agentic Access](agentic-access/stayingapi-agentic-access.yml)
- [Authentication](authentication/stayingapi-authentication.yml)
- [OpenAPI](openapi/_original/stayingapi-openapi-original.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [L L Ms Txt](llms/stayingapi-llms.txt)
- [Well Known](well-known/stayingapi-well-known.yml)
- [A P I Catalog](https://stayingapi.com/.well-known/api-catalog)
- [M C P Server](mcp/stayingapi-mcp.yml)
- [Tool Crosswalk](mcp/stayingapi-tool-crosswalk.yml)
- [Agent Skill](skills/_index.yml)
- [Packages](packages/stayingapi-packages.yml)
- [S D Ks](packages/stayingapi-packages.yml)
- [O Auth Scopes](scopes/stayingapi-scopes.yml)
- [Conventions](conventions/stayingapi-conventions.yml)
- [Error Catalog](errors/stayingapi-error-codes.yml)
- [Lifecycle](lifecycle/stayingapi-lifecycle.yml)
- [Status Page](https://status.stayingapi.com)
- [Deprecation](https://stayingapi.com/docs/stability)
- [Changelog](changelog/stayingapi-changelog.yml)
- [Changelog](https://stayingapi.com/changelog)
- [Sandbox](sandbox/stayingapi-sandbox.yml)
- [Console](https://stayingapi.com/docs/try-it)
- [Conformance](conformance/stayingapi-conformance.yml)
- [Data Model](data-model/stayingapi-data-model.yml)
- [Overlay](overlays/stayingapi-openapi-overlay.yaml)
- [Rate Limits](rate-limits/stayingapi-rate-limits.yml)
- [Plans](plans/stayingapi-plans.yml)
- [Arazzo](arazzo/stayingapi-cross-ota-price-comparison.yml) — [Arazzo Specification](https://spec.openapis.org/arazzo/latest.html)
- [Arazzo](arazzo/stayingapi-availability-then-price.yml) — [Arazzo Specification](https://spec.openapis.org/arazzo/latest.html)
- [Developer Portal](https://stayingapi.com/docs)
- [Documentation](https://stayingapi.com/docs)
- [API Reference](https://stayingapi.com/docs/endpoints/search)
- [Getting Started](https://stayingapi.com/docs/quickstart)
- [Support](https://stayingapi.com/contact)
- [GitHub Organization](https://github.com/stayingapi)
- [Pricing](https://stayingapi.com/pricing)
- [Sign Up](https://stayingapi.com/signup)
- [Login](https://stayingapi.com/login)
- [Terms of Service](https://stayingapi.com/terms)
- [Privacy Policy](https://stayingapi.com/privacy)

## Maintainers

**FN:** StayingAPI
**Email:** hello@stayingapi.com
**URL:** https://stayingapi.com
