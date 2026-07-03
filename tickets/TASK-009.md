---
id: TASK-009
type: task
title: "DB migration: transaction_relations + members tables + enums"
story: STORY-03
epic: EPIC-02
owner: backend
status: ready
priority: P0
estimate: S
created: 2026-07-03T17:03Z
depends_on: [TASK-005]
blocks: [TASK-010]
---

## Description

Create the database migration for `transaction_relations`, `transaction_relation_members` tables, and associated enums (`relation_type`, `member_role`) as defined in `docs/architecture/db-schema.md`.

## Acceptance Criteria

- [ ] Migration creates `relation_type` enum: `transfer_pair`, `group`
- [ ] Migration creates `member_role` enum: `outgoing`, `incoming`, `member`
- [ ] Migration creates `transaction_relations` table (id, type, label, created_at)
- [ ] Migration creates `transaction_relation_members` table (id, relation_id, transaction_id, role, created_at)
- [ ] Foreign keys with ON DELETE CASCADE on both FKs in members table
- [ ] Unique constraint `uq_relation_transaction` on (relation_id, transaction_id)
- [ ] Indexes: `idx_trm_relation`, `idx_trm_transaction`
- [ ] Migration is reversible
- [ ] TypeORM entities created: `TransactionRelation`, `TransactionRelationMember`

## Technical Notes

- Transfer pair max 2 members enforced at application layer, not DB
- Label is nullable (optional for pairs, expected for groups)
