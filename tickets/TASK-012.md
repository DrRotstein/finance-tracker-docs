---
id: TASK-012
type: task
title: "Outstanding transfers view page"
story: STORY-03
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-011]
blocks: []
---

## Description

Build the outstanding transfers view showing unmatched transfer legs (money lent/borrowed that hasn't been returned).

## Acceptance Criteria

- [ ] Page at route `/outstanding` shows all incomplete transfer pairs
- [ ] Two sections: "They owe you" (incoming missing) and "You owe" (outgoing missing)
- [ ] Each entry shows: person/account name, amount, date of original transaction, description
- [ ] Summary at top: total owed to you, total you owe, net balance
- [ ] Action button on each entry: "Mark as returned" → opens form to create the return leg transaction and auto-link to the pair
- [ ] Filter by person/account
- [ ] Empty state: "No outstanding transfers — all settled up! 🎉"

## Technical Notes

- Fetch from `GET /transactions/outstanding`
- "Mark as returned" flow: creates a new transaction (opposite direction) + adds it to the existing pair via `POST /relations/:id/members`
- Consider confirmation before creating the return transaction
