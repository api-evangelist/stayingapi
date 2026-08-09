---
name: stayingapi-rate-parity-monitor
description: Watch how your own listing's rate shows across OTAs on a schedule and flag any platform underselling the market median. Powered by the StayingAPI REST API / MCP server.
version: 1.0.0
homepage: https://stayingapi.com/workflows/rate-parity-monitor
license: Proprietary — see https://stayingapi.com/terms
tools: [price-compare, listing]
auth: bearer-api-key | oauth2-pkce
---

# Cross-OTA rate-parity monitor → parity-exception digest

Rate parity erodes quietly: one OTA quietly undersells the rate you want your property to hold, and you only find out when direct bookings dry up. This monitor calls the flagship price-compare endpoint for your property on a schedule, ranks every OTA offer, measures each against the StayingAPI-computed median, and posts a parity-exception digest — which platforms are below the median, by how much, and the total spread — so a revenue manager can act on a paper trail instead of a hunch.

- **Base URL:** `https://api.stayingapi.com/v1` (REST) · **MCP:** `https://mcp.stayingapi.com/mcp`
- **Auth:** `Authorization: Bearer stay_live_…` (free sandbox: `stay_test_…`).
- **Get a free key** (no card): https://stayingapi.com/signup · Full machine contract: https://api.stayingapi.com/openapi.json

## Steps

1. **Point it at your property + a target stay** — Give the workflow your property name (plus an optional location to disambiguate), the check-in / check-out dates and occupancy to monitor, and a currency.
2. **Pull every OTA rate for the property** — On each scheduled run it calls GET /v1/price-compare, which resolves the one property and returns every OTA offer for those dates plus StayingAPI-computed min and median aggregates.
3. **Flag the parity exceptions** — The transform ranks the offers, measures each against the median, and flags any OTA sitting below it — the platforms undercutting the rate you want to hold — and computes the overall spread.
4. **Deliver the parity digest** — A digest (median, spread, each OTA with its delta vs. median, and the flagged exceptions) is posted to Slack — swap the last node for email or a Google Sheet to keep a running parity log.

## When to use this

The user is a host, property manager or revenue manager who wants to know whether their own
property is being **undersold on any OTA** — a rate-parity problem — rather than shopping for the
cheapest deal. Reach for the flagship `price-compare` endpoint: it resolves one property and
returns every OTA offer for the dates, plus StayingAPI-computed `min` and `median`.

## How to do it

1. Resolve the property with **one** of `name`, `googleHotelId`, or `location` (+ `checkIn`,
   `checkOut`, optional `adults`, `currency`).
2. Call `GET /v1/price-compare`.
3. Rank `data.offers[]` by `totalPrice`. Compare each against `data.median` (or the host's stated
   target/direct rate if they gave you one). **Flag every OTA below that reference** — those are the
   parity exceptions — and report the spread (`max - min`).

## Reading the result

Report, per exception: the OTA, its `totalPrice`, the delta vs. the reference, and the `url`.
Lead with the count of exceptions and the largest gap. If `meta.partial` is true, note which
platforms are missing from `meta.platformResults[]`.

## Scheduling

This is a monitor: run it on a cadence (daily is typical) and deliver a recurring digest, so parity
drift is caught the day it appears rather than at month-end.

### Example — REST

```bash
curl -sS "https://api.stayingapi.com/v1/price-compare?name=Hotel%20X%20Sibenik&location=Sibenik,HR&checkIn=2026-07-13&checkOut=2026-07-20&currency=EUR" \
  -H "Authorization: Bearer $STAYINGAPI_KEY"
```

### Example — @stayingapi/sdk

```ts
import { StayingApiClient } from '@stayingapi/sdk';

const scout = new StayingApiClient({ apiKey: process.env.STAYINGAPI_KEY });

const { data } = await scout.priceCompare({
  name: 'Hotel X Sibenik',
  location: 'Sibenik, HR',
  checkIn: '2026-07-13',
  checkOut: '2026-07-20',
  currency: 'EUR',
});

const below = data.offers.filter((o) => o.totalPrice < data.median);
console.log(below.length, 'OTA(s) below median', data.median);
```

## Async & partial failures

A live call that has to scrape returns `202` with `data.jobId`, `data.pollUrl` and
`data.estimatedSeconds` (the `202` itself charges 0). Poll `GET /v1/jobs/{jobId}` (free)
until `data.status` is TERMINAL — `completed` **or** `failed`.

- **`completed`** → the payload is at `data.result` (the same schema the sync call returns;
  `data` itself is just `{jobId, result, status}`). `meta` carries `partial`,
  `platformResults[]` and `warnings[]`. A completed job may still return an **empty**
  result (`data.result: []`) — the reason is in `meta.warnings[]` (e.g. `no_results`), and
  empty results charge 0.
- **`failed`** → HTTP is still **200**, not an HTTP error. The failure is nested at
  `data.error` (`code`, `type`, `message`, `retryable`). Detect it with
  `data.status === "failed"`, **not** a top-level `error`. `creditsCharged` is 0, and `meta`
  carries only `{requestId, creditsCharged, platforms}` — do **not** read `partial`,
  `platformResults` or `warnings` on a failed job.

Pace your polling: honour the `Retry-After` header, back off between attempts, and cap the
number of attempts. A tight loop hits `429 rate_limit_exceeded` (120 requests/minute).

The `@stayingapi/sdk` auto-polls and applies this contract for you.

## Platform coverage for this workflow

This workflow calls `/v1/listing`, which `google` does **not** support — those return `400 platform_not_enabled`. Scope this workflow to `airbnb`, `booking` or `vrbo` for that step. (`google` is fine for search, availability, price and price-compare.)

## Credit awareness

Costs are per-endpoint and metered by result (v3). **Failed, empty and blocked calls are never
billed**, and sandbox (`stay_test_`) calls are always free. The exact, current costs live only in
https://stayingapi.com/pricing and the machine-readable https://api.stayingapi.com/openapi.json — read them there, don't assume.

---

**Get your free key → https://stayingapi.com/signup** · Docs: https://stayingapi.com/docs · Workflow: https://stayingapi.com/workflows/rate-parity-monitor
