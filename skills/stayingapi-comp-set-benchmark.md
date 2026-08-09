---
name: stayingapi-comp-set-benchmark
description: Benchmark your listing’s rate and availability against a defined comp-set and get a weekly position report. Powered by the StayingAPI REST API / MCP server.
version: 1.0.0
homepage: https://stayingapi.com/workflows/comp-set-benchmark
license: Proprietary — see https://stayingapi.com/terms
tools: [price, availability, listing]
auth: bearer-api-key | oauth2-pkce
---

# Competitor rate & availability benchmark → report

For a defined comp-set of listings, pull each one’s price and day-by-day availability, then benchmark your own listing against the set — where your rate ranks, the cheapest and median rates, and an occupancy signal from how many dates each comp has open. It fans the comp-set out, calls GET /v1/price and GET /v1/availability per listing, and correlates both into one report. A revenue-management staple, on a schedule.

- **Base URL:** `https://api.stayingapi.com/v1` (REST) · **MCP:** `https://mcp.stayingapi.com/mcp`
- **Auth:** `Authorization: Bearer stay_live_…` (free sandbox: `stay_test_…`).
- **Get a free key** (no card): https://stayingapi.com/signup · Full machine contract: https://api.stayingapi.com/openapi.json

## Steps

1. **Define the comp-set and your listing** — List the platform, the comma-separated listing ids for the whole comp-set (including your own), which id is yours, and the stay dates.
2. **Price every listing in the set** — The workflow fans the comp-set out and calls GET /v1/price for each listing and the dates, returning a real total per competitor.
3. **Check each listing’s availability** — It also calls GET /v1/availability per listing over the window, so occupancy density (how many dates each comp has open) feeds the benchmark.
4. **Build and deliver the benchmark** — A Code node correlates price and availability by listing, ranks the rates, flags where you sit versus the cheapest and median, and posts the report to Slack — swap for email or a Google Sheet for a weekly digest.

## When to use this

A host, PM or revenue manager wants to benchmark a listing against a defined comp-set — "how does
my rate rank against these five competitors for this week, and how full are they?"

## How to do it

1. Take the `platform`, the comp-set `listingIds` (including your own), `yourListingId`, and the
   `checkIn`/`checkOut` dates.
2. For each listing in the set: call `GET /v1/price` (rate) and `GET /v1/availability` over the
   window (occupancy). Use `@stayingapi/sdk` or the REST endpoints.
3. Correlate by `listingId`: sort the totals to rank your listing, compute the cheapest and median,
   and count each comp's bookable days as a demand signal.

## Cost & scheduling

Cost scales with the comp-set size (one price + one availability call per listing). Run it weekly on
a schedule for a recurring position report. Current per-call credit costs are on the pricing page.

## Partial failures

A listing with no price (a typed error) is free — treat it as "no reading" and rank the rest.
Check `meta.warnings[]` and skip any comp that could not be resolved this run.

### Example — REST

```bash
# Price one comp (repeat per listing in the set)…
curl -sS "https://api.stayingapi.com/v1/price?platform=booking&listingId=abramovic2&checkIn=2026-07-13&checkOut=2026-07-20&currency=EUR" \
  -H "Authorization: Bearer $STAYINGAPI_KEY"
# …and its availability over the same window
curl -sS "https://api.stayingapi.com/v1/availability?platform=booking&listingId=abramovic2&startDate=2026-07-13&endDate=2026-07-20&onlyAvailable=true" \
  -H "Authorization: Bearer $STAYINGAPI_KEY"
```

### Example — @stayingapi/sdk

```ts
import { StayingApiClient } from '@stayingapi/sdk';

const scout = new StayingApiClient({ apiKey: process.env.STAYINGAPI_KEY });
const platform = 'booking';
const compSet = ['abramovic2', 'amadria-park', 'hotel-x'];
const yourId = 'abramovic2';
const dates = { checkIn: '2026-07-13', checkOut: '2026-07-20', currency: 'EUR' };

const rows = [];
for (const listingId of compSet) {
  const { data } = await scout.price({ platform, listingId, ...dates });
  rows.push({ listingId, total: data.totalPrice, currency: data.currency });
}
rows.sort((a, b) => a.total - b.total);
const rank = rows.findIndex((r) => r.listingId === yourId) + 1;
console.log('your rank', rank, 'of', rows.length, '· cheapest', rows[0].total);
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

**Get your free key → https://stayingapi.com/signup** · Docs: https://stayingapi.com/docs · Workflow: https://stayingapi.com/workflows/comp-set-benchmark
