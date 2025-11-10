# Brainstorming Session: User Flow Improvements

Date: 2025-11-10

This document summarizes the brainstorming session regarding the user flows for the AI-Powered Personal Study Planner, based on the `proposal.md` file.

## General Suggestions

Two cross-cutting themes were identified for improving the overall user experience:

1.  **First-Time User Experience (Onboarding):**
    *   **Issue:** The user flows do not account for the "empty state" a new user encounters after their first login.
    *   **Suggestion:** Design a welcoming dashboard for new users that clearly guides them to perform the first critical action, such as "Add your first course to get started!"

2.  **System Feedback and Error Handling:**
    *   **Issue:** The flows primarily describe the "happy path."
    *   **Suggestion:** Implement UI feedback mechanisms. This includes showing a loading indicator during potentially long operations (e.g., AI plan generation) and displaying clear, user-friendly error messages if a process fails.

## Flow-Specific Feedback

### Flow 1: Student Onboarding and Course Creation

*   **Registration:** Add a "Resend Verification Email" option for users who have trouble with the initial sign-up email.
*   **Course Creation Form:** The `JSON` field is too technical for the target user. It should be renamed to something intuitive like "Advanced Settings" or be abstracted away from the user entirely.
*   **Workflow Streamlining:** To make the process smoother, the application could proactively ask the user if they want to generate a study plan immediately after a new course is successfully saved.

### Flow 2: Student Updates Activity Status

*   **Status Terminology:** The `progress_status` options ("Not Started," "Completed," "Not Completed") are ambiguous. "Not Completed" could mean "missed" or "in progress."
*   **Recommendation:** Use clearer status labels, such as: `Not Started`, `In Progress`, `Completed`, `Missed`. This provides more granular tracking and better data for the dynamic rescheduling feature.
*   **UI Simplification:** Consider implementing an auto-save feature when the user updates an activity's status, removing the need for an extra click on a "Save" button.

### Flow 3: Student Deletes Course

*   **Major Logical Flaw:** The entry point for deleting a *course* is incorrectly placed within the editing of a *calendar activity*. This is highly counter-intuitive.
*   **Recommendation:** This functionality must be moved. The logical place for it is within the main course management area.

### Flow 4: CRUD Functionality On the Courses

*   **Centralized Management:** This flow correctly identifies the need for a centralized page to manage all courses.
*   **Consolidation:** This section should be the single source of truth for all course-related CRUD operations (Create, Read, Update, Delete).
    *   The "Add New Course" functionality from Flow 1 should be consolidated here to avoid redundancy.
    *   The "Delete Course" functionality from Flow 3 should be moved here.

## Summary of Recommendations

The core user journeys are logical, but the flows can be significantly improved by:
1.  **Consolidating** all course management into a single, clear interface (Flow 4).
2.  **Refining** UI/UX with better feedback, clearer language, and streamlined workflows.
3.  **Designing** for the new user to ensure a smooth onboarding process.
