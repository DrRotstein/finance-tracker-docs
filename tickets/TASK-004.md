---
id: TASK-004
type: task
title: "Account create/edit form + delete confirmation"
story: STORY-01
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-002, TASK-003]
blocks: []
---

## Description

Build the account creation/editing form and delete confirmation dialog.

## Acceptance Criteria

- [ ] Form accessible from "Add Account" button and account card edit action
- [ ] Fields: name (text), type (select dropdown), starting balance (number), currency (select, default EUR), is_external (toggle/checkbox)
- [ ] Client-side validation: name required, starting balance ≥ 0
- [ ] When `is_external` is toggled on, label changes to "Person/Entity" context
- [ ] Successful create/edit shows success toast and navigates back to list
- [ ] Delete action shows confirmation dialog with account name
- [ ] Delete shows error toast if account has transactions (409 from API)
- [ ] Form reuses between create (empty) and edit (prefilled) modes

## Technical Notes

- Use React Hook Form + Zod for validation
- Modal/drawer or separate page — either pattern acceptable
- Optimistic update on edit, invalidate query on create/delete
