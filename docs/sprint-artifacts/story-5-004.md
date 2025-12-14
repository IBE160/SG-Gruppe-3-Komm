# Story 5.004: Implement Welcome Back Wizard Overdue Task Summary and Rescheduling Options

Status: ready-for-dev

## Story

As a student,
I want the "Welcome Back" wizard to show me my overdue tasks and give me clear options to reschedule them,
so that I can easily choose how to get back on track and see my updated plan immediately.

## Acceptance Criteria

1. The "Welcome Back" wizard summarizes the count of overdue tasks (AC4 from Tech Spec).
2. The wizard presents simple options for rescheduling overdue tasks: "Spread it Out", "Intensive Catch-up", "Fresh Start" (AC4 from Tech Spec).
3. Selecting an option triggers a call to `POST /reschedule-plan` with the appropriate `reason` (e.g., "WELCOME_BACK_SPREAD") (AC5 from Tech Spec).
4. Upon successful plan update, the wizard closes and the user is returned to the dashboard with the newly organized plan visible (AC5 from Tech Spec).
5. Visual feedback (e.g., animation of calendar reorganizing) is provided after option selection and before returning to dashboard.

## Tasks / Subtasks

- [ ] Enhance `WelcomeBackWizard` UI to display overdue task count.
- [ ] Implement UI elements for rescheduling options ("Spread it Out", "Intensive Catch-up", "Fresh Start").
- [ ] Implement `onClick` handlers for these options within the `WelcomeBackWizard`.
  - [ ] On click, call `POST /reschedule-plan` with the correct `course_id` and `reason`.
- [ ] Implement frontend logic to close the wizard and navigate to the dashboard upon successful plan update.
- [ ] Implement visual feedback (e.g., loading spinner, animation) during the rescheduling process.
- [ ] Ensure backend `ReschedulingService` correctly interprets and executes the "Welcome Back" rescheduling reasons.

## Dev Notes

- Relevant architecture patterns and constraints: This story completes the "Welcome Back" wizard functionality, integrating frontend UI with the backend rescheduling service. It heavily relies on existing `POST /reschedule-plan` endpoint and `ReschedulingService`.
- Source tree components to touch: Existing `WelcomeBackWizard` component (enhancement), existing frontend `DashboardManager` (to call backend endpoint), FastAPI backend `ReschedulingService` (enhancement).
- Testing standards summary: Component tests for `WelcomeBackWizard` option selection and feedback. Integration tests for the frontend-to-backend call to `POST /reschedule-plan` with different reasons. E2E tests for the full wizard flow, including successful plan update and dashboard return.

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Enhancing existing `WelcomeBackWizard` component.

### References

- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Overview]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Detailed-Design]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Workflows-and-Sequencing]
- [Source: docs/sprint-artifacts/tech-spec-epic-5.md#Acceptance-Criteria-Authoritative]
- [Source: docs/Fase-1/ux-design-specification.md#2.2-The-Defining-Experience:-The-"Welcome-Back"-Wizard]
- [Source: docs/architecture/solution-architecture.md#3.-Component-Diagram-(C4-Level-2)]
- [Source: docs/sprint-artifacts/story-5-001.md]
- [Source: docs/sprint-artifacts/story-5-002.md]
- [Source: docs/sprint-artifacts/story-5-003.md]

## Dev Agent Record

### Context Reference

<!-- Context Path: docs/sprint-artifacts/story-5-004.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

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
- **Architectural Decisions**: Extended dynamic plan adaptation functionality to handle early completion, reusing the `POST /reschedule-plan` endpoint and `ReschedulingService` from story-5-001. New rescheduling logic for pulling future tasks forward implemented.

**From Story 5.003 (Status: ready-for-dev)**
- **New Services/Components Created**: `WelcomeBackWizard` UI component.
- **Architectural Decisions**: Implemented frontend logic to store and retrieve last user activity, and detect conditions for displaying the "Welcome Back" wizard. Conditional rendering of the wizard based on login and overdue tasks.

[Source: docs/sprint-artifacts/story-5-001.md]
[Source: docs/sprint-artifacts/story-5-002.md]
[Source: docs/sprint-artifacts/story-5-003.md]
