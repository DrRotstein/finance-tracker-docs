---
id: TASK-008
type: task
title: "Transaction create/edit form (dynamic fields by type)"
story: STORY-02
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-006, TASK-007]
blocks: []
---

## Description

Build the transaction creation/editing form with dynamic field visibility based on transaction type.

## Acceptance Criteria

- [ ] Form accessible from "Add Transaction" button and transaction row click (edit)
- [ ] Type selector (expense/income/transfer) at top — controls which account fields show
- [ ] Expense: shows `from_account` (required), hides `to_account`
- [ ] Income: shows `to_account` (required), hides `from_account`
- [ ] Transfer: shows both `from_account` and `to_account` (both required)
- [ ] Account dropdowns populated from `GET /accounts` (separate own vs external)
- [ ] Fields: amount (number, > 0), date (date picker, default today), category (searchable select from preset list), description (optional textarea)
- [ ] Client-side validation mirrors backend rules
- [ ] Success toast + redirect to transaction list
- [ ] Edit mode prefills all fields; type field disabled in edit mode

## Technical Notes

- Use React Hook Form + Zod
- Category presets defined as constant array (shared between FE components)
- Account selector groups: "My Accounts" vs "People/External"
- Consider quick-add mode (minimal fields) vs full form
