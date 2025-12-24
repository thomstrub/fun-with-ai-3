# Product Requirements Document (PRD) - TODO App Upgrade: Due Dates, Priority, Filters

## 1. Overview

We are upgrading the basic TODO app (currently supporting title and completed state) to add due dates, simple priorities, and date-based filters. The goal is a simple, teachable MVP with no backend changes and local-only storage, enabling users to better identify urgent tasks and organize work without increasing complexity.

---

## 2. MVP Scope

- **Title:** required.
- **Priority:** enum `P1 | P2 | P3`; default `P3`.
- **Due Date:** optional; ISO format `YYYY-MM-DD`. Invalid values are ignored (treated as absent).
- **Filters:** `All`, `Today`, `Overdue`.
- **Filter behavior:**
  - `All`: shows all tasks (completed and incomplete).
  - `Today` and `Overdue`: show incomplete tasks only.
- **Storage:** local-only; no backend or external storage changes.

---

## 3. Post-MVP Scope

- **Overdue highlighting:** visually emphasize overdue tasks.
- **Sorting rules:**
  - Order: overdue first → priority (P1 → P3) → due date ascending → undated last.

---

## 4. Out of Scope

- **Notifications**
- **Recurring tasks**
- **Multi-user**
- **Keyboard navigation**
- **External storage / backend changes**