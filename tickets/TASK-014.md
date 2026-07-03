---
id: TASK-014
type: task
title: "Balance calculation endpoint (per-account balances)"
story: STORY-04
epic: EPIC-02
owner: backend
status: blocked
priority: P0
estimate: S
created: 2026-07-03T17:03Z
depends_on: [TASK-006]
blocks: [TASK-016]
---

## Description

Implement endpoint that returns current balance for each account (starting balance + transactions sum).

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/accounts/balances` | Get all account balances |

## Acceptance Criteria

- [ ] Returns all non-external accounts with computed `current_balance`
- [ ] Balance formula: `starting_balance + SUM(incoming amounts) - SUM(outgoing amounts)`
- [ ] Optionally include external accounts if `?include_external=true`
- [ ] Response includes: account id, name, type, currency, starting_balance, current_balance
- [ ] Also returns `total_balance` (sum of all own-account balances, same currency assumed for MVP)
- [ ] Efficient query (single query, not N+1)
- [ ] Unit + integration tests

## Technical Notes

- Use the balance query from db-schema.md reference
- Consider caching strategy if this becomes a performance concern (not needed for MVP)
- This is separate from the account list endpoint to keep concerns clean
