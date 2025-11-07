# Seed 1 Design Document — First Draft

Status: Draft  
Reference: docs/prd_v1.2_final.md

## Overview
This document expands the PRD into a concrete Seed 1 (Minimum Lovable Product) design. It captures architecture, user flows, data handling, privacy constraints, and open questions to enable implementation planning and handoff.

## Goals
- Deliver Seed 1 features: URL shortener, Tracking URL builder, QR generator, Public/private text sharer.
- Respect privacy-first constraints (no third-party trackers, expirable data).
- Produce a draft suitable for implementation and review.

## Scope (Seed 1)
- URL shortening service with optional tracking parameters and expiry.
- QR code generation for shortened URLs.
- Simple public/private text sharing endpoint (anonymous).
- Optional: secure file sender is out of scope for initial Seed 1 delivery (TBD).

## Architecture
- Monorepo layout (high-level):
  - apps/ (Expo Universal App)
  - packages/ (shared, UI components, utils)
  - api/ (Router API Routes backend)
  - docs/
- Hosting: Expo / Vercel for frontend; edge/serverless functions for APIs.
- Storage options:
  - Short-term key-value store (edge KV) for short URLs & metadata (preferred for low-latency, TTL support).
  - Fallback: serverless DB or object store with TTL for durability.

## API surface (high-level)
- POST /api/shorten
  - payload: { url, ttl?, trackingParams? }
  - response: { shortId, shortUrl }
- GET /:shortId
  - redirects to original URL, records anonymous stats if enabled
- POST /api/text
  - payload: { text, visibility: public|private, ttl? }
  - response: { id, url }
- POST /api/qr
  - payload: { url, size? }
  - response: { qrDataUrl }

Note: Keep API surfaces minimal; all analytics collection must be anonymous and opt-in at feature level.

## Data Flow
- Client submits creation request → API route validates and persists to KV with TTL.
- Redirect path reads KV by shortId → performs redirect; optionally increments an anonymized counter.
- For tracking, store only aggregated counters or ephemeral events; do not store identifying data.

## User Flows
- Shorten a URL:
  1. User inputs long URL, optionally sets expiry and tracking params.
  2. Client calls /api/shorten → receives shortUrl → user can copy/share or generate QR.
- Generate QR:
  1. User selects short URL → requests QR generation → receives image/data URL.
- Share text (public/private):
  1. User posts text → receives shareable link; private items include a secret token in the URL.

## Privacy & Security
- No third-party tracking or analytics by default.
- Analytics must be anonymous (no IP logging or PII); prefer aggregated counters in KV.
- TTLs: allow creators to set reasonable expiries; default expiry applied for anonymous shares.
- Private shares: include a secret token that is part of the URL path or fragment; store only the content and a token hash if necessary.
- Rate limiting / abuse mitigation: apply per-IP or per-key throttles at the edge.

## Tradeoffs
- Edge KV (fast, TTL) vs. traditional DB (durable, queryable):
  - Use edge KV for speed and TTL semantics for Seed 1.
  - Add a persistence sync to a DB for long-term analytics in later seeds if needed.
- No-login model simplifies UX but limits accountability and advanced features (custom domains, per-user dashboards) to later seeds.

## Open Questions & Risks
- Should we support per-link passwords vs. token-in-URL for private shares?
- How strict should default TTL be for anonymous shared content?
- Abuse vectors: link spam, resource usage—what is the initial rate limit policy?
- Hosting costs and scaling: estimate cost model for anticipated Seed 1 load.

## Acceptance Criteria (for this draft)
- Document includes sections: Overview, Goals, Architecture, Data Flow, User Flows, Privacy/Security, Tradeoffs, Open Questions, Acceptance Criteria.
- References docs/prd_v1.2_final.md.
- Contains actionable next steps and a small list of open questions for the maintainers to decide.
- Suitable for conversion into implementation issues/PRs.

## Next steps (for reviewers)
- Review architecture decisions (edge KV vs DB) and confirm defaults for TTL and rate limits.
- Answer open questions and mark items for implementation in tracked issues.
- Move to implementation backlog once architecture choices are confirmed.
