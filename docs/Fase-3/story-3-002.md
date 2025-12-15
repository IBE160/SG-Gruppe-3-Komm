# User Story: User Can Specify Study Availability and Preferences

**ID:** story-3-002
**Epic:** Epic 3: AI Study Plan Generation
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** specify my preferred weekly study hours and whether I study on weekends,
**So that** the AI can generate a study plan that fits my personal schedule and commitments.

## 2. Acceptance Criteria

1.  **AC1: Preference Input UI:** Within the "Initial Study Plan Generation" wizard (specifically Step 4: "Set Your Pace"), the user is presented with intuitive UI controls to define their study availability:
    *   A control (e.g., slider with numerical input, simple number input) for `hours_per_week`, allowing them to set their desired total study hours per week (e.g., a range from 1 to 40).
    *   A toggle or checkbox for `study_weekends`, allowing them to indicate whether they are available to study on Saturdays and Sundays.
2.  **AC2: Input Validation & Feedback:** The UI enforces basic validation on `hours_per_week` (e.g., positive integer, within a reasonable range) and provides immediate, user-friendly feedback for invalid inputs (e.g., inline error messages).
3.  **AC3: Preference Data Capture:** The selected `hours_per_week` and `study_weekends` values are accurately captured and maintained in the frontend state, ready to be passed as part of the `user_preferences` object to the backend's schedule generation endpoint.
4.  **AC4: UI Persistence (Pre-filling):** If the user navigates away from and then returns to this step of the wizard, their previously entered preferences are pre-filled in the UI controls.
5.  **AC5: Progression to Next Step:** Upon confirming their preferences, the user can proceed seamlessly to the next step of the wizard (Step 5: "Generation & Completion").

## 3. Dependencies

-   Next.js Frontend: UI implementation for wizard Step 4 ("Set Your Pace").
-   The `user_preferences` object structure expected by the `POST /generate-schedule` endpoint on the FastAPI backend (as defined in `tech-spec-epic-3.md`).

## 4. Notes

-   The collected preferences (`hours_per_week`, `study_weekends`) will be part of the `user_preferences` object sent to the `POST /generate-schedule` endpoint.
-   The exact algorithm for how these preferences influence the distribution and creation of `study_sessions` is a backend concern and will be implemented as part of a later story (AC5 of Epic 3, for the actual `generate-schedule` endpoint). This story focuses only on capturing the user's input.
-   Consider using Shadcn UI components for sliders, number inputs, and toggles to maintain design system consistency.
