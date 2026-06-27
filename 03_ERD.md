# LifeGame ERD v0.2

작성일: 2026-06-13
## 1. 확정 테이블

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

## 2. 핵심 관계

```text
users 1:N life_goals
users 1:N projects
life_goals N:M projects via life_goal_projects
projects 1:N quests
quests N:M quests via quest_relations
quests 1:N todos
projects 1:N todos
users 1:N calendar_events
users 1:N status_logs
users 1:N body_profiles
users 1:N body_part_statuses
```

## 3. 테이블 상세

### users

사용자 기본 정보. 초기에는 1인 앱이어도 웹서비스 확장성을 위해 유지한다.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| email | varchar(255) | UNIQUE | True |  |  |
| name | varchar(100) |  | False |  |  |
| avatar_url | text |  | True |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- unique(email)

### life_goals

인생 단위의 장기 목표.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| title | varchar(200) |  | False |  |  |
| description | text |  | True |  |  |
| category | varchar(50) |  | True |  |  |
| priority | smallint |  | False | 3 |  |
| status | varchar(30) |  | False | active |  |
| progress | numeric(5,2) |  | False | 0 |  |
| start_date | date |  | True |  |  |
| target_date | date |  | True |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- status
- priority

### projects

Life Goal을 달성하기 위한 중기 단위 프로젝트.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| title | varchar(200) |  | False |  |  |
| description | text |  | True |  |  |
| category | varchar(50) |  | True |  |  |
| status | varchar(30) |  | False | active |  |
| priority | smallint |  | False | 3 |  |
| progress | numeric(5,2) |  | False | 0 |  |
| start_date | date |  | True |  |  |
| target_date | date |  | True |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- status
- priority
- target_date

### life_goal_projects

Life Goal과 Project의 다대다 연결. weight는 목표 기여도.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| life_goal_id | uuid | FK → life_goals.id | False |  |  |
| project_id | uuid | FK → projects.id | False |  |  |
| weight | numeric(5,2) |  | False | 1.0 |  |
| created_at | timestamptz |  | False |  |  |

Indexes:
- life_goal_id
- project_id
- unique(life_goal_id, project_id)

### quests

프로젝트 내 중간 달성 단위 또는 미션.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| project_id | uuid | FK → projects.id | True |  |  |
| title | varchar(200) |  | False |  |  |
| description | text |  | True |  |  |
| importance | smallint |  | False | 3 |  |
| difficulty | smallint |  | False | 3 |  |
| status | varchar(30) |  | False | todo |  |
| progress | numeric(5,2) |  | False | 0 |  |
| quest_type | varchar(50) |  | True |  |  |
| start_date | date |  | True |  |  |
| due_date | date |  | True |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- project_id
- status
- importance
- due_date

### quest_relations

Quest Board를 위한 퀘스트 간 관계.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| source_quest_id | uuid | FK → quests.id | False |  |  |
| target_quest_id | uuid | FK → quests.id | False |  |  |
| relation_type | varchar(30) |  | False |  |  |
| created_at | timestamptz |  | False |  |  |

Indexes:
- source_quest_id
- target_quest_id
- relation_type

### todos

실행 가능한 가장 작은 행동 단위. quest_id/project_id는 nullable.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| quest_id | uuid | FK → quests.id | True |  |  |
| project_id | uuid | FK → projects.id | True |  |  |
| title | varchar(200) |  | False |  |  |
| description | text |  | True |  |  |
| status | varchar(30) |  | False | todo |  |
| priority | smallint |  | False | 3 |  |
| due_date | date |  | True |  |  |
| completed_at | timestamptz |  | True |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- quest_id
- project_id
- status
- priority
- due_date

### status_logs

사용자의 상태 기록. MVP에서는 유연한 key-value 로그로 사용한다.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| status_type | varchar(50) |  | False |  |  |
| value | text |  | True |  |  |
| numeric_value | numeric(10,2) |  | True |  |  |
| unit | varchar(30) |  | True |  |  |
| note | text |  | True |  |  |
| recorded_at | timestamptz |  | False |  |  |
| created_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- status_type
- recorded_at

### calendar_events

다가오는 일정 및 캘린더 이벤트.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| title | varchar(200) |  | False |  |  |
| description | text |  | True |  |  |
| event_type | varchar(50) |  | True |  |  |
| start_at | timestamptz |  | False |  |  |
| end_at | timestamptz |  | True |  |  |
| location | varchar(255) |  | True |  |  |
| related_project_id | uuid | FK → projects.id | True |  |  |
| related_quest_id | uuid | FK → quests.id | True |  |  |
| priority | smallint |  | False | 3 |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- start_at
- priority
- related_project_id

### body_profiles

사용자의 기본 신체 프로필 스냅샷. 가장 최신 record를 My Status에서 사용한다.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| age | smallint |  | True |  |  |
| gender | varchar(30) |  | True |  |  |
| height_cm | numeric(5,2) |  | True |  |  |
| weight_kg | numeric(5,2) |  | True |  |  |
| body_fat_percentage | numeric(5,2) |  | True |  |  |
| basal_metabolic_rate | integer |  | True |  |  |
| recorded_at | timestamptz |  | False |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- recorded_at

### body_part_statuses

부위별 상태. My Status 아바타/신체 프로필과 연결된다.

| column | type | key | nullable | default | note |
|---|---:|---|---:|---|---|
| id | uuid | PK | False |  |  |
| user_id | uuid | FK → users.id | False |  |  |
| body_part | varchar(50) |  | False |  |  |
| status | varchar(30) |  | False | unknown |  |
| note | text |  | True |  |  |
| last_checked_at | timestamptz |  | True |  |  |
| created_at | timestamptz |  | False |  |  |
| updated_at | timestamptz |  | False |  |  |

Indexes:
- user_id
- body_part
- status

## 4. Enum / 값 규칙

### common_status

`active`, `paused`, `completed`, `archived`

### todo_status

`todo`, `in_progress`, `done`, `cancelled`

### quest_status

`todo`, `in_progress`, `done`, `blocked`, `cancelled`

### relation_type

`prerequisite`, `related`, `blocked_by`, `parent_child`

### body_part_status

`normal`, `tired`, `watch`, `needs_care`, `pain`, `unknown`

### event_type

`work`, `health`, `personal`, `project`, `social`, `other`

### priority_scale

1=highest, 5=lowest

## 5. v0.3 우선 확장 후보

- `health_check_logs`: 검진, 통증, 병원 방문, 건강 체크 기록
- `exercise_logs`: 운동 기록
- `meal_logs`: 식단 기록
- `water_logs`: 물 섭취 기록
