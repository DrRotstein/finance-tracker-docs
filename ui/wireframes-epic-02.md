# EPIC-02 — UI Wireframes

> Core financial tracking screens. Design principle: **FASTER than Excel**.
> Minimal clicks, smart defaults, keyboard-friendly, single-user (no auth).

---

## Screen 1: Account List + Create/Edit Form

### P-01 Account List View

```
┌─────────────────────────────────────────────────────────────┐
│  💰 Accounts                              [+ New Account]   │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌───────────────────────────────────────────────────────┐  │
│  │  🏦 Checking — Bank of America         $4,230.50  ✏️  │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │  💳 Credit Card — Visa                 -$1,200.00 ✏️  │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │  💵 Cash                                  $320.00 ✏️  │  │
│  ├───────────────────────────────────────────────────────┤  │
│  │  🏦 Savings — Ally                    $12,500.00  ✏️  │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                             │
│  ─── Summary ───────────────────────────────────────────    │
│  Total Net Balance:  $15,850.50                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Interactions:**
- Click `[+ New Account]` → inline form appears at top of list (no modal)
- Click ✏️ → row transforms to inline edit (same form, pre-filled)
- Click account name → navigates to filtered transaction list for that account

### P-02 Account Create/Edit Form (Inline)

```
┌─────────────────────────────────────────────────────────────┐
│  Name: [___________________________]                        │
│  Type: [Checking ▾]   Currency: [ILS ▾]                    │
│  Initial Balance: [0.00_________]                           │
│                                                             │
│  [Save]  [Cancel]                                           │
└─────────────────────────────────────────────────────────────┘
```

**UX Notes:**
- `Type` dropdown: Checking, Savings, Credit Card, Cash, Investment
- `Currency` defaults to ILS (user's locale)
- `Initial Balance` defaults to `0.00`
- `Save` validates name is non-empty → adds to list immediately
- `Cancel` collapses the form; no confirmation needed
- **Keyboard:** Tab through fields, Enter to save, Escape to cancel

---

## Screen 2: Transaction List + Create Form

### P-03 Transaction List View

```
┌─────────────────────────────────────────────────────────────┐
│  📋 Transactions    Account: [All ▾]    [+ New Transaction] │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ── July 2026 ──────────────────────────── Σ -$1,450.00 ── │
│                                                             │
│  │ Jul 03 │ Expense  │ Groceries    │ Supermarket  │-$85.20│
│  │ Jul 02 │ Expense  │ Transport    │ Gas station  │-$45.00│
│  │ Jul 01 │ Income   │ Salary       │ Monthly pay  │+$5,200│
│  │ Jul 01 │ Transfer │ Check→Saving │ Monthly save │-$1,000│
│                                                             │
│  ── June 2026 ──────────────────────────── Σ -$2,100.00 ── │
│                                                             │
│  │ Jun 30 │ Expense  │ Rent         │ Apartment    │-$1,800│
│  │ Jun 28 │ Expense  │ Utilities    │ Electric     │  -$120│
│  │ ...    │          │              │              │        │
│                                                             │
│  [Load more]                                                │
└─────────────────────────────────────────────────────────────┘
```

**Interactions:**
- Grouped by **month** (newest first), with monthly subtotal
- `Account` filter dropdown (All, or specific account)
- Click row → expand inline to edit (same as create form, pre-filled)
- `[+ New Transaction]` → form slides in at top

### P-04 Transaction Create Form (Dynamic by Type)

```
┌─────────────────────────────────────────────────────────────┐
│  Type: ( ● Expense ) ( ○ Income ) ( ○ Transfer )            │
│                                                             │
│  Date:     [2026-07-03]  ← defaults to TODAY                │
│  Account:  [Checking — Bank of America ▾]                   │
│  Category: [Groceries ▾]  ← REQUIRED                       │
│  Amount:   [___________] ILS                                │
│  Note:     [___________________________] (optional)         │
│                                                             │
│  [Save & New]  [Save & Close]  [Cancel]                     │
└─────────────────────────────────────────────────────────────┘
```

**Dynamic behavior by type:**

| Field        | Expense        | Income         | Transfer              |
|-------------|----------------|----------------|-----------------------|
| Account     | From account   | To account     | Hidden (see below)    |
| Category    | Expense cats   | Income cats    | Auto: "Transfer"      |
| Extra field | —              | —              | From/To account pair  |

**Transfer variant:**
```
│  From Account: [Checking ▾]                                 │
│  To Account:   [Savings ▾]                                  │
│  Amount:       [1000.00___] ILS                             │
```

**UX Notes:**
- **Date defaults to today** — no extra click needed for most entries
- **Category is REQUIRED** — save button disabled until selected
- `[Save & New]` clears form but keeps Type + Account selected (batch entry)
- `[Save & Close]` returns to list
- Amount field: numeric only, auto-formats to 2 decimals on blur
- **Keyboard:** Tab order optimized for rapid entry; Enter = Save & New

---

## Screen 3: Transaction Relations

### P-05 Transfer Linking UI

```
┌─────────────────────────────────────────────────────────────┐
│  🔗 Link Transactions                                       │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  This transaction:                                          │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Jul 01 │ Transfer │ Checking │ -$1,000 │ → Savings  │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                             │
│  Linked counterpart:                                        │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Jul 01 │ Transfer │ Savings  │ +$1,000 │ ← Checking │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                             │
│  Status: ✅ Matched                [Unlink]                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

**Automatic linking:** When a Transfer is created, the system auto-creates the counterpart transaction in the target account and links them. No manual linking needed for new transfers.

### P-06 Outstanding Transfers View

```
┌─────────────────────────────────────────────────────────────┐
│  ⚠️ Outstanding Transfers (unmatched)          [Resolve All]│
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  │ Jun 15 │ Checking → ??? │ -$500 │ "ATM withdrawal"      │
│  │        │ [Link to existing] [Create counterpart] [Ignore]│
│  │                                                          │
│  │ Jun 10 │ ??? → Savings  │ +$200 │ "Deposit"             │
│  │        │ [Link to existing] [Create counterpart] [Ignore]│
│                                                             │
│  ── 2 unmatched transfers ──────────────────────────────    │
└─────────────────────────────────────────────────────────────┘
```

**Interactions:**
- `[Link to existing]` → opens search/filter to find the counterpart among existing transactions
- `[Create counterpart]` → pre-fills a new transaction form with mirrored data
- `[Ignore]` → marks as intentionally unlinked (e.g., cash withdrawal)
- `[Resolve All]` → steps through each one sequentially
- Accessible from main nav badge: `Transfers ⚠️2`

---

## Screen 4: Balance Dashboard

### P-07 Per-Account Balances

```
┌─────────────────────────────────────────────────────────────┐
│  📊 Dashboard                     Period: [July 2026 ▾]     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────────── Account Balances ──────────────────────┐  │
│  │                                                       │  │
│  │  Checking      ████████████████░░░░  $4,230   (27%)   │  │
│  │  Savings       ████████████████████  $12,500  (79%)   │  │
│  │  Credit Card   ██░░░░░░░░░░░░░░░░░░  -$1,200 (-8%)   │  │
│  │  Cash          ██░░░░░░░░░░░░░░░░░░  $320     (2%)   │  │
│  │                                                       │  │
│  │  NET TOTAL:                           $15,850.50      │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### P-08 Monthly Breakdown

```
┌─────────────────────────────────────────────────────────────┐
│  ┌─────────────── July 2026 Breakdown ───────────────────┐  │
│  │                                                       │  │
│  │  Income:    +$5,200.00                                │  │
│  │  Expenses:  -$2,050.20                                │  │
│  │  Transfers: -$1,000.00 (internal, net zero)           │  │
│  │  ─────────────────────                                │  │
│  │  Net:       +$2,149.80                                │  │
│  │                                                       │  │
│  │  ── Expense by Category ──────────────────────────    │  │
│  │                                                       │  │
│  │  Rent          ████████████████████  $1,800  (88%)    │  │
│  │  Utilities     ██░░░░░░░░░░░░░░░░░░  $120    (6%)    │  │
│  │  Groceries     █░░░░░░░░░░░░░░░░░░░  $85     (4%)    │  │
│  │  Transport     █░░░░░░░░░░░░░░░░░░░  $45     (2%)    │  │
│  │                                                       │  │
│  │  ── Monthly Trend (last 6 months) ────────────────    │  │
│  │                                                       │  │
│  │  $6k │          ·                                     │  │
│  │  $4k │    ·  ·     ·  ·                               │  │
│  │  $2k │ ·                 ·                            │  │
│  │  $0k ├──┬──┬──┬──┬──┬──┐                             │  │
│  │       Feb Mar Apr May Jun Jul                         │  │
│  │                                                       │  │
│  │  [← Previous Month]          [Next Month →]          │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

**Interactions:**
- Period dropdown: month picker (defaults to current month)
- Click category bar → filters transaction list to that category
- Click account bar → navigates to filtered transaction list
- Monthly trend is a sparkline; click a month → navigates to that month's breakdown
- `[← Previous Month]` / `[Next Month →]` for quick navigation

---

## Navigation Structure

```
┌─────────────────────────────────────────────────────────────┐
│  [💰 Accounts]  [📋 Transactions]  [🔗 Transfers ⚠️2]  [📊 Dashboard] │
└─────────────────────────────────────────────────────────────┘
```

- Top-level tab bar (4 items max — no hamburger menu)
- Badge on Transfers shows unmatched count
- Active tab highlighted
- Keyboard: `Alt+1` through `Alt+4` for tab switching

---

## Global UX Principles

| Principle | Implementation |
|-----------|---------------|
| Faster than Excel | Inline editing, no modals, tab-through, batch entry |
| Date = today | All date fields pre-filled with current date |
| Category required | Save disabled without category; visual indicator |
| Monthly grouping | Transactions grouped by month; dashboard is monthly |
| Single user | No login screen, no user switcher, no permissions UI |
| Minimal clicks | Inline forms, smart defaults, `Save & New` for batch |
| Keyboard-first | Full tab order, Enter/Escape shortcuts documented |

---

## Responsive Behavior

- **Desktop (≥1024px):** Full layout as shown above
- **Tablet (768–1023px):** Stack account balance bars vertically; transaction table gains horizontal scroll
- **Mobile (< 768px):** Bottom tab bar; transaction list becomes card-based; forms go full-screen

---

## Design Token References

| Element | Token |
|---------|-------|
| Positive amount | `color.semantic.success` |
| Negative amount | `color.semantic.error` |
| Transfer amount | `color.semantic.info` |
| Category bar fill | `color.primary.500` |
| Tab active | `color.primary.600` |
| Card border | `color.neutral.200` |
| Spacing between rows | `spacing.sm` (8px) |
| Section spacing | `spacing.lg` (24px) |
| Border radius | `radius.md` (8px) |

---

*Generated by Iris 🎨 — 2026-07-03*
