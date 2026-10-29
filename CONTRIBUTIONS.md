# My contributions — `jiachaoDing/music-ai-server`

Evidence of authorship for the Echo AI Music Community backend.
Original repository: https://github.com/jiachaoDing/music-ai-server (course-owned, not mine).

**10 pull requests opened, 9 merged · 22 authored commits · +4,868 / −828 lines across merged PRs.**
Authored 2026-07-06 → 2026-07-21.

## Scope note

The full repository is a 10-person team effort. This file lists **only what I wrote**.

Two merge commits that appear under my identity are **not** my code and are excluded:

| PR | Branch | PR author | Code author | My role |
|---|---|---|---|---|
| #15 | `feature/xuna-ai-radio-dj-generation` | xunanana | xu---na | opened and merged the PR |
| #17 | `feature/xuna-ai-creation-mode-refactor` | xunanana | xu---na | opened and merged the PR |

I worked with three git identities as my local config changed over the term —
`nn27` (Gitee identity), `Nieziqi` and `ZiqiNie` (GitHub identity). All three are me;
`my_contributions.txt` lists every commit under all three.

These three identities were verified, not assumed: every `nn27` commit sits on a
`feature/nieziqi-*` or `fix/nieziqi-*` branch and inside a pull request opened by `ZiqiNie`,
and it touches Echo's own files (`src/ai/*`, `src/admin/*`, `prisma/schema.prisma`). The
repository's first commit is the instructor's scaffold on 2026-06-28, so no history from an
earlier project is carried into this one.

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

Full version in [`my_contributions.txt`](./my_contributions.txt), grouped by identity.

```
## Implementation commits - 11 (inside my own PR branches)
2026-07-21 | f22c4b3 | fix: retry MiniMax business limits and preserve concurrency slots
2026-07-21 | 97bf01b | fix: align AI concurrency limiter with provider requests
2026-07-21 | 544aa7b | 修复 AppController 单测避免加载 Prisma Client
2026-07-21 | 6ca5aa9 | 实现后端 AI 任务并发队列
2026-07-18 | 8e1fd2b | 触发管理后台 API 契约 CI
2026-07-18 | 1c2da9d | 补充管理后台鉴权兼容
2026-07-18 | 9cfa4e5 | 对齐管理后台 API 契约
2026-07-16 | 2eaf69e | feat: persist generated cover images locally
2026-07-09 | 0345bc9 | chore: update deployment config and migration
2026-07-08 | c894737 | fix: update generate api
2026-07-06 | a605a1d | 新增核心数据库表

## Commits pushed straight to main - 2
2026-07-08 | 60b2fac | feat: 添加sql文件 SQL for 22 tables
2026-07-08 | f1020b2 | feat: add login/register APIs and full database schema

## Merge commits of my own pull requests - 9
2026-07-21 | cadfc0c | Merge pull request #28 from jiachaoDing/fix/nieziqi-minimax-retry-timeout
2026-07-21 | 8c0c222 | Merge pull request #27 from jiachaoDing/fix/nieziqi-ai-provider-concurrency
2026-07-21 | 42ebcab | Merge pull request #26 from jiachaoDing/feature/nieziqi-ai-concurrency-backend
2026-07-21 | 0371b45 | Merge pull request #25 from jiachaoDing/feature/nieziqi-ai-concurrency-backend
2026-07-18 | e77d15a | Merge pull request #12 from jiachaoDing/feature/nieziqi-admin-api-contract
2026-07-18 | bcf0dae | Merge pull request #11 from jiachaoDing/feature/nieziqi-admin-api-contract
2026-07-16 | ecbf387 | Merge pull request #7 from jiachaoDing/feature/nieziqi-cover-storage
2026-07-09 | c29909c | Merge pull request #3 from jiachaoDing/fix/nieziqi-generate-api
2026-07-08 | ec71b9d | Merge pull request #2 from jiachaoDing/feature/nieziqi-generate-api
```

Reproduce with:

```bash
git clone https://github.com/jiachaoDing/music-ai-server.git
cd music-ai-server
git log --all --author="nn27" --author="Nieziqi" --author="ZiqiNie" \
  --date=short --pretty=format:"%ad | %h | %s"
```

Three `--author` flags are OR-ed by git and return 24 commits: the 22 above plus the two
merge commits for teammate PRs #15 and #17 that this file excludes on purpose.

Single PR check, for example #28:

```bash
git log --all --author="nn27" --grep="concurrency slots" --stat
```
