# LifeGame Progress

Last updated: 2026-06-18

## Current Project Location

The active project is located at:

`C:\Users\dadog\Desktop\Baradun\LIFEGAME_v2`

Do not use the old OneDrive path:

`C:\Users\dadog\OneDrive\Desktop\Baradun\LIFEGAME_v2`

The user intentionally rolled back OneDrive's Desktop-folder relocation.

## Current Phase

LifeGame is still in the planning and UI prototype phase. No production frontend,
backend, API, or PostgreSQL implementation exists yet.

The current working artifact is:

`dev/prototypes/my_status.html`

Use `sample_images/Real_final.png` as the original visual reference and
`sample_images/bw_removed_3.png` as the current avatar image asset.

## Stable Product Direction

- Product: LifeGame
- Vision: Life Operating System
- Core hierarchy: `Life Goal -> Project -> Quest -> Todo`
- MVP home screen: My Status
- Root folder contains planning/handoff documents.
- New development files belong under `dev/`.
- Prototype screens should clarify UI and storage requirements before PostgreSQL/API work.

## My Status Prototype

### Overall Layout

- Responsive dashboard intended primarily for a tablet-sized representative screen.
- Top navigation is retained from the reference design.
- Main content uses:
  - left avatar/current-status panel
  - right unified editable widget grid
- Dashboard should fit the viewport without unnecessary vertical scrolling.
- Panel height currently uses:
  - `clamp(640px, calc(100vh - 108px), 960px)`
- Dashboard sits close to the top navigation with reduced spacing.

### Avatar Panel

- Greeting: `고경태님 안녕하세요.`
- Greeting is a future nickname-driven value from user settings.
- Avatar asset: `sample_images/bw_removed_3.png`
- Geometric/Vitruvian-style background layer behind avatar.
- Compact top-left health stats:
  - `72kg`
  - `178cm`
  - `118/76`
- Condition summary remains at the bottom of the panel.
- Earlier age/height/weight full-width rows were removed.

### Widget Grid

- Center and right sections were merged into one continuous grid panel.
- Grid model: 6 columns x 8 rows.
- Widgets have explicit grid coordinates and sizes rather than automatic placement.
- Current default widgets:
  - upcoming schedule
  - upcoming deadlines
  - water habit
  - sugar-control habit
  - rules/habits
  - project progress
- Small widgets use compact labels/icons, such as `물` and `당`.
- Empty cells expose `+` buttons only while edit mode is active.
- The widget add menu opens near the selected empty cell.
- There is no separate floating add button or empty-state explanation box.

### Edit Mode

- A widget edit button exists beside the settings gear.
- Normal mode hides:
  - empty-slot plus buttons
  - remove buttons
  - resize handles
  - drag interactions
- Edit mode enables:
  - add widget
  - remove widget
  - resize using lower-right handles
  - move widgets by dragging
- Widget position is stored temporarily in DOM data attributes:
  - `data-col`
  - `data-row`
  - `data-cols`
  - `data-rows`
- Grid occupancy and collision detection are implemented.
- Dragging and resizing only apply placements that remain inside the 6 x 8 grid
  and do not overlap another visible widget.
- Empty-cell add buttons are hidden for occupied cells.
- Restoring a hidden widget searches for the nearest free placement to the selected cell.
- Layout persistence is not implemented.

### Theme Settings

- Top-right settings gear opens a side panel.
- Theme is the current active settings tab.
- Placeholder tabs exist for future layout and notification settings.
- Theme presets:
  - Clear Blue
  - Mint Focus
  - Soft Mono
  - Warm Light
- User-adjustable colors:
  - page background
  - primary/button color
  - panel color
  - text color
- Theme values are not persisted yet.

## Known Limitations

- Browser automation was unavailable during much of the prototype work.
- Several visual changes were checked using user screenshots rather than automated screenshots.
- Add-widget actions only restore existing prototype widgets.
- Layout, theme, nickname, and widget choices are not persisted.
- Mobile behavior has not received the same scrutiny as the tablet layout.
- The single HTML file contains substantial legacy CSS from discarded iterations and needs cleanup.

## Immediate Next Work

1. Open `dev/prototypes/my_status.html` and visually verify the latest edit-mode behavior.
2. Fix the viewport height based on the actual tablet/browser viewport if bottom whitespace remains.
3. Visually test grid collision behavior while dragging and resizing widgets.
4. Persist nickname, theme, widget visibility, position, and size in `localStorage`.
5. Clean discarded/unused CSS and markup from the prototype.
6. Decide whether the My Status prototype is sufficiently stable to extract its data contract.

## After Prototype Approval

1. Document component data requirements.
2. Map UI data to ERD v0.2.
3. Resolve schema gaps for:
   - user nickname/preferences
   - widget configuration
   - habits/rules
   - health metrics
4. Decide frontend/backend stack.
5. Create `dev/database/` and PostgreSQL migrations/seed data.
6. Define `GET /api/my-status`.
7. Convert the prototype into the real frontend.

## Existing Backlog

- Projects prototype
- Project Detail prototype
- Quest Board prototype
- Life To Do prototype
- PostgreSQL schema and seed data
- My Status API
- Real frontend/backend project structure
