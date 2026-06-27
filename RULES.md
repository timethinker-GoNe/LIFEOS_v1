# LifeGame Project Rules

This file records implementation and product rules that future Codex sessions should follow.

## Product Rules

- Use `Life Goal -> Project -> Quest -> Todo` as the core hierarchy.
- Treat `My Status` as the MVP home screen.
- Keep the first My Status screen focused:
  - current status/avatar panel
  - upcoming 1-2 events
  - today's core quests
  - active projects
  - project todos
  - basic body/condition profile
- Do not add exercise or diet summaries to the first My Status screen unless the user changes this decision.
- Keep the visual direction bright, simple, modern, and not overly decorative.

## Data Rules

- ERD v0.2 is the current database baseline.
- Preserve the 11 confirmed tables unless the user explicitly approves a schema change.
- Use UUID primary keys unless a later architecture decision changes this.
- Keep `created_at` and `updated_at` on mutable entities.
- Use indexes that support My Status queries early, especially by `user_id`, status, due/start dates, and priority.
- v0.3 health expansion candidates are:
  - `health_check_logs`
  - `exercise_logs`
  - `meal_logs`
  - `water_logs`

## Engineering Rules

- Prefer small, readable foundations over clever abstractions while the app is being born.
- Keep planning/handoff files at the repository root.
- Put new app development files under `dev/`.
- Use standalone HTML prototypes to explore screen design before building the final app structure.
- Let prototype component needs inform PostgreSQL schema/API priorities.
- After every visible UI/prototype change, verify that the rendered result actually matches the user's requested layout and visual intent. Do not rely only on code inspection.
- Before claiming a UI element was removed, hidden, moved, or restyled, check the final cascade/layout state for conflicting CSS rules and confirm the element is not still occupying visible space.
- If browser or screenshot verification is unavailable, explicitly say the UI was not visually verified and avoid confident claims about the rendered appearance.
- When replacing visual assets such as avatars, prefer simple robust shapes or real assets over complex unverified SVG paths that can visually break.
- Keep planning docs and implementation docs separate:
  - product truth: `01_LifeGame_Master_Plan.md`
  - next implementation tasks: `02_Next_Tasks.md`
  - schema truth: `03_ERD.md` and `lifegame_erd_v0_2.json`
  - Codex operating notes: `CODEX.md`, `PROGRESS.md`, `RULES.md`
- Update `PROGRESS.md` after meaningful work.
- Update this file only when a rule is stable enough to guide future work.

## Documentation Rules

- When adding acronyms, explain them once on first use.
- Keep Korean product notes natural and precise.
- Keep generated technical artifacts in English where that matches common tooling, such as SQL identifiers and API names.
