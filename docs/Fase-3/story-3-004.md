# User Story: User Can Manually Input Syllabus Topics

**ID:** story-3-004
**Epic:** Epic 3: AI Study Plan Generation
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** have an option to manually input study topics,
**So that** I can generate a study plan even if AI syllabus parsing is not desired, unavailable, or provides incorrect topics.

## 2. Acceptance Criteria

1.  **AC1: Manual Input Option:** Within the "Initial Study Plan Generation" wizard (Step 2: "Add Syllabus"), alongside the options for AI-driven syllabus processing, a clear and prominent choice is presented to "Paste Topics Manually" or "Add Topics Individually" (or similar phrasing).
2.  **AC2: Manual Topic Entry UI:** When the manual input option is selected, the user is presented with a dedicated UI to facilitate the entry of topics. This UI allows the user to:
    *   Add new topics (each requiring a title and optionally a description).
    *   Edit the title and description of existing manually added topics.
    *   Remove individual manually added topics.
3.  **AC3: Topic Data Capture & Structure:** Manually entered topics are captured and stored in the frontend state, ensuring they conform to the expected data structure for topics (e.g., `{ title: string, description?: string }`) that will eventually be sent to the backend for plan generation.
4.  **AC4: Manual Topics in Review:** When the user proceeds to the "Confirm Topics" (Step 3) screen, the manually entered topics are displayed for review, editable and deletable, identical to how AI-extracted topics are presented.
5.  **AC5: Persistence for Manual Topics:** If the user navigates back to Step 2 or 3 within the wizard, their manually entered topics are retained and pre-filled in the respective UI.
6.  **AC6: Progression to Next Step:** After manually entering and confirming their topics, the user can proceed seamlessly to the next step of the wizard (Step 4: "Set Your Pace").

## 3. Dependencies

-   Next.js Frontend: UI implementation for wizard Step 2 ("Add Syllabus") to offer the manual input choice, and enhanced UI for Step 3 ("Confirm Topics") to handle both AI-extracted and manually entered topics.
-   The `topics` data structure expected by the `POST /generate-schedule` endpoint on the FastAPI backend (as defined in `tech-spec-epic-3.md`).

## 4. Notes

-   This story specifically covers **AC3 of Epic 3**, providing a critical fallback mechanism for plan generation.
-   The UI should provide a user-friendly way to add multiple topics efficiently (e.g., an "Add Topic" button that appends a new editable row).
-   Consider how the UI visually distinguishes between the "AI parsing" and "Manual input" modes in Step 2, and how a user can switch between them, potentially clearing one set of inputs if they choose the other.
-   No direct backend API call is triggered by manual topic input; the topics are managed client-side until the final `generate-schedule` call.
