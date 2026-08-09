---
name: stayingapi-search
description: Search and compare accommodation prices across Airbnb, Booking.com, Vrbo and Google Hotels via the StayingAPI REST API. Use when a user wants to find stays, check availability, get a price, compare one property across OTAs, or read reviews. Covers Bearer auth, the async 202→poll job contract, the unified response envelope, and error handling.
license: Proprietary — see https://stayingapi.com/terms
---

# StayingAPI — search & price-compare (REST)

StayingAPI is one accommodation-data API across **Airbnb, Booking.com, Vrbo and
Google Hotels**. Every platform is normalized to the same schema, so a single
integration covers all four. Base URL: `https://api.stayingapi.com/v1`. Full machine contract:
https://api.stayingapi.com/openapi.json.

## 1. Get a key
Create a free account and make a key at https://stayingapi.com/dashboard/keys.
- **Sandbox** keys (`stay_test_…`) return deterministic fixtures, are always free,
  and answer **synchronously** — use these to build and test with no cost or sign-up
  friction.
- **Live** keys (`stay_live_…`) run real cross-platform scrapes. Live credits unlock
  after a one-click email verification. Costs are on https://stayingapi.com/pricing.

Send the key as a Bearer token on every request:
```
Authorization: Bearer $STAYINGAPI_KEY
```
A missing/invalid key returns `401 authentication_error` (never billed).

## 2. The one contract that trips people up: live is asynchronous
- Sandbox calls and live **cache hits** answer synchronously with HTTP **200**.
- A **live** call that has to scrape returns HTTP **202** with a job handle:
  ```json
  { "data": { "jobId": "job_…", "status": "pending", "pollUrl": "/v1/jobs/job_…", "estimatedSeconds": 25 },
    "meta": { "requestId": "req_…", "creditsCharged": 0, "platforms": ["airbnb"] } }
  ```
  Poll `GET /v1/jobs/{jobId}` (free) until `data.status` is TERMINAL — `completed` **or**
  `failed`. On `completed`, read the payload from **`data.result`** (NOT `data`) — `data`
  itself is just `{jobId, result, status}`. Jobs can take several minutes; honour the
  `Retry-After` header on each poll, back off, and cap your attempts — a tight loop hits
  `429 rate_limit_exceeded` (120 req/min).
- On a **failed** job HTTP is still **200**: `data.status` is `failed` and the failure is nested
  at `data.error` (`code`, `type`, `message`, `retryable`), with 0 credits charged. Detect it
  via `data.status`, not a top-level `error`. `meta` then carries only
  `{requestId, creditsCharged, platforms}` — do **not** read `partial`/`platformResults`/`warnings`
  on a failed job.
- A `completed` job can still return an **empty** `data.result: []`; the reason is in
  `meta.warnings[]` (e.g. `no_results`), and empty results charge 0.
- Prefer the SDK (section 6) — it auto-polls, so you always get the synchronous shape.

## 3. Endpoints
All under `https://api.stayingapi.com/v1`. Credit costs are per-endpoint and live only in
https://api.stayingapi.com/openapi.json + https://stayingapi.com/pricing.

- `GET /v1/search` → `Property[]`. Cross-platform discovery. Key params:
  `location` (required, e.g. "Split, HR" or "lat,lng"), `checkIn`/`checkOut`
  (YYYY-MM-DD), `adults`, `children`, `platforms` (csv of airbnb,booking,vrbo,google),
  `limit` (1–100), `cursor`. Cursor-paginated on synchronous results.
- `GET /v1/price-compare` → `PriceCompare`. Flagship: compare one property across OTAs
  with StayingAPI-computed `min` and `median`. Params: `name` or `googleHotelId` (one
  of), `location`, `checkIn`, `checkOut`.
- `GET /v1/price` → `Price`. A real quote for one listing. Params: `platform`,
  `listingId` (platform-native — numeric on Airbnb/Vrbo, a slug string on
  Booking.com/Google — or a full `url`), `checkIn`, `checkOut` (plus optional
  occupancy and `currency`). See https://api.stayingapi.com/openapi.json for the exact parameter list.
- `GET /v1/listing/{platform}/{id}` → `Property`. Full detail; passing dates embeds a
  best-effort live price (can be null).
- `GET /v1/availability` → `Availability[]`. Day-by-day for a known listing over a
  window. Params: `platform`, `listingId` (or `listingIds[]`/`url`), `startDate`,
  `endDate`.
- `GET /v1/reviews` → `Review[]`. Normalized, paginated reviews. Params: `platform`,
  `listingId` (or `url`), `limit`, `cursor`.
- `GET /v1/account` → `Account`. Your plan, available credits, held credits, key env and rate limit.
  **Synchronous, free.** Read `data.credits.available` to check spendable credits from code.

## 4. Response envelope
Success: `{ "data": <payload>, "meta": { requestId, platforms, cached, partial,
creditsCharged, currency, pagination, platformResults, warnings } }`. Only `data`
varies by endpoint. On a **partial fan-out** (some platforms fail, ≥1 succeeds) you get
HTTP 200 with `meta.partial = true`, only the successful platforms in `data`, and each
failed platform charged 0.

## 5. Errors (failed calls are free)
Errors are `{ "error": { type, code, message, param, requestId, creditsCharged,
retryable, docUrl } }` with `creditsCharged: 0`. Handle at least:
- `401 authentication_error` — fix the key.
- `402 insufficient_credits` (`credit_balance_too_low`) — top up / upgrade.
- `429 rate_limited` — honour `Retry-After`, back off with jitter.
- `503 upstream_unavailable` / `504 upstream_timeout` — retryable; retry with backoff.
Failed, empty and blocked calls are never billed. Full catalog: https://stayingapi.com/docs/errors.

## 6. SDK (recommended)
```bash
npm install @stayingapi/sdk
```
```ts
import { StayingApiClient } from '@stayingapi/sdk';
const scout = new StayingApiClient({ apiKey: process.env.STAYINGAPI_KEY });
// Auto-polls a live 202 to completion — you get the finished { data, meta }.
const { data } = await scout.search({ location: 'Split, HR', platforms: ['airbnb', 'booking'], limit: 5 });
const compare = await scout.priceCompare({ name: 'Hotel X Sibenik', location: 'Sibenik, HR', checkIn: '2026-07-13', checkOut: '2026-07-20' });
console.log(compare.data.min, compare.data.median);
```

## 7. Try it now (sandbox — free, synchronous)
```bash
curl -sS "https://api.stayingapi.com/v1/search?location=Split,HR&platforms=airbnb,booking&limit=5" \
  -H "Authorization: Bearer $STAYINGAPI_KEY"   # stay_test_ key → HTTP 200, data[] directly
```
Read the returned `data[]` (each item is a normalized Property) and `meta.platforms`.
For a cross-OTA comparison, call `/v1/price-compare` with a property `name` + `location`
and read `data.min` / `data.median`.

## More
Docs: https://stayingapi.com/docs · Quickstart: https://stayingapi.com/docs/quickstart · OpenAPI: https://api.stayingapi.com/openapi.json
· Agents can also use the MCP server (skill: stayingapi-mcp).
