---
name: stayingapi-availability-alert
description: Watch a listing over a date window and get alerted the moment a wanted date becomes available. Powered by the StayingAPI REST API / MCP server.
version: 1.0.0
homepage: https://stayingapi.com/workflows/availability-alert
license: Proprietary — see https://stayingapi.com/terms
tools: [availability, listing]
auth: bearer-api-key | oauth2-pkce
---

# Property availability watch → alert

Given a known listing (or a batch) and a date window, poll day-by-day availability on a schedule and alert the instant a wanted date becomes bookable. It calls GET /v1/availability with onlyAvailable=true, flattens the returned calendar, de-dups against the previous run so you are only pinged on a real change, and posts the newly-available dates. This is the automation twin of the App’s availability-alert saved search.

- **Base URL:** `https://api.stayingapi.com/v1` (REST) · **MCP:** `https://mcp.stayingapi.com/mcp`
- **Auth:** `Authorization: Bearer stay_live_…` (free sandbox: `stay_test_…`).
- **Get a free key** (no card): https://stayingapi.com/signup · Full machine contract: https://api.stayingapi.com/openapi.json

## Steps

1. **Pick the listing and the date window** — Set the platform, the listing id (or a full listing URL), and the start / end dates to watch (window ≤ 365 days, not in the past).
2. **Poll availability on a schedule** — Every few hours the workflow calls GET /v1/availability with onlyAvailable=true, returning the day-by-day calendar for the listing.
3. **Detect what newly became available** — A Code node flattens the calendar to the bookable dates and compares them to the previous run (stored in n8n static data), so you are alerted only when the available set changes — no duplicate pings.
4. **Send the availability alert** — When a wanted date opens up, a message listing the newly-available dates is posted to Slack — swap the last node for email, Telegram, a webhook or Discord.

## When to use this

The user wants to know when a specific stay (or one of a batch) becomes bookable over a date
window — e.g. "tell me when this Airbnb opens up for my week." Reach for `availability`.

## How to do it

1. Take `platform` + `listingId` (or a full listing `url`) and the `startDate`/`endDate` window
   (≤ 365 days, not in the past).
2. Call `GET /v1/availability` with `onlyAvailable=true` (or the `check_availability` MCP tool, or
   `@stayingapi/sdk`).
3. Flatten `data[].dates[]` and keep the entries where `available && bookable`. Compare to what you
   saw last time and report only the NEWLY-available dates so you never notify twice.

## Scheduling

To watch continuously, re-run on a cadence (n8n Schedule Trigger, or your agent’s scheduler). Each
re-run is a real billed call — align the cadence to the 6-hour availability cache so you are not
paying for identical results.

## Partial failures

Check `meta.partial` and `meta.warnings[]`; a listing that returns no calendar is charged 0. Report
what you have.

### Example — REST

```bash
curl -sS "https://api.stayingapi.com/v1/availability?platform=airbnb&listingId=42307961&startDate=2026-07-13&endDate=2026-07-20&onlyAvailable=true" \
  -H "Authorization: Bearer $STAYINGAPI_KEY"
```

### Example — @stayingapi/sdk

```ts
import { StayingApiClient } from '@stayingapi/sdk';

const scout = new StayingApiClient({ apiKey: process.env.STAYINGAPI_KEY });

const { data } = await scout.availability({
  platform: 'airbnb',
  listingId: '42307961',
  startDate: '2026-07-13',
  endDate: '2026-07-20',
  onlyAvailable: true,
});

const open = data.flatMap((l) => l.dates).filter((d) => d.bookable).map((d) => d.date);
console.log(open.length, 'bookable dates', open.join(', '));
```

## MCP (no key pasted into the agent)

On an MCP-capable runtime, connect the StayingAPI server at **https://mcp.stayingapi.com/mcp** (OAuth 2.1 + PKCE) and use:
- `check_availability` — day-by-day availability for a known listing over a date window.

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

**Get your free key → https://stayingapi.com/signup** · Docs: https://stayingapi.com/docs · Workflow: https://stayingapi.com/workflows/availability-alert
