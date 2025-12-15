# Story 5.003: Implement Welcome Back Wizard Trigger and UI

Status: ready-for-dev

## Story

As a student,
I want to be greeted by a "Welcome Back" wizard when I return to the app after a long absence,
so that I can easily get back on track with my study plan without feeling overwhelmed.

## Acceptance Criteria

1. On login, the frontend checks the date of the user's last activity (AC3 from Tech Spec).
2. If the last activity exceeds a defined threshold (e.g., 3 days) and there are overdue tasks, the "Welcome Back" wizard is displayed instead of the standard dashboard.
3. The wizard presents a user-friendly UI as described in the UX spec, with supportive messaging ("Welcome back! Life happens. Let's get you back on track.").

## Tasks / Subtasks

- [ ] Implement frontend logic to store and retrieve the date of last user activity (e.g., last login or interaction).
- [ ] Implement frontend logic on login to compare last activity date with current date and check for overdue tasks.
- [ ] Develop the "Welcome Back" wizard UI component.
  - [ ] Design the full-screen, non-judgmental modal with supportive messaging.
  - [ ] Implement initial display of overdue task count.
- [ ] Integrate the wizard to conditionally replace the dashboard view.
- [ ] Ensure the wizard handles cases where there are no overdue tasks despite a long absence (it should not be displayed).

## Dev Notes

- Relevant architecture patterns and constraints: This story focuses heavily on frontend logic and UI implementation, interacting with user session data and existing dashboard data. It adheres to UX principles of guidance over control and clarity over clutter.
- Source tree components to touch: Frontend login/session management, new "Welcome Back" wizard UI component, Dashboard component (conditional rendering).
- Testing standards summary: Unit tests for last activity date calculation and overdue task detection. Component tests for the "Welcome Back" wizard UI states (e.g., displaying overdue tasks). E2E tests for the full login flow, verifying the wizard appears under correct conditions.

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Introduce new UI component for the wizard within `src/components/`. Update login flow logic.

### References

- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Overview]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Objectives-and-Scope]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Detailed-Design]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Workflows-and-Sequencing]
- [Source: docs/Fase-1/ux-design-specification.md#2.2-The-Defining-Experience:-The-"Welcome-Back"-Wizard]
- [Source: docs/architecture/solution-architecture.md#3.-Component-Diagram-(C4-Level-2)]
- [Source: docs/sprint-artifacts/story-5-001.md]
- [Source: docs/sprint-artifacts/story-5-002.md]

## Dev Agent Record

### Context Reference

<!-- Context Path: docs/sprint-artifacts/story-5-003.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

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

**From Story 5.002 (Status: ready-for-dev)**
- **New Services/Components Created**: N/A (reused existing components, but enhanced logic)
- **Architectural Decisions**: Extended dynamic plan adaptation functionality to handle early completion, reusing the `POST /reschedule-plan` endpoint and `ReschedulingService` from story-5-001. New rescheduling logic for pulling future tasks forward implemented.

[Source: docs/sprint-artifacts/story-5-001.md]
[Source: docs/sprint-artifacts/story-5-002.md]
