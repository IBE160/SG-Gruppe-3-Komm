# Epic Technical Specification: Dynamic Plan Adaptation

Date: 2025-12-08
Author: BIP
Epic ID: 5
Status: Draft

---

## Overview

This document provides the technical specification for Epic 5: Dynamic Plan Adaptation. This epic implements the "smart" features that make the study planner truly adaptive. It covers the automatic rescheduling of tasks when a user falls behind and the "Welcome Back" wizard designed to help users get back on track after a break. This functionality is critical to the core value proposition of reducing student stress and keeping the plan achievable. The implementation will involve a combination of frontend triggers, backend logic, and database updates.

## Objectives and Scope

**In-Scope:**
-   Automatic rescheduling of remaining topics when a study session is marked as 'Missed'.
-   Adjustment of the plan when a study session is completed ahead of schedule.
-   A "Welcome Back" wizard that triggers for users returning after a long absence.
-   The wizard will summarize overdue tasks and provide simple options for rescheduling them.

**Out-of-Scope:**
-   Proactive notifications to the user about falling behind.
-   AI-powered suggestions for *how* to study a topic differently.
-   Manual drag-and-drop rescheduling by the user on the calendar.

## System Architecture Alignment

This epic leverages the backend-centric model for complex business logic, as defined in the solution architecture.

-   **Component Interaction:**
    1.  The **Next.js Frontend** detects a trigger event (e.g., a task is marked 'Missed', or a user logs in after a long absence).
    2.  It sends a request to a dedicated endpoint on the **FastAPI Backend**.
    3.  The **FastAPI Backend** contains the core rescheduling logic. It fetches the current state of the user's plan from the **Supabase Database**, recalculates the schedule for future tasks, and performs a bulk `UPDATE` on the affected `study_sessions`.
    4.  Thanks to Supabase Realtime (from Epic 4), the user's dashboard will update automatically to reflect the new schedule.
-   **Rationale:** Placing the complex rescheduling logic in the backend ensures it is consistent, testable, and can be invoked from different triggers without duplicating code on the client.

## Detailed Design

### Services and Modules

| Service/Module | Responsibility | Owner |
| :--- | :--- | :--- |
| **Next.js Frontend** | Triggers rescheduling events. Implements the UI for the "Welcome Back" wizard. | Frontend Team |
| **FastAPI Backend** | Contains the core rescheduling algorithm and exposes an endpoint to trigger it. | Backend Team |
| **Supabase Database** | The source of truth for the current plan state and the target for the updated plan. | Supabase (Managed) |

### Data Models and Contracts

This epic heavily reads and updates the `study_sessions` table. No data model changes are required.

-   **Contract:** The rescheduling algorithm must only operate on sessions with a status of 'Not Started' or 'Missed'. It must not alter 'Completed' or 'In Progress' sessions.

### APIs and Interfaces

**FastAPI Backend Endpoint:**

`POST /reschedule-plan`
-   **Request Body:** `{ "course_id": 123, "reason": "TASK_MISSED" | "WELCOME_BACK_SPREAD" }`
-   **Response Body:** `{ "success": true, "updated_sessions": 45 }`
-   **Action:**
    1.  Fetches all `study_sessions` for the given `course_id` that are not yet 'Completed'.
    2.  Gathers the remaining topics/hours to be scheduled.
    3.  Gathers the available future time slots up to the `exam_date`.
    4.  Re-distributes the remaining study sessions across the available slots.
    5.  Performs a bulk `UPDATE` on the `scheduled_date` for the affected sessions.

### Workflows and Sequencing

1.  **Automatic Rescheduling (Task Missed):**
    -   User marks a task as 'Missed' in the frontend (as in Epic 4).
    -   The `updateSessionStatus` handler in the frontend, after updating the status, makes a fire-and-forget call to `POST /reschedule-plan` with the relevant `course_id`.
    -   The backend reschedules the plan.
    -   The user's dashboard updates via the existing real-time subscription.

2.  **"Welcome Back" Wizard:**
    -   On login, the frontend checks the date of the last activity. If it exceeds a threshold (e.g., 3 days) and there are overdue tasks, it displays the wizard instead of the dashboard.
    -   The wizard presents the options described in the UX spec ("Spread it Out", "Intensive Catch-up", "Fresh Start").
    -   Based on the user's choice, the frontend calls the `POST /reschedule-plan` endpoint with the appropriate `reason`.
    -   The backend executes the rescheduling, and upon a success response, the frontend closes the wizard and shows the newly organized dashboard.

## Non-Functional Requirements

### Performance

-   The rescheduling algorithm on the backend must complete in under 5 seconds, even for a course with hundreds of study sessions.
-   The algorithm should be optimized to minimize the number of database queries. It should fetch all necessary data upfront, perform calculations in memory, and then write the results back in a single bulk update.

### Security

-   The `/reschedule-plan` endpoint must be protected and verify that the requesting user owns the `course_id`.

### Reliability/Availability

-   The rescheduling algorithm must be transactional. If any part of it fails, the user's study plan should not be left in a corrupted or partially updated state.

### Observability

-   Log the execution time of the rescheduling algorithm.
-   If the algorithm fails for any reason, log the error with the `course_id` and the state of the plan that caused the failure.

## Dependencies and Integrations

| Dependency | Type | Purpose |
| :--- | :--- | :--- |
| **`fastapi`, `psycopg2-binary`**| Python Packages (Backend)| For the backend API and database connection. |
| **`axios`** | NPM Package (Frontend) | For calling the `/reschedule-plan` endpoint. |
| **`date-fns`** | NPM Package (Frontend) | For date calculations to determine if the "Welcome Back" wizard should be shown. |

## Acceptance Criteria (Authoritative)

1.  **AC1:** When a user marks a study session as 'Missed', the remaining 'Not Started' sessions for that course are automatically rescheduled.
2.  **AC2:** When a user completes a study session ahead of schedule, the plan is adjusted (e.g., future tasks are pulled forward).
3.  **AC3:** A user returning to the app after a long absence is greeted by a "Welcome Back" wizard.
4.  **AC4:** The wizard summarizes overdue tasks and provides simple options for rescheduling.
5.  **AC5:** Choosing an option in the wizard successfully updates the user's plan and returns them to the dashboard.

## Traceability Mapping

| AC | Spec Section(s) | Component(s)/API(s) | Test Idea |
| :--- | :--- | :--- | :--- |
| **AC1,2**| APIs and Interfaces | `POST /reschedule-plan` | Integration test: update a task and verify the schedule changes. |
| **AC3,4**| Workflows and Sequencing| "Welcome Back" Wizard UI | E2E Test: set clock forward, log in, verify wizard appears. |
| **AC5** | Workflows and Sequencing| "Welcome Back" Wizard UI | E2E Test: select an option in the wizard and verify the plan changes. |

## Risks, Assumptions, Open Questions

-   **Risk:** The rescheduling algorithm could have complex edge cases (e.g., no available time slots left before the exam).
    -   **Mitigation:** The algorithm must handle this gracefully. If a full reschedule is not possible, it should do its best and potentially flag the "crammed" sessions in the UI.
-   **Assumption:** The "fire-and-forget" call to the reschedule endpoint from the frontend is acceptable. The user does not need to wait for it to complete.
-   **Question:** What is the precise logic for "completing a session ahead of schedule"?
    -   **Next Step:** Define this as part of the implementation. A simple approach is that if a task scheduled for tomorrow is completed today, the system can attempt to pull a future task into the now-empty slot. This can be a post-MVP enhancement if too complex.

## Test Strategy Summary

-   **Unit Tests:**
    -   (Backend) This is the most critical part. Create an extensive test suite for the rescheduling algorithm. Test it with numerous scenarios: plans with no room, plans with ample room, plans with many missed tasks, etc. The algorithm should be a pure function that can be tested in isolation.
-   **Integration Tests:**
    -   (Backend) Test the `/reschedule-plan` endpoint, mocking the database to provide various plan states and verifying the `UPDATE` queries it generates.
-   **E2E Tests:**
    -   Test the full "Welcome Back" wizard flow.
    -   Test the automatic rescheduling by marking a task as missed and asserting that the calendar view updates correctly.
