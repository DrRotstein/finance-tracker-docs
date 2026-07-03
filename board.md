# Board — finance-tracker

_Updated: 2026-07-03T17:03Z_

## Epics

| ID | Title | Status | Stories | Priority |
|---|---|---|---|---|
| EPIC-01 | Onboarding & stack selection | done | — | P0 |
| EPIC-02 | Core Transaction Tracking (MVP) | in-progress | STORY-01, STORY-02, STORY-03, STORY-04 | P0 |

## Stories

| ID | Title | Epic | Owner | Status | Priority |
|---|---|---|---|---|---|
| STORY-01 | Account management | EPIC-02 | — | ready | P0 |
| STORY-02 | Transaction logging | EPIC-02 | — | blocked-by:STORY-01 | P0 |
| STORY-03 | Transaction relations | EPIC-02 | — | blocked-by:STORY-02 | P0 |
| STORY-04 | Balance dashboard | EPIC-02 | — | blocked-by:STORY-02 | P0 |

## Tasks

| ID | Title | Story | Owner | Status | Depends On |
|---|---|---|---|---|---|
| TASK-001 | DB migration: accounts table + account_type enum | STORY-01 | backend | ready | — |
| TASK-002 | Accounts CRUD API endpoints | STORY-01 | backend | blocked | TASK-001 |
| TASK-003 | Account list page + account card component | STORY-01 | frontend | blocked | TASK-002 |
| TASK-004 | Account create/edit form + delete confirmation | STORY-01 | frontend | blocked | TASK-002, TASK-003 |
| TASK-005 | DB migration: transactions table + constraints | STORY-02 | backend | ready | TASK-001 |
| TASK-006 | Transactions CRUD API endpoints with filtering | STORY-02 | backend | blocked | TASK-002, TASK-005 |
| TASK-007 | Transaction list page with filters | STORY-02 | frontend | blocked | TASK-006 |
| TASK-008 | Transaction create/edit form (dynamic fields by type) | STORY-02 | frontend | blocked | TASK-006, TASK-007 |
| TASK-009 | DB migration: transaction_relations + members tables | STORY-03 | backend | ready | TASK-005 |
| TASK-010 | Transaction relations API (pairs + groups + linking) | STORY-03 | backend | blocked | TASK-006, TASK-009 |
| TASK-011 | Outstanding transfers endpoint | STORY-03 | backend | blocked | TASK-010 |
| TASK-012 | Outstanding transfers view page | STORY-03 | frontend | blocked | TASK-011 |
| TASK-013 | Transaction linking UI (pair + group) | STORY-03 | frontend | blocked | TASK-010, TASK-007 |
| TASK-014 | Balance calculation endpoint (per-account balances) | STORY-04 | backend | blocked | TASK-006 |
| TASK-015 | Monthly summary endpoint (income/expense/transfer totals) | STORY-04 | backend | blocked | TASK-006 |
| TASK-016 | Balance dashboard page (balances + monthly breakdown) | STORY-04 | frontend | blocked | TASK-014, TASK-015, TASK-003 |

## Bugs

_(empty)_
