---
id: ADR-001
title: Stack Selection
status: accepted
date: 2026-07-03
deciders: Cassius (Architect), Finn (User)
epic: EPIC-01
---

# ADR-001 — Stack Selection

## Context

We need to select the technology stack for the Finance Tracker application. The user (Finn) has expressed clear preferences:

- **Backend:** NestJS with TypeScript
- **Database:** PostgreSQL with TypeORM
- **Frontend:** React
- **Infrastructure:** Docker per repo

Constraints:
- Budget ceiling: €20/month on infrastructure
- Data must never be lost or become inconsistent (critical risk)
- UX must be faster/better than a spreadsheet
- Single user (Finn), no mobile-native requirement

## Decision

We **accept the user's preferred stack without changes**:

| Layer | Technology | Version (target) |
|-------|-----------|-----------------|
| Backend runtime | Node.js 20 LTS | ^20.x |
| Backend framework | NestJS | ^10.x |
| Language | TypeScript | ^5.x |
| Database | PostgreSQL | 16 |
| ORM | TypeORM | ^0.3.x |
| Frontend framework | React | ^18.x |
| Frontend build | Vite | ^5.x |
| Containerization | Docker + docker-compose | per repo |

## Options Considered

### Option A: User's preferred stack (chosen)
NestJS + TypeScript, PostgreSQL + TypeORM, React + Vite, Docker.

**Pros:**
- Finn is already familiar with these technologies
- NestJS provides excellent structure (modules, guards, pipes, interceptors) for a CRUD-heavy finance app
- PostgreSQL is the gold standard for data integrity (ACID transactions, foreign keys, constraints)
- TypeORM supports migrations, enabling safe schema evolution
- React ecosystem is mature with excellent tooling
- Docker ensures reproducible environments and easy deployment
- Entire stack fits within €20/month (single VPS or free tier)

**Cons:**
- TypeORM has known issues with complex queries and migrations (mitigated by keeping the schema simple early on)
- NestJS has higher boilerplate than Express alone (acceptable for structure it provides)

### Option B: Lighter alternative (Express + Prisma + React)
Express.js, Prisma ORM, React + Vite.

**Pros:**
- Less boilerplate than NestJS
- Prisma has better type-safety and migration DX than TypeORM

**Cons:**
- Express lacks built-in structure → risk of inconsistency as app grows
- User explicitly prefers NestJS
- Prisma's query engine adds a binary dependency

### Option C: Full-stack framework (Next.js)
Next.js with API routes, Prisma, PostgreSQL.

**Pros:**
- Single repo, single deploy
- SSR for fast perceived load

**Cons:**
- Conflates frontend and backend → harder to scale independently
- User explicitly wants separate repos with Docker per repo
- Overkill for a single-user finance app

## Consequences

1. **Data integrity** — PostgreSQL with TypeORM migrations gives us ACID transactions and schema versioning. We will enforce foreign key constraints and use database-level `CHECK` constraints for balance consistency.
2. **Budget** — Stack runs comfortably on a single €5–10/month VPS (e.g., Hetzner CX22 or Railway free tier for dev). PostgreSQL included.
3. **Developer experience** — TypeScript end-to-end (backend + frontend) means shared type definitions are possible via a contracts package or shared types file.
4. **Deployment** — Docker Compose for local dev; single `docker-compose.yml` per repo. Production can be a single VPS running both containers + managed/containerized PostgreSQL.
5. **Known risk: TypeORM migrations** — We will keep migrations simple and test them in CI. If TypeORM migration DX proves painful, we can revisit (new ADR) without changing the rest of the stack.

## References

- [NestJS Documentation](https://docs.nestjs.com/)
- [TypeORM Documentation](https://typeorm.io/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/16/)
- Vision: `project/vision.md`
- Q&A: `requirements/Q&A-onboarding.md`
