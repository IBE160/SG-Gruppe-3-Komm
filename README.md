# SG-Gruppe-3-Komm
Repository for SG-Gruppe-3-Komm - IBE160 Programmering med KI.

# 🧠 AI-Powered Personal Study Planner

## Overview
A **web-based application** that helps students structure and manage their study time efficiently before exams.  
By combining **AI scheduling** and **adaptive planning**, the system automatically generates personalized study plans based on uploaded syllabi, exam dates, and user preferences.

---

## 🎯 Purpose
Many students struggle to organize study time across several courses.  
This application reduces cognitive load by automatically:
- Distributing topics and allocating study sessions  
- Adjusting the plan dynamically when sessions are missed or completed early  
- Tracking progress across multiple courses

---

## 👩‍🎓 Target Users
- **Primary:** University and college students preparing for exams  
- **Secondary:** Adult and part-time learners balancing study with work or family life

---

## ⚙️ Core Features (MVP)
- **Login & Authentication:** Secure email verification via Supabase Auth  
- **Dashboard:** Calendar view with course progress bars  
- **AI-Generated Study Plan:** Day-by-day schedule generated from syllabus and exam dates  
- **Customization:** Adjust available hours, weekends, and topic priorities  
- **Dynamic Rescheduling:** Plan updates automatically based on progress  
- **Data Persistence:** Each user’s plan stored securely in Supabase  

**Optional Extensions**
- Google / Outlook calendar sync  
- AI-generated quizzes and flashcards  
- Progress charts and motivational streaks  
- Admin panel for user management  
- Offline PWA support  

---

## 🧩 Tech Stack
| Layer | Technology |
|--------|-------------|
| **Frontend** | Next.js 14, TypeScript, Tailwind CSS, Shadcn UI, Zustand |
| **Backend** | FastAPI (Python), Supabase (PostgreSQL + Auth) |
| **AI Integration** | Pydantic AI + Gemini 2.5 Pro/Flash for syllabus parsing and plan generation |
| **Deployment** | Vercel (frontend + backend), Supabase Cloud |
| **Testing** | Pytest, automatic OpenAPI docs via FastAPI |

---

## 📊 Data Model
- **User** → multiple **Courses** → multiple **Activities**  
- Stored securely with Supabase Row Level Security (RLS)

| Entity | Example Fields |
|--------|----------------|
| **User** | name, email, preferences |
| **Course** | title, syllabus_text, json_topics |
| **Activity** | topic, start_time, end_time, progress_status |

---

## 🧠 AI Integration
- **Gemini 2.5 Pro/Flash** parses syllabus content and extracts topics and hierarchy  
- **Pydantic AI** validates, structures, and serializes model data  
- **Scheduling algorithm** allocates topics dynamically based on user availability and progress  

---

## 🧭 User Journey
1. **Onboarding:** User registers and verifies email, guided to add first course.  
2. **Add Course:** Upload syllabus text; the app parses and confirms extracted topics.  
3. **Generate Plan:** AI and algorithm generate daily activities based on user time and exams.  
4. **Track Progress:** Users update daily activities (`Not Started`, `In Progress`, `Completed`).  
5. **Manage Courses:** CRUD operations through a central page, with soft delete for recovery.

---

## ✅ Success Criteria
- Study plan generated in under **10 seconds**  
- Data stored securely and persistently  
- Dynamic rescheduling fully functional  
- Stable and responsive web app for desktop and tablet use  

---

## 🔮 Future Improvements
- “Welcome Back” wizard for users returning after inactivity  
- Difficulty tagging and drag-and-drop editing of study sessions  
- Collaborative study groups  
- Advanced analytics and motivational features

---

## ⚖️ Assumptions
- Users have access to their syllabus in digital text format.  
- Students are open to following an AI-generated study plan.  
- Supabase and Gemini 2.5 APIs remain available and stable.

---

## 📚 Team
**Project:** IBE160 – Programming with AI  
**Group:** SG Gruppe 3 Komm  
**Institution:** Høgskolen i Molde  

---

## 📄 License
MIT License – see [LICENSE](LICENSE) for details.
