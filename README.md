# TideLinx — contest-safe repository

Proprietary production components are excluded from the public contest repository. This is not the production reconciliation engine. The repository contains the deployable contest interface, architecture documentation and permitted demonstration components.

**Live interface (the deployable contest demo):**  
https://tidelinx.com/ · https://tidelinx.com/floor · https://tidelinx.com/login · https://tidelinx.com/judges · https://tidelinx.com/proof-of-concept

TideLinx verifies externally executed payments. The merchant’s bank holds the funds. TideLinx is matching software, not a custodian, not a bank login, and not a wallet.

## What is in this tree
| Path | What it is |
|---|---|
| `ARCHITECTURE.md` | High-level deploy shape. No recipe. |
| `AGENT_WORKFLOW.md` | Inara, Mako, Deon, Una, Felix, Kai. |
| `SETUP.md` | How to review the live demo. |
| `RESPONSIBLE_AI.md` | Compliance statement. |
| `LICENSE` | MIT, for this public tree only. |
| `examples/` | Generic CSV. No real accounts. |
| `demo/` | Pointer to the live demo. No parser source. |
| `public-api/` | Public routes only. No secrets. |
| `PROOF_OF_CONCEPT.md` | Redacted evidence chain and POC-01..08 test matrix. |
| `LOGBOOK.md` | Build log and decisions for judges. |

## What is not in this tree
Production matching, bank-statement maps, scoring, prompts, connectors, vault, `.env`, and security internals. Those remain trade secrets. Patent pending. U.S. provisional patent application no. 64/134,982 has been filed for this technology. Do not say patented.

The private repo `https://github.com/RAYKUNJAL/tidelinx` is **not** this repository.

## Honest product facts
- `payment.matched` webhook emit exists; sister apps are not subscribed.
- Conserve/FX is a sandbox ledger halt — no USD pool custody.
- Ingest: 8 TT e-statement CSV layouts + generic CSV. Not a bank login.
- Hope: Caribbean e-comm ~USD $2.8B (2024); 72% of online spend on foreign sites. T&T 77% of household MSMEs with no business account — labeled T&T.
