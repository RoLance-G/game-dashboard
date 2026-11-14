# Game Dashboard

A local-first game update and task dashboard, served as a single static [`index.html`](./index.html) from GitHub Pages. The app stores user records in the browser's IndexedDB, **not** in this Git repository.

## Documentation for future dashboard development

- [Reusable Dashboard Skill blueprint](docs/DASHBOARD_SKILL_BLUEPRINT.md) — portable development workflow and lessons for other dashboards.
- [Game Dashboard case study](docs/GAME_DASHBOARD_CASE_STUDY.md) — current architecture, decisions, design principles, risks and verified limits.
- [Iteration log template](docs/iterations/TEMPLATE.md) — mandatory format for future version conversations.
- [Historical v1–v4 retrospective](docs/iterations/2026-11-14-v1-v4-retrospective.md) — backfilled source-grounded decisions.
- [Documentation-workflow iteration](docs/iterations/2026-11-14-knowledge-workflow.md) — why the knowledge base was created.
- [Working agreement for coding assistants](AGENTS.md) — **read before changing this repository**.

**Future version rule:** every code/design/feature iteration gets a dated `docs/iterations/YYYY-MM-DD-<slug>.md` capturing its conversation-driven requirements, implementation, test evidence, trade-offs and deployment status, committed to GitHub together with its changes. Logs describe engineering decisions, not verbatim private chat archives.

**Privacy:** Do not commit personal IndexedDB JSON exports, Google Drive backups, OAuth tokens, Client Secrets or other local browser state.