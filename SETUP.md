# Setup — review the contest demo

This repository does **not** ship the production matching engine. The deployable contest interface is already live.

## 1. Open the live demo
- Public story: https://tidelinx.com/
- Agent floor: https://tidelinx.com/floor
- Operator login: https://tidelinx.com/login

## 2. Confirm the API is up
```bash
curl -sS https://tidelinx.com/api/health
```
Expect JSON: `status=healthy`, `readOnlyBanking=true`.

## 3. Optional public Ask (read-only)
```bash
curl -sS -X POST https://tidelinx.com/api/public/ask \
  -H 'content-type: application/json' \
  -d '{"question":"Are you a bank?"}'
```
This box cannot approve payments or reveal secrets.

## 4. Generic sample file
See `examples/sample-statement.csv`. It is a teaching file: date, description, amount, currency, reference. No real account numbers. It is **not** a bank-layout map.

## 5. What you should not do
- Do not clone or publish `github.com/RAYKUNJAL/tidelinx` (private, crown jewels).
- Do not add parser maps, scoring, prompts, or `.env` to this tree.
- Do not claim a wired unlock to Juvay or other sister apps.
