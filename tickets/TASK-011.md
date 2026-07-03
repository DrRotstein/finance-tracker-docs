---
id: TASK-011
type: task
title: "Outstanding transfers endpoint"
story: STORY-03
epic: EPIC-02
owner: backend
status: blocked
priority: P0
estimate: S
created: 2026-07-03T17:03Z
depends_on: [TASK-010]
blocks: [TASK-012]
---

## Description

Implement a dedicated endpoint to retrieve outstanding (incomplete) transfer pairs — transfers where only one leg has been logged.

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/transactions/outstanding` | List all outstanding transfer pairs |

## Acceptance Criteria

- [ ] Returns all transfer_pair relations that have exactly 1 member
- [ ] Response includes: relation_id, the existing transaction details, the linked account (who owes / is owed)
- [ ] Indicates direction: "you owe" (outgoing exists, incoming missing) vs "owes you" (incoming exists, outgoing missing)
- [ ] Supports filter: `account_id` (show outstanding involving specific account/person)
- [ ] Sorted by transaction date DESC (most recent outstanding first)
- [ ] Response includes total outstanding amount (sum)
- [ ] Unit + integration tests

## Technical Notes

- Query pattern from db-schema.md: find transfer_pair relations with count of members = 1
- Consider adding a `summary` field: total owed to user vs total user owes
- This is a read-only analytical endpoint — no mutations
