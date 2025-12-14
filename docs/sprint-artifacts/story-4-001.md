# Story 4.001: Dashboard Initial Load and Basic Status Update

Status: ready-for-dev

## Story

As a student,
I want to see my study activities on a dashboard and update their status,
so that I can easily track my progress and keep my study plan up-to-date.

## Acceptance Criteria

1. The dashboard displays a calendar view of the user's study activities (AC1 from Tech Spec).
2. A user can update the status of a study activity ('Not Started', 'Completed', 'Missed') (AC4 from Tech Spec).
3. Progress updates are saved automatically and are persistent across sessions (AC5 from Tech Spec).
4. Changes made to the study plan are reflected on the dashboard in near real-time without requiring a page refresh (AC6 from Tech Spec).

## Tasks / Subtasks

- [ ] Implement dashboard component to display study activities.
  - [ ] Fetch initial study session data from Supabase.
  - [ ] Render study activities in a calendar view.
- [ ] Implement `StudyTaskCard` component for displaying individual study activities.
  - [ ] Design interactive element to update status.
  - [ ] Integrate status update logic with `DashboardManager.updateSessionStatus`.
- [ ] Implement `DashboardManager` service to handle data fetching and status updates.
  - [ ] `getDashboardData()` to fetch initial courses and sessions.
  - [ ] `updateSessionStatus(sessionId, newStatus)` to send updates to Supabase.
  - [ ] Integrate Supabase Realtime for `study_sessions` table changes.
- [ ] Ensure all data interactions are subject to RLS policies.
- [ ] Implement optimistic updates for task status changes in the UI.

## Dev Notes

- Relevant architecture patterns and constraints: This story heavily relies on the "daily-use loop" described in the Solution Architecture, focusing on the Next.js Frontend's direct integration with Supabase for data fetching and updates. Supabase Realtime is crucial for AC6.
- Source tree components to touch: Next.js Frontend components (Dashboard, StudyTaskCard), client-side services (DashboardManager).
- Testing standards summary: Unit tests for logic in Zustand store and course progress calculation. Component tests for StudyTaskCard in all states. Integration/E2E tests for full flow, especially real-time updates.

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Adhere to Next.js project structure, organize components and services logically.
- Detected conflicts or variances (with rationale): None apparent at this stage.

### References

- [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Overview]
- [Source: docs/sprint-artifacts/tech-spec-epic-4.md#System-Architecture-Alignment]
- [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Detailed-Design]
- [Source: docs/sprint-artifacts/tech-spec-epic-4.md#Acceptance-Criteria-Authoritative]
- [Source: docs/architecture/solution-architecture.md#2.-System-Context-Diagram-(C4-Level-1)]
- [Source: docs/architecture/solution-architecture.md#3.-Component-Diagram-(C4-Level-2)]
- [Source: docs/Fase-1/ux-design-specification.md#6.2-Custom-Component-Definitions]

## Dev Agent Record

### Context Reference

<!-- Context Path: docs/sprint-artifacts/story-4-001.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

### Agent Model Used

gemini-1.5-flash

### Debug Log References

### Completion Notes List

### File List
