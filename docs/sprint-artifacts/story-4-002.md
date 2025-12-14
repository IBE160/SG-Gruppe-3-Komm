# Story 4.002: Display Course Progress Bars

Status: ready-for-dev

## Story

As a student,
I want to see my progress in each course as a progress bar on the dashboard,
so that I can quickly understand my overall standing in each subject.

## Acceptance Criteria

1. The dashboard displays a progress bar for each course (AC2 from Tech Spec).
   - The progress bar accurately reflects the ratio of completed study sessions to total study sessions for that course.

## Tasks / Subtasks

- [ ] Implement a `CourseProgressBar` component.
  - [ ] Fetch total and completed study sessions for each course.
  - [ ] Calculate course progress percentage.
  - [ ] Render a visual progress bar based on the calculated percentage.
- [ ] Integrate `CourseProgressBar` component into the dashboard view.
- [ ] Ensure real-time updates to `study_sessions` are reflected in course progress bars.

## Dev Notes

- Relevant architecture patterns and constraints: This story extends the "daily-use loop" by visualizing course progress. It builds upon the existing Next.js Frontend and Supabase integration.
- Source tree components to touch: Dashboard component, a new `CourseProgressBar` component, and potentially updates to `DashboardManager` to include course progress calculation.
- Testing standards summary: Unit tests for course progress calculation logic. Component tests for `CourseProgressBar` in various states (e.g., 0%, 50%, 100% complete). Integration tests to ensure real-time updates correctly impact progress bar display.

### Project Structure Notes

- Alignment with unified project structure (paths, modules, naming): Introduce a new `CourseProgressBar` component within `src/components/`.

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

<!-- Context Path: docs/sprint-artifacts/story-4-002.context.xml --><!-- Path(s) to story context XML will be added here by context workflow -->

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

[Source: docs/sprint-artifacts/story-4-001.md]
