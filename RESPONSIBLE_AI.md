# TideLinx — Compliance and Responsible AI
**Required statement (300–500 words).** Patent pending (provisional filed). TideLinx is not a custodian.

TideLinx is matching software. Customers pay at a local bank. The merchant’s bank holds the funds. TideLinx verifies that an externally executed payment belongs to an invoice and may then emit a `payment.matched` signal. It does not take deposits, operate a wallet, initiate transfers, or log into banks. If TideLinx goes down, there is no TideLinx balance to empty.

Data minimization is the default. Live ingest is a merchant-supplied e-statement CSV or drop-folder file, plus receivables the merchant already created. We keep the fields needed to name an invoice — date, amount, memo, payer label — not a full customer banking profile and not a bank-login session. Unnecessary account credentials, portal cookies, and unused bank-info fields are not retained. The public health flag is `readOnlyBanking: true`.

Encryption, tenant isolation, and role-based access protect operator data. Sessions use httpOnly cookies. Admin surfaces require authentication. One merchant’s statements and labels are not another merchant’s. Role-based access limits who can approve a match. Audit logs record ingest, match proposals, human decisions, and unlock emits.

Ambiguous matches wait for a human (Deon). Verification is deterministic first: the match agent compares statement evidence to an invoice and writes a rationale. An LLM, if present, may polish language or answer public Ask. It does not approve payments, move money, or run uncontrolled tools. Public Ask is read-only Q&A and cannot seed, approve, or reveal secrets.

We treat finance-adjacent automation as sensitive. GDPR and CCPA/CPRA awareness applies if EU or California residents later appear (diaspora checkout, operator accounts): purpose limitation, access, deletion on request, and no sale of personal information. Caribbean data sovereignty: statement data stays with the merchant’s bank and the merchant’s operator console. We do not train a foundation model on deposits. We are not claiming a completed DPIA, a money-transmitter licence, or production-ready FX.

Bias mitigation starts from noisy Caribbean bank memos. Exact rows may auto-reconcile; uncertain rows stay in queue until a person signs. TideLinx does not social-score payers and does not collect or profile biometrics. Responsible AI here means a stop condition — human sign-off on ambiguous matches, and a sandbox FX halt with no USD pool custody — plus honest limits: sister apps are not subscribed to `payment.matched`; Conserve/FX is a ledger stop, not a licensed exchange; TideLinx is not a bank, EMI, or money transmitter.

The contest-safe public tree is MIT-licensed documentation and permitted demo surface. Production matching, bank maps, scoring, and prompts remain excluded trade secrets.
