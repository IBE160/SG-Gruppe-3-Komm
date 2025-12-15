# User Story: User Can View and Restore Soft-Deleted Courses

**ID:** story-2-004
**Epic:** Epic 2: Course Management
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** view a list of my soft-deleted courses and be able to restore them,
**So that** I can recover accidentally deleted courses or bring back previously soft-deleted courses for continued use.

## 2. Acceptance Criteria

1.  **AC1: "Trash" View Access:** A clearly accessible UI element (e.g., a link, button, or tab) is available on the Course Management page to navigate to a "Trash" or "Archived" view specifically for soft-deleted courses.
2.  **AC2: Display Soft-Deleted Courses:** The "Trash" view accurately displays a list of all courses that have been soft-deleted by the current user (i.e., where `deleted_at IS NOT NULL`).
3.  **AC3: Restore Action UI:** Each soft-deleted course entry in the "Trash" view includes a clearly visible and interactive UI element (e.g., a "Restore" button or icon) to initiate its restoration.
4.  **AC4: Restore Function Call:** Clicking the restore action triggers the `CourseManager.restoreCourse(courseId)` function.
5.  **AC5: Database Update:** The `deleted_at` column for the specified `courseId` in the `public.courses` table is successfully set back to `NULL`.
6.  **AC6: Removal from "Trash" and Return to Active List:** After a successful restoration, the course is immediately removed from the "Trash" view and automatically reappears in the user's active course list on the dashboard.
7.  **AC7: RLS Enforcement:** The restore operation must adhere to Row Level Security (RLS), ensuring a user can only restore courses they own.

## 3. Dependencies

-   Relies on the `public.courses` table and its `deleted_at` column.
-   Relies on the `CourseManager` client-side service, specifically the `restoreCourse` method, for interaction with Supabase.
-   Assumes the `getCourses` method (used for displaying the active list) correctly incorporates the `WHERE deleted_at IS NULL` filter.

## 4. Notes

-   The "Trash" view should clearly differentiate soft-deleted courses from active ones, potentially by displaying the `deleted_at` timestamp.
-   The UI for restoration should be intuitive, and a small, non-intrusive success notification (toast) after restoration would enhance user experience.
-   No confirmation dialog is required for the restore action, as it is non-destructive.
