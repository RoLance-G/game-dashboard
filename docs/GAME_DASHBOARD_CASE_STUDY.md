# Game Dashboard — Implementation Case Study and Project Context

> Last reviewed: 2026-11-14. Based on the current `main/index.html`, prior project discussion, and recorded deployment. **Not** a word-for-word transcript. Statements about unverified production behavior are marked as such.

## 1. Purpose and user constraints

One-file, static-hosted game update/task tracker meant for many years of use, retaining potentially thousands of archived entries. Priorities: low maintenance, small runtime footprint, clean Blue Archive-inspired blue/white UI, reliable local data, export/restore and minimal complexity.

- **Repo:** `RoLance-G/game-dashboard` (`main`, root `index.html`).
- **Host:** GitHub Pages. Git source is **not** the data store.
- **Data:** browser IndexedDB, same-origin and browser-profile scoped.
- **Historical source:** spreadsheet to HTML/JS; earlier `localStorage` implementations.
- **Current milestone:** v4 Google Drive on-open weekly backup support, committed as [`b8540e4`](https://github.com/RoLance-G/game-dashboard/commit/b8540e4ddcc22861416c1d06c007807505e2ad04).

## 2. Visible functionality

- Games: create, rename, reorder, filter/select.
- Categories: per-game ordering, renaming, deletion.
- Updates: create/manage versions, archive/restore, per-update summaries, lazy archive browsing.
- Tasks: create/edit/delete/complete; category-aware list; search; all/pending/done filters; active/all/archived update view.
- Site shortcuts: per-game URL list, favicon fallbacks.
- Settings: category/update/site management, local JSON import/export, Google Drive backup.

## 3. Actual local persistence architecture (v4 source verified)

`DB_NAME = 'GameDashboardLocalDB'`, IndexedDB schema version 1:

| Object store | Key / indexes | Purpose |
|---|---|---|
| `games` | `id` | Game names, categories, site shortcuts and sort order |
| `updates` | `id` | Game update versions; `archived`, `taskCount`, `pendingCount` and sort order |
| `items` | `id`; `by_bucket`, `by_update`, `by_game` | Tasks with `active`/`archived` bucket, parent update and sort order |
| `meta` | key/value | Initialization marker |

- First-run migration checks `localStorage` `gameDashboardV1` and fallback `gameTrackerV3`, leaves legacy copy intact, then writes to IndexedDB.
- Initial load queries all games, updates and **active** tasks; archived tasks are fetched via `by_update` when needed (8 update groups per chunk).
- Archive counters are maintained in `updates` and combined with active counts.
- Writes run through a serialized queue, with state-snapshot diffs; DB transaction failures trigger a visible warning.
- Export (`buildCompleteBackupPayload`) reads **all** three data stores directly from DB after waiting for writes.
- Export JSON structure: `{ exportedAt, app: 'Game Dashboard', version: 1, data: { games, updates, items } }`. The import route supports the wrapped format and a compatible raw-data form.

**Known review items, not claims of a present bug:** check write-failure/snapshot consistency under rapid edits; test multiple tabs and storage failure recovery; consider virtualization if active task DOM becomes large.

## 4. UI decisions and why

Three columns: left game navigation, center tracker, right site shortcuts. The settings view **reuses** left game selection rather than showing another duplicate game list. Blue Archive-inspired design favors bright blue accent but little repeated chrome.

- Barlow for titles/numbers and Nunito Sans for English UI where loaded, system CJK sans-serif fallback.
- Main action emphasis; lower visual weight for category labels, secondary and destructive actions.
- Semantic color and spacing variables; cleaner muted backgrounds, fewer repeated HUD labels and blue borders.
- Empty, filtered-empty, loading, error/retry states were introduced in Design System v3.
- CSS redundancy and repeated game-count scans were reduced in v3. Historical code cleanup claims came from earlier test sessions; don't assume ongoing regression coverage.

## 5. Google Drive v4 backup — actual behavior

Config key: `localStorage['gameDashboardDriveBackupV1']`. Google OAuth scope: `https://www.googleapis.com/auth/drive.file`.

- User enters OAuth Web Client ID; selecting an **existing** folder via Picker additionally requires API key and Cloud project number.
- User may choose an existing folder or create a `Game Dashboard Backups` folder; `folderId` persists for subsequent backups.
- Checks whether `lastSuccessAt` is more than 7 days old at app initialization and reports due status.
- If a token remains valid in the **current page session**, the app may upload; after a fresh load the token is typically absent, so **user interaction is required to re-authorize**. Not an unattended cron job.
- Tokens are kept in volatile JS memory; local settings hold non-secret IDs, folder and status metadata, not tokens or Client Secret.
- Manual backup, retry and error UI. Small JSON uses multipart upload; >4 MiB uses resumable upload session. Upload is checked against returned parent folder and metadata before updating last-success status.
- Backup payload includes all archived tasks (not only current UI state); the JSON format remains compatible with local export/import.
- No automatic old-file rotation/retention deletion in current implementation. A future task would need an explicit retention policy and permission review.

**Verification boundary:** simulated success/failure/folder flows and code checks were reported before the v4 release. Real Google consent, Picker and Drive upload to the user's account have **not been conclusively confirmed** in the recorded conversation. A successful GitHub commit does not verify cloud backup success.

## 6. Key milestones / decision history

| Milestone | Decision | Why / trade-off |
|---|---|---|
| Early HTML iterations | Single-file HTML/CSS/JS, GitHub Pages | Simple hosting, easy manual replace; requires careful source maintenance |
| Blue Archive visual direction | Blue-white game HUD, restrained typography, 3-column layout | Distinct personality without heavy visual runtime |
| IndexedDB upgrade | DB indexes, active-first load, archived lazy load | Supports years of history; still device/browser-local |
| Typography update | Barlow/Nunito Sans + Chinese fallback | Better readability and identity |
| UI Refinement v2 | Reduce HUD clutter, improve typography and action hierarchy | More visual restraint, less CRUD feel |
| Design System v3 | Semantic tokens, spacing, empty states, de-duplicated settings selector | UI consistency and lower repeated work |
| v4 backup | Google Drive + on-open weekly due check + manual upload | Better off-device recovery; needs interactive OAuth and cloud setup |
| Documentation workflow | Dated per-iteration Markdown + reusable skill blueprint | Reuse hard-won lessons on future dashboards, trace decisions |

## 7. Quality gate for the next iteration

1. Obtain a current JSON backup **before data migrations**.
2. Test both active and archived flows; export count must include unloaded archives.
3. Run JS syntax, functional state transitions, visual regression at common sizes and performance sampling for realistic list sizes.
4. Treat mock OAuth tests as insufficient: perform real browser OAuth + Picker + manual upload + restore validation when authorized.
5. Keep the project-specific record here updated when architecture changes, and add a *new* entry under `docs/iterations/` for every iteration.
6. Use the GitHub connector to inspect `main` before writing and verify paths after commit; avoid unrelated changes.

## 8. Source provenance

- Live source at time of review: [`index.html` on main](https://github.com/RoLance-G/game-dashboard/blob/main/index.html).
- Historical discussion: available chat/project narrative; early portions were a **summary** rather than a verbatim log.
- v4 deployment commit: [`b8540e4`](https://github.com/RoLance-G/game-dashboard/commit/b8540e4ddcc22861416c1d06c007807505e2ad04).
- Current user-facing GitHub and Google Cloud setup progress: two relevant Google APIs enabled; OAuth and production manual backup pending confirmation.
## 9. Documentation ownership and Skill promotion (2026-11-14)

This repository is the source of truth for **Game Dashboard-specific** architecture, implementation and migration notes, UI decisions, user requirements, tests and dated version logs. Reusable dashboard development guidance belongs in a distinct `dashboard-development-skill` repository once created. The old `docs/DASHBOARD_SKILL_BLUEPRINT.md` is temporarily retained **as a frozen migration source** and should not be maintained in parallel after the separate repo is accessible.

For each later app iteration, **commit app code and its project-specific log first**, then explicitly decide whether a validated and broadly transferable lesson justifies a separate Skill update. `No change` is an acceptable outcome. If the Skill repo is not yet accessible, mark promotion pending rather than claiming that it happened.
