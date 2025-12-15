# Story Validation: story-2-003 - User Can Soft-Delete a Course

**Verdict: READY**

## Rationale:

The story "User Can Soft-Delete a Course" (story-2-003) is well-defined and meets the criteria for being development-ready.

-   **Independent:** It focuses on the soft-deletion functionality and can be developed and tested in isolation, though it naturally relies on the `getCourses` displaying only non-deleted items (which is also defined).
-   **Negotiable:** Minor UI details for the delete button and confirmation modal can be adjusted, but the core functionality is clear.
-   **Valuable:** Provides essential functionality for managing courses, allowing users to clean up their active list without permanent data loss.
-   **Estimable:** The scope is clear (updating a single database column and removing from view), making it estimable within 1-2 development days.
-   **Small:** Focused on a single, atomic piece of functionality, making it suitable for a sprint.
-   **Testable:** The acceptance criteria provide clear points for testing the soft-delete mechanism and its effect on the active course list.

The story directly addresses AC6 and AC7 of Epic 2 ("The user can delete a course, which soft-deletes it in the database" and "Soft-deleted courses do not appear in the main course list"). It aligns with the technical specifications in `tech-spec-epic-2.md`, particularly regarding the `CourseManager.softDeleteCourse` method, the `deleted_at` column, and RLS.

No revisions are immediately required.
