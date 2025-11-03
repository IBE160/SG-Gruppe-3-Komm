# Brainstorming Session Results: AI-Powered Personal Study Planner

**Date:** October 30, 2025  
**Technique Used:** Chaos Engineering  
**Objective:** To identify potential failure points, deviations, and edge cases in the project proposal and design robust solutions to improve application resilience.

---

## Session Focus Area

This session focused primarily on the following area from the project brainstorming context:

- **Technical Risks and Challenges** - What could go wrong?

---

## Round 1: Onboarding and Plan Generation

### 1. Email & Login

*   **Problem:** Verification or password reset emails fail to arrive or go to spam.
    *   **Solution:**
        *   On failed login for unverified accounts, show a specific error ("Your account is not yet verified...") and provide a rate-limited "Resend verification email" button.
        *   On the sign-up screen, proactively tell users to check their spam folder.
        *   For password resets, provide a "Contact Support" link as a manual fallback if the automated email fails. Support would then have a workflow to manually verify and reset the user's access.

### 2. Syllabus & AI Parsing

*   **Problem:** User uploads an unsupported file format (scanned PDF, .docx).
    *   **Solution:**
        *   Validate file format on the front end and clearly state accepted formats.
        *   If backend parsing fails, provide a specific, helpful error message that guides the user to the manual input option.

*   **Problem:** The AI misunderstands the syllabus, returns nonsensical topics, or crashes.
    *   **Solution:**
        *   **Show, Don't Assume:** After parsing, present the extracted topics to the user in an editable list for confirmation. Allow them to add, edit, or delete topics before accepting.
        *   Implement a reasonable timeout (e.g., 30 seconds) for the AI call to avoid infinite loading spinners and show a helpful error if it fails.

*   **Problem:** The "Manual Input" fallback flow is unclear.
    *   **Solution:**
        *   Provide a simple, large text area prompting the user to "Paste your syllabus topics here, one topic per line."
        *   Give real-time feedback by showing the topics being added to a list as the user types.

### 3. Plan Generation

*   **Problem:** The AI generates a technically perfect but humanly impossible study plan.
    *   **Solution:**
        *   Use "smarter prompting" with human-centric constraints (e.g., no more than 2 hours on one topic without a break).
        *   Allow users to tag topics by difficulty ("easy," "medium," "hard") to inform the AI.
        *   Make the final plan editable via a drag-and-drop interface, treating the AI output as a starting point.

*   **Problem:** User enters invalid data, like a past exam date or zero available study hours.
    *   **Solution:**
        *   Use a date-picker that disables past dates.
        *   Run a pre-generation validation check to ensure the date range is valid and study hours are greater than zero, providing specific error messages if validation fails.

---

## Round 2: Dynamic Updates, Data Integrity, and Dependencies

### 1. Dynamic Rescheduling

*   **Problem:** How to handle a user finishing tasks early.
    *   **Solution:**
        *   When the last task for the day is done, prompt the user with a choice:
            *   **"Get Ahead":** Pull the next single task from the following day.
            *   **"Finish for the Day":** Congratulate the user and give them free time (default behavior).

*   **Problem:** A user returns after a week-long absence to a demotivating wall of overdue tasks.
    *   **Solution:** The "Welcome Back" Wizard.
        *   Detect the absence and trigger a special "triage" flow.
        *   Offer clear rescheduling strategies: "Reschedule All" (intelligently spreading tasks out), "Intensive Catch-up" (adding a few tasks to upcoming days), or "Skip For Now" (moving tasks to a separate "Review Later" list).

*   **Problem:** A user marks a task complete while offline.
    *   **Solution:** Optimistic UI with a background sync queue.
        *   The UI updates instantly.
        *   A service worker queues the failed request and sends it automatically when the network connection is restored.

### 2. Data Integrity

*   **Problem:** A user accidentally deletes an important course.
    *   **Solution:** Implement "Soft Deletes."
        *   Mark the course as `deleted_at` in the database instead of permanently deleting it.
        *   Provide a "Trash" or "Archived Courses" section in the app where users can view and restore deleted items for a set period (e.g., 30 days).

*   **Problem:** Race condition where a user edits a course while the AI is generating a plan for it.
    *   **Solution:** Use state management to lock the UI.
        *   If the user is in an "edit state," disable the "Generate Plan" button until they save or cancel.
        *   If the AI is generating a plan, disable all "Edit" buttons for that course.

### 3. Backend & API Dependencies

*   **Problem:** The OpenAI API is down.
    *   **Solution:** Graceful degradation to "Manual Mode."
        *   The backend detects the API failure and informs the frontend.
        *   The UI displays a message: "The AI planner is temporarily unavailable. You can still add study blocks manually."
        *   The core calendar functionality remains available for manual planning.

*   **Problem:** A major Supabase outage occurs.
    *   **Solution:** Acknowledge RPO/RTO and have a communication plan.
        *   **RPO (Recovery Point Objective):** 24 hours, based on Supabase's daily backups.
        *   **RTO (Recovery Time Objective):** A few hours, dependent on Supabase's SLA for restoring the backup.
        *   **Communication:** Use an external status page to keep users informed.

*   **Problem:** A malicious user spams the expensive AI generation function.
    *   **Solution:** Implement backend rate limiting.
        *   Allow a generous number of generations initially (e.g., 3-5 times per course).
        *   After that, apply a stricter limit (e.g., once per hour).
        *   Return a `429 Too Many Requests` error with a friendly message in the UI when the limit is exceeded.

---

## Conclusion

This Chaos Engineering session was highly effective. By systematically probing for weaknesses, we identified numerous potential risks to the user experience and application stability. The solutions designed here provide a clear blueprint for building a more resilient, user-friendly, and robust Personal Study Planner.