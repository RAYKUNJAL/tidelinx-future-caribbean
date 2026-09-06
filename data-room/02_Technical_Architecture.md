# TideLinx — Technical Architecture
Contest-safe. No match recipe, no parser column maps, no scoring weights, no secrets.

## Deployed shape
Live at https://tidelinx.com.

```
Merchant bank (holds funds)
        │  e-statement CSV / drop-folder
        ▼
┌─────────────┐   ┌──────────────┐   ┌─────────────┐
│  Next web   │──▶│  Fastify API │──▶│   Worker    │
│  /  /floor  │   │  /api/*      │   │  ingest     │
│  /login     │   └──────┬───────┘   └─────────────┘
└─────────────┘          │
                    Postgres + Redis
                          │
          ┌───────────────┼────────────────┐
          ▼               ▼                ▼
   HITL queue      payment.matched    sandbox FX
   (Deon)          emit (Una)         halt (Felix)
```

Stack: Next.js operator/public UI, Fastify API, background worker, PostgreSQL, Redis, Docker behind Caddy/Coolify. Health: `GET https://tidelinx.com/api/health` → `{"status":"healthy","service":"tidelinx-api","readOnlyBanking":true}`.

## Data in
- Merchant-created receivables (invoice + bank memo).
- Merchant-supplied statement files: **8 TT e-statement CSV layouts + generic CSV**.
- Operator approve / reject / defer labels.

TideLinx does **not** log into banks, scrape portals, or store portal credentials for unattended control. Portal automation is gated and unused. IMAP is not live.

## Data out
- A written match rationale and a queue state.
- `payment.matched` webhook **emit** (signed). Destination allowlisted. **Sister apps are not subscribed.**
- Sandbox conserve ledger: halt if a USD debit would exceed sandbox USD credit. **No custody, no conversion, no payout, no customer crypto.**

## Isolation and access
Tenant-scoped records. Role-based operator access. Auth-gated admin APIs. Public contest surface is listed in the companion repo under `public-api/` (health, public Ask, demo seed, webhook sink). Cookies are httpOnly. No `.env` or vault material is in this package.

## What this package excludes
Production matching internals, bank-map parsers, scoring, prompts, connector secrets, and security runbooks. Those stay in the private implementation layer. See `05_IP_Defensibility_Statement.md` and `09_CONFIDENTIAL_IP_NOTICE.md`.

## Models and tools (honest)
Deterministic verification is the source of truth. An optional hosted LLM may polish a rationale or answer public Ask. If no key is present, templates and a grounded FAQ run. The model does not approve payments or move money. No custom-trained foundation model on deposits. No Plaid / open banking. No Twilio in this pass.
