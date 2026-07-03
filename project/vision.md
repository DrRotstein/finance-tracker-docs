---
slug: finance-tracker
created: 2026-07-03T15:09Z
deadline: none (ship incrementally ASAP)
status: onboarding
---
# Vision

This project exists so that Finn can track his expenses, income, transactions, and transfers better than today.

## Target users

Dual student with limited income, managing personal finances + a dorm cashier account, with frequent cross-account transfers (bank ↔ dorm, cash ↔ PayPal, informal friend loans).

## Top jobs to be done

1. Log a transaction (expense/income) with account, date, category, and optional description
2. See current balance of each account
3. Log money lent to / received back from a friend (split tracking)

## Non-goals

- Not a group-expense tracker
- Not a forecasting tool (yet)
- Not a bank integration (yet)
- Not mobile-native (yet)

## Constraints

- Deadline: None — ship incrementally ASAP
- Budget: €20/month max on infra/services
- Stack: NestJS + TypeScript, PostgreSQL + TypeORM, React, Docker per repo (open to architect pushback via ADR-001)
