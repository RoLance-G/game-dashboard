# Repository working agreement — Game Dashboard

This file is the **repo-local workflow contract** for any coding assistant or human contributor working on this repository.

## Start here

1. Read `docs/DASHBOARD_SKILL_BLUEPRINT.md` (reusable dashboard-building method).
2. Read `docs/GAME_DASHBOARD_CASE_STUDY.md` (this app's constraints, architecture, decisions, and known limitations).
3. Read the latest entries in `docs/iterations/` and inspect the actual `index.html` before designing changes.
4. Distinguish verified code behavior, prior assistant claims, and unverified real-world integrations.

## Non-negotiable rules for every version iteration

1. Preserve the user's existing data and functional behavior unless change is explicitly requested. Keep the same IndexedDB database and JSON import/export contract unless a **tested migration** is part of the task.
2. Avoid unnecessary frameworks, global event listeners, repeated O(n²) scans, huge initial DOMs, needless CSS overrides, and high-cost animation/blur. Prefer clear state management and lazy historical loading.
3. Back up before risky storage/schema changes; test empty, active, archived, imported, and failure states. Never imply mock tests equal production verification.
4. Do **not** commit personal OAuth tokens, Client Secrets, user data exports, Google Drive backup JSON files, or local browser settings to the repository.
5. **Every iteration MUST produce a new Markdown summary** at `docs/iterations/YYYY-MM-DD-<short-slug>.md` based on `docs/iterations/TEMPLATE.md`. Log the user request, decisions, alternatives, actual changes, tests, limitations, and deploy status. A request can include UI-only, performance, storage, cloud backup, or docs-only changes.
6. Commit that iteration log **together with the code** when possible. If no code changes, commit a documentation-only log. Update reusable guidance or case study when a new pattern or lesson emerges. Do not overwrite the historic log; treat entries as append-only.
7. Before pushing, inspect the repository and current branch, examine the diff, and avoid replacing unrelated files. Verify GitHub accepted the write and re-read changed paths; do not claim GitHub Pages publication without independent verification.
8. End each version response with the commit link, concise changes, test outcomes, deployment/verification status, and unresolved risks.

## Delivery checklist

- [ ] Inspect source and prior iteration notes
- [ ] Define scope and compatibility guarantees
- [ ] Implement minimally; review readability/performance/security
- [ ] Run applicable syntax, behavior, integration, and visual checks; note any gaps
- [ ] Create dated Markdown iteration note from `TEMPLATE.md`
- [ ] Update `DASHBOARD_SKILL_BLUEPRINT.md` or case study if lessons generalize
- [ ] Commit code + docs to the intended branch and re-fetch to verify
- [ ] Clearly distinguish Git commit success from live-site availability

**Important:** This rule is repository guidance, not a background process. A future assistant must still have this repo and authenticated GitHub access to write a log; nothing runs automatically when nobody initiates an iteration.