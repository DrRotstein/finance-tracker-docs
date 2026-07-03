---
id: EPIC-01
type: epic
title: Onboarding & stack selection
parent: null
owner: architect
status: ready
priority: P0
estimate: M
created: 2026-07-03T15:09Z
acceptance:
  - "ADR-001 exists and is approved, selecting the stack per user preferences (NestJS+TS, PostgreSQL+TypeORM, React, Docker)"
  - "docs/architecture/overview.md exists with a one-page system sketch"
  - "Backend repo finance-tracker-backend contains README, .gitignore, Dockerfile, and basic NestJS scaffold"
  - "Frontend repo finance-tracker-frontend contains README, .gitignore, Dockerfile, and basic React scaffold"
depends_on: []
blocks: []
---

## Context

This is the bootstrap Epic. The team cannot proceed until the architect has selected a stack (ADR-001) and produced an overview. Vision, Q&A, and non-goals are attached.

User has strong preferences: NestJS + TypeScript, PostgreSQL + TypeORM, React, Docker per repo. Architect may challenge via ADR-001 but should default to user preferences unless there's a compelling reason.

## Scope

- Author ADR-001 confirming or adjusting the stack.
- Sketch a one-page system overview (docs/architecture/overview.md).
- Initialize both code repo skeletons (README, license placeholder, .gitignore, Dockerfile, basic scaffold).

## Non-goals

- No feature work this Epic.
- No DB schema yet — that belongs to the first feature Epic.

## Repos

- Backend: https://github.com/DrRotstein/finance-tracker-backend
- Frontend: https://github.com/DrRotstein/finance-tracker-frontend
- Docs: https://github.com/DrRotstein/finance-tracker-docs

## Open questions

- (filled as architect discovers them via `question` messages)
