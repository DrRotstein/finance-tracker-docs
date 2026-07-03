---
id: EPIC-02
type: epic
title: Core Transaction Tracking (MVP)
parent: null
owner: architect
status: ready
priority: P0
estimate: L
created: 2026-07-03T16:58Z
acceptance:
  - "Users can create, edit, and delete accounts"
  - "Users can log transactions (expense/income/transfer) with amount, from/to account, date, category, optional description"
  - "Transactions can be linked as transfer pairs or grouped under a label"
  - "Outstanding transfers view shows unmatched transfer legs (i.e. 'who owes me what')"
  - "Balance dashboard shows current balance per account, grouped monthly"
  - "Transfers never inflate income or expense totals"
depends_on:
  - EPIC-01
blocks: []
---

## Context

This is the first feature Epic. It delivers the core transaction loop — the three week-1 jobs from onboarding:
1. Log a transaction with account, date, category, description
2. See current balance per account
3. Track money lent/received (modeled as transfer pairs, not a separate loan concept)

## Data model principles (for architect)

- **Three transaction types:** expense, income, transfer.
- **Transfer** = money moves between accounts (internal or via a person). Net zero. Covers: internal transfers, loans, repayments, cash↔PayPal swaps.
- **Transaction relations** are flexible links between transactions:
  - **Transfer pair:** two transactions linked as one logical transfer. Until the return leg is logged, it shows as "outstanding."
  - **Group:** multiple transactions under a shared label/project (e.g. "3 Amazon orders for dorm supplies").
- **Key rule:** if money is coming back or already went out as part of a pair, it is always a **transfer**, never expense/income.

## Stories

### STORY-01: Account management
CRUD accounts. Fields: name, type (bank/cash/paypal/other), starting balance, currency (EUR default). No multi-currency math for MVP.

### STORY-02: Transaction logging
Create a transaction: amount, type (expense/income/transfer), from_account, to_account, date, category, optional description. For expense: from_account required, to_account null. For income: to_account required, from_account null. For transfer: both required (one may be external/person).

### STORY-03: Transaction relations
Link transactions together:
- As a **transfer pair** (two transactions, one outgoing + one incoming, linked as one logical transfer). If only one leg exists → outstanding.
- As a **group** (N transactions under a shared label).
Outstanding transfers view = all transfer-pair links where the return leg is missing.

### STORY-04: Balance dashboard
Show current balance per account (starting balance + sum of transactions). Group transactions by month. Totals for income, expenses, transfers (separate). Transfers must not inflate income/expense.

## Non-goals (this Epic)

- Monthly recurring payments (EPIC-03)
- Group payment splitting with per-person tracking (EPIC-03)
- Categories management UI (use preset list for now)
- Multi-currency support

## Repos

- Backend: https://github.com/DrRotstein/finance-tracker-backend
- Frontend: https://github.com/DrRotstein/finance-tracker-frontend
- Docs: https://github.com/DrRotstein/finance-tracker-docs

## Open questions

- (filled as team discovers them)
