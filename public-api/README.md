# public-api

Permitted public routes on the live deploy. No secrets. No admin recipes.

| Method | Route | What it does |
|---|---|---|
| GET | `/api/health` | Liveness. Returns `healthy` and `readOnlyBanking: true`. |
| POST | `/api/public/ask` | Read-only Q&A. Cannot approve, seed, or dump secrets. |
| POST | `/api/demo/seed` | Sandbox fixture load for the floor demo. |
| POST | `/api/webhooks/sink` | Demo sink that can receive a `payment.matched` emit. |

Base: `https://tidelinx.com`

Admin, inbox, candidates, agent-chat, and bank-connection routes are **not** public and are not documented here.

Do not commit API keys, webhook secrets, or session cookies to this folder.
