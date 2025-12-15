# Story Validation: story-2-004 - User Can View and Restore Soft-Deleted Courses

**Verdict: READY**

## Rationale:

The story "User Can View and Restore Soft-Deleted Courses" (story-2-004) is well-defined and meets the criteria for being development-ready.

-   **Independent:** It focuses on viewing and restoring soft-deleted courses, which is a self-contained feature, building logically on the soft-delete functionality.
-   **Negotiable:** Minor UI details for the "Trash" view and the "Restore" button can be adjusted, but the core functionality is clear.
-   **Valuable:** Provides essential data recovery and management capabilities, significantly improving the user's control over their courses and addressing the "reliability" non-functional requirement.
-   **Estimable:** The scope is clear (fetching and displaying deleted records, then updating a single database column), making it estimable within 1-2 development days.
-   **Small:** Focused on a specific, atomic piece of functionality, making it suitable for a sprint.
-   **Testable:** The acceptance criteria provide clear points for testing the display of deleted courses, the restoration process, and the subsequent return to the active list.

The story directly addresses AC8 of Epic 2 ("The system provides a mechanism to restore a soft-deleted course (e.g., from a 'Trash' view)"). It aligns with the technical specifications in `tech-spec-epic-2.md`, particularly regarding the `CourseManager.restoreCourse` method and the `deleted_at` column.

No revisions are immediately required.
