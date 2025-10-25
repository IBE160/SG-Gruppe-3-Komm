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
- **Login:** User registration and authentication system with email verification
- **Dashboard** Calendar, My courses, Course progressbar
- **AI-Generated Study Plan:** Automatically generate a day-by-day study schedule from uploaded syllabus and exam dates.  
- **Customization:** Users can adjust available hours, weekends, and topic priorities.  
- **Dynamic Rescheduling:** Missed or completed sessions trigger real-time updates to the plan.  
- **Authentication & Data Persistence:** Each user securely saves and retrieves their personalized plan.

### Nice-to-Have (Optional Extensions)
- **Calendar Integration:** Sync sessions with Google or Outlook calendar.  
- **Quiz/Flashcard Generation:** AI generates short review quizzes per topic.  
- **Progress Visualization:** Display progress charts, motivational streaks, and badges.  
- **Admin Panel:** Manage users and handle login issues (remove inactive users).  
- **PWA Features:** Offline access and home-screen installation.

---

## Data Requirements
| Entity | Key Fields | Description |
|--------|-------------|-------------|
| **User** | name, email, hashed_password, preferences | Authentication and settings |
| **Course** | name, system_prompt, topic, syllabus_content, json | Course in study |
| **Activity** | activity_topic, starttime, endtime, progress_status | Daily activity with progress status types: Not Started - Completed - Not Completed |

**Relationships:** one-to-many — each **Users** → multiple **Courses** → multiple **Activities**.

## User Flows

### Flow 1: Student Adds New User In Webapplication
**Entry Point**: Student lands on homepage

1. **Dashboard Page**
   - If not logged in - go to point 2. Authentication
   - Student views the dashboard that shows the calender content 

2. **Authentication**
   - If not logged in: Redirects to registration/login page
   - Student registers with email and password
   - Receives verification email and clicks verification link if new user
   - Redirected back to platform and automatically logged in
  

### Flow 2: Student Adds New Course And Content (based on this course content the AI is generating the calender activity JSON file as input to the LLM)
**Entry Point**: Student are logged inn to Dashboard

1. **Dashboard**
   - Student clicks "Add course" button in Dashboard
   - Moves to "New Course" page
   - 
2. **Student Adds Course And Syllaby Content**
   - Student enters title, topic, sullabus content, JSON format and relevant dates into mandertory fields
   - Clicks "Save" button
   - Optional: Clicks "Generate AI Powered calendar" button (after "Save" is pressed) if the Student wants to create the calendar "on the fly"
   - Moves back to Dashboard

### Flow 3: Student Updates Activity Status
**Entry Point**: Student are logged inn to Dashboard

1. **Dashboard**
   - Student clicks the calender activity
  
2. **Student updates activity content**
   - Student updates status on activity (Ex: Completed or Not Completed)
   - Student clicks "Save" button to update info
   - Moves back to Dashboard
  
### Flow 4 EXTRA: Student AI Generates New Date For Not Performed Activity
**Entry Point**: Student are logged inn to Dashboard

1. **Dashboard**
   - Student locates the past activity

2. **Student AI generates new date for activity**
   - Student clicks "AI locate new date" button on activity
   - Moves back to Dashboard

### Flow 5 EXTRA: Student Deletes Course
**Entry Point**: Student are logged inn to Dashboard

1. **Dashboard**
   - Student clicks the "Edit" button on an existing calender activity
  
2. **Student Confirms Deletes Course**
   - Student clicks the "Delete" button in the course "Edit" window
   - Ask if the Student is sure if the Course should be deleted
   - Student clicks "Yes" button and the course and all course calender activities is deleted
   - Moves back to Dashboard 

3. **Student Confirms Not to Deletes Course**
   - Student is sure the Course should be deleted
   - Clicks "No" button 
   - Moves back to Dashboard without any action

### Flow 5 EXTRA: Show All Courses
**Entry Point**: Student are logged inn to Dashboard

1. **Dashboard**
   - Student clicks the "Course" button on Dashboard
  
2. **Student Select One The Courses**
   - Student clicks on one of the courses in the Courselist
   - Student can now Edit, Read, Delete or Add a new course (CRUD - Create, Read, Update and Delete)
   - Student clicks "Save" button when content is added or updated
   - Moves back to Dashboard

---

## Technical Constraints

**Platform Requirements:**
- Must be web-based and accessible via modern browsers (Chrome, Firefox, Safari, Edge)
- Must be responsive and functional on desktop, laptop, and tablet devices (minimum screen width: 768px)
- Mobile phone support is optional for MVP but should be considered in design

**Performance Requirements:**
- Application must load within 3 seconds on standard broadband connection

**Security Requirements:**
- Must use Supabase Auth for secure user authentication with JWT tokens
- Must leverage Supabase Row Level Security (RLS) for data access control
- Must encrypt sensitive data (passwords handled by Supabase, payment info by Stripe) at rest and in transit

**Integration Requirements:**
- Must integrate with Supabase for database, authentication, and real-time features
- Must integrate with OpenAI API or similar LLM service for AI decision-making and question generation
- Supabase Auth handles email delivery for authentication (verification, password resets)
- API design must support future mobile app development

**Data Requirements:**
- Must support data export in common formats (CSV, PDF)
- Must implement database backups and disaster recovery

**Development Constraints:**
- Must complete development within 6 weeks with AI-assisted development tools
- Must use proven, well-documented technologies suitable for AI-assisted coding
- Must include comprehensive API documentation

---

## Success Criteria
- Study plan generation under 10s.  
- Upload syllabus, customize plan, save progress.  
- Dynamic rescheduling for missed sessions.  
- Data persistence across sessions.  
- MVP deployed by Week 6.  
- Optional: Calendar sync and AI quiz generation.

---

## Technical Specifications

### Frontend Specification
- **Framework**: Next.js 14+ with App Router for server-side rendering and optimal performance
- **Language**: TypeScript for type safety and better AI-assisted development
- **Styling**: Tailwind CSS for rapid, responsive UI development
- **State Management**: Zustand for lightweight, scalable global state management
- **Data Visualization**: Recharts for interactive, customizable supply chain visualization
- **Shadcn UI**: Shadcn UI for rapid, responsive UI development
- **Forms**: React Hook Form with Zod validation for robust form handling
- **Authentication UI**: Supabase Auth UI components + custom styling
- **Real-time Updates**: Supabase Realtime client for live game monitoring and multiplayer
- **API Communication**: Axios with interceptors for authenticated requests
- **Deployment**: Vercel for frontend hosting with automatic CI/CD

**Architecture Pattern**: Component-based architecture with clear separation between presentation components, container components, and business logic hooks.

### Backend Specification
- **Framework**: FastAPI (Python) for high-performance RESTful API development
- **Language**: Python for AI integration compatibility and rapid development
- **Database**: Supabase (PostgreSQL) for managed database and real-time capabilities
- **Authentication**: Supabase Auth for built-in user management, JWT tokens, and email verification
- **Authorization**: Row Level Security (RLS) policies in Supabase + role-based middleware (student/teacher/admin roles)
- **ORM**: SQLAlchemy for database operations and type safety
- **Database Migrations**: Alembic for version-controlled schema changes
- **Email Service**: Supabase Auth for authentication emails + SendGrid for custom transactional emails
- **API Documentation**: FastAPI automatic OpenAPI/Swagger documentation
- **Testing**: Pytest for unit and integration tests
- **Build Tool**: UV for fast Python package management
- **Deployment**: Vercel (FastAPI supports Vercel deployment)

**API Architecture**: RESTful API design with versioning (/api/v1/) and clear resource-oriented endpoints.

### Database Specification
- **Database Type**: Supabase (PostgreSQL-based relational database)
- **ORM**: SQLAlchemy for Python-based type-safe database access
- **Migrations**: Alembic for database schema version control
- **Hosting**: Supabase managed cloud (includes automatic backups, scaling, and monitoring)

**Implementation**:
- **Model**: Gemini 2.5 pro/flash
- **Rate Limiting**: Implement request queuing and caching for cost optimization

**API Integration Architecture**:
- Separate service layer for AI calls
- Retry logic with exponential backoff
- Response validation and sanitization
- Caching for repeated similar scenarios

### Platform Type
**Primary Platform**: Web application (browser-based)

**Target Devices**:
- Desktop computers (primary): Windows, macOS, Linux
- Laptops (primary): All operating systems
- Tablets (secondary): iPad, Android tablets (landscape orientation recommended)
- Mobile phones (future): iOS and Android via responsive design or dedicated apps

**Browser Compatibility**:
- Chrome 90+ (primary testing target)
- Firefox 88+
- Safari 14+
- Edge 90+

**Responsive Breakpoints**:
- Desktop: 1280px+ (optimal experience)
- Laptop: 1024px-1279px (full features)
- Tablet: 768px-1023px (adapted layout)
- Mobile: 375px-767px (future phase - simplified UI)

### User Authentication Specification
**Authentication Method**: Supabase Auth with JWT-based authentication

**Features**:
- Email/password registration with built-in validation
- Automatic email verification via Supabase Auth email templates
- Secure password reset flow with magic links
- Session management with automatic refresh token rotation
- "Remember me" functionality via Supabase persistent sessions
- Account lockout and rate limiting built into Supabase Auth

**Implementation Details**:
- Passwords automatically hashed by Supabase (bcrypt)
- JWT access tokens managed by Supabase (automatic expiry and refresh)
- Refresh tokens securely stored by Supabase (httpOnly cookies)

**Supabase Auth Benefits**:
- Built-in security best practices (password hashing, token management)

---

## AI Integration Plan
| Function | Model / Tool | Description |
|-----------|---------------|-------------|
| **Syllabus Parsing** | GPT-4 | Extract topics and hierarchy from PDF/text syllabus |
| **Plan Generation** | GPT-4 + Algorithm | Combine AI understanding with time allocation logic |
| **Dynamic Updates** | Algorithmic (JS) | Redistribute remaining sessions after missed days |

**Prompt Example:**  
> “Extract all chapters and subtopics from the following syllabus text and return them as a JSON list sorted by logical order.”

**Fallback:** Manual input if parsing fails.  
**Cost Control:** Cache AI responses and limit API re-requests.

---

## Timeline and Milestones (6 Weeks)

**Total Duration**: 5 weeks following BMAD-methodology (4-phase model)

This timeline follows the 4-phase model of the BMAD-methodology, where phases 1 and 2 are done in 2 weeks, phase 3 is done in 2 weeks, and phase 4 is done in 2 weeks.

| Phase | Duration | Week | Focus |
|-------|----------|------|-------|
| Phase 1 & 2: Analyze and Planning | 1 week | Requirements analysis, project planning  |
| Phase 3: Solution Architecture and UI/UX Design | 2 weeks | Technical architecture, database design, UI/UX mockups, API design |
| Phase 4: Development and Deployment | 2 weeks | Implementation, testing, deployment |

### BMAD-Methodology Alignment

**Phase 1 (Analyze)**: Deep understanding of business problem, user needs, and constraints
**Phase 2 (Planning)**: Strategic planning of solution approach with clear milestones
**Phase 3 (Architecture & Design)**: Complete technical and visual blueprint before coding
**Phase 4 (Development)**: Rapid AI-assisted implementation following the blueprint

## Reflection Summary — Feedback Implementation
- Added full **technical architecture** — fixes backend & missing details.  
- Introduced **AI/ML plan** with GPT-4 usage and logic.  
- Added **5-week timeline** and BMAD phase link.  
- Refined **scope** (MVP vs optional).  
- Specified **auth method** .  
- Clarified **database structure**.  
- Strengthened **success criteria** and academic rigor. 