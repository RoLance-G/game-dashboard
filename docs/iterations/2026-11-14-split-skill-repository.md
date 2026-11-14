# 2026-11-14 — Split Game Dashboard docs from Dashboard Skill development

> Status: `partially completed` — project-side docs updated; separate Skill repository still needs user creation and access.  
> Repository: `RoLance-G/game-dashboard` (`main`)  
> App code: unchanged (v4)  
> Source: user's direct request to maintain project-specific Markdown here and reusable Dashboard Skill material in a separate GitHub repository.

## 1. User request and starting point

The user wants a new GitHub repository devoted to developing and iterating a reusable Dashboard Skill. The Game Dashboard repository should retain its own project Markdown. After **every application iteration**, first update and commit relevant app docs, **then** extract and evaluate reusable lessons, and update the external Skill repo only when needed.

Inspected the existing GitHub `main` files: `AGENTS.md`, `README.md`, `docs/DASHBOARD_SKILL_BLUEPRINT.md`, `docs/GAME_DASHBOARD_CASE_STUDY.md` and `docs/iterations/TEMPLATE.md`. The current one-repository approach mixed universal Skill guidance with app-specific records.

## 2. Decisions and rationale

| Decision | Why | Trade-off / condition |
|---|---|---|
| Two distinct repositories | Keep Game Dashboard facts separate from portable development instructions | Requires occasional cross-repo coordination |
| App docs and verified app commit first | Skill lessons should be grounded in actual results, not speculative plans | Reusable updates may lag the app release |
| Mandatory `Promote / No change / Pending` assessment | Avoid updating a global Skill for every app-specific tweak | Adds a short documentation check |
| Keep legacy blueprint temporarily | Do not discard its only GitHub copy before external repo exists | Must move/remove after remote migration is verified |
| Independent Skill update logs | Each general rule should link the specific project evidence | Two linked histories, not duplicate full transcripts |

## 3. Actual Game Dashboard changes

- `AGENTS.md`: two-stage cross-repository working agreement and verification requirements.
- `README.md`: documents project-only ownership and planned Skill destination.
- `docs/iterations/TEMPLATE.md`: adds mandatory Skill promotion assessment section.
- `docs/GAME_DASHBOARD_CASE_STUDY.md`: explains documentation ownership and transition.
- New append-only dated iteration record (this file).
- **No modifications** to `index.html`, IndexedDB schema, task data or Google Drive backup implementation.

## 4. Verification and remaining work

- Checked Markdown structure and links to repo-local paths; no personal credentials or backups intentionally included.
- This was documentation-only; no new application runtime tests are claimed.
- Current GitHub integration supports updating existing repositories, but **does not expose an action to create a new repository**.
- A prepared new Skill repository seed (with `SKILL.md`, reusable playbook, patterns, templates, and Skill change log) is a local deliverable, **not yet a published GitHub repo**.

## 5. Skill promotion assessment

- **Candidate:** an evidence-gated two-repository cycle: app code/docs/commit first → assess transferability → optional separate Skill update and separate commit.
- **Transferability:** high; applicable to multiple software/dashboard projects.
- **Decision:** `Pending access` — seed prepared, but new repository must be created/authorized before publishing.
- **Follow-up:** once the Skill repo is live, import and verify the seed. Then make a separate Game Dashboard docs-only cleanup commit to remove/redirect the frozen generic blueprint. Historical commits remain intact.
