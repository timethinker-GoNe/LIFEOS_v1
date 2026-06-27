# LifeGame Master Plan v0.2

작성일: 2026-06-13

## 1. 프로젝트 개요

### 프로젝트명
LifeGame

### 비전
LifeGame은 목표, 프로젝트, 일정, 기억, 인간관계를 하나의 AI가 통합 관리하는 인생 운영체제(Life Operating System, 삶 전체를 관리하는 플랫폼)이다.

기존의 Todo 앱이나 일정 관리 앱은 특정 영역만 관리한다. LifeGame은 사용자의 삶 전체를 하나의 시스템으로 연결하여 관리하는 것을 목표로 한다.

---

## 2. 핵심 철학

### 사람의 삶은 연결되어 있다
삶은 다음 요소들이 서로 영향을 주며 이루어진다.

- 목표
- 프로젝트
- 행동
- 기억
- 인간관계
- 취미
- 건강
- 커리어
- 자산

LifeGame은 이러한 요소들을 개별 서비스가 아닌 하나의 통합 시스템으로 관리한다.

---

## 3. 핵심 데이터 구조

LifeGame의 가장 중요한 구조는 다음과 같다.

```text
Life Goal → Project → Quest → Todo
```

### Life Goal
인생 단위의 장기 목표.

예시:
- 건강한 삶
- 경제적 자유
- 행복한 가정
- 성공적인 사업

### Project
목표를 달성하기 위한 중기 단위 프로젝트.

예시:
- 다이어트
- AI 사업 개발
- 영어 학습
- 투자 포트폴리오 구축

### Quest
프로젝트 내의 달성 단위.

예시:
- MVP 개발
- 5kg 감량
- 영어 시험 준비

### Todo
실행 가능한 가장 작은 행동 단위.

예시:
- 로그인 페이지 구현
- 30분 걷기
- 영어 단어 50개 암기

---

## 4. 현재 MVP 페이지 구조

### 1. My Status
LifeGame의 메인 첫 화면이다.

역할:
- 오늘의 현재 상태 확인
- 다가오는 일정 1~2개 확인
- 오늘의 핵심 퀘스트 확인
- 진행중인 프로젝트 확인
- 프로젝트별 할 일 확인
- 기본 신체/컨디션 프로필 확인

현재 확정된 화면 방향:
- 밝은 톤 기반
- 심플하고 모던한 구성
- 너무 장식적이지 않음
- 적당한 그림자와 입체감
- 그리드형 정보 배치
- 아바타/상태 패널은 가장 왼쪽
- 아바타는 파란색 실루엣, 배경은 흰색
- 오른쪽 상단에는 다가오는 일정 1~2개
- 그 아래에는 프로젝트별 할 일
- 운동/식단 요약은 첫 화면에서는 제외

### 2. Life Goals
인생 목표 목록 및 상세 관리 페이지.

### 3. Projects
사용자가 수행하는 프로젝트 목록 페이지.

### 4. Project Detail
프로젝트 상세 페이지.

포함 요소:
- 진행률
- 일정
- 관련 Quest
- 관련 Todo
- 프로젝트 로그/메모

### 5. Quest Board
LifeGame의 핵심 차별화 기능.

Quest들을 시각적으로 연결하여 보여주는 페이지. 기존 Todo 리스트가 아닌 Quest Network 형태를 제공한다.

### 6. Life To Do
인생 전체 관점의 할 일 관리 페이지.

---

## 5. MVP 로드맵

### Phase 1
목표: 핵심 시스템 검증.

구성:
- My Status
- Life Goals
- Projects
- Quest Board
- Life To Do

### Phase 2
생산성 기능 강화.

구성:
- Calendar
- AI Recommendation
- Schedule Assistant

### Phase 3
기억 관리 시스템 구축.

구성:
- Memory
- Photo Analysis

### Phase 4
인간관계 관리 시스템 구축.

구성:
- Social Status

### Phase 5
완전한 AI 인생 비서.

구성:
- Life OS AI Agent

---

## 6. AI 비서 비전

최종 목표는 사용자가 질문하면 “오늘 무엇을 해야 하는가”를 AI가 답하는 것이다.

예시:

사용자:
> 오늘 뭐 하지?

AI:
> 현재 인생 목표 기준 우선순위는 다음과 같습니다.
> 1. LifeGame 로그인 기능 개발
> 2. 운동 30분
> 3. 투자 공부 1시간
>
> 추천 이유: 현재 목표 달성에 가장 큰 영향을 주는 행동들입니다.

---

## 7. ERD v0.2 확정 범위

현재 확정된 테이블은 다음 11개다.

```text
users
life_goals
projects
life_goal_projects
quests
quest_relations
todos
status_logs
calendar_events
body_profiles
body_part_statuses
```

이 11개 테이블은 My Status, Life Goals, Projects, Quest Board, Life To Do, Calendar 기본 연동을 커버한다.

---

## 8. Health / Exercise / Diet v0.3 우선 확장 예정

전체 구조를 잡은 뒤 실제로 가장 먼저 개선하면서 사용할 가능성이 높은 페이지는 건강/운동/식단 페이지다.

따라서 v0.3 우선 확장 후보는 다음과 같다.

```text
health_check_logs
exercise_logs
meal_logs
water_logs
```

초기에는 다른 건강 앱과의 연동 없이, 사용자가 직접 입력하고 기록하는 방식으로 시작한다. 건강 앱 연동은 추후 계획으로 둔다.

---

## 9. 용어 규칙

약어 사용 시 최초 1회 반드시 설명한다.

예시:
- MVP (Minimum Viable Product, 최소 기능 제품)
- ERD (Entity Relationship Diagram, 개체 관계도)
- API (Application Programming Interface, 시스템 간 연결 인터페이스)
- AI (Artificial Intelligence, 인공지능)

---

## 10. 다음 작업 방향

1. ERD v0.2를 기준으로 DB schema 작성
2. My Status 첫 화면 개발
3. Projects / Project Detail / Quest Board / Life To Do 순서로 확장
4. Health / Exercise / Diet 페이지 설계 및 ERD v0.3 확장
5. My Status와 건강/운동/식단 요약 위젯 연결
