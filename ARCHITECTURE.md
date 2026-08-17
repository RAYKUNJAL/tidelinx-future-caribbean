# Architecture (contest-safe)

```
Customer ── pays at local bank ──▶ merchant account (funds stay here)
                                      │
                                      │ e-statement CSV / drop-folder
                                      ▼
                              TideLinx matching layer
                         (Inara → Mako → Deon → Una → Felix)
                                      │
                                      ├── operator floor (Kai)
                                      └── payment.matched emit
                                           (sister apps not subscribed)
```

**Runtime (live):** Next.js public/operator UI, Fastify API, worker, PostgreSQL, Redis, Docker.

**Health:** `GET https://tidelinx.com/api/health` → healthy, `readOnlyBanking: true`.

**Ingest:** merchant file. Eight Trinidad & Tobago e-statement CSV layouts plus generic CSV. No portal. No open banking.

**Verify:** deterministic comparison of a statement row to an invoice, with a written rationale. Ambiguous rows wait for a human.

**Unlock:** signed `payment.matched` webhook. Emit is live. Tenants are not subscribed.

**Conserve:** sandbox ledger halt. TideLinx does not hold a USD pool.

**Excluded from this repo:** matching internals, parser maps, weights, prompts, secrets.
