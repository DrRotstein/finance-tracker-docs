---
id: TASK-010
type: task
title: "Transaction relations API (pairs + groups + linking)"
story: STORY-03
epic: EPIC-02
owner: backend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-006, TASK-009]
blocks: [TASK-011, TASK-013]
---

## Description

Implement API endpoints for creating, listing, and managing transaction relations (both transfer pairs and groups).

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| POST | `/relations/transfer-pair` | Create a transfer pair (1 or 2 transaction IDs) |
| POST | `/relations/group` | Create a group with label + transaction IDs |
| GET | `/relations` | List relations (filter by type) |
| GET | `/relations/:id` | Get relation with all member transactions |
| POST | `/relations/:id/members` | Add a transaction to existing relation |
| DELETE | `/relations/:id/members/:transactionId` | Remove a transaction from a relation |
| DELETE | `/relations/:id` | Delete entire relation (cascades members) |

## Acceptance Criteria

- [ ] Transfer pair creation validates: max 2 members, roles must be `outgoing` + `incoming`, transactions must be of type `transfer`
- [ ] Transfer pair can be created with 1 member (outstanding) — second added later via POST members
- [ ] Group creation requires label, accepts 1+ transaction IDs, all get role `member`
- [ ] GET /relations supports filter: `type=transfer_pair|group`
- [ ] GET /relations/:id returns full member details (transaction + account names)
- [ ] Cannot add same transaction to a relation twice (unique constraint → 409)
- [ ] Application-layer validation: transfer_pair cannot exceed 2 members
- [ ] Unit + integration tests

## Technical Notes

- Service validates business rules (type constraints, member limits)
- Consider: when creating a transaction of type=transfer, auto-suggest creating a transfer pair
