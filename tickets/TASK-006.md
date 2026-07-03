---
id: TASK-006
type: task
title: "Transactions CRUD API endpoints with filtering"
story: STORY-02
epic: EPIC-02
owner: backend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-002, TASK-005]
blocks: [TASK-008, TASK-010]
---

## Description

Implement REST API endpoints for transaction management with filtering and pagination.

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| POST | `/transactions` | Create a new transaction |
| GET | `/transactions` | List transactions (filtered, paginated) |
| GET | `/transactions/:id` | Get single transaction with account details |
| PUT | `/transactions/:id` | Update transaction |
| DELETE | `/transactions/:id` | Delete transaction (cascades relation members) |

## Acceptance Criteria

- [ ] All 5 endpoints functional with proper HTTP status codes
- [ ] POST validates account rules per type (expense needs from_account, income needs to_account, transfer needs both)
- [ ] POST validates referenced account IDs exist
- [ ] GET /transactions supports filters: `type`, `account_id` (matches from or to), `category`, `date_from`, `date_to`
- [ ] GET /transactions supports pagination: `page`, `limit` (default 20, max 100)
- [ ] GET /transactions returns total count in response metadata
- [ ] Results sorted by date DESC by default, with optional `sort` param
- [ ] PUT does not allow changing `type` (would violate account constraints)
- [ ] Proper error responses (400, 404, 422)
- [ ] Unit tests for service layer
- [ ] Integration tests for each endpoint

## Technical Notes

- Use NestJS controller + service + repository
- DTO validation with class-validator (different DTOs for create vs update)
- Response includes populated account names (not just IDs)
- Amount stored positive; no sign flipping needed at API layer
