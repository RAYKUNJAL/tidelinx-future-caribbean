# TideLinx — Contest Logbook

Track: Financial Services. This logbook documents the build, the tests and the evidence behind the TideLinx submission. It is kept up to date alongside the submission.

## The problem

Most Caribbean customers pay by bank transfer or in person at the bank, not by international credit card. Merchants receive payments across Republic Bank, FCB, RBC and Scotiabank. But the banks offer no public API, so merchants reconcile payments by hand — reading WhatsApp screenshots of deposit slips, typing order numbers into spreadsheets, and trusting that the money actually arrived. Orders stay locked until someone manually confirms payment, which is slow and error-prone.

## The idea

TideLinx is matching software. A customer writes a payment reference on their bank payment. The merchant uploads the bank statement CSV. TideLinx matches the reference, amount and currency to the unpaid order, then tells the website to release the product. The money stays in the merchant bank account. No bank login, no custody, no card processing.

## What we built

- A financial-institution adapter layer (Mercury first) that turns any bank CSV export into one common transaction format.
- A deterministic reconciliation engine that matches payments to unpaid invoices and never authorizes on a guess.
- Duplicate protection: the same payment or the same file can never authorize twice.
- A signed webhook that tells connected websites when an order is paid, so the product goes live automatically.
- An audit log and correlation ID that link one payment from the bank statement all the way to the released order.
- A connected-app demo (Juvay, PatWaGo, SweetHand, WeFetePass) showing real websites plugging in through the API.
- A live public interface at https://tidelinx.com with a judges floor.

## Key decisions and why

1. Validation is deterministic, not AI. The AI agent helps read and explain statements and flags uncertain matches, but only the exact-match rules can authorize a payment. This is what makes the system trustworthy enough for money.
2. No bank login, ever. The system only ever receives CSV exports. Bank credentials, OTPs and sessions must never be exposed.
3. Adapter pattern. Every bank can differ, so each bank gets a small adapter that converts its format into the common schema. The reconciliation engine never contains bank-specific logic.
4. Real evidence over simulation. The first proof uses a real 10.17 USD payment into a real Mercury account, exported as the real bank CSV. Simulated transactions are never presented as real proof.

## Testing

- Automated unit and integration tests: 83 tests across 17 test files, all passing. They cover the Mercury adapter (detection, parsing, normalization, amount/date handling), the pipeline, reconciliation, authorization idempotency, webhook signing, replay protection and tenant isolation.
- Live failure battery on production: wrong amount, unknown reference, duplicate transaction, duplicate file, invalid CSV, changed headers and ambiguous transactions — every case produced the safe outcome (no automatic authorization).
- Full loop test: receivable created, real payment matched, payment verified, authorization event emitted, connected order released — completed with the real settled transfer on 31 Aug 2026 (ORDER-POC-001 LOCKED → RELEASED).

## Evidence

See PROOF_OF_CONCEPT.md in this repository. The redacted evidence chain (source file SHA-256, authorization ID, correlation ID, webhook event ID) is recorded from the live system. The real settled transfer (10.17 USD, settled 28 Aug 2026) was recorded and verified on 31 Aug 2026. Public proof status remains PENDING until the Review step signs the frozen record.

## Patent

Patent pending. U.S. provisional patent application no. 64/134,982 has been filed for this technology.

## What is next

- Complete the Review sign-off on the frozen record so public proof moves to PASS.
- Add Republic Bank, First Citizens, RBC and Scotiabank CSV adapters (layout work is partially mapped).
- Publish the connected-app API contract for third parties who want to link their websites to TideLinx.
- Record the Loom demo video (90 seconds – 3 minutes maximum, per contest rules) for the submission.

## Log entries

- 2026-08-17: Contest-safe public repository published at github.com/RAYKUNJAL/tidelinx-future-caribbean.
- 2026-08-24: Master build specification written (real-bank POC and CSV ingestion spec).
- 2026-08-26: Full test suite run and green (83 tests). POC-01..08 validated live against production. Evidence package regenerated from the frozen record. Real 10.17 USD Mercury transfer initiated (arrives 28–31 Aug).
- 2026-08-31: Real settled Mercury transfer recorded and verified end to end. The 10.17 USD payment (settled 28 Aug) was exported from Mercury as the real CSV, uploaded to TideLinx, matched by exact reference + amount + currency, and ORDER-POC-001 moved from LOCKED to RELEASED via the signed webhook. Evidence package regenerated from the frozen record (new file SHA-256, authorization and correlation IDs).
