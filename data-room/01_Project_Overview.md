# TideLinx — Project Overview
**Contest:** Future Caribbean Global AI Buildathon 2026  
**Track:** Finance, Payments & MSME Capital  
**Team:** Ray Kunjal  
**Live:** https://tidelinx.com/ · https://tidelinx.com/floor · https://tidelinx.com/login  
**Deadline context:** 17 August 2026, midnight AST  
**IP:** Patent pending (provisional filed). Not a granted patent.

## Problem
Caribbean customers already pay at the bank. Card-only checkouts still lock the website, ticket, tour, or SKU until someone hunts the statement. There is no open banking in most of the region. Card wallets take a cut. Diaspora and tourist USD never meet the local deposit that should turn a product on. MSMEs delay digital goods they have already been paid for.

Sourced backdrop (not TideLinx revenue): Caribbean e-commerce about **USD $2.8B (2024)** with **72% of online spend leaving on foreign sites** (Hope Research Group). In Trinidad & Tobago, **77% of household MSMEs have no business bank account** (TTIFC/UNCDF 2024 — labeled T&T).

## Solution
TideLinx is matching software. It verifies an **externally executed** payment and names the invoice. **The merchant’s bank holds the funds.** TideLinx is not a wallet, not a custodian, and not a bank login.

1. **Pay** — customer pays at a local bank. Memo is the invoice name.
2. **Ingest (Inara)** — that day’s e-statement as CSV (upload or drop-folder). Eight Trinidad & Tobago e-statement layouts plus a generic CSV. Same file twice is ignored. **No bank login. No portal.**
3. **Match (Mako)** — compare deposit to invoice and write why.
4. **Decide (Deon)** — uncertain rows wait for a human. The label is kept.
5. **Unlock (Una)** — a `payment.matched` webhook may tell a tenant the SKU is paid. **Sister apps are not subscribed today.** No money moves through TideLinx.
6. **Conserve (Felix)** — sandbox ledger halt: USD bills stop if the sandbox USD ledger is short. **No USD pool custody.** Not a licensed FX product.
7. **Floor (Kai)** — operator surface: onboard an invoice, watch the close, sign the uncertain row.

## What is live vs not
**Live:** tidelinx.com (200), `/floor`, `/login`, `GET /api/health` → healthy, `readOnlyBanking: true`. CSV / drop-folder ingest. Match + written rationale. HITL queue. Unlock **emit**. Public Ask (read-only). Sandbox FX halt demo.

**Not live / do not claim:** bank portal login, IMAP, tenant webhook subscription (Juvay and sisters are up as sites, not wired), production FX, customer crypto. Contest-safe GitHub is public: `https://github.com/RAYKUNJAL/tidelinx-future-caribbean` (docs+demo only). Do not submit private `RAYKUNJAL/tidelinx`.

## Business model and GTM
**Wedge:** statement-first collections truth where cards and open banking fail.  
**Tenant zero:** Juvay. Sister sites (PatWaGo, SweetHand, WeFetePass, Likkle Legends, Fresh Catch, Callyuh) are live distribution surface — unlock is not subscribed. trade.juvay.app is a Caribbean B2B landing only — not a live marketplace and not unlocked.  
**Scale:** white-label the same pay-at-bank → match → unlock pattern to any Caribbean digital app.  
**Revenue (modelled, not a forecast):** Juvay ARPU + a thin take on matched volume + white-label seats. Headline for judges: coordination of a multi-billion extra-regional payments system, not year-1 ARR. We do not take the deposit.

## One sentence
TideLinx matches a local-bank deposit to a digital invoice and unlocks the product. The merchant’s bank holds the money.
