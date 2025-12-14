# Story 5.002: Implement Automatic Plan Adjustment for Early Completion

Status: ready-for-dev

## Story

As a student,
I want my study plan to automatically adjust when I complete a session ahead of schedule,
so that I can make progress faster and optimize my study time.

## Acceptance Criteria

1. When a user completes a study session ahead of schedule, the remaining 'Not Started' sessions for that course are automatically adjusted (AC2 from Tech Spec).
   - The adjustment logic should attempt to pull future tasks forward into newly available time slots.
   - This should also trigger the `POST /reschedule-plan` endpoint in the backend.

## Tasks / Subtasks

- [ ] Enhance the frontend's `updateSessionStatus` handler to detect early completion.
  - [ ] If early completion is detected, make a `fire-and-forget` call to `POST /reschedule-plan` with `course_id` and `reason: "EARLY_COMPLETION"`.
- [ ] Enhance the `ReschedulingService` in the FastAPI Backend to handle `reason: "EARLY_COMPLETION"`.
  - [ ] Implement logic to identify newly available time slots.
  - [ ] Implement logic to pull future 'Not Started' tasks into these slots.
  - [ ] Perform a bulk `UPDATE` on `scheduled_date` for affected `study_sessions` in Supabase.
- [ ] Ensure the backend rescheduling algorithm considers the impact of early completion on future tasks.
- [ ] Implement robust error handling and logging for this specific rescheduling scenario in the backend.

## Dev Notes

- Relevant architecture patterns and constraints: This story extends the dynamic plan adaptation functionality. It reuses the `POST /reschedule-plan` endpoint and `ReschedulingService` from story-5-001, but with new rescheduling logic.
- Source tree components to touch: Existing frontend `updateSessionStatus` logic (modification), existing FastAPI backend `ReschedulingService` (modification), Supabase `study_sessions` table (update).
- Testing standards summary: Unit tests for the new early completion rescheduling logic in the backend. Integration tests for the `POST /reschedule-plan` endpoint with the `EARLY_COMPLETION` reason. E2E tests to verify early completion leads to correct schedule adjustments on the dashboard.

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Reusing existing `ReschedulingService` and `DashboardManager`.

### References

- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Overview]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Objectives-and-Scope]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#System-Architecture-Alignment]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Detailed-Design]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Non-Functional-Requirements]
- [Source: docs/architecture/solution-architecture.md#2.-System-Context-Diagram-(C4-Level-1)]
- [Source: docs/architecture/solution-architecture.md#3.-Component-Diagram-(C4-Level-2)]
- [Source: docs/sprint-artifacts/story-5-001.md]

## Dev Agent Record

### Context Reference

<!-- Context Path: docs/sprint-artifacts/story-5-002.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

### Agent Model Used

gemini-1.5-flash

### Debug Log References

### Completion Notes List

### File List

### Learnings from Previous Story

**From Story 5.001 (Status: ready-for-dev)**
- **New Services/Components Created**: FastAPI backend endpoint `POST /reschedule-plan`, `ReschedulingService` (backend), enhancement of frontend `updateSessionStatus` handler.
- **Architectural Decisions**: Introduction of core backend logic for dynamic plan adaptation, involving Next.js Frontend, FastAPI Backend, and Supabase interaction. Implementation of a fire-and-forget call from frontend to backend for rescheduling.
- **Interfaces to Reuse**: `POST /reschedule-plan` endpoint (request/response body definitions).

[Source: docs/sprint-artifacts/story-5-001.md]
