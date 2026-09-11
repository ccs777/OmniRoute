# INRouter — OmniRoute upstream record

Pinned upstream engine used by the INRouter opportunity-routing program.
Per the INRouter Global Constraints, this revision is the audited starting point and
**every subsequent upstream update must be recorded here**.

## Pinned revision

| Field | Value |
| --- | --- |
| Repository | `https://github.com/ccs777/OmniRoute.git` (public) |
| Pinned commit | `af49d4972ed9b69e43f322453ebccca997a0ab94` |
| Upstream branch | `release/v3.8.51` |
| Commit date | `2026-09-10 18:25:31 -0300` |
| Commit subject | `fix(stream): accept the buffer size glm.ts has been passing since #12179 (#12925)` |
| Package | `omniroute` version `3.8.51` |
| License | MIT — `Copyright (c) 2026 diegosouzapw` (see `LICENSE`) |

Local layout:

| Path | Branch | Revision |
| --- | --- | --- |
| `/home/ubuntu/OmniRoute` | `release/v3.8.51` | `af49d497…` |
| `/home/ubuntu/OmniRoute/.worktrees/inrouter-engine` | `omr_work` | `af49d497…` |

`.worktrees` is already ignored by the upstream `.gitignore` (line 179); no ignore change was
needed. The `omr_work` branch exists only in this clone — nothing has been pushed anywhere.

## Node runtime requirement

`.node-version` in this revision is **`24`**. The host currently provides **Node `v22.23.2`**.
This is a real gap for any build/run step in milestone 01 Task 2 and must be resolved
(install Node 24, or record an explicit, verified compatibility decision) before the engine
is started. Do not assume 22.x is supported because the INRouter plan names 22.23.2 — that
pin is for the INRouter repo, not for OmniRoute.

## Examined paths (verified present at this revision)

These specific paths were confirmed to exist before being named here. Nothing in this file
should be added without a source match — see the upstream documentation-accuracy rule.

| Path | Relevance to INRouter |
| --- | --- |
| `src/app/api/v1/chat/completions/route.ts` | The engine entry point INRouter reuses for `/v1/chat/completions`. |
| `src/app/api/keys/route.ts` | Key-management route — must NOT be exposed publicly. |
| `src/sse/handlers/chat.ts` | SSE chat handling / circuit-breaker wiring read during integration. |
| `open-sse/handlers/chatCore.ts` | Core dispatch (`handleChatCore`) — combo routing and dispatch path. |
| `open-sse/services/combo.ts` | Combo strategies — the auto/combo escape routes that must be constrained. |
| `src/app/api/free-tier/summary/route.ts` | Public community catalog source for offer discovery (milestone 02). |
| `AGENTS.md` | Upstream project rules — binding on any agent working this repo. |
| `LICENSE`, `THIRD_PARTY_NOTICES.md` | Notices that must be preserved in distributable artifacts. |

Not yet examined in depth (do so before wiring against them):
`src/domain/` (policy engine, cost rules, fallback logic), `src/lib/db/` (migrations),
`src/sse/services/auth.ts` (connection selection), `src/shared/utils/circuitBreaker.ts`.

## Upstream rules that bind our work

From the upstream `AGENTS.md` (read in full before edits):

- **Never `git stash` anywhere in this repo**, including inside a worktree and inside any
  subagent. It operates on the shared object store and has clobbered parallel sessions before.
  To compare against a base ref use `git show <ref>:<path>` / `git diff <ref> -- <path>`.
- **Never merge, push, rebase, or force-push a branch another session owns.** Check
  `git worktree list` before merging anything you did not create this session.
- `_tasks/` is a separate git repository and is append/edit-only — never move, rename,
  delete, or track it.
- Root hygiene: tests belong under `tests/`, scripts under a `scripts/` subdirectory, and the
  repo root only holds config/dependency/documentation/CI files.
- Documentation must describe verified behavior. Before naming an API, endpoint, path, command,
  or env var, confirm it has a source match; measure counts rather than writing them from memory.
- Public upstream credentials must go through `resolvePublicCred()` — never string literals.
- Error responses must route through `buildErrorBody()` / `sanitizeErrorMessage()`.

## Update log

Every subsequent upstream update (rebase, cherry-pick, or re-pin) gets a row here: new
revision, what changed upstream, and what we did about it.

| Date | New revision | Reason | Action taken |
| --- | --- | --- | --- |
| 2026-09-11 | `af49d4972ed9b69e43f322453ebccca997a0ab94` | Initial audited pin | Cloned; engine worktree created on `omr_work` |