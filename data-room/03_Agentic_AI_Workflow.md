# TideLinx — Agentic AI Workflow
Six software roles. One close. A human still signs.

This is agentic because each role has a job, tools, shared state, and a **stop condition**. It is not “we call a chatbot on a CSV.”

```
CSV / drop-folder
      │
      ▼
  Inara  ── ingest, ignore a file already seen
      │
      ▼
  Mako   ── propose a match + write why
      │
      ▼
  Deon   ── if uncertain, wait for a human
      │
      ▼
  Una    ── emit payment.matched (tenants not subscribed)
      │
      ▼
  Felix  ── sandbox FX halt if USD ledger is short
      │
      ▼
  Kai    ── floor: onboard, watch, let the operator sign
```

| Agent | Role | Autonomy | Human |
|---|---|---|---|
| **Inara** | Ingest | Read statement CSV / drop-folder. Skip a file already seen. | Bank-format exceptions. No portal. |
| **Mako** | Match | Compare deposit to invoice. Write a rationale. | Does not auto-pay an ambiguous row. |
| **Deon** | HITL | Hold uncertain rows. Apply approve / reject / defer / split. Persist the label. | Every tap is a training label. Split is audit-only in this demo (no auto-allocation). |
| **Una** | Unlock | Emit `payment.matched`. Mark the purchase paid in TideLinx. | Refunds / disputes. **Sister apps not subscribed.** |
| **Felix** | Sandbox FX | Ledger halt if a USD debit would exceed sandbox USD credit. | Treasurer override (logged). **No USD pool custody.** |
| **Kai** | Floor | Operator surface: create the invoice and bank memo, run the close view, route chat to a desk. | Operator signs. |

## Loop properties
- **Shared memory:** operator labels and floor turns. Product log, not a public dataset, not a trained foundation model.
- **Stop conditions:** Deon holds the near-miss; Felix halts USD bills in the sandbox; public Ask cannot approve or seed.
- **Tools:** database, queue, signed webhook, demo sink. Payment tools never transfer — they name an invoice.
- **Reasoning:** deterministic verification first. LLM, if present, explains. It does not get credentials, portal control, or send/transfer/pay.

## Honest limits
Inara’s live path is CSV / drop-folder, not IMAP or bank mail. Una’s emit is wired; Juvay, PatWaGo, and the other sister sites are **not** webhook subscribers. Felix is a conservation demo, not a licensed FX book. Kai’s floor is the judge path; Watch-the-close is a demo, not a production settlement.
