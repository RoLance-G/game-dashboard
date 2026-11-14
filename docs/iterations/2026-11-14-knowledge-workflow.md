# 2026-11-14 — Establish reusable dashboard knowledge and iteration logs

> Status: `docs-only`  
> Repository/branch: `RoLance-G/game-dashboard` / `main`  
> Code version: v4 unchanged; last app-code commit [`b8540e4`](https://github.com/RoLance-G/game-dashboard/commit/b8540e4ddcc22861416c1d06c007807505e2ad04)  
> Docs commit: see Git history for this file's initial commit

## 1. Request from this conversation

The user clarified that a previously generated chat log was **not** the needed deliverable. The real goal is to reuse this Dashboard development experience when developing other dashboards; write structured Markdown as input to a future Skill. For **every subsequent version iteration**, summarize that iteration's discussion as Markdown and upload it to GitHub along with the work.

## 2. Starting evidence

- Read the previously generated `Game_Dashboard_Chat_Log.md` (historical source summary, not complete original transcript).
- Inspected the currently deployed GitHub repository's v4 `index.html` locally and via GitHub; confirmed its IndexedDB store names, JSON export format and Google Drive flow.
- Inspected existing repository root; it contained only `index.html` before this documentation change.
- No historical `AGENTS.md`, case study or iteration templates were present.

## 3. Decisions and trade-offs

| Decision | Reason | Trade-off |
|---|---|---|
| Store reusable method separately from project facts | Other dashboard domains should reuse patterns, not game-specific variables | More than one Markdown file to maintain |
| Add repo-root `AGENTS.md` | Future code-editing assistants have an explicit instruction to inspect source and write logs | Only works if future assistant reads/follows it; not a scheduled job |
| Use append-only dated iteration docs | Preserves design rationale and failures over many versions | Adds a small step to every iteration |
| Backfill historical work as one retrospective | Original early turn-by-turn messages and exact releases unavailable | Less granular than future notes, but does not invent chronology |
| Keep v4 HTML unchanged | Documentation request has no functional change | No code regression scope introduced |

## 4. Changes

- `AGENTS.md`: mandatory working agreement and per-iteration Markdown checklist.
- `docs/DASHBOARD_SKILL_BLUEPRINT.md`: transferable architecture, UX, storage, performance, security, test and release process for a future Skill.
- `docs/GAME_DASHBOARD_CASE_STUDY.md`: exact current system, data and backup architecture, design decisions, limitations and known risks.
- `docs/iterations/TEMPLATE.md`: structured log format capturing request, implementation, evidence, tests, deployment and lessons.
- `docs/iterations/2026-11-14-v1-v4-retrospective.md`: backfilled history with honest source limitations.
- `docs/iterations/2026-11-14-knowledge-workflow.md`: this documentation iteration.

## 5. Tests and review

- Documentation files checked for Markdown links to repo-local paths, UTF-8 readability, and exclusion of secrets/user data exports.
- `index.html` deliberately not changed; therefore no new JS code or production UI path needs a regression claim for this docs-only commit.
- GitHub remote confirmation is required after upload; if the upload cannot be verified, status must be reported explicitly.

## 6. Deployment and future practice

- Publish the Markdown files to `main` as a documentation-only commit; GitHub Pages' entry HTML remains unchanged.
- For the next version request, inspect latest code and prior notes, complete changes/tests, then create **a new** dated log from `TEMPLATE.md` in the same commit or alongside it.
- There is no always-running automation. Execution requires the next development conversation and access to the GitHub connector.

## 7. Reusable lesson

A reliable coding Skill needs a **playbook + grounded case study + per-iteration evidence trail**. A chat transcript is useful as primary source, but by itself does not communicate why choices were made or how to repeat the implementation safely.