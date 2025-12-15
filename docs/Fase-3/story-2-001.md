# User Story: User Can Add and View a New Course

**ID:** story-2-001
**Epic:** Epic 2: Course Management
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** add a new course by providing a title and syllabus content,
**So that** it appears in my list of courses on the dashboard.

## 2. Acceptance Criteria

1.  **AC1: Create Course Form:** A UI component (form) is available that allows a user to input a `name` (text) and `syllabus` (text) for a new course.
2.  **AC2: Form Submission:** Submitting the form triggers the `CourseManager.createCourse` function, passing the name and syllabus content.
3.  **AC3: Database Record:** A new record is successfully created in the `public.courses` table. The record includes the `user_id` of the currently authenticated user, the course `name`, and the raw `syllabus` content.
4.  **AC4: Display in List:** After creation, the new course is immediately visible in the user's main course list on the dashboard.
5.  **AC5: List Filtering:** The course list view must only display courses where `deleted_at IS NULL`.
6.  **AC6: Prompt for Plan Generation:** Upon successful course creation, the user is prompted to generate a study plan for the new course, as per the epic's workflow.

## 3. Dependencies

-   Relies on the `public.courses` table as defined in the solution architecture and epic tech spec.
-   Relies on the `CourseManager` client-side service for Supabase interactions.

## 4. Notes

-   Per the epic tech spec, the "syllabus content" should be saved as raw text. AI parsing of the syllabus is out of scope for this story and will be handled in Epic 3.
-   The implementation must add a `syllabus TEXT` column to the `courses` table to fulfill the requirements, as it is specified in the `ICourseManager` interface but missing from the initial `CREATE TABLE` script in the tech spec.
