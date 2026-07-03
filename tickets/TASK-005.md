---
id: TASK-005
type: task
title: "DB migration: transactions table + transaction_type enum + constraints"
story: STORY-02
epic: EPIC-02
owner: backend
status: ready
priority: P0
estimate: S
created: 2026-07-03T17:03Z
depends_on: [TASK-001]
blocks: [TASK-006]
---

## Description

Create the database migration for the `transactions` table, `transaction_type` enum, and all associated constraints/indexes as defined in `docs/architecture/db-schema.md`.

## Acceptance Criteria

- [ ] Migration creates `transaction_type` enum: `expense`, `income`, `transfer`
- [ ] Migration creates `transactions` table with all columns per schema
- [ ] CHECK constraint `chk_transaction_accounts` enforced (from_account/to_account rules per type)
- [ ] CHECK constraint `chk_amount_positive` enforced (amount > 0)
- [ ] Foreign keys to `accounts(id)` on from_account_id and to_account_id
- [ ] All indexes created: `idx_transactions_date`, `idx_transactions_type`, `idx_transactions_from_account` (partial), `idx_transactions_to_account` (partial), `idx_transactions_category` (partial)
- [ ] Migration is reversible
- [ ] TypeORM entity class created for `Transaction` with relations to `Account`

## Technical Notes

- Partial indexes use WHERE clause (TypeORM supports via `@Index` decorator with `where` option)
- FK columns are nullable per schema design
