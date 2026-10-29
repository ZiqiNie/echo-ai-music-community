# Echo — AI Music Community · Backend

Team coursework project, Summer 2026 — Shandong University Software College × Shanruan Huawen.

## About this repository

This is a **portfolio extract**, not the full project. Echo's backend lives in a course repository
owned by the instructor; here I document and excerpt only the parts I personally authored.

→ PR-level evidence of authorship: **[CONTRIBUTIONS.md](CONTRIBUTIONS.md)**

| | |
|---|---|
| Role | Backend developer — data model, authentication, admin API, AI generation pipeline |
| Team size | 10 |
| Contribution | **9 merged pull requests** out of 10 opened, 22 authored commits, +4,868 / −828 lines |
| Duration | 2026.07 |

Only work I authored is claimed here. Two pull requests in the course repository (#15, #17) were
opened by a teammate — I merged them but did not write that code, so they are excluded from every
count on this page. See [CONTRIBUTIONS.md](CONTRIBUTIONS.md) for the per-PR breakdown.

## The product

Echo is an AI music community. A user describes a theme and mood; the backend calls MiniMax to
generate lyrics and melody, stores the resulting audio and cover art, and publishes the track into a
community feed where comments, playlists, battles and an AI host operate on top.

## What I built

### Data model — 22 tables

Defined the complete PostgreSQL schema in Prisma (`prisma/schema.prisma`, ~430 lines) plus a
hand-written SQL reference (`prisma/sql/echo_music_ai_all_tables.sql`, ~620 lines), the initial
migration and the seed script. Every downstream module — songs, playlists, comments, battles,
invite codes, points ledger — is built on this schema.

### Authentication and authorisation

JWT register / login / me / logout, a JWT strategy, a `@CurrentUser` decorator, a role-based guard,
and a `@Public` decorator that opts specific endpoints out of the global auth guard.

### Admin API

A ~630-line admin controller covering: user CRUD, password reset and points adjustment; song
moderation and status transitions; invite-code issuance and revocation; comment moderation.

### AI generation pipeline

- `common/services/cover-storage.service.ts` — local persistence for generated cover images
- **Album generation** — a multi-track prompt builder that assigns each track a narrative position
  (opening / development / turn / response / departure / coda) and de-duplicates generated track
  titles across the album
- **Graceful degradation** — falls back to a mock service when the provider call fails, so
  generation endpoints stay reachable

### AI concurrency control

- `ai/ai-concurrency.service.ts` — a semaphore-style queue capping parallel provider calls
  (`MAX_AI_CONCURRENCY`, default 2), exposing active / pending counters and a per-task
  queue-position lookup used for progress reporting
- `ai/minimax.service.ts` — a generic `runWithRetry` wrapper with linear backoff and a
  `shouldRetry` predicate, so provider-side **business** rejections (HTTP 200 with an error body)
  are retried without leaking the reserved concurrency slot
- `ai/minimax.service.spec.ts` — unit tests covering the retry path

## Stack

NestJS · TypeScript · Prisma · PostgreSQL · JWT · MiniMax API · Vitest · Docker Compose

## Excluded

Instructor-provided scaffolding, teammate code, API keys, `.env` files and user data are not
included in this repository. The full source remains within the course repository.
