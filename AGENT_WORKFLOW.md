# Agent workflow (contest-safe)

Six software agents, one daily close.

1. **Inara — ingest.** Read the merchant’s statement file (CSV upload or drop-folder). Ignore a file already seen. No bank login.
2. **Mako — match.** Compare the deposit to the invoice. Write why. Do not auto-pay an ambiguous row.
3. **Deon — HITL.** Hold uncertain rows. Operator approves, rejects, defers, or splits (split is audit-only in this demo). The label is saved.
4. **Una — unlock.** Emit `payment.matched`. Mark the purchase paid inside TideLinx. Sister apps are not subscribed, so this does not light a storefront today.
5. **Felix — sandbox FX.** If a USD debit would exceed sandbox USD credit, halt. No custody, no conversion, no customer crypto.
6. **Kai — floor.** Operator surface: create the invoice and memo, watch the close, route a question to a desk. A human still signs.

Stop conditions: Deon (human), Felix (sandbox halt), public Ask (read-only — cannot approve).

Shared memory is operator labels and floor turns. Not a trained foundation model on deposits.
