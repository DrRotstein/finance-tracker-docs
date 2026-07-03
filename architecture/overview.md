# Architecture Overview — Finance Tracker

> One-page system sketch. For detailed decisions, see `adr/`.

## System Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        User (Browser)                           │
└────────────────────────────────┬────────────────────────────────┘
                                 │ HTTPS
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                     Frontend (React + Vite)                      │
│  • SPA served as static files (nginx or Vite preview)           │
│  • Communicates with backend via REST/JSON                      │
│  • Runs in its own Docker container                             │
│  • Port: 3000 (dev) / 80 (prod)                                │
└────────────────────────────────┬────────────────────────────────┘
                                 │ HTTP REST (JSON)
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                   Backend (NestJS + TypeScript)                  │
│  • RESTful API (JSON request/response)                          │
│  • Modules: Auth, Accounts, Transactions, Transfers, Debts      │
│  • Validation via class-validator + class-transformer            │
│  • TypeORM entities + migrations for schema evolution            │
│  • Runs in its own Docker container                             │
│  • Port: 4000                                                   │
└────────────────────────────────┬────────────────────────────────┘
                                 │ TCP :5432
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                     PostgreSQL 16 Database                       │
│  • Single database: finance_tracker                             │
│  • ACID transactions for balance consistency                    │
│  • Foreign key + CHECK constraints                              │
│  • Runs as Docker container (dev) or managed service (prod)     │
│  • Data volume mounted for persistence                          │
└─────────────────────────────────────────────────────────────────┘
```

## Repository Layout

| Repo | Purpose | Key contents |
|------|---------|-------------|
| `finance-tracker-docs` | Architecture, ADRs, tickets, requirements | This file, ADRs, board, vision |
| `finance-tracker-backend` | NestJS API server | `src/`, `Dockerfile`, `docker-compose.yml`, migrations |
| `finance-tracker-frontend` | React SPA | `src/`, `Dockerfile`, `docker-compose.yml`, Vite config |

## Technology Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Backend | NestJS 10 + TypeScript 5 | Structured, modular, decorator-based DI |
| Database | PostgreSQL 16 | ACID, constraints, proven reliability |
| ORM | TypeORM 0.3 | Migrations, decorators align with NestJS |
| Frontend | React 18 + Vite 5 | Fast dev, mature ecosystem |
| Containers | Docker + Compose | Reproducible local & prod environments |
| Runtime | Node.js 20 LTS | Stable, long-term support |

## Key Architectural Decisions

1. **Separate repos** — Backend and frontend are independently deployable. This keeps Docker images small and CI fast.
2. **REST over GraphQL** — Simpler for CRUD-dominant domain. No over-fetching concern for a single user.
3. **Database as source of truth** — All balances are derived from transaction history (no cached balance fields that can drift). If needed for performance later, we add materialized views.
4. **Migrations-first schema** — Every schema change goes through a TypeORM migration. No `synchronize: true` in production.
5. **Single-user auth** — Initially simple (JWT or session). No multi-tenant complexity.

## Deployment Target (€20/month budget)

```
Single VPS (e.g., Hetzner CX22 — €5/month)
├── docker-compose (production)
│   ├── frontend (nginx serving built React)
│   ├── backend (NestJS)
│   └── postgres (with volume mount)
└── Reverse proxy (Caddy or nginx) for HTTPS
```

Alternatively: Railway / Render free tiers for dev, upgrade to paid when needed.

## Data Integrity Strategy

- PostgreSQL ACID transactions wrap all balance-affecting operations
- Foreign keys enforce referential integrity (no orphaned transactions)
- `CHECK` constraints prevent negative balances where appropriate
- TypeORM migrations are versioned and tested before deploy
- Database volume is persistent and backed up (cron + pg_dump to object storage)

## Communication Flow

1. User interacts with React SPA in browser
2. SPA calls backend REST endpoints (`/api/v1/...`)
3. Backend validates input, applies business logic, persists via TypeORM
4. PostgreSQL enforces constraints, returns result
5. Backend sends JSON response to frontend
6. Frontend updates UI optimistically or on response

## Future Considerations (not in scope now)

- Bank integration (read-only import)
- Mobile app (React Native or PWA)
- Forecasting module
- Multi-user / sharing
