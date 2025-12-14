# Story 4.003: View Study Activity Details

Status: ready-for-dev

## Story

As a student,
I want to click on a study activity on the dashboard to view its details,
so that I can get more information about the task and prepare for it.

## Acceptance Criteria

1. A user can click on a study activity to view its details (AC3 from Tech Spec).
   - Clicking a study activity displays a modal or dedicated view with comprehensive details (e.g., topic, description, estimated time, associated course).

## Tasks / Subtasks

- [ ] Enhance `StudyTaskCard` to be clickable.
  - [ ] Implement `onClick` handler for the `StudyTaskCard`.
- [ ] Implement a `StudyActivityDetailModal` component.
  - [ ] Display details such as topic title, description, course name, scheduled date/time, estimated hours.
  - [ ] Fetch additional details if not already available in the initial `study_sessions` data.
- [ ] Integrate `StudyActivityDetailModal` with the Dashboard view.
  - [ ] Pass selected study activity data to the modal.
- [ ] Ensure data displayed is consistent with the data model.

## Dev Notes

- Relevant architecture patterns and constraints: This story extends the user interaction within the "daily-use loop". It builds upon the existing Next.js Frontend and Supabase integration, primarily interacting with the `study_sessions` and `syllabus_topics` data models.
- Source tree components to touch: `StudyTaskCard` (modification), new `StudyActivityDetailModal` component, Dashboard component (integration), and potentially `DashboardManager` for fetching more detailed information if needed.
- Testing standards summary: Component tests for `StudyActivityDetailModal` in various states (e.g., with full details, minimal details). E2E tests to verify clicking a card correctly opens the modal and displays accurate information.

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Introduce a new `StudyActivityDetailModal` component within `src/components/`.

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

<!-- Context Path: docs/sprint-artifacts/story-4-003.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

### Agent Model Used

gemini-1.5-flash

### Debug Log References

### Completion Notes List

### File List

### Learnings from Previous Story

**From Story 4.001 (Status: ready-for-dev)**
- **New Services/Components Created**: Dashboard component, `StudyTaskCard` component, `DashboardManager` service. Supabase Realtime integration pattern established.
- **Architectural Decisions**: Next.js Frontend direct integration with Supabase for data fetching and updates. Optimistic updates for UI feedback.
- **Technical Debt**: Tasks in "Tasks / Subtasks" section do not explicitly reference Acceptance Criteria numbers (e.g., "(AC: #1)"). Consider improving traceability in future stories.
- **Interfaces to Reuse**: `IDashboardManager` interface (`getDashboardData`, `updateSessionStatus`, `onSessionsChange`).

**From Story 4.002 (Status: ready-for-dev)**
- **New Services/Components Created**: `CourseProgressBar` component.
- **Architectural Decisions**: Extended "daily-use loop" by visualizing course progress. Built upon existing Next.js Frontend and Supabase integration.
- **Technical Debt**: The same minor issue of AC mapping in tasks persists.

[Source: docs/sprint-artifacts/story-4-001.md]
[Source: docs/sprint-artifacts/story-4-002.md]
