# Story 5.001: Implement Automatic Rescheduling for Missed Study Sessions

Status: ready-for-dev

## Story

As a student,
I want my study plan to automatically adjust when I mark a session as 'Missed',
so that my schedule remains realistic and I can stay on track without manual effort.

## Acceptance Criteria

1. When a user marks a study session as 'Missed' in the frontend, the remaining 'Not Started' sessions for that course are automatically rescheduled by the backend (AC1 from Tech Spec).
   - The rescheduling logic prioritizes distributing tasks evenly across available time slots before the exam date.

## Tasks / Subtasks

- [ ] Enhance the frontend's `updateSessionStatus` handler to make a `fire-and-forget` call to `POST /reschedule-plan` when a session is marked 'Missed'.
  - [ ] Pass `course_id` and `reason: "TASK_MISSED"` in the request body.
- [ ] Implement the `POST /reschedule-plan` endpoint in the FastAPI Backend.
  - [ ] Verify user authorization for the given `course_id`.
  - [ ] Fetch all 'Not Started' study sessions for the course.
  - [ ] Implement the core rescheduling algorithm to redistribute tasks.
  - [ ] Perform a bulk `UPDATE` on `scheduled_date` for affected `study_sessions` in Supabase.
- [ ] Ensure the backend rescheduling algorithm completes within performance requirements (< 5 seconds).
- [ ] Implement robust error handling and logging for the rescheduling process in the backend.

## Dev Notes

- Relevant architecture patterns and constraints: This story introduces core backend logic for plan adaptation. It involves interaction between the Next.js Frontend and FastAPI Backend, leveraging Supabase as the data store. The rescheduling algorithm should be efficient and transactional.
- Source tree components to touch: Existing frontend `updateSessionStatus` logic (modification), new FastAPI backend endpoint and rescheduling service, Supabase `study_sessions` table (update).
- Testing standards summary: Extensive unit tests for the backend rescheduling algorithm. Integration tests for the `POST /reschedule-plan` endpoint. E2E tests to verify marking a task 'Missed' leads to correct schedule adjustments on the dashboard (via real-time updates).

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Introduce new FastAPI endpoint in the backend, and backend service for rescheduling logic.

### References

- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Overview]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Objectives-and-Scope]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#System-Architecture-Alignment]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Detailed-Design]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Non-Functional-Requirements]
- [Source: docs/architecture/solution-architecture.md#2.-System-Context-Diagram-(C4-Level-1)]
- [Source: docs/architecture/solution-architecture.md#3.-Component-Diagram-(C4-Level-2)]

## Dev Agent Record

### Context Reference

<!-- Context Path: docs/sprint-artifacts/story-5-001.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

### Agent Model Used

gemini-1.5-flash

### Debug Log References

### Completion Notes List

### File List

### Learnings from Previous Story

**From Epic 5 - First story in epic - no predecessor context.**
