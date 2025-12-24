# Cloud Architecture Overview

This diagram shows the system context for the monorepo: a React frontend interacting with an Express API backed by an in-memory SQLite store (better-sqlite3). There are no external services or persistent cloud databases.

```mermaid
C4Container
title TODO App - System Context (Monorepo)
Person(user, "User", "Uses the web UI")
System_Boundary(s1, "TODO App"){
  Container(web, "React Frontend", "React", "Runs in browser; renders UI; calls API")
  Container(api, "Express API", "Node.js/Express", "REST endpoints for tasks")
  ContainerDb(db, "In-Memory Store", "SQLite (better-sqlite3)", "Volatile storage in memory")
}
Rel(user, web, "Uses", "HTTPS")
Rel(web, api, "Fetch JSON", "HTTP")
Rel(api, db, "SQL queries")
```

## User Creates a TODO – Sequence

```mermaid
sequenceDiagram
title User Creates a TODO
participant U as User
participant FE as React Frontend (Browser)
participant API as Express API
participant DB as In-Memory Store (SQLite)
U->>FE: Enter title/description/due date
FE->>FE: Normalize due date to YYYY-MM-DD
FE->>FE: Validate title (required)
alt Title missing or blank
  FE-->>U: Show validation error
else Valid input
  FE->>API: POST /api/tasks {title, description, due_date}
  API->>DB: INSERT INTO tasks (...)
  DB-->>API: OK (new id)
  API-->>FE: 201 Created {task}
  FE->>FE: Refresh list view
  FE-->>U: Show new task
end
```
