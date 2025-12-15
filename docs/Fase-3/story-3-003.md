# User Story: User Can Trigger Study Plan Generation and View the Generated Plan

**ID:** story-3-003
**Epic:** Epic 3: AI Study Plan Generation
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** finalize my topic selection and study preferences and trigger the AI to generate my study plan,
**So that** I can immediately see my personalized study schedule on my dashboard.

## 2. Acceptance Criteria

1.  **AC1: Trigger Generation UI:** Within the "Initial Study Plan Generation" wizard (specifically Step 5: "Generation & Completion"), a prominent and clearly labeled "Generate My Plan!" button is available to the user.
2.  **AC2: API Call to Backend:** Clicking the "Generate My Plan!" button triggers an asynchronous API call to the FastAPI backend's `POST /generate-schedule` endpoint. This request body must accurately include the `course_id`, `exam_date`, the final confirmed list of `topics` (from story-3-001), and the collected `user_preferences` (from story-3-002).
3.  **AC3: Progress Indicator:** While the backend is processing the request, performing the scheduling algorithm, interacting with Supabase, and persisting data, a clear and continuous progress indicator is displayed on the frontend. The "Generate My Plan!" button should be disabled during this period to prevent multiple submissions.
4.  **AC4: Successful Plan Persistence:** Upon a successful response from the `POST /generate-schedule` endpoint, the FastAPI backend has successfully processed the request, generated the `syllabus_topics` and `study_sessions` records, and inserted them into the Supabase database.
5.  **AC5: Display Generated Plan:** After successful plan generation, the wizard interface automatically closes, and the user is seamlessly navigated to their dashboard or a course-specific view where the newly generated study plan (i.e., the `study_sessions` for that course) is prominently and immediately visible.
6.  **AC6: Success Notification:** A brief, non-intrusive success notification (e.g., a "toast" message) appears on the dashboard to confirm the successful generation of the study plan.
7.  **AC7: Error Handling & Feedback:** If the `POST /generate-schedule` API call fails for any reason (e.g., backend error, database constraint violation, validation error), a user-friendly error message is displayed on the frontend, guiding the user on how to troubleshoot or retry.
8.  **AC8: Performance Adherence:** The entire end-to-end process, from the user clicking "Generate My Plan!" to the generated plan being visible on the dashboard, completes within the required **less than 10 seconds**, as specified in the Epic 3 Non-Functional Requirements.

## 3. Dependencies

-   FastAPI Backend: Full implementation of the `POST /generate-schedule` endpoint, including the scheduling algorithm, Supabase database interaction for `syllabus_topics` and `study_sessions`, and security checks.
-   Next.js Frontend: UI implementation for wizard Step 5 ("Generation & Completion"), robust handling of loading and error states, and logic for navigating to the dashboard/course view.
-   Supabase Database: Readiness of the `public.syllabus_topics` and `public.study_sessions` tables to receive generated data.
-   Data from `story-3-001` (confirmed topics) and `story-3-002` (user preferences).

## 4. Notes

-   The backend's scheduling algorithm is the core logic responsible for distributing topics over time based on user preferences and course exam dates. This algorithm needs dedicated unit tests.
-   Frontend needs to aggregate all data collected from previous wizard steps (`course_id`, `exam_date`, `topics`, `user_preferences`) and pass it correctly in the `POST /generate-schedule` request.
-   The dashboard or course detail view must be capable of querying and rendering the newly created `study_sessions` records.
-   Consider using a library like `react-query` or `useSWR` for managing the asynchronous call state (loading, error, data) on the frontend.
