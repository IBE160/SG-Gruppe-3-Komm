# User Story: User Can Submit Syllabus and Review AI-Extracted Topics

**ID:** story-3-001
**Epic:** Epic 3: AI Study Plan Generation
**Author:** BIP (sm)
**Status:** Ready for Dev

---

## 1. Story

**As a** student,
**I want to** provide my course syllabus text and see the topics the AI extracts from it,
**So that** I can ensure the AI understands my course content correctly before generating a study plan.

## 2. Acceptance Criteria

1.  **AC1: Syllabus Input UI:** Within the "Initial Study Plan Generation" wizard (specifically Step 2: "Add Syllabus"), the user is presented with clear options to either paste raw plain text syllabus content into a textarea or upload a plain text file (e.g., `.txt`, `.md`, `.pdf` converted to text on client-side if feasible).
2.  **AC2: Syllabus Submission & API Call:** Submitting the syllabus content (via paste or file upload) triggers an asynchronous API call to the FastAPI backend's `POST /parse-syllabus` endpoint, securely sending the raw syllabus text.
3.  **AC3: Loading Indicator:** While the backend is processing the request and communicating with the AI service, a visible and appropriate loading indicator is displayed on the frontend to inform the user of ongoing activity.
4.  **AC4: Display AI-Extracted Topics:** Upon successful receipt of a structured JSON response from the `POST /parse-syllabus` endpoint, the "Confirm Topics" (Step 3) screen of the wizard displays the list of topics (title and description) extracted by the AI in an editable format.
5.  **AC5: Topic Review, Editing, and Deletion:** The user can review the displayed topics, make inline edits to their titles or descriptions, and delete unwanted topics from the list.
6.  **AC6: Backend Error Handling & Frontend Feedback:** If the `POST /parse-syllabus` call fails (e.g., due to network error, AI service error, or malformed response from OpenAI), the backend returns an appropriate error. The frontend then displays a user-friendly error message, ideally suggesting a retry or the manual topic input option (AC3 of Epic 3, to be implemented in a subsequent story).
7.  **AC7: Backend Security & User Context:** The FastAPI backend securely manages the OpenAI API key and validates that the request is from an authenticated user. It ensures that the operation is performed in the context of the user's current course (e.g., by validating `course_id` if passed or inferred).

## 3. Dependencies

-   FastAPI Backend: `POST /parse-syllabus` endpoint implementation, including integration with OpenAI API.
-   OpenAI API: External service for natural language processing and topic extraction.
-   Next.js Frontend: UI implementation for wizard Steps 2 ("Add Syllabus") and 3 ("Confirm Topics").
-   Authentication/Authorization: The backend must be able to identify the authenticated user.

## 4. Notes

-   The AI is expected to return topics in a structured JSON format (e.g., `{"topics": [{"title": "...", "description": "..."}]}`) as specified in `tech-spec-epic-3.md`.
-   The "Confirm Topics" UI (Step 3) requires interactive components to allow for editing and removal of individual topics.
-   Consider using the `useSWR` or `react-query` pattern on the frontend for efficient data fetching and caching for the API call.
