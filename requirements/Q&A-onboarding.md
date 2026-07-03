# Q&A — Onboarding

### Q1: Project slug
**Asked:** 2026-07-03T14:52Z
**Answer:** finance-tracker
**My read:** Slug is `finance-tracker`.

### Q2: One-sentence vision
**Asked:** 2026-07-03T14:53Z
**Answer:** "I can better track my expenses, my income and my transactions and transfers"
**My read:** This project exists so that Finn can track expenses, income, transactions, and transfers better than today.

### Q3: Target user
**Asked:** 2026-07-03T14:55Z
**Answer:** "I am a dual student, have little income and need to make sure I don't spend too much money. I also manage the cashier of my dorm, and sometimes I need to make transactions from my bank account to the dorm account, or exchange cash for bank account money. Sometimes I give cash to my friends and they send it back on Paypal and so on"
**My read:** Dual student with limited income, managing personal finances + dorm cashier account, frequent cross-account transfers (bank ↔ dorm, cash ↔ PayPal, informal friend loans).

### Q4: Top 3 jobs to be done (week 1)
**Asked:** 2026-07-03T14:59Z
**Answer:** 1. Log a transaction (expense/income) with account, date, category, optional description. 2. See current balance of each account. 3. Log money lent to / received back from a friend (split tracking).
**My read:** Core loop = log transactions across accounts, see balances, track informal debts.

### Q5: Deadline horizon
**Asked:** 2026-07-03T15:00Z
**Answer:** "Just ASAP, there is no deadline at the moment. But you got nothing else to do anyways"
**My read:** No hard deadline — continuous priority, ship incrementally ASAP.

### Q6: Budget signal
**Asked:** 2026-07-03T15:01Z
**Answer:** "20 a month max"
**My read:** €20/month ceiling on infra/services.

### Q7: Code repo URL
**Asked:** 2026-07-03T15:02Z
**Answer:** https://github.com/DrRotstein/finance-tracker-backend and https://github.com/DrRotstein/finance-tracker-frontend
**My read:** Separate backend and frontend repos.

### Q8: Docs repo URL
**Asked:** 2026-07-03T15:02Z
**Answer:** https://github.com/DrRotstein/finance-tracker-docs
**My read:** Standalone docs repo.

### Q9: Stack preferences
**Asked:** 2026-07-03T15:04Z
**Answer:** "Backend should be NestJS with TypeScript, PostgreSQL database and TypeORM. Frontend should be React. Definitely set up Docker in each repo."
**My read:** NestJS + TS, PostgreSQL + TypeORM, React, Docker per repo. Open to architect pushback.

### Q10: Non-goals
**Asked:** 2026-07-03T15:05Z
**Answer:** Not a group-expense tracker. Not a forecasting tool (yet). Not a bank integration (yet). Not mobile-native (yet).
**My read:** Four clear non-goals; "yet" signals future consideration but not now.

### Q11: Deal-breakers / known risks
**Asked:** 2026-07-03T15:09Z
**Answer:** "Data inconsistency, the data should never be lost. Worse UX than just using Excel."
**My read:** Two kill conditions: data integrity and UX speed vs. spreadsheet.

### Q12: User profile
**Asked:** 2026-07-03T15:09Z
**Answer:** "I'm Finn, UTC+2 Berlin, brief, punchy, casual"
**My read:** Finn, Europe/Berlin, brief casual comms.
