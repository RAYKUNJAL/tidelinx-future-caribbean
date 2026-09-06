# TideLinx — IP Defensibility Statement
**Status:** Patent pending (provisional filed). Do not say “patented.”  
**Owner:** Ray Kunjal / TideLinx  
**This package:** contest-safe description only. No implementation recipe.

## What is claimed at a high level
A statement-first matching layer for markets without open banking: a merchant’s customer pays at the merchant’s own bank; software names the invoice; a signed unlock may tell a tenant the SKU is paid; a conservation halt can stop USD bills when a sandbox USD ledger is short. TideLinx verifies externally executed payments. It does not hold the money.

That idea is **provider-agnostic**. It does not depend on a single LLM vendor, a single bank API, or a single cloud. Ingest is a file the merchant already has. Matching is deterministic verification with a human on ambiguous rows. An optional model may explain; it is not the source of truth.

## What is not in this package
The **trade-secret implementation layer** stays out of the contest tree and out of any public repo:

- production matching internals
- bank-statement layout maps
- scoring and thresholds
- prompts and safety-stub text
- connector and vault material
- `.env` and operational secrets

The existing private repository `https://github.com/RAYKUNJAL/tidelinx` contains crown jewels. It is **not** the contest-safe repository and must not be submitted or made public as the judge artifact.

## Defensibility without a recipe
- **Filed position:** provisional application on file (patent pending).
- **Know-how:** labeled operator decisions on real Caribbean memos — a data moat, not a prompt dump.
- **Distribution:** live sister apps as a white-label path; unlock subscription is still the missing wire.
- **Architecture choice:** not a custodian, so the product is software + webhook, not a competing balance sheet.

Judges and partners may review this statement, the live demo, and the contest-safe tree. They may not be given parser maps, weights, or hash recipes. Future Caribbean receives a non-exclusive licence to feature the project; TideLinx retains ownership.
