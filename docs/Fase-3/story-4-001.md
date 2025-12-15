# Story 4.001: Dashboard Initial Load and Basic Status Update

Status: ready-for-dev

## Story

As a student,
I want to see my study activities on a dashboard and update their status,
so that I can easily track my daily progress.

## Acceptance Criteria

1.  The dashboard successfully loads and displays a calendar view of the user's study activities.
    (Source: tech-spec-epic-4.md#AC1)
2.  A user can update the status of a study activity (e.g., 'Not Started', 'Completed', 'Missed') by interacting with the `StudyTaskCard` component.
    (Source: tech-spec-epic-4.md#AC4, ux-design-specification.md#Component:StudyTaskCard)
3.  Changes to a study activity's status are saved automatically and are persistent across sessions.
    (Source: tech-spec-epic-4.md#AC5)

## Tasks / Subtasks

-   [ ] Implement initial Dashboard component for displaying study activities. (AC: #1)
    -   [ ] Fetch `study_sessions` for the current user from Supabase.
    -   [ ] Render `StudyTaskCard` components for each session.
-   [ ] Develop the `StudyTaskCard` component to display individual study activities. (AC: #1)
    -   [ ] Implement visual states for 'Not Started', 'In Progress', 'Completed', 'Missed'.
-   [ ] Implement functionality to update study activity status via `StudyTaskCard`. (AC: #2)
    -   [ ] Implement click handler for status cycling (`Not Started` -> `In Progress` -> `Completed`).
    -   [ ] Implement "x" icon for marking as 'Missed' (on hover).
-   [ ] Integrate `DashboardManager.updateSessionStatus` to persist status changes to Supabase. (AC: #3)
    -   [ ] Ensure status updates are transactional and durable.
-   [ ] Add unit tests for `StudyTaskCard` component states and interactions.
-   [ ] Add integration tests for dashboard loading and status update persistence.

## Dev Notes

-   **Relevant architecture patterns and constraints:**
    -   The Next.js Frontend will directly interact with Supabase for `study_sessions` data (fetch and update).
    -   Row Level Security (RLS) on `study_sessions` table ensures data isolation per user.
    -   The `status` field in `study_sessions` table uses an enum `('Not Started', 'In Progress', 'Completed', 'Missed')`.
    -   Client-side state management for dashboard will use Zustand.
    -   `@supabase/supabase-js` will be used for all Supabase interactions.
    (Source: docs/architecture/solution-architecture.md#3. Component Diagram, docs/architecture/solution-architecture.md#4. Data Model, docs/sprint-artifacts/tech-spec-epic-4.md#System Architecture Alignment)

-   **Source tree components to touch:**
    -   `src/components/dashboard/Dashboard.tsx` (new)
    -   `src/components/study-task-card/StudyTaskCard.tsx` (new)
    -   `src/services/dashboard-manager.ts` (new)
    -   `src/stores/zustand-store.ts` (modify for `study_sessions` state)

-   **Testing standards summary:**
    -   Unit tests for Zustand store and `StudyTaskCard` component.
    -   Integration/E2E tests for dashboard load and status update persistence.
    -   Focus on happy path for MVP.
    (Source: docs/sprint-artifacts/tech-spec-epic-4.md#Test Strategy Summary)

### Project Structure Notes

-   New components will follow existing component structure in `src/components/`.
-   New services will follow existing service structure in `src/services/`.
-   State management will integrate with the existing Zustand store.
(Source: docs/Fase-1/ux-design-specification.md#6.1 Component Strategy)

### References

-   [Source: docs/architecture/solution-architecture.md#3. Component Diagram]
-   [Source: docs/architecture/solution-architecture.md#4. Data Model]
-   [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Overview]
-   [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Objectives and Scope]
-   [Source: docs/sprint-artifacts/tech-spec-epic-4.md#System Architecture Alignment]
-   [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Detailed Design]
-   [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Acceptance Criteria (Authoritative)]
-   [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Test Strategy Summary]
-   [Source: docs/Fase-1/ux-design-specification.md#2.1 Defining Experience]
-   [Source: docs/Fase-1/ux-design-specification.md#6.2 Custom Component Definitions#Component:StudyTaskCard]

## Dev Agent Record

### Context Reference
- [x] sprint-artifacts/story-4-001.context.xml

### Agent Model Used

gemini-1.5-flash

### Debug Log References

### Completion Notes List

### File List
NEW: src/components/dashboard/Dashboard.tsx
NEW: src/components/study-task-card/StudyTaskCard.tsx
NEW: src/services/dashboard-manager.ts
MODIFIED: src/stores/zustand-store.ts

## Change Log

