# Reusable Dashboard Development — Skill Source / Playbook

> **Purpose:** A reusable source document from which to create a formal dashboard-development Skill for future projects (not a verbatim chat transcript, not itself an installed Skill).
>
> **Evidence:** Derived from Game Dashboard development discussions and checked against the v4 repository `index.html` (2026-11-14). Project-specific facts live in `GAME_DASHBOARD_CASE_STUDY.md`; everything below is intended to be portable across domains.

## 1. What the future Skill should do

**Trigger examples:** “Build a tracker/dashboard from a spreadsheet”, “Improve my existing dashboard UI”, “Make my browser-only dashboard scale for years”, “Add backups/restore”, “Audit rendering and storage performance”, “Deploy this dashboard to GitHub Pages”, or “Continue the next iteration.”

**Inputs to collect / inspect (do not guess):**
- Existing repository, source files, screenshots, and/or data shape; existing deployment URL and branch.
- Key entities and operations: add/edit/delete/complete, ordering, filters, archives, shortcuts, exports.
- Expected data growth; device/browser constraints; offline needs; hosting, auth and privacy expectations.
- Non-negotiable visual direction and what must stay unchanged.
- Available backup and rollback path before storage-related work.

**Outputs:**
1. A working artifact or repository commit, with tests and limits disclosed.
2. A brief deploy/rollback guide and exact validation steps.
3. A new `docs/iterations/YYYY-MM-DD-<slug>.md` covering the actual conversation and work, not just the code diff.
4. Updated reusable guidance if the iteration uncovers a durable lesson.

## 2. Recommended end-to-end workflow

### Phase A — Discover the existing system

- Inspect actual code rather than relying on the previous assistant's description.
- Identify rendering, state, persistence, import/export, migration, event handling, and external integrations.
- Trace the user journey, including *empty, failure, loading, and archival* states.
- Establish a baseline (code size, data stores, key views, usability/performance bottlenecks).

### Phase B — Design information architecture first

- Make primary objects and core tasks prominent; navigation, tools, and metadata secondary.
- Establish one navigation/selection source of truth; eliminate duplicated selectors when they convey the same state.
- Use type scale, spacing, proximity, and low/high contrast purposefully. Don't scatter colors or hardcoded spacing across components.
- Use **semantic tokens** (`--accent`, `--text`, `--muted`, `--surface`, `--border`, spacing steps) to support future evolution.
- Give each region one clearly dominant action; make destructive and auxiliary actions quieter.
- Keep iconography, headings, empty states, hover/focus and error states coherent.
- Reference material can inspire a style; avoid copying an aesthetic at the expense of task completion.

### Phase C — Build for multi-year data growth

Choose persistence **based on constraints**:
- `localStorage`: simple preference data or tiny records, synchronous and size-limited. Not ideal as the primary long-term store for thousands of records.
- `IndexedDB`: browser-local structured data, async transactions and indexes; appropriate for static hosting with no server, **but not cross-device synchronization**.
- Hosted database: for multi-device sync, scheduled server jobs, collaboration, or true remote backup without a browser visit; brings auth, security and cost/operations.

For local-first dashboards:
- Use stable IDs and explicit storage schema/indexes; version migrations rather than silently changing data shape.
- Keep current/active records readily available. Load archive/history only on demand in bounded batches.
- Cache or materialize summary counters where helpful; watch for stale counters and invalidation.
- Avoid re-querying or re-sorting full data for every row/game; prefer one-pass aggregation and scoped rendering.
- Use event delegation for repeated rows, debounced search, and minimal re-rendering after small interactions.
- Be honest about DOM scaling: archive lazy-loading doesn't solve a page with tens of thousands of **active** rows; use pagination or virtualization when measurements justify it.
- Treat persistence success, snapshot timing, concurrent writes, and transaction failure handling as correctness-critical.

### Phase D — Protect data and design recovery

- Require a verified JSON export before destructive migration/import; preserve legacy data until recovery is tested.
- Export **all** underlying records, including archives not present in UI memory; don't serialize only visible state.
- Keep a stable, documented JSON compatibility contract and validate incoming data before replacing stores.
- Confirm exported file parses, data counts match, and restore works in a clean browser/test profile.
- Distinguish a *source-code deployment* (e.g. GitHub Pages) from *user data storage* (e.g. IndexedDB); deployments don't automatically back up user data.
- A scheduled task running in the cloud cannot access an arbitrary user's browser IndexedDB without a sync path.

### Phase E — External backup integration with least privilege

- Decide between (A) on-open / user-triggered backup and (B) a server-scheduled backup of synchronized data.
- For Google Drive in a static frontend: use Google Identity Services, least-privilege `drive.file`, and a user-authorized folder selection workflow; never embed a Client Secret in a public page.
- Store access tokens in memory, not durable browser storage or Git; allow explicit re-authentication and visible retry.
- A fresh page load typically has no token, so **checking backup due != fully automatic backup after reload**. Show a useful reminder.
- Upload the full database-derived JSON, check API response and target folder before marking a backup successful. Verify failure handling without updating last-success state.
- Plan for future large exports, duplicate uploads on retried network failures, Drive quota, consent-screen testing limits, and manual recovery.
- Do not claim real OAuth/Drive integration is validated from mock-network tests alone.

### Phase F — Self-audit and test

**Functional:** add/edit/delete/reorder; filters/search; archive/restore; category rename/delete; import/export and compatibility.  
**Persistence:** migration, async write queue, transaction failures, storage quota, browser origin changes, multi-tab behavior.  
**UI:** typography hierarchy, contrast, visual regression at common screen sizes, empty/loading/errors, long labels, keyboard focus.  
**Performance:** counts of active/archived rows, initial load time, DOM size, repeat scans, event-listener growth, style recalculations, CSS override accumulation.  
**Integrations:** OAuth popup, permissions, token expiration, folder select/cancel, upload retry, actual end-to-end upload and restore under real account.  

Use a *testing evidence table* to distinguish code inspection, syntax checks, mocked tests, local browser tests, and production tests. Never label a test “passed” if it wasn't run.

### Phase G — Ship safely and document the conversation

1. Confirm target repository and branch, read latest remote files, check for concurrent edits.
2. Keep commits scoped; do not overwrite unrelated files. Preserve a rollback commit.
3. Prepare `docs/iterations/YYYY-MM-DD-<slug>.md` from `docs/iterations/TEMPLATE.md` **in the same change set**.
4. Re-fetch remote file(s) to verify the GitHub write, then separately verify hosting/deployment when possible.
5. Present the user with commit link, tests actually performed, risks and the next manual verification step.
6. Maintain an append-only history: later iterations should reference rather than rewrite earlier decision records.

## 3. Design lessons extracted from the project

| Earlier symptom | Better reusable practice |
|---|---|
| Good-looking UI felt like a CRUD admin panel | Prioritize typography hierarchy, clear primary action, reduced button parity |
| Repetitive blue lines, HUD labels, borders | Use semantic color roles and reserve bright accent for actionable states |
| Settings had a second game list | Reuse a single navigation/selection model across views |
| Incrementally appended CSS grew unwieldy | Consolidate tokens/selectors and perform before/after visual regression |
| Long-term archives made localStorage questionable | IndexedDB with indexes, summaries and lazy archive loading |
| Sidebar repeated whole-task scans | Aggregate in one pass, then render counts |
| Previous exports omitted potential unloaded history | Export from the database, not only the rendered state |
| Weekly backup was mistaken for an unattended job | Clarify OAuth/page-lifecycle constraints before choosing architecture |
| A Git commit was mistaken for completed live deployment | Verify repo write and hosted page independently |
| A chat transcript alone wasn't reusable | Capture rationale, implementation, tests, trade-offs and lessons in dated Markdown |

## 4. Skill design notes for future conversion

A future Skill author can turn this document into `SKILL.md` with:
- **Name:** `dashboard-development-workflow`.
- **Description:** build, refine, audit and safely deploy local-first or cloud-backed dashboards, including data migration, UI system, backup, testing and per-iteration documentation.
- **Workflow:** Sections 2A–2G, with mandatory repo inspection and per-iteration Markdown creation.
- **References:** `GAME_DASHBOARD_CASE_STUDY.md` as an example; the `iterations/` directory as real decisions and evidence.
- **Guards:** never assume a deployment URL, OAuth status, cloud capability or database contents without verification; never upload personal backup data to Git; do not substitute screenshots for editable source.
- **Acceptance test:** a simulated iteration must result in both a tested code change **and** a scoped, traceable Markdown note (or a docs-only note if no code changed).

This playbook intentionally records transferable principles separately from Game Dashboard's exact classes, store names, URLs and theme.