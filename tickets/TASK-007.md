---
id: TASK-007
type: task
title: "Transaction list page with filters"
story: STORY-02
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-006]
blocks: [TASK-008]
---

## Description

Build the transaction list page with filtering, pagination, and visual type indicators.

## Acceptance Criteria

- [ ] Page at route `/transactions` shows paginated list of transactions
- [ ] Each transaction row shows: date, type indicator (color/icon), amount, from→to accounts, category, description (truncated)
- [ ] Filter bar with: type (multi-select), account (dropdown), category (dropdown), date range (date pickers)
- [ ] Pagination controls (prev/next, page indicator, total count)
- [ ] Expense shown in red, income in green, transfer in blue
- [ ] Empty state with CTA to log first transaction
- [ ] Loading skeleton for initial load and filter changes
- [ ] Click on transaction row navigates to detail/edit view

## Technical Notes

- Fetch from `GET /transactions` with query params for filters
- Use React Query with keepPreviousData for smooth pagination
- Filter state persisted in URL search params (shareable/bookmarkable)
- Responsive: table on desktop, cards on mobile
