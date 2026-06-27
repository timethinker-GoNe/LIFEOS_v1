# LifeGame Conversation and Decision History

Last updated: 2026-06-18

This document preserves the important context from the original long Codex conversation.
It is intended for a new session that does not have access to that chat history.

## 1. How The Work Started

The repository originally contained only planning and ERD handoff materials:

- `README.md`
- `01_LifeGame_Master_Plan.md`
- `02_Next_Tasks.md`
- `03_ERD.md`
- `lifegame_erd_v0_2.json`
- `lifegame_erd_v0_2.xlsx`
- `lifegame_planning_viewer.html`
- sample images

The user asked Codex to inspect the folder and create persistent working-memory documents.
Codex created:

- `CODEX.md`
- `PROGRESS.md`
- `RULES.md`

The agreed folder convention was:

- repository root: planning and handoff files
- `dev/`: all new application development
- `dev/prototypes/`: standalone HTML UI prototypes

The agreed implementation order was:

1. Build HTML screen prototypes.
2. Determine component and storage requirements from the screens.
3. Map those requirements to the ERD.
4. Build PostgreSQL schema/seed data.
5. Define APIs.
6. Build the real frontend/backend application.

## 2. My Status Initial Direction

The user selected `sample_images/Real_final.png` as the visual reference.

Initial requested elements:

- keep the left avatar section
- keep upcoming schedule
- move body-profile information inside the avatar panel
- use the remaining area as a flexible widget board
- initial widgets:
  - upcoming schedule
  - upcoming deadlines
  - rules/habits such as drinking water and avoiding sweets
  - project progress

The user did not want My Status to be permanently dominated by:

- today's core quests
- project-specific todos

Those may be added later as optional widgets.

## 3. Important Failure and Rule Changes

Codex initially tried to hide the old quest/todo column with CSS. A later `.stack`
rule overrode `display: none`, so the supposedly removed panels remained visible and
pushed the widget board downward.

Codex also claimed the layout was correct without visually verifying the rendered page.
The user strongly objected, correctly pointing out that the visible result contradicted
the request.

As a result, `RULES.md` was updated with these principles:

- Verify visible UI changes in the rendered result.
- Check final CSS cascade before claiming an element was removed or moved.
- If visual verification is unavailable, say so explicitly.
- Do not confidently describe unverified rendered appearance.

The old quest/todo markup was then removed from the DOM entirely.

## 4. Avatar Evolution

Several avatar approaches were attempted:

1. CSS body assembled from simple shapes.
   - It looked like connected sticks.
   - Rejected.
2. Hand-written SVG human figures.
   - They rendered badly and looked broken.
   - Rejected.
3. `gemini_figure.png`.
   - The checkerboard transparency pattern was baked into the image.
   - Codex's attempted background removal was also judged poor.
   - Rejected.
4. User-provided transparent assets:
   - `bw_removed_1.png`
   - `bw_removed_2.png`
   - `bw_removed_3.png`

Current asset:

`sample_images/bw_removed_3.png`

The user explicitly prefers using a real bitmap asset over Codex hand-drawing complex
human SVGs.

Current avatar panel decisions:

- human silhouette should be large and visually dominant
- geometric/Vitruvian-style lines and nodes behind the figure
- compact health values in the upper-left
- values do not need verbose labels
- examples:
  - weight icon + `72kg`
  - height icon + `178cm`
  - health/blood-pressure icon + `118/76`
- full-width age/height/weight rows waste space and were removed
- greeting is `고경태님 안녕하세요.`
- later the name should come from the nickname in settings

## 5. Widget Board Evolution

The widget area went through several structures:

1. Fixed right-side panels.
2. A general widget board.
3. Half default widgets / half empty add zone.
4. Three equal page columns:
   - avatar
   - default widgets
   - add zone
5. Unified center/right widget canvas.

The current direction is a single unified 6-column x 8-row grid next to the avatar.

The user wants:

- flexible widget sizes
- widgets movable by drag
- widgets resizable by dragging the border/handle
- different information density for different sizes
- examples:
  - large habit widget: `물 많이 마시기` plus details/streak
  - small habit widget: `물`
  - very small representation may eventually become icon-only

Current prototype widgets include:

- upcoming schedule
- upcoming deadlines
- water habit
- sugar-control habit
- habits/rules list
- active project status

## 6. Add Widget Interaction

Rejected approaches:

- separate right-side dashed add panel
- top-right floating plus button
- empty-state explanation box saying the grid is empty

Current direction:

- each empty grid cell has a subtle `+`
- `+` is visible only in edit mode
- clicking it opens the widget-add menu near that cell
- if a widget occupies the area, the widget visually covers the underlying plus cells

Future correction needed:

- calculate actual occupancy
- disable/hide plus buttons for occupied cells instead of relying only on visual covering

## 7. Normal Mode vs Edit Mode

The user identified that always-active drag/resize controls would interfere with future
touch interactions.

Current decision:

- default is normal mode
- edit-mode button sits beside the settings gear
- only edit mode enables:
  - add buttons
  - remove buttons
  - resize handles
  - widget dragging

The current prototype implements this with a body class:

`body.editing`

The mode is not persisted yet.

## 8. Widget Positioning

Earlier widgets used normal CSS Grid auto-placement. The user requested explicit movement.

Current prototype uses:

- `data-col`
- `data-row`
- `data-cols`
- `data-rows`

The JavaScript applies explicit grid coordinates and updates them while dragging.

Current default coordinates/sizes are prototype values only.

Important missing behavior:

- collision detection
- occupied-cell calculation
- preventing overlap
- finding nearest valid free position
- saving layout

## 9. Panel Height and Tablet Priority

The page is intended primarily as a representative tablet dashboard.

The user does not want routine vertical scrolling.

Height iterations included:

- overly tall fixed panel
- fixed `720px`
- viewport-based clamp

Current CSS uses:

`clamp(640px, calc(100vh - 108px), 960px)`

The user previously showed screenshots with unused space below the dashboard. This remains
an area to verify in the actual new session/browser.

The navigation-to-dashboard gap was reduced because the user wanted them close together.

## 10. Theme Settings

A settings gear opens a side settings panel.

Current active sub-tab:

- Theme

Reserved future tabs:

- Layout
- Notifications

Theme presets:

- Clear Blue
- Mint Focus
- Soft Mono
- Warm Light

Direct controls:

- background color
- button/primary color
- panel color
- text color

The user expects more settings later, so theme was intentionally implemented as a sub-tab,
not as the whole settings experience.

No settings persistence exists yet.

## 11. User Experience Preferences

The user values:

- direct visual fidelity to the requested layout
- checking the actual rendered result
- efficient use of tablet viewport space
- modularity and future configurability
- compact UI rather than explanatory labels
- icon/value presentation where text labels are unnecessary
- editable widgets without edit controls interfering with normal interaction
- real visual assets rather than poor hand-drawn substitutes

Avoid:

- confidently claiming a UI change without checking the result
- leaving supposedly removed content hidden only through fragile CSS
- oversized explanatory headings like `위젯 보드`
- visible instructional text that is obvious from context
- wasting rows on global add buttons or empty-state messages
- forcing scrolling on the main tablet dashboard

## 12. Current Files and Authority

Read in this order:

1. `CODEX.md`
2. `PROGRESS.md`
3. `HISTORY.md`
4. `RULES.md`
5. `01_LifeGame_Master_Plan.md`
6. `02_Next_Tasks.md`
7. `03_ERD.md`
8. `lifegame_erd_v0_2.json`

Current prototype:

`dev/prototypes/my_status.html`

Current avatar:

`sample_images/bw_removed_3.png`

Original visual reference:

`sample_images/Real_final.png`

## 13. Recommended First Prompt In The New Session

Use:

> LifeGame 작업을 이어가자. 먼저 CODEX.md, PROGRESS.md, HISTORY.md, RULES.md를 모두
> 읽고 dev/prototypes/my_status.html의 현재 구현을 확인해. 실제 프로젝트 경로는
> C:\Users\dadog\Desktop\Baradun\LIFEGAME_v2 이고 OneDrive 경로는 사용하지 마.

