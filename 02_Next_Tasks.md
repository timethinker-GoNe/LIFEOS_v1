# LifeGame Next Tasks

작성일: 2026-06-13

## 1. 현재 확정 사항

### 프로젝트
- 프로젝트명: LifeGame
- 핵심 비전: 인생 운영체제(Life Operating System)
- 핵심 구조: Life Goal → Project → Quest → Todo
- My Status를 첫 화면으로 확정

### ERD v0.2 확정 테이블
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

### v0.3 우선 확장 후보
- health_check_logs
- exercise_logs
- meal_logs
- water_logs

---

## 2. Codex에게 바로 시킬 작업 순서

### Step 1. 프로젝트 초기 구조 생성
- 프론트엔드/백엔드 기술 스택 결정
- DB 연결 설정
- 기본 라우팅 구조 생성
- 환경변수 구조 작성

추천 폴더 예시:

```text
lifegame/
  docs/
  frontend/
  backend/
  database/
  scripts/
```

---

### Step 2. DB Schema 작성

기준 파일:
- `03_ERD.md`
- `lifegame_erd_v0_2.json`
- `lifegame_erd_v0_2.xlsx`

작업:
- PostgreSQL 기준 migration SQL 작성
- enum 또는 check constraint 정의
- foreign key 정의
- index 정의
- seed 데이터 작성

우선순위:
1. users
2. life_goals
3. projects
4. life_goal_projects
5. quests
6. todos
7. quest_relations
8. calendar_events
9. status_logs
10. body_profiles
11. body_part_statuses

---

### Step 3. My Status API 설계

My Status 첫 화면에서 필요한 데이터:

```text
GET /api/my-status
```

응답 구성:
- user
- body_profile
- body_part_statuses
- upcoming_events
- core_quests
- active_projects
- project_todos
- latest_status_summary

---

### Step 4. My Status UI 개발

현재 화면 설계 기준:
- 상단 가로 네비게이션
- 왼쪽: 현재 상태 / 아바타 패널
- 중앙: 오늘의 핵심 퀘스트 + 진행중인 프로젝트
- 오른쪽 상단: 다가오는 일정 1~2개
- 오른쪽 중하단: 프로젝트별 할 일
- 하단: 신체 프로필 또는 컨디션 요약

운동/식단 요약은 첫 화면에서는 제외한다.

---

### Step 5. Projects 페이지 개발

주요 기능:
- 진행중인 프로젝트 전체 목록
- 중요도 / 마감일 / 상태 / 진행률 정렬
- 프로젝트 카드 클릭 시 Project Detail 이동

---

### Step 6. Health / Exercise / Diet 페이지 준비

v0.3에서 확장할 테이블:
- health_check_logs
- exercise_logs
- meal_logs
- water_logs

초기 기능:
- 물 섭취 기록
- 오늘 운동 추천/기록
- 식단 메모
- 체중/체지방 기록
- 부위별 상태와 연결

외부 건강 앱 연동은 후순위다.

---

## 3. 개발 우선순위

### 1순위
- DB schema
- My Status API
- My Status UI

### 2순위
- Projects
- Project Detail
- Life To Do

### 3순위
- Quest Board
- Life Goals

### 4순위
- Health / Exercise / Diet v0.3 확장

---

## 4. Codex 작업 지시문 예시

```text
LifeGame 프로젝트의 ERD v0.2 문서를 기준으로 PostgreSQL schema와 seed 데이터를 작성해줘.
핵심 구조는 Life Goal → Project → Quest → Todo이며,
확정 테이블은 users, life_goals, projects, life_goal_projects, quests, quest_relations, todos, status_logs, calendar_events, body_profiles, body_part_statuses이다.
각 테이블의 foreign key, status/priority enum, created_at/updated_at을 포함하고,
My Status 첫 화면에서 필요한 조회가 쉽도록 index를 함께 설계해줘.
```

---

## 5. 아직 결정해야 할 것

- 사용할 백엔드 프레임워크
- 사용할 프론트엔드 프레임워크
- DB는 PostgreSQL로 갈지 SQLite로 로컬 MVP를 먼저 할지
- 로그인/계정 기능을 MVP에서 넣을지
- progress 값을 저장할지 계산할지
- Quest 추천 로직을 rule-based로 시작할지 AI 기반으로 시작할지
