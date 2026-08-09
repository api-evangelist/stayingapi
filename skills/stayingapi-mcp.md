---
name: stayingapi-mcp
description: Connect an AI agent to the StayingAPI Model Context Protocol (MCP) server for accommodation search, availability, pricing, cross-OTA price comparison and reviews. Use when the agent runtime supports MCP connectors (e.g. Claude) and you want OAuth-based access without managing API keys. Covers the OAuth 2.1 + PKCE connect flow, the seven read-only tools, and when to prefer MCP vs REST.
license: Proprietary — see https://stayingapi.com/terms
---

# StayingAPI — connect the MCP server

StayingAPI ships a native **Model Context Protocol** server so an agent can query
accommodation data across Airbnb, Booking.com, Vrbo and Google Hotels as first-class
tools — no API key pasted into the agent.

- Server URL: **https://mcp.stayingapi.com/mcp** (Streamable HTTP transport).
- Auth: **OAuth 2.1 + PKCE (S256)** with dynamic client registration. You authorize
  once in a browser popup; the connector is linked to your StayingAPI account and its
  credit balance.
- OAuth protected-resource metadata (RFC 9728): https://mcp.stayingapi.com/.well-known/oauth-protected-resource

## Connect (Claude.ai / Claude Desktop / Claude Code)
1. Open your agent's connector settings and **add a custom connector** (MCP server).
2. Use the URL `https://mcp.stayingapi.com/mcp`.
3. Complete the **OAuth** prompt in the browser popup — this links the connector to your
   StayingAPI account. (First-time users: create an account and verify email first; a
   sandbox account works for evaluation. See https://stayingapi.com/docs/mcp.)
4. The seven tools below become available to the agent.

## The seven read-only tools
- `search_stays` — search stays across platforms by location, dates, occupancy, filters.
- `check_availability` — day-by-day availability for a known listing over a date window.
- `get_listing` — full detail for one listing (amenities, photos, host, ratings).
- `get_price` — a real price quote for one listing for specific dates + occupancy.
- `compare_prices` — compare one property across OTAs with computed min + median.
- `get_reviews` — normalized, paginated reviews for one listing on one platform.
- `get_job` — poll status + fetch results of an async scrape job (costs 0).

## Async behavior
The tools share the same async contract as REST: a live call that has to scrape returns
a pending job; the agent (or the tool layer) polls `get_job` with the returned `jobId`
until it reaches a terminal state, and the result payload arrives under `data.result`. A job can
terminate as `failed` as well as `completed` — if it does, stop polling and report
`data.error`; do not keep polling a failed job. Sandbox and
cache hits return immediately.

## Credits & limits
MCP calls draw from the **same single credit balance** as your REST keys, but are
rate-limited on a **separate per-user bucket**. Costs and rate limits: https://stayingapi.com/pricing.

## MCP vs REST — which to use
- **MCP** — best for interactive agents/assistants (e.g. Claude) that support connectors:
  OAuth instead of key management, tools surfaced natively to the model.
- **REST** (skill: stayingapi-search) — best for programmatic backends, servers, cron
  jobs, and any runtime without MCP support: a Bearer key + the `@stayingapi/sdk`.

Both hit the same data and the same unified schema. Docs: https://stayingapi.com/docs/mcp.
