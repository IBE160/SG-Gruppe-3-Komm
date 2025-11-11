# Epics and User Stories for AI-Powered Personal Study Planner

This document breaks down the project requirements into actionable epics and user stories.

---

## Epic 1: User Authentication

**Goal:** To ensure secure and persistent access for users to their personal study plans.

**User Stories:**
- As a new user, I want to register for an account using my email and a password so that I can access the platform.
- As a new user, I want to receive a verification email and click a link to confirm my account, ensuring my email is valid.
- As a returning user, I want to log in with my email and password to access my dashboard and study plans.
- As a logged-in user, I want my session to be remembered so I don't have to log in every time I visit.
- As a user who has forgotten my password, I want to request a password reset link via email so I can regain access to my account.

---

## Epic 2: Dashboard & Core Study Plan

**Goal:** To provide users with a central, intuitive interface to view and interact with their study schedule.

**User Stories:**
- As a logged-in user, I want to see a dashboard that serves as my main hub for all study-related activities.
- As a user, I want to view my study activities organized in a calendar view on the dashboard so I can see what I need to do each day.
- As a user with multiple courses, I want to see a "My Courses" section on the dashboard with progress bars for each course, giving me a quick overview of my progress.
- As a user, I want to click on a calendar activity to view its details and update its status.

---

## Epic 3: Course Management

**Goal:** To allow users to easily add, update, and remove courses from their study planner.

**User Stories:**
- As a user, I want to add a new course by providing a title, topic, and the syllabus content.
- As a user, I want to be able to view a list of all my courses.
- As a user, I want to be able to edit the details of an existing course.
- As a user, I want to be able to delete a course I no longer need, which should also remove all associated study activities after a confirmation.

---

## Epic 4: AI-Powered Plan Generation

**Goal:** To leverage AI to automatically create a personalized and optimized study plan from user-provided course materials.

**User Stories:**
- As a user who has added a course, I want to click a button to have the AI generate a personalized study calendar based on my syllabus and exam dates.
- As a user, I want the AI to parse my syllabus content (plain text) to identify topics, important dates, and fixed events.
- As a user, I want to be able to customize the plan by specifying my available study hours and weekend preferences.
- As a user, I want the generated plan to be saved and automatically displayed in my dashboard calendar.

---

## Epic 5: Dynamic Rescheduling

**Goal:** To make the study plan adaptive and responsive to a user's actual progress.

**User Stories:**
- As a user who has missed a study session, I want the system to automatically reschedule the remaining topics to ensure I stay on track.
- As a user who has completed a study session, I want to mark it as "Completed" to accurately reflect my progress.
- As a user who could not complete a session, I want to mark it as "Not Completed" to trigger the rescheduling logic.

---

## Epic 6: Calendar Integration (Nice-to-Have)

**Goal:** To allow users to sync their study schedule with their primary personal or work calendars.

**User Stories:**
- As a user, I want to connect my Google Calendar or Outlook Calendar to the application.
- As a user, I want my generated study sessions to automatically appear as events in my connected external calendar.

---

## Epic 7: Gamification & Quizzes (Nice-to-Have)

**Goal:** To increase user motivation and knowledge retention through engaging features.

**User Stories:**
- As a user, I want to see my progress visualized through charts and graphs on the dashboard.
- As a user, I want to earn badges or maintain "streaks" for consistent studying to keep me motivated.
- As a user, I want the AI to generate short quizzes or flashcards for a specific topic so I can test my knowledge.

---

## Epic 8: Admin Panel (Nice-to-Have)

**Goal:** To provide administrators with the tools to manage the platform and its users.

**User Stories:**
- As an admin, I want to view a list of all registered users.
- As an admin, I want to be able to resolve common user issues, such as login problems.
- As an admin, I want to be able to identify and remove inactive user accounts to maintain a clean database.
