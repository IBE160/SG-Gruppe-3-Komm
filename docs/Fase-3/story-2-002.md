# User Story: User Can Edit an Existing Course

**ID:** story-2-002
**Epic:** Epic 2: Course Management
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** edit the name and syllabus content of an existing course,
**So that** I can correct mistakes or update course information.

## 2. Acceptance Criteria

1.  **AC1: Edit Course UI:** A UI component is available (e.g., an edit form or modal) that pre-populates with the current course's `name` and `syllabus` content and allows for their modification.
2.  **AC2: Update Function Call:** Submitting the edited form triggers the `CourseManager.updateCourse(courseId, { name, syllabus })` function.
3.  **AC3: Database Update:** The corresponding record in the `public.courses` table for the specified `courseId` is successfully updated with the new `name` and `syllabus` values.
4.  **AC4: Display Updated Information:** After a successful update, the course's information is immediately reflected in the user's course list or detail view.
5.  **AC5: RLS Enforcement:** The update operation respects Row Level Security (RLS), ensuring a user can only update courses they own.

## 3. Dependencies

-   Relies on the `public.courses` table.
-   Relies on the `CourseManager` client-side service for Supabase interactions, specifically the `updateCourse` method.
-   Requires a UI element (e.g., an "Edit" button/icon) to initiate the edit workflow for a selected course.

## 4. Notes

-   The `syllabus` content should continue to be saved as raw text. AI parsing of the syllabus is out of scope for this story.
-   Consider how to handle validation for the `name` field (e.g., cannot be empty).
