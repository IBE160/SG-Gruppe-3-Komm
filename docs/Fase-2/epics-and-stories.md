# Epics and User Stories for AI-Powered Personal Study Planner

This document outlines the epics and user stories for the MVP of the AI-Powered Personal Study Planner, based on the project proposal, PRD, and product brief.

---

### Epic 1: User Authentication & Onboarding

This epic covers the entire user lifecycle from registration and login to account recovery, ensuring a secure and smooth entry point for users.

*   **Story:** As a new user, I want to register for an account using my email and password so that I can create and manage my personal study plans.
*   **Story:** As a new user, I want to receive a verification email after registration so that I can confirm my email address and secure my account.
*   **Story:** As a user who has not verified their email, I want to see an option to resend the verification email so that I can complete my registration if the first email didn't arrive.
*   **Story:** As a registered user, I want to log in to my account securely using my email and password so that I can access my dashboard and study plans.
*   **Story:** As a user who has forgotten their password, I want a "Forgot Password" option that sends a reset link to my email so that I can regain access to my account.
*   **Story:** As a logged-in user, I want to be able to log out of my account so that I can protect my private information on a shared device.

---

### Epic 2: Course Management

This epic focuses on providing users with the tools to create, view, update, and delete their courses and associated syllabus content.

*   **Story:** As a logged-in user, I want to access a centralized course management page so that I can view, add, edit, and delete all my courses in one place.
*   **Story:** As a user, I want to add a new course by providing a title and its syllabus content so that the system can use this information to generate a study plan.
*   **Story:** As a user, I want to be prompted to generate a study plan immediately after creating a new course so that I can quickly get started.
*   **Story:** As a user, I want to view a list of all my existing courses on my dashboard so that I can get a quick overview of my studies.
*   **Story:** As a user, I want to edit the title and syllabus content of an existing course so that I can correct mistakes or update information.
*   **Story:** As a user, I want to delete a course that I no longer need so that I can keep my dashboard clean and focused.
*   **Story:** As a user who accidentally deleted a course, I want the system to perform a "soft delete" so that I have the option to restore it within 30 days.

---

### Epic 3: AI Study Plan Generation

This epic covers the core AI functionality of parsing a syllabus, understanding user preferences, and generating a personalized study schedule.

*   **Story:** As a user, I want the AI to parse my uploaded syllabus text to automatically identify topics and deadlines so that I don't have to enter them manually.
*   **Story:** As a user, I want to review and confirm the topics extracted by the AI before the final study plan is generated so that I can ensure its accuracy.
*   **Story:** As a user, I want the option to manually input or edit topics if the AI parsing fails or is inaccurate, providing a reliable fallback.
*   **Story:** As a user, I want to customize my available study hours per day and week so that the generated plan fits my personal schedule.
*   **Story:** As a user, I want to be able to set priorities for different topics or courses so that the study plan allocates more time to more important subjects.
*   **Story:** As a user, I want to see a loading indicator while the AI is generating my study plan so that I know the system is working.
*   **Story:** As a user, I want to be notified with a clear error message if the study plan generation fails so that I know what went wrong and can try again.
*   **Story:** As a user, I want the study plan generation to complete in under 10 seconds so that I can get my schedule quickly.

---

### Epic 4: Dashboard & Progress Tracking

This epic describes the main user interface for interacting with the study plan, viewing progress, and updating task status.

*   **Story:** As a logged-in user, I want to see a dashboard with a calendar view of my study activities so that I know what I need to study each day.
*   **Story:** As a user, I want to see progress bars for each of my courses on the dashboard so that I can visually track my overall progress at a glance.
*   **Story:** As a user, I want to click on a daily activity in the calendar to view its details, such as the topic and allocated time.
*   **Story:** As a user, I want to update the status of a study activity (e.g., 'Not Started', 'Completed', 'Missed') so that the system can track my progress accurately.
*   **Story:** As a user, I want my progress to be saved automatically when I update an activity's status so that I don't have to worry about losing my updates.
*   **Story:** As a user, I want my data to be securely saved and persistent across sessions so that my study plan is always up-to-date when I log in.

---

### Epic 5: Dynamic Plan Adaptation

This epic covers the "smart" features of the planner, including automatic rescheduling and helping users get back on track after a break.

*   **Story:** As a user, when I mark a study session as 'Missed', I want the system to automatically reschedule the remaining topics so that my study plan stays up-to-date and achievable.
*   **Story:** As a user, when I complete a study session ahead of schedule, I want the system to adjust the plan accordingly, potentially freeing up future time slots.
*   **Story:** As a user returning to the app after a long absence, I want to be greeted by a "Welcome Back" wizard so that I can easily manage my overdue tasks.
*   "**Story:** As a user in the ""Welcome Back"" wizard, I want to see a summary of my overdue tasks and be given options to reschedule them so that I don't feel overwhelmed and can get back on track."
