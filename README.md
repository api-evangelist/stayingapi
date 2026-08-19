# StayingAPI (stayingapi)

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
