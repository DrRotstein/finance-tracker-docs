---
id: TASK-001
type: task
title: "DB migration: accounts table + account_type enum"
story: STORY-01
epic: EPIC-02
owner: backend
status: ready
priority: P0
estimate: S
created: 2026-07-03T17:03Z
depends_on: []
blocks: [TASK-002]
---

## Description

Create the initial database migration that sets up the `accounts` table and `account_type` enum as defined in `docs/architecture/db-schema.md`.

## Acceptance Criteria

- [ ] Migration creates `account_type` enum: `bank`, `cash`, `paypal`, `person`, `other`
- [ ] Migration creates `accounts` table with all columns per schema (id, name, type, starting_balance, currency, is_external, created_at, updated_at)
- [ ] All constraints applied: NOT NULL, defaults (type='bank', starting_balance=0.00, currency='EUR', is_external=false)
- [ ] Indexes created: `idx_accounts_type`, `idx_accounts_is_external`
- [ ] Migration is reversible (down drops table + enum)
- [ ] TypeORM entity class created for `Account`

## Technical Notes

- Use TypeORM migration CLI to generate + customize
- UUID PK with `gen_random_uuid()` default
- `updated_at` should auto-update (use TypeORM `@UpdateDateColumn`)
