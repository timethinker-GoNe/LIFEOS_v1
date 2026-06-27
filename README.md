# LifeGame ERD Handoff Package

이 패키지는 Codex 또는 Claude Code에 넘겨서 LifeGame 프로젝트의 초기 DB/API/UI 작업을 시작하기 위한 자료입니다.

## 포함 파일

- `01_LifeGame_Master_Plan.md`: 현재 기획 기준 문서
- `02_Next_Tasks.md`: 앞으로 할 일 및 Codex 지시 순서
- `03_ERD.md`: ERD v0.2 상세 문서
- `lifegame_erd_v0_2.json`: Codex가 파싱하기 좋은 구조화 ERD
- `lifegame_erd_v0_2.xlsx`: 사람이 보기 좋은 ERD 스프레드시트
- `lifegame_planning_viewer.html`: 브라우저에서 여는 기획 요약 뷰어

## 권장 사용법

1. Codex에게 `01_LifeGame_Master_Plan.md`, `02_Next_Tasks.md`, `03_ERD.md`, `lifegame_erd_v0_2.json`을 함께 제공한다.
2. 먼저 PostgreSQL schema 및 seed 데이터를 생성하게 한다.
3. 이후 My Status API와 첫 화면 구현으로 이어간다.

## 확정 ERD

v0.2 확정 테이블:
- users
- life_goals
- projects
- life_goal_projects
- quests
- quest_relations
- todos
- status_logs
- calendar_events
- body_profiles
- body_part_statuses

v0.3 우선 확장 후보:
- health_check_logs
- exercise_logs
- meal_logs
- water_logs
