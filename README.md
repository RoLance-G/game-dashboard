# Game Dashboard

A local-first game update and task dashboard deployed as a single GitHub Pages [`index.html`](./index.html). Personal task records live in browser IndexedDB, **not** in this GitHub repository.

## Documentation owned by the Game Dashboard repository

- [Game Dashboard case study](docs/GAME_DASHBOARD_CASE_STUDY.md) — app-specific architecture, data model, UI decisions, backup behavior and known risks.
- [Iteration log template](docs/iterations/TEMPLATE.md) — required for each feature, UI, performance, storage or docs iteration.
- [Iteration history](docs/iterations/) — append-only decisions, implementation details, actual tests and verification gaps.
- [Working agreement](AGENTS.md) — **read before changing the app**.

## Separate Dashboard Development Skill

Portable lessons will be maintained in an independent repository proposed as `RoLance-G/dashboard-development-skill` (**not yet created** as of this documentation update). The historical [Dashboard Skill blueprint](docs/DASHBOARD_SKILL_BLUEPRINT.md) remains here **temporarily for safe migration**; it is frozen and should not receive new general-purpose material. Once the new repository is created, granted access and verified, move ownership of general guidance there and replace/remove the legacy blueprint here.

**Mandatory sequence for each version:** finish and verify the app change → update **Game Dashboard-specific** Markdown and commit the project → decide whether a transferable lesson is new and sufficiently evidenced → **only if yes**, update the separate Skill repository, with its own dated note and commit. A decision of "no Skill change needed" is valid.

Do not commit personal IndexedDB JSON exports, Google Drive backups, OAuth tokens, Client Secrets or browser state.
