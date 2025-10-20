# 🧠 AI-Powered Personal Study Planner

## Background
Many students struggle to structure their study time effectively before exams. Balancing multiple courses, deadlines, and limited energy often leads to inefficient study habits and stress. An AI-powered study planner can automate scheduling, reduce cognitive load, and help students achieve consistent progress through data-driven personalization.

## Purpose
The goal of this project is to create a **web-based application** that generates a **personalized, adaptive study plan** based on:
- Exam dates and syllabus content  
- The user’s available study time  
- Their progress updates and preferences  

The system will automatically distribute topics, schedule repetitions, and dynamically reschedule sessions when users fall behind or complete topics early.

## Target Users
- **Primary Users:** University and college students preparing for multiple exams.  
- **Secondary Users:** High-school and adult learners balancing study with work or family commitments.

---

## Core Functionality

### Must-Have (MVP)
- ✅ **AI-Generated Study Plan:** Automatically generate a day-by-day study schedule from uploaded syllabus and exam dates.  
- ✅ **Customization:** Users can adjust available hours, weekends, and topic priorities.  
- ✅ **Dynamic Rescheduling:** Missed or completed sessions trigger real-time updates to the plan.  
- ✅ **Authentication & Data Persistence:** Each user securely saves and retrieves their personalized plan.

### Nice-to-Have (Optional Extensions)
- ⭐ **Calendar Integration:** Sync sessions with Google or Outlook calendar.  
- ⭐ **Quiz/Flashcard Generation:** AI generates short review quizzes per topic.  
- ⭐ **Progress Visualization:** Display progress charts, motivational streaks, and badges.  
- ⭐ **Admin Panel:** Manage users and handle login issues (remove inactive users).  
- ⭐ **PWA Features:** Offline access and home-screen installation.

---

## Data Requirements
| Entity | Key Fields | Description |
|--------|-------------|-------------|
| **User** | name, email, hashed password, preferences | Authentication and settings |
| **StudyPlan** | syllabus_topics, exam_date, allocated_hours, daily_tasks | Core study schedule |
| **ProgressLog** | date, completed_sessions, missed_sessions | Used for rescheduling |
| **AIInput** | syllabus_text, parsed_topics, model_response | Stores AI parsing data |
| **Admin** (optional) | id, credentials, activity_log | Admin management tools |

**Relationships:** one-to-many — each **User** → multiple **StudyPlans** → multiple **ProgressLogs**.

---

## Technical Architecture

| Layer | Technology | Purpose |
|--------|-------------|----------|
| **Frontend** | React + Vite + Tailwind CSS | SPA interface, responsive UI |
| **Backend** | Node.js (Express) | REST API endpoints, AI and DB integration |
| **Database** | Firebase Firestore *(alt: PostgreSQL + Prisma)* | Cloud storage for users, plans, and progress |
| **Authentication** | Firebase Auth (JWT-based) | Secure login and user management |
| **AI/ML Services** | OpenAI GPT-4 API | Syllabus parsing and study-plan generation |
| **Hosting** | Vercel (frontend) + Render (backend) | Free-tier student hosting |
| **Version Control** | GitHub + Git branching | Collaborative development workflow |

---

## AI/ML Integration Plan
| Function | Model / Tool | Description |
|-----------|---------------|-------------|
| **Syllabus Parsing** | GPT-4 | Extract topics and hierarchy from PDF/text syllabus |
| **Plan Generation** | GPT-4 + Algorithm | Combine AI understanding with time allocation logic |
| **Dynamic Updates** | Algorithmic (JS) | Redistribute remaining sessions after missed days |
| **Quiz Generation (optional)** | GPT-4 | Generate short quiz questions per topic |

**Prompt Example:**  
> “Extract all chapters and subtopics from the following syllabus text and return them as a JSON list sorted by logical order.”

**Fallback:** Manual input if parsing fails.  
**Cost Control:** Cache AI responses and limit API re-requests.

---

## Timeline and Milestones (6 Weeks)
| Week | Milestone | Deliverables |
|------|------------|--------------|
| 1 | Project Setup | GitHub repo, Firebase setup, authentication |
| 2 | Database + Auth Integration | Firestore schema, user registration/login |
| 3 | Syllabus Parsing Prototype | PDF upload + GPT-4 extraction |
| 4 | Study Plan Generation | AI-assisted schedule creation + frontend display |
| 5 | Dynamic Rescheduling & Testing | Handle missed/completed sessions, QA |
| 6 | Polish & Deployment | Responsive design, optional features, docs |

---

## BMAD Alignment Summary
| BMAD Stage | Description | Implementation |
|-------------|-------------|----------------|
| **Business** | Identify student need for structured study | Pain point: stress & poor time use |
| **Motivation** | Improve efficiency & reduce anxiety | Personalized AI plan for smarter studying |
| **Architecture** | Define stack & data flow | React frontend, Node backend, Firebase + GPT |
| **Development** | Build & iterate | 6-week agile cycle with weekly milestones |

---

## Success Criteria
- ✅ Study plan generation under 10s.  
- ✅ Upload syllabus, customize plan, save progress.  
- ✅ Dynamic rescheduling for missed sessions.  
- ✅ Data persistence across sessions.  
- ✅ MVP deployed by Week 6.  
- ⭐ Optional: Calendar sync and AI quiz generation.

---

## Reflection Summary — Feedback Implementation
- ✅ Added full **technical architecture** — fixes backend & missing details.  
- ✅ Introduced **AI/ML plan** with GPT-4 usage and logic.  
- ✅ Added **6-week timeline** and BMAD phase link.  
- ✅ Refined **scope** (MVP vs optional).  
- ✅ Specified **auth method** (Firebase).  
- ✅ Clarified **database structure**.  
- ✅ Strengthened **success criteria** and academic rigor.  

---

**File Name Suggestion:**  
`AI-Powered_Personal_Study_Planner_Revised.md`
