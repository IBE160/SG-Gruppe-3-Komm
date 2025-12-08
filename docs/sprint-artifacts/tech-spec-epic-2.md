# Epic Technical Specification: Course Management

Date: 2025-12-08
Author: BIP
Epic ID: 2
Status: Draft

---

## Overview

This document provides the technical specification for Epic 2: Course Management. This epic focuses on providing users with the core functionality to create, view, update, and delete their courses. This is a central feature of the application, as courses are the primary containers for study plans. The implementation will involve creating a dedicated UI for course management and corresponding CRUD (Create, Read, Update, Delete) operations that interact directly with the Supabase database.

## Objectives and Scope

**In-Scope:**
-   A centralized page for managing all courses.
-   Functionality to add a new course with a title and syllabus content.
-   A prompt to generate a study plan immediately after course creation.
-   A view of all existing courses on the user's dashboard.
-   The ability to edit a course's title and syllabus.
-   "Soft delete" functionality for courses, allowing for restoration within a 30-day period.

**Out-of-Scope:**
-   Archiving courses (vs. soft deleting).
-   Sharing courses with other users.
-   Bulk import/export of courses.

## System Architecture Alignment

This epic builds directly on the established data model and security principles of the solution architecture.

-   **Data Model:** This epic introduces and primarily interacts with the `public.courses` table. All operations will be governed by the Row Level Security (RLS) policies defined for this table, ensuring a user can only manage their own courses. The `user_id` column is the critical link to the `auth.users` table.
-   **Frontend/Backend Interaction:** The Next.js frontend will be responsible for all UI related to course management. It will use the `supabase-js` client library to perform CRUD operations directly against the `courses` table in the Supabase database. No backend API (FastAPI) is required for these simple data manipulations.
-   **Security:** The RLS policy `CREATE POLICY "Enable all access for own courses" ON public.courses FOR ALL USING (auth.uid() = user_id);` is the key security mechanism. It ensures that all `SELECT`, `INSERT`, `UPDATE`, and `DELETE` queries are automatically scoped to the currently authenticated user.

## Detailed Design

### Services and Modules

| Service/Module | Responsibility | Owner |
| :--- | :--- | :--- |
| **Next.js Frontend** | Provides UI for the Course Management page, including forms for creating/editing courses and lists of existing courses. | Frontend Team |
| **`CourseManager` (Client-side)** | A dedicated module in the Next.js app to handle all CRUD operations for courses, wrapping the `supabase-js` client. Manages course-related state via Zustand. | Frontend Team |
| **Supabase Database** | Persists all course data in the `courses` and `syllabus_topics` tables. Enforces data access rules via RLS. | Supabase (Managed) |

### Data Models and Contracts

The epic revolves around the `courses` and `syllabus_topics` tables. A "soft delete" will be implemented by adding a `deleted_at` column to the `courses` table.

```sql
-- Courses Table: Stores information about each course a user adds.
CREATE TABLE public.courses (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    user_id UUID NOT NULL REFERENCES public.users(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    exam_date DATE,
    deleted_at TIMESTAMPTZ, -- For soft delete
    created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Syllabus Topics Table: Stores topics extracted from a course's syllabus.
CREATE TABLE public.syllabus_topics (
    id BIGINT PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    course_id BIGINT NOT NULL REFERENCES public.courses(id) ON DELETE CASCADE,
    title TEXT NOT NULL,
    description TEXT,
    estimated_hours NUMERIC(4, 2)
);
```
-   **Contract:** Queries for courses must filter for `deleted_at IS NULL` to exclude soft-deleted records from normal views.

### APIs and Interfaces

The `CourseManager` service will expose methods to the UI components.

```typescript
// Example interface for the CourseManager service
interface ICourseManager {
  getCourses(): Promise<{ courses, error }>;
  createCourse(courseData: { name, syllabus }): Promise<{ course, error }>;
  updateCourse(courseId: number, updates: { name?, syllabus? }): Promise<{ course, error }>;
  softDeleteCourse(courseId: number): Promise<{ error }>;
  restoreCourse(courseId: number): Promise<{ error }>;
}
```

### Workflows and Sequencing

1.  **Create Course:**
    -   User fills out the "Add New Course" form.
    -   `CourseManager.createCourse` is called.
    -   The service makes an `INSERT` call to the `courses` table in Supabase.
    -   On success, the UI prompts the user to generate a study plan for the new course.

2.  **Soft Delete Course:**
    -   User clicks "Delete" on a course.
    -   A confirmation modal appears.
    -   On confirmation, `CourseManager.softDeleteCourse` is called.
    -   The service issues an `UPDATE` command to set the `deleted_at` column to the current timestamp for the specified `courseId`.
    -   The UI removes the course from the active list.

## Non-Functional Requirements

### Performance

-   Queries to fetch the list of user's courses should complete in under 500ms.
-   An index should be created on the `courses(user_id)` column to ensure fast lookups.

### Security

-   All course-related database operations MUST be protected by the RLS policies defined in the architecture to prevent users from accessing or modifying another user's courses.

### Reliability/Availability

-   The "soft delete" feature ensures that accidental deletions are recoverable for a 30-day period, improving data resiliency for the user.

### Observability

-   Any database errors during CRUD operations should be logged to a monitoring service with context (e.g., the failed operation and course ID).

## Dependencies and Integrations

| Dependency | Type | Purpose |
| :--- | :--- | :--- |
| **`@supabase/supabase-js`** | NPM Package | For all direct database interactions with the `courses` and `syllabus_topics` tables. |
| **`zustand`** | NPM Package | For managing the client-side state of the course list. |

## Acceptance Criteria (Authoritative)

1.  **AC1:** A logged-in user can access a centralized course management page.
2.  **AC2:** A user can add a new course by providing a title and syllabus content.
3.  **AC3:** After adding a course, the user is prompted to generate a study plan.
4.  **AC4:** The user can see a list of all their non-deleted courses on their dashboard.
5.  **AC5:** The user can edit the title and syllabus of an existing course.
6.  **AC6:** The user can delete a course, which soft-deletes it in the database.
7.  **AC7:** Soft-deleted courses do not appear in the main course list.
8.  **AC8:** The system provides a mechanism to restore a soft-deleted course (e.g., from a "Trash" view).

## Traceability Mapping

| AC | Spec Section(s) | Component(s)/API(s) | Test Idea |
| :--- | :--- | :--- | :--- |
| **AC1,4**| APIs and Interfaces | `CourseManager.getCourses` | Integration test fetching and displaying a list of courses. |
| **AC2** | APIs and Interfaces | `CourseManager.createCourse` | E2E test: fill out and submit the "Add Course" form. |
| **AC3** | Workflows and Sequencing| UI Component | Test that the "Generate Plan" prompt appears after creation. |
| **AC5** | APIs and Interfaces | `CourseManager.updateCourse` | E2E test: edit a course and verify the changes persist. |
| **AC6,7**| APIs and Interfaces | `CourseManager.softDeleteCourse`| E2E test: delete a course and verify it disappears from the list. |
| **AC8** | APIs and Interfaces | `CourseManager.restoreCourse` | E2E test: find a deleted course and restore it. |

## Risks, Assumptions, Open Questions

-   **Risk:** The logic for parsing the syllabus during course creation might be complex and better suited for the AI epic.
    -   **Mitigation:** For this epic, "syllabus content" can be treated as a simple text field. The actual AI parsing will be handled in Epic 3. This spec assumes the `createCourse` method just saves the raw text.
-   **Assumption:** A 30-day restoration period for soft-deleted courses is sufficient.
-   **Question:** How should the UI for restoring deleted courses be presented?
    -   **Next Step:** Propose a "Trash" or "Archived" view accessible from the course management page. This can be designed as part of the implementation task.

## Test Strategy Summary

-   **Unit Tests:** Test the `CourseManager` service by mocking the `supabase-js` client to ensure it constructs the correct `select`, `insert`, `update` queries.
-   **Integration/E2E Tests:**
    -   Create a course, verify it appears in the list.
    -   Update a course, verify the changes are saved.
    -   Delete a course, verify it's gone from the main list.
    -   Restore the deleted course, verify it reappears.
-   **Security Testing:** Write tests to confirm that a user (`User A`) cannot fetch, create, update, or delete courses belonging to `User B`.
