# Epic Technical Specification: Dashboard & Progress Tracking

Date: 2025-12-08
Author: BIP
Epic ID: 4
Status: Draft

---

## Overview

This document provides the technical specification for Epic 4: Dashboard & Progress Tracking. This epic covers the primary user interface for daily interaction with the study planner. It's where users will visualize their generated schedule, track their progress, and update the status of their study tasks. The goal is to create a dashboard that is clear, motivating, and makes the daily check-in loop fast and satisfying. The implementation is primarily frontend-focused, leveraging Supabase's real-time capabilities to keep the view in sync.

## Objectives and Scope

**In-Scope:**
-   A main dashboard view featuring a calendar of study activities.
-   Progress bars for each course, giving a visual overview of completion.
-   The ability to click on a daily activity to view its details.
-   Functionality to update the status of a study activity (e.g., 'Not Started', 'Completed', 'Missed').
-   Automatic and persistent saving of progress updates.

**Out-of-Scope:**
-   Advanced data visualizations (e.g., burndown charts, velocity).
-   Gamification elements (e.g., streaks, badges).
-   Manual rescheduling of tasks directly on the calendar (this is handled by the dynamic adaptation epic).

## System Architecture Alignment

This epic realizes the "daily-use loop" described in the architecture and relies heavily on the frontend and its direct integration with Supabase.

-   **Component Interaction:** The **Next.js Frontend** is the star of this epic. It will fetch all `study_sessions` for the user directly from the **Supabase Database** and render them in the UI. When a user updates a task's status, the frontend will send an `UPDATE` query directly to Supabase.
-   **Real-time Capabilities:** This epic is a perfect candidate for using **Supabase Realtime**. The frontend can subscribe to changes in the `study_sessions` table. When a status is updated (either by the user or by a rescheduling event), Supabase will push the change to the client, allowing the UI to update automatically without needing a page refresh. This provides a dynamic and responsive user experience.
-   **Data Model:** This epic primarily reads from the `study_sessions` and `courses` tables and performs updates on the `status` column of the `study_sessions` table.

## Detailed Design

### Services and Modules

| Service/Module | Responsibility | Owner |
| :--- | :--- | :--- |
| **Next.js Frontend** | Contains all components for the dashboard, including the calendar view, course progress bars, and the `StudyTaskCard`. | Frontend Team |
| **`DashboardManager`** | A client-side service to fetch all dashboard data (`courses`, `study_sessions`) and handle status updates. | Frontend Team |
| **`StudyTaskCard` Component**| The custom, interactive component for displaying and updating a single study session, as defined in the UX Design Spec. | Frontend Team |
| **Supabase Realtime** | Pushes data changes from the database to the connected clients, enabling a live-updating UI. | Supabase (Managed) |

### Data Models and Contracts

This epic reads from the `courses` and `study_sessions` tables. The key interaction is updating the `status` field of the `study_sessions` table.

```sql
-- Study Sessions Table: The core of the study plan.
CREATE TABLE public.study_sessions (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    ...
    status TEXT NOT NULL DEFAULT 'Not Started' CHECK (status IN ('Not Started', 'In Progress', 'Completed', 'Missed')),
    ...
);
```
-   **Contract:** The frontend UI will correctly map the `status` enum to the visual states defined for the `StudyTaskCard` (e.g., 'Completed' -> green checkmark, strikethrough).

### APIs and Interfaces

All interactions are via the `supabase-js` client.

```typescript
// Example interface for the DashboardManager service
interface IDashboardManager {
  // Fetches initial data
  getDashboardData(): Promise<{ courses, sessions, error }>;
  
  // Updates the status of a session
  updateSessionStatus(sessionId: number, newStatus: 'Not Started' | 'In Progress' | 'Completed' | 'Missed'): Promise<{ error }>;
  
  // Subscribes to real-time updates
  onSessionsChange(callback: (payload: RealtimePayload) => void): Subscription;
}
```

### Workflows and Sequencing

1.  **Dashboard Load:**
    -   User navigates to the dashboard.
    -   `DashboardManager.getDashboardData` fetches all courses and study sessions for the user.
    -   The frontend renders the calendar view with `StudyTaskCard` components for each session.
    -   `DashboardManager.onSessionsChange` subscribes to future updates on the `study_sessions` table.1

2.  **Update Task Status:**
    -   User clicks on a `StudyTaskCard`.
    -   An `onClick` handler in the component calls `DashboardManager.updateSessionStatus` with the new status.
    -   The service sends the `UPDATE` query to Supabase.
    -   **If Realtime is active:** Supabase pushes the change to all subscribed clients. The `onSessionsChange` callback fires, and the UI updates to reflect the new status.
    -   **As a fallback:** The `updateSessionStatus` method can also optimistically update the local Zustand state to provide instant feedback before the real-time event arrives.

## Non-Functional Requirements

### Performance

-   Initial dashboard load, including all sessions for the upcoming month, should take less than 2 seconds.
-   UI updates after changing a task's status should feel instantaneous (< 200ms), leveraging optimistic updates and real-time events.

### Security

-   All data fetching is subject to the RLS policies on the `courses` and `study_sessions` tables, ensuring users only ever see their own data.

### Reliability/Availability

-   The frontend should be able to handle temporary disconnects from the Supabase Realtime service and automatically re-subscribe when the connection is restored.
-   If the real-time connection is unavailable, the dashboard should still be functional (allowing status updates), though it may require a manual refresh to see changes from other sessions/devices.

### Observability

-   Log any errors during real-time subscription or status updates to a frontend monitoring service.

## Dependencies and Integrations

| Dependency | Type | Purpose |
| :--- | :--- | :--- |
| **`@supabase/supabase-js`** | NPM Package | For data fetching, updates, and real-time subscriptions. |
| **`zustand`** | NPM Package | For managing the client-side state of the dashboard (courses, sessions). |
| **`react-big-calendar`** (or similar) | NPM Package | A component library for rendering the main calendar view. |
| **`date-fns`** | NPM Package | For date manipulation required by the calendar. |

## Acceptance Criteria (Authoritative)

1.  **AC1:** The dashboard displays a calendar view of the user's study activities.
2.  **AC2:** The dashboard displays a progress bar for each course.
3.  **AC3:** A user can click on a study activity to view its details.
4.  **AC4:** A user can update the status of a study activity ('Not Started', 'Completed', 'Missed').
5.  **AC5:** Progress updates are saved automatically and are persistent across sessions.
6.  **AC6:** Changes made to the study plan are reflected on the dashboard in near real-time without requiring a page refresh.

## Traceability Mapping

| AC | Spec Section(s) | Component(s)/API(s) | Test Idea |
| :--- | :--- | :--- | :--- |
| **AC1,2**| Detailed Design | Dashboard UI Components | Visual regression test of the dashboard layout. |
| **AC3** | Detailed Design | `StudyTaskCard` Component | E2E test: click a card and verify a details modal appears. |
| **AC4** | APIs and Interfaces | `DashboardManager.updateSessionStatus` | E2E test: click a card to cycle through and save its status. |
| **AC5** | Detailed Design | Supabase DB | Verify in a test that the status update persists after a page reload. |
| **AC6** | APIs and Interfaces | `DashboardManager.onSessionsChange` | Integration test the real-time subscription callback. |

## Risks, Assumptions, Open Questions

-   **Risk:** A large number of study sessions could make the initial dashboard load slow.
    -   **Mitigation:** Initially, only fetch sessions for a limited time window (e.g., current month +/- 1 month). Implement pagination or infinite scrolling for navigating further in time.
-   **Risk:** Handling real-time updates and synchronizing state can be complex and lead to bugs.
    -   **Mitigation:** Have a clear state management strategy (Zustand) and a single source of truth. Rely on the real-time event as the primary mechanism for state updates.
-   **Assumption:** A calendar view is the most effective way to visualize the study plan.
    -   **Next Step:** This is validated by the UX Design. Stick to this for MVP.

## Test Strategy Summary

-   **Unit Tests:**
    -   Test the logic for calculating course progress based on the number of completed sessions.
    -   Test the state update logic in the Zustand store.
-   **Component Tests:**
    -   Extensively test the `StudyTaskCard` component in all its visual states (`Not Started`, `Completed`, etc.).
    -   Test the calendar component to ensure it renders events correctly.
-   **Integration/E2E Tests:**
    -   Test the full flow: load the dashboard, change a task's status, and assert that the UI updates correctly.
    -   Use Supabase's testing tools to write a test that updates the database directly and asserts that the subscribed frontend client receives the notification and updates the UI. This specifically tests the real-time integration.
