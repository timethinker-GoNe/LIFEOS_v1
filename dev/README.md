# LifeGame Development Workspace

This folder contains new app development work.

The repository root stays focused on planning and handoff documents. New prototypes,
database files, frontend code, backend code, scripts, and implementation notes should
live under this folder.

## Intended Structure

```text
dev/
  prototypes/
  database/
  frontend/
  backend/
  scripts/
  docs/
```

## Current Build Order

1. Design standalone HTML screen prototypes.
2. Extract component and data requirements from those prototypes.
3. Build PostgreSQL schema, migrations, and seed data.
4. Define API contracts.
5. Implement the real app pages.

## First Prototype Target

Start with `My Status`, because it is the MVP home screen and touches the most important
data surfaces: user status, avatar/body profile, upcoming events, core quests, active
projects, and project todos.
