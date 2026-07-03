---
id: TASK-002
type: task
title: "Accounts CRUD API endpoints"
story: STORY-01
epic: EPIC-02
owner: backend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-001]
blocks: [TASK-004, TASK-006]
---

## Description

Implement REST API endpoints for account management (create, read, update, delete).

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| POST | `/accounts` | Create a new account |
| GET | `/accounts` | List all accounts (with optional filter: `?type=bank&is_external=false`) |
| GET | `/accounts/:id` | Get single account by ID |
| PUT | `/accounts/:id` | Update account fields |
| DELETE | `/accounts/:id` | Delete account (fails if transactions exist) |

## Acceptance Criteria

- [ ] All 5 endpoints functional and returning proper HTTP status codes
- [ ] Input validation: name required (max 100 chars), type must be valid enum, currency is 3-char ISO code
- [ ] DELETE returns 409 if account has linked transactions
- [ ] GET /accounts supports query params: `type`, `is_external`
- [ ] Proper error responses (400 validation, 404 not found, 409 conflict)
- [ ] Unit tests for service layer
- [ ] Integration tests for each endpoint

## Technical Notes

- Use NestJS controller + service + repository pattern
- DTO validation with class-validator
- Return account with computed `current_balance` field on GET endpoints (use the balance query from db-schema.md)
