# User Story: User Can Soft-Delete a Course

**ID:** story-2-003
**Epic:** Epic 2: Course Management
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** soft-delete a course,
**So that** it is no longer visible in my active course list but can be restored later.

## 2. Acceptance Criteria

1.  **AC1: Delete Action UI:** A clear UI element (e.g., a "Delete" button or icon) is present for each course in the course listing or detail view.
2.  **AC2: High-Friction Confirmation:** Clicking the delete action presents a confirmation dialog. To confirm deletion, the user must explicitly type the course's name into an input field, which then enables the final "Soft-Delete" button. The dialog also clearly informs the user about the 30-day restoration period.
3.  **AC3: Soft-Delete Function Call:** Upon user confirmation, the `CourseManager.softDeleteCourse(courseId)` function is invoked.
4.  **AC4: Database Update:** The `deleted_at` column for the specified `courseId` in the `public.courses` table is updated with the current timestamp.
5.  **AC5: Removal from Active List:** Immediately after a successful soft-delete, the course is removed from the user's active course list displayed on the dashboard (i.e., queries for active courses filter `WHERE deleted_at IS NULL`).
6.  **AC6: RLS Enforcement:** The soft-delete operation must adhere to Row Level Security (RLS), preventing users from soft-deleting courses they do not own.

## 3. Dependencies

-   Relies on the `public.courses` table and its `deleted_at` column.
-   Relies on the `CourseManager` client-side service, specifically the `softDeleteCourse` method, for interaction with Supabase.
-   Assumes the `getCourses` method (used for displaying the active list) already incorporates the `WHERE deleted_at IS NULL` filter.

## 4. Notes

-   This story covers the "soft-delete" mechanism only. The UI/functionality for viewing and restoring soft-deleted courses (AC8 of Epic 2) will be addressed in a subsequent story.
-   The confirmation dialog should clearly inform the user about the 30-day restoration period mentioned in the Epic Tech Spec.
