# Repository working agreement — Game Dashboard

This repository owns **the Game Dashboard app and its project-specific engineering history**. Reusable Dashboard-development Skill guidance belongs in the verified [separate Skill repository](https://github.com/RoLance-G/dashboard-development-skill), not here.

## Read first

1. Inspect the actual `index.html`, current GitHub branch, newest `docs/iterations/` entries, and `docs/GAME_DASHBOARD_CASE_STUDY.md`. Never assume an earlier assistant summary matches live source.
2. Use `docs/iterations/TEMPLATE.md` for every app, UI, storage, deployment or documentation iteration.
3. Read the [Dashboard Development Skill](https://github.com/RoLance-G/dashboard-development-skill/blob/main/SKILL.md) for transferable principles only when applicable. The former local generic blueprint has been migrated; project-specific documents remain here.

## Mandatory two-stage workflow for each iteration

### Stage 1 — Game Dashboard FIRST

1. Inspect the current project and explicitly define scope, data compatibility and rollback.
2. Implement, self-audit, test and verify the change. Distinguish static checks, mocks, browser tests and real third-party integrations.
3. Produce a **new append-only** `docs/iterations/YYYY-MM-DD-<slug>.md` using the template. Capture the user request, rationale, actual code/UX changes, tests, unresolved risks and **Skill promotion assessment**.
4. Update `docs/GAME_DASHBOARD_CASE_STUDY.md` when app-specific architecture, validation status, constraints or decisions changed.
5. Commit project code + project documents and re-fetch changed paths to verify the project commit. Verify GitHub Pages separately when deployment matters.

### Stage 2 — Only then evaluate the Skill

6. Assess whether the completed project iteration produced a durable, evidenced, nonduplicative principle applicable to other dashboards.
7. Record **Promote / No change / Pending evidence or access** in the project iteration log, including the reasoning. It is normal for many app iterations **not** to change the Skill.
8. **Only after the project commit is verified**, if warranted, inspect and update the separate Skill repo's `SKILL.md` and/or `references/`; add a dated Skill-side `docs/updates/` entry linking to the source project log and project commit. Commit and re-fetch that repo independently.
9. If the Skill repo does not exist, is not accessible, or evidence is insufficient, mark the proposed update pending. Do not block the app release or claim the Skill was updated.

## Safety and quality

- Preserve the current IndexedDB database identifier and JSON import/export contract unless a tested migration is requested.
- Avoid giant eager DOMs, repeated whole-data scans, redundant CSS override layers, unnecessary listeners and expensive animations.
- Cover active, archived, empty, error, import/export and restore flows when applicable.
- Never commit real user exports, JSON backups, OAuth tokens, Client Secrets or other private credentials.
- Do not rewrite historical iteration logs to disguise earlier uncertainty. Append corrections.
- This is an assistant/contributor workflow, **not** a background automation or guarantee that future chats without repo access can push changes.

## Completion checklist

- [ ] Current code and project docs inspected
- [ ] Implementation and appropriate tests completed, with gaps stated
- [ ] Project-specific dated iteration Markdown committed with code (or docs-only commit)
- [ ] Game Dashboard case study updated when necessary
- [ ] Project commit and changed files verified from GitHub
- [ ] Skill promotion decision documented (including valid "no change")
- [ ] If warranted, Skill repo updated **after** project commit, with evidence and separate changelog
- [ ] User informed of actual commits, deployment state and remaining risks
