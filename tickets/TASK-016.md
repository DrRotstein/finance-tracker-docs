---
id: TASK-016
type: task
title: "Balance dashboard page (balances + monthly breakdown)"
story: STORY-04
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: L
created: 2026-07-03T17:03Z
depends_on: [TASK-014, TASK-015, TASK-003]
blocks: []
---

## Description

Build the main dashboard page showing account balances and monthly income/expense breakdown.

## Acceptance Criteria

- [ ] Page at route `/dashboard` (also the app's home/landing page)
- [ ] Top section: account balance cards (each own account with current balance)
- [ ] Total balance prominently displayed (sum of all own accounts)
- [ ] Middle section: monthly breakdown chart (bar or area chart showing income vs expenses per month)
- [ ] Transfer totals shown separately (not mixed into income/expense bars)
- [ ] Month selector or scrollable range (default: last 6 months)
- [ ] Bottom section: quick summary — this month's income, expenses, net
- [ ] Clicking an account card navigates to that account's transaction list (filtered)
- [ ] Responsive layout: stacks vertically on mobile
- [ ] Loading skeletons for each section independently

## Technical Notes

- Fetch from `GET /accounts/balances` and `GET /transactions/monthly-summary`
- Use a charting library (e.g., Recharts or Chart.js via react-chartjs-2)
- Both API calls in parallel (independent data)
- Consider pulling chart library as a lazy-loaded chunk (code splitting)
