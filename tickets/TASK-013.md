---
id: TASK-013
type: task
title: "Transaction linking UI (pair + group)"
story: STORY-03
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-010, TASK-007]
blocks: []
---

## Description

Build UI for manually linking transactions together as transfer pairs or groups.

## Acceptance Criteria

- [ ] From transaction detail/list, action menu includes "Link transactions"
- [ ] Link as transfer pair: select one other transfer transaction to pair with (search/select UI)
- [ ] Link as group: enter group label + select multiple transactions
- [ ] Visual indicator on transactions that are part of a relation (badge/icon)
- [ ] Clicking the relation indicator shows the linked transactions
- [ ] Can unlink (remove from relation) via the relation detail view
- [ ] Validation: transfer pairs only accept transfer-type transactions, max 2

## Technical Notes

- Uses `POST /relations/transfer-pair`, `POST /relations/group`, `POST /relations/:id/members`
- Transaction search/select could be a modal with the existing transaction list (filtered)
- Show relation info inline on transaction cards/rows
