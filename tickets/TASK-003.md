---
id: TASK-003
type: task
title: "Account list page + account card component"
story: STORY-01
epic: EPIC-02
owner: frontend
status: blocked
priority: P0
estimate: M
created: 2026-07-03T17:03Z
depends_on: [TASK-002]
blocks: [TASK-004]
---

## Description

Build the accounts list page showing all user accounts as cards, with current balance displayed.

## Acceptance Criteria

- [ ] Page at route `/accounts` lists all accounts
- [ ] Each account displayed as a card showing: name, type (with icon), current balance, currency
- [ ] Cards visually distinguish between own accounts and external (person) accounts
- [ ] Empty state shown when no accounts exist (with CTA to create first account)
- [ ] Loading skeleton while fetching
- [ ] Error state with retry option
- [ ] "Add Account" button prominently placed

## Technical Notes

- Fetch from `GET /accounts`
- Use React Query for data fetching + caching
- Account card is a reusable component (`AccountCard`)
- Type icons: bank 🏦, cash 💵, paypal (PayPal icon), person 👤, other 📦
