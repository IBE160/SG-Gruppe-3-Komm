# ibe160 - Product Requirements Document

**Author:**  BIP
**Date:** 2025-11-11
**Version:** 1.0

---

## Executive Summary

This document outlines the project brief for the AI-Powered Personal Study Planner, a web-based application designed to help students effectively structure their study time. The application will generate personalized and adaptive study plans based on exam dates, syllabus content, and user progress. By automating scheduling and dynamically adjusting to the user's performance, the planner aims to reduce stress, improve learning efficiency, and provide a data-driven approach to academic preparation.

### What Makes This Special

- **Dynamic Rescheduling:** Automatically adapts the study plan based on real-time user progress.
- **AI-Powered Syllabus Parsing:** Intelligently extracts topics and deadlines from user-provided syllabus content.
- **Personalized & Adaptive:** Tailors the plan to individual study habits, availability, and topic difficulty.
- **"Welcome Back" Wizard:** Proactively helps users who have been away to triage overdue tasks and get back on track without feeling overwhelmed.

---

## Project Classification

**Technical Type:** Web Application
**Domain:** EdTech
**Complexity:** Medium

The project is a modern web application utilizing a Next.js 14+ frontend with App Router, TypeScript, Tailwind CSS, Shadcn UI, and Zustand for state management. The backend is built with FastAPI (Python), Supabase (PostgreSQL) for database and authentication, and integrates with OpenAI GPT-4 for AI capabilities.

---

## Success Criteria

### Business Objectives

- Achieve a high rate of user adoption and satisfaction within the target student demographic.
- Reduce the manual planning effort required by students by at least 75%.
- Establish a platform that can be extended with future premium features.

### Key Performance Indicators

- **Adoption:** Number of active users and new sign-ups per week.
- **Engagement:** Daily/Weekly active users, average number of sessions per user.
- **Retention:** Percentage of users who continue to use the app after the first week and first month.
- **Task Completion Rate:** Percentage of study tasks marked as "Completed."
- **Plan Generation Speed:** Study plan generation should take under 10 seconds.

### MVP Success Criteria

- Users can successfully generate a study plan in under 10 seconds.
- Users can upload a syllabus, customize the plan, and save their progress.
- The dynamic rescheduling feature correctly adjusts the plan when a session is marked as missed.
- User data persists securely across sessions.
- The MVP is successfully deployed within the 6-week timeline.

---

## Product Scope

### MVP - Minimum Viable Product

- **Login:** User registration and authentication system with email verification.
- **Dashboard:** A central view containing a calendar of activities, a list of "My Courses," and progress bars for each course.
- **AI-Generated Study Plan:** Automatically generate a day-by-day study schedule from uploaded syllabus and exam dates.
- **Customization:** Users can adjust available hours, weekends, and topic priorities.
- **Dynamic Rescheduling:** Missed or completed sessions trigger real-time updates to the plan.
- **Authentication & Data Persistence:** Each user securely saves and retrieves their personalized plan.

### Out of Scope for MVP

- **Calendar Integration:** Syncing sessions with Google or Outlook calendar.
- **Quiz/Flashcard Generation:** AI-generated review quizzes per topic.
- **Progress Visualization:** Advanced progress charts, motivational streaks, and badges.
- **Admin Panel:** A dedicated interface for managing users and handling login issues.
- **PWA Features:** Offline access and home-screen installation.

---

## Functional Requirements

The user journey is designed to be intuitive, from onboarding to daily use. Key refinements from brainstorming sessions have been incorporated:

1.  **Onboarding:** A new user is greeted with a welcoming dashboard that guides them to add their first course. The system includes a "Resend Verification Email" option to handle email delivery issues.
2.  **Course Creation:** The user adds a course by providing a title and syllabus content. The technical `JSON` field is abstracted away. The application will proactively ask to generate a study plan immediately after course creation.
3.  **Plan Generation:** The AI parses the syllabus, and the user confirms the extracted topics before the plan is generated. The UI includes loading indicators and clear error messages if the AI fails. A manual input option is available as a fallback.
4.  **Daily Interaction:** The user views their daily tasks on a calendar dashboard. They update the status of activities using clear labels (`Not Started`, `In Progress`, `Completed`, `Missed`). An auto-save feature simplifies this interaction.
5.  **Course Management:** All course CRUD (Create, Read, Update, Delete) operations are consolidated into a single, centralized management page. Deleting a course is a "soft delete," allowing users to restore it within 30 days.

---

## Non-Functional Requirements

- **Platform Requirements:**
    - Must be web-based and accessible via modern browsers (Chrome, Firefox, Safari, Edge).
    - Must be responsive and functional on desktop, laptop, and tablet devices (minimum screen width: 768px).
    - Mobile phone support is optional for MVP but should be considered in design.
- **Performance Requirements:**
    - Application must load within 3 seconds on standard broadband connection.
- **Security Requirements:**
    - Must use Supabase Auth for secure user authentication with JWT tokens.
    - Must leverage Supabase Row Level Security (RLS) for data access control.
    - Must encrypt sensitive data (passwords handled by Supabase, payment info by Stripe) at rest and in transit.
- **Integration Requirements:**
    - Must integrate with Supabase for database, authentication, and real-time features.
    - Must integrate with OpenAI API or similar LLM service for AI decision-making and question generation.
    - Supabase Auth handles email delivery for authentication (verification, password resets).
    - API design must support future mobile app development.
- **Data Requirements:**
    - Must support data export in common formats (CSV, PDF).
    - Must implement database backups and disaster recovery.
- **Development Constraints:**
    - Must complete development within 6 weeks with AI-assisted development tools.
    - Must use proven, well-documented technologies suitable for AI-assisted coding.
    - Must include comprehensive API documentation.

---

## Implementation Planning

### Epic Breakdown Required

Requirements must be decomposed into epics and bite-sized stories.

**Next Step:** See the `epics.md` file for a detailed breakdown.

---

## References

- proposal.md
- product-brief-2025-11-10.md

---

## Next Steps

1. **Epic & Story Breakdown** - See `epics.md`
2. **UX Design** (if UI) - Run: `workflow ux-design`
3. **Architecture** - Run: `workflow create-architecture`

---

_This PRD captures the essence of ibe160 - an adaptive, AI-powered personal study planner._

_Created through collaborative discovery between  BIP and AI facilitator._
