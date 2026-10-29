# My contributions — `jiachaoDing/music-ai-server`

Evidence of authorship for the Echo AI Music Community backend.
Original repository: https://github.com/jiachaoDing/music-ai-server (course-owned, not mine).

**9 merged pull requests** out of 10 opened · 13 commits · **+4,868 / −828 lines** across merged PRs.
Period: 2026-06-28 → 2026-07-21.

## Pull requests

| PR | What it delivered | Status | Files | +/− |
|---|---|---|---|---|
| [#1](https://github.com/jiachaoDing/music-ai-server/pull/1) | Initial 22-table core schema (superseded by #2) | closed | 4 | +751 / −20 |
| [#2](https://github.com/jiachaoDing/music-ai-server/pull/2) | 22-table Prisma schema + SQL reference + migration + JWT auth module | merged | 34 | +2,303 / −8 |
| [#3](https://github.com/jiachaoDing/music-ai-server/pull/3) | Generate-API corrections, migration fixes | merged | 8 | +128 / −69 |
| [#7](https://github.com/jiachaoDing/music-ai-server/pull/7) | Local persistence for generated cover images | merged | 4 | +106 / −6 |
| [#11](https://github.com/jiachaoDing/music-ai-server/pull/11) | Admin API contract aligned with v3 spec (630-line controller) | merged | 2 | +653 / −34 |
| [#12](https://github.com/jiachaoDing/music-ai-server/pull/12) | Role-based guard, `@Public` decorator, admin-key utility | merged | 4 | +47 / −1 |
| [#25](https://github.com/jiachaoDing/music-ai-server/pull/25) | **AI task concurrency queue** + public AI endpoints + sample compat layer | merged | 7 | +782 / −98 |
| [#26](https://github.com/jiachaoDing/music-ai-server/pull/26) | Fix AppController unit test so it no longer loads Prisma Client | merged | 3 | +21 / −9 |
| [#27](https://github.com/jiachaoDing/music-ai-server/pull/27) | Align AI concurrency limiter with actual provider requests | merged | 3 | +592 / −543 |
| [#28](https://github.com/jiachaoDing/music-ai-server/pull/28) | **Retry MiniMax business-level rejections while preserving concurrency slots** + unit tests | merged | 2 | +236 / −60 |

## Grouped by area

**Data model** — PRs #1, #2, #3
Full 22-table PostgreSQL schema in `prisma/schema.prisma` (~430 lines), a hand-written SQL
reference (~620 lines), the initial migration and the seed script.

**Authentication & authorisation** — PRs #2, #12
JWT register / login / me / logout, JWT strategy, `@CurrentUser` decorator, role-based guard,
`@Public` decorator, admin-key utility.

**Admin API** — PR #11
~20 endpoints: user CRUD, password reset, points adjustment, song moderation and status
transitions, invite-code issuance and revocation, comment moderation.

**AI generation pipeline** — PRs #2, #3, #7, #25
Generate endpoints, local cover-image persistence, album multi-track prompt builder, mock fallback.

**AI concurrency control** — PRs #25, #26, #27, #28
Semaphore-style queue capping parallel provider calls (with queue-position reporting), limiter
alignment with the provider's real request pattern, linear-backoff retry with a `shouldRetry`
predicate that releases and re-reserves concurrency slots without leaking them.

## Raw commit log

```
2026-07-21 | cadfc0c | Merge pull request #28 from jiachaoDing/fix/nieziqi-minimax-retry-timeout
2026-07-21 | 8c0c222 | Merge pull request #27 from jiachaoDing/fix/nieziqi-ai-provider-concurrency
2026-07-21 | 42ebcab | Merge pull request #26 from jiachaoDing/feature/nieziqi-ai-concurrency-backend
2026-07-21 | 0371b45 | Merge pull request #25 from jiachaoDing/feature/nieziqi-ai-concurrency-backend
2026-07-20 | fb31b2e | Merge pull request #17 from jiachaoDing/feature/xuna-ai-creation-mode-refactor
2026-07-18 | 958ff81 | Merge pull request #15 from jiachaoDing/feature/xuna-ai-radio-dj-generation
2026-07-18 | e77d15a | Merge pull request #12 from jiachaoDing/feature/nieziqi-admin-api-contract
2026-07-18 | bcf0dae | Merge pull request #11 from jiachaoDing/feature/nieziqi-admin-api-contract
2026-07-16 | ecbf387 | Merge pull request #7 from jiachaoDing/feature/nieziqi-cover-storage
2026-07-09 | c29909c | Merge pull request #3 from jiachaoDing/fix/nieziqi-generate-api
2026-07-08 | ec71b9d | Merge pull request #2 from jiachaoDing/feature/nieziqi-generate-api
2026-07-08 | 60b2fac | feat: 添加 sql 文件 SQL for 22 tables
2026-07-08 | f1020b2 | feat: add login/register APIs and full database schema
```

Reproduce with:

```bash
git clone https://github.com/jiachaoDing/music-ai-server.git
cd music-ai-server
git log --all --author="Ziqi" --date=short --pretty=format:"%ad | %h | %s"
```
