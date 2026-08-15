---
name: open-banking-io
description: |
  open-banking.io integration. Read bank account balances and transactions from European banks via PSD2 open banking APIs. Use when the user wants to check balances, list recent transactions, categorise spending, or reconcile payments across EU/UK bank accounts — without eIDAS certificates or AISP licences.
compatibility: Requires network access and an open-banking.io account (free tier available). Authenticates with an API key; sensitive fields are end-to-end encrypted and decrypted locally with your private key.
license: MIT
homepage: https://open-banking.io
repository: https://github.com/open-banking-io/skills
metadata:
  author: open-banking-io
  version: "1.0"
  categories: finance, banking, open-banking, psd2, accounting
---

# open-banking.io

Self-serve PSD2 bank-data API for EU/UK accounts: accounts, balances and
transactions behind an API key — no eIDAS QWAC/QSealC certificates required.

## When to use

- "What's my balance on <bank>?"
- "Summarise last month's transactions" / "How much did I spend on groceries?"
- "Which of my bank connections need re-consent?"
- Reconciling invoices/payments against bank statement lines

## Tool surface

Prefer the official MCP server (read-only tools: `list_accounts`,
`get_balances`, `get_transactions`, `list_connections`):
https://github.com/open-banking-io/mcp-server

## Configuration

- `OBI_CREDENTIALS` — path to (or inline JSON of) the credentials bundle
  exported from the open-banking.io app (preferred), or
- `OBI_API_KEY` + `OBI_PRIVATE_KEY` + `OBI_BASE_URL` (split env vars)

## Notes

- Read-only by design: no payments, no consent management through this skill.
- PSD2 consents expire (~90 days typical, bank-dependent): surface
  `needs_reconnect` / `valid_until` to the user instead of retrying silently.
- Transactions carry stable bank-side IDs — dedupe on them rather than
  (amount, date) pairs.
