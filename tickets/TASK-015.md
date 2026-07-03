---
id: TASK-015
type: task
title: "Monthly summary endpoint (income/expense/transfer totals)"
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

Implement endpoint that returns monthly aggregated totals for income, expenses, and transfers.

## Endpoints

| Method | Path | Description |
|--------|------|-------------|
| GET | `/transactions/monthly-summary` | Get monthly totals |

## Acceptance Criteria

- [ ] Returns array of monthly summaries sorted by month DESC
- [ ] Each entry: month (YYYY-MM), total_income, total_expenses, total_transfers, net (income - expenses)
- [ ] Transfers are reported separately and do NOT inflate income or expense totals
- [ ] Supports filter: `from` and `to` (date range, defaults to last 12 months)
- [ ] Supports filter: `account_id` (totals for specific account only)
- [ ] Months with no transactions still appear if within the requested range (with zeros)
- [ ] Unit + integration tests

## Technical Notes

- Use the monthly totals query from db-schema.md as reference
- `DATE_TRUNC('month', date)` for grouping
- Generate zero-filled months in application layer (SQL gaps are expected)
- Response format: `{ months: [...], summary: { total_income, total_expenses, total_transfers } }`
