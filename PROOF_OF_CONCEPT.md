# TideLinx Proof of Concept — TLX-POC-MERCURY-001

## Status

The TideLinx reconciliation software path has been validated against the live system. The real settled Mercury payment is in transit (expected 28–31 Aug 2026). Public proof status moves from PENDING to PASS only after the Review step signs the frozen evidence record — the system never marks its own proof complete.

## What TideLinx does, in one paragraph

A customer pays at the bank (or by bank transfer) and writes a payment reference on the transaction — for example TLX-POC-MERCURY-001. The merchant exports the bank statement as a CSV file and uploads it to TideLinx. TideLinx reads the file, finds the payment, checks that the reference, the amount and the currency all match an unpaid invoice, and then tells the connected website that the order is paid so the product, ticket or tour can go live. The merchant keeps the money in their own bank account. TideLinx is matching software — it never holds money and it never logs into a bank.

## How the proof works

1. Create a receivable (an unpaid invoice) with a payment reference and an amount.
2. The connected website order is LOCKED until payment is confirmed.
3. A real payment lands in the bank with the reference on it.
4. The statement is exported as CSV and uploaded to TideLinx.
5. The Mercury adapter detects the file format and parses the transactions.
6. The reconciliation engine matches reference + amount + currency.
7. TideLinx verifies the payment and emits a signed commerce.authorization.created event.
8. The connected website receives the event and releases the order.

The whole chain is linked by one correlation ID, and every step is written to an audit log.

## Test matrix (run live against production)

| Test | What we did | Result (correct behaviour) |
|---|---|---|
| POC-01 Valid payment | Matched a correct reference + amount + currency | PASS — payment verified, order authorized |
| POC-02 Wrong amount | Correct reference, wrong amount | PASS — no automatic authorization (review required) |
| POC-03 Unknown reference | Correct amount, unknown reference | PASS — unmatched, no automatic authorization |
| POC-04 Duplicate transaction | Imported the same payment twice | PASS — duplicate detected, no second authorization |
| POC-05 Same CSV re-uploaded | Uploaded the identical file again | PASS — file duplicate detected, no double authorization |
| POC-06 Invalid CSV | Uploaded a file that is not a CSV | PASS — rejected, no rows accepted |
| POC-07 Changed column headers | Uploaded a CSV with renamed columns | PASS — unknown format flagged, no silent guessing |
| POC-08 Ambiguous transaction | Near-match amount with the same reference | PASS — review required, no automatic authorization |

Every failure case above produced the safe outcome: no money-side action without an exact, verified match.

## Evidence chain (from the live system, redacted)

| Field | Value |
|---|---|
| Proof ID | TLX-POC-MERCURY-001 |
| Institution | Mercury |
| Method | Institution-originated CSV transaction export |
| Expected amount | 10.17 USD |
| Payment reference | TLX-POC-MERCURY-001 |
| Source file SHA-256 | b76286245a7def82addb772082c15e9c717f9077a6262269f968d604a2d61307 |
| Receivable ID | a96c7d15-2f3b-4d40-9588-5399019c92af |
| Authorization ID | auth_4d17ee935826321d |
| Correlation ID | poc_corr_20260826_082A56 |
| Webhook event ID | evt_7e8a0cd9-1b8c-46cb-a078-07e89a9cec8b |

Account numbers, bank credentials and personal data are never stored in this repository.

## What this proves

- A bank payment can be verified without a bank API, using only the statement CSV.
- Matching is deterministic and safe: exact reference + amount + currency, with duplicate protection.
- A verified payment releases a product automatically through a signed webhook.
- Failure cases do not authorize anything by mistake.

## What this does NOT prove

- It does not claim a partnership or integration with Mercury. Evidence is validated using Mercury-originated transaction data.
- It does not hold or move customer money.
- Public proof status stays PENDING until the real settled transfer is recorded and Review signs it.

## Patent

Patent pending. U.S. provisional patent application no. 64/134,982 has been filed for this technology. Do not describe the product as patented; it is patent pending.

See the live pages: https://tidelinx.com/judges and https://tidelinx.com/proof-of-concept
