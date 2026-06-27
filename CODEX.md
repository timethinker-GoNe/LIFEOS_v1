# Codex Working Memory

Read this file first before changing the LifeGame project.

## Active Project Path

Use:

`C:\Users\dadog\Desktop\Baradun\LIFEGAME_v2`

Do not use:

`C:\Users\dadog\OneDrive\Desktop\Baradun\LIFEGAME_v2`

The user intentionally rolled back OneDrive's unwanted Desktop-folder relocation.

## Required Reading Order

1. `CODEX.md`
2. `PROGRESS.md`
3. `HISTORY.md`
4. `RULES.md`
5. `01_LifeGame_Master_Plan.md`
6. `02_Next_Tasks.md`
7. `03_ERD.md`
8. `lifegame_erd_v0_2.json`

`HISTORY.md` contains important conversation context, rejected approaches, user
preferences, and reasons behind the current UI direction. Do not skip it.

## Project Snapshot

- Project: LifeGame
- Vision: Life Operating System
- Core model: `Life Goal -> Project -> Quest -> Todo`
- MVP home screen: My Status
- Current phase: UI prototype and storage-requirement discovery
- Current artifact: `dev/prototypes/my_status.html`
- Current avatar asset: `sample_images/bw_removed_3.png`

## Current Priority

Stabilize the My Status tablet prototype:

1. Visually verify normal/edit mode.
2. Tune viewport height.
3. Add grid collision and occupancy logic.
4. Persist nickname, theme, and widget layout.
5. Extract the data/storage contract.

After prototype approval:

1. Map UI data needs to ERD v0.2.
2. Decide the application stack.
3. Build PostgreSQL migrations and seed data.
4. Define `GET /api/my-status`.
5. Build the real application.

## Working Convention

- Keep planning/handoff files at the repository root.
- Put development files under `dev/`.
- Update `PROGRESS.md` after meaningful work.
- Update `HISTORY.md` when a design decision, rejected direction, or user preference
  would be important to a future session.
- Update `RULES.md` when a stable working rule is established.
- Do not claim visible UI changes are correct without rendered verification.
- When asked for a recap, use `PROGRESS.md` for current state and `HISTORY.md` for context.
