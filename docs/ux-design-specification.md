# {{project_name}} UX Design Specification

_Created on fredag 21. november 2025 by BIP_
_Generated using BMad Method - Create UX Design Workflow v1.0_

---

## 1. Project Vision & UX Strategy

### 1.1 Vision & Core Experience

-   **Vision:** To create an AI-powered study planner that transforms academic stress into calm, focused productivity by providing an intelligent, adaptive schedule.
-   **Core Experience:** An effortless daily check-in loop and a magical initial plan generation, all supported by a dynamic rescheduling engine that adapts to the user's life.
-   **Desired Emotional Goal:** To make the user feel **empowered, in control, calm, and quietly confident**.

### 1.2 Platform & Technical Foundation

-   **Platform:** A responsive web application primarily targeting **desktop, laptop, and tablet** use.
-   **Technical Foundation:** The UI will be built upon **Shadcn UI**, leveraging its clean, modern, and accessible components as a starting point. Inspiration is drawn from the clear, structured interaction patterns of applications like Trello and Notion.

### 1.3 UX Complexity Assessment

The project is assessed as being of **Medium Complexity**. Key factors include:
-   **Single User Role (Student):** Simplifies the core experience.
-   **Multiple Key Journeys:** Onboarding, Plan Generation, Daily Check-in, and the "Welcome Back" wizard.
-   **Medium Interaction Complexity:** While daily task management is simple, the AI-driven plan generation and dynamic rescheduling logic require careful and clear UX design.
-   **Novel Interaction Pattern:** The "Welcome Back" wizard represents a unique UX challenge that requires a novel design solution to be effective and empathetic.

---

## 1. Design System Foundation

### 1.1 Design System Choice

The project will be built upon **Shadcn UI**.

-   **System:** Shadcn UI
-   **Rationale:** This decision was made based on the system's alignment with the project's technical and design goals. Shadcn UI is not a traditional component library but a collection of reusable, composable, and accessible components built on Tailwind CSS and Radix. This provides the perfect balance between the development speed of using pre-built elements and the creative freedom required to achieve a unique and polished user experience.
-   **Key Benefits:**
    -   **Modern & Clean Aesthetic:** Aligns with the desired emotional goal of a calm and focused user experience.
    -   **High Customizability:** Allows for easy theming to establish a unique brand identity.
    -   **Accessibility by Default:** Provides a strong foundation for building an inclusive application that is usable by everyone.
    -   **Developer Efficiency:** The use of Tailwind CSS enables rapid development and iteration.
-   **Provides:** A comprehensive set of foundational components such as buttons, forms, modals, calendars, and menus, which will accelerate the development of the user interface.

---

## 2. Core User Experience

### 2.1 Defining Experience

The defining experience of the AI-Powered Personal Study Planner is **intelligent, adaptive scheduling**. The application's primary role is to serve as a dynamic and responsive guide for the user's academic journey.

-   **Core User Action:** The most frequent and central user action is the daily check-in. The user will view their dashboard, identify the day's tasks, and update their status (e.g., `Completed`, `Missed`). This interaction must be exceptionally fast, simple, and satisfying to encourage daily engagement.

-   **Most Effortless Interaction:** The "Welcome Back" wizard is a critical and defining feature. When a user returns after a period of inactivity, the application must proactively and gently help them triage overdue tasks and reschedule their plan. This process must be designed to alleviate anxiety and prevent the user from feeling overwhelmed, reinforcing the application's role as a supportive tool.

-   **Most Critical Moment:** The initial study plan generation is the single most critical moment in the user journey. This is the "magic moment" where the user's unstructured syllabus is transformed into a clear, actionable plan. Success at this stage builds immediate trust and demonstrates the core value of the product. The process must be transparent, allowing user confirmation of parsed topics before committing to the full plan.

### Platform

The application will be a **responsive web application**. The primary experience is designed for **desktop, laptop, and tablet** use (minimum screen width of 768px), as these are the primary devices students use for focused study sessions. While not the primary target for the MVP, the design will consider mobile-friendliness for future expansion.

### 2.2 The Defining Experience: The "Welcome Back" Wizard

While daily check-ins are the most frequent interaction, the app's most defining and emotionally resonant feature is the **"Welcome Back" Wizard**. This interaction pattern is novel to our application and represents the core value of an adaptive, empathetic planner. It is triggered when a user returns after a significant period of inactivity (e.g., >3 days) and is faced with a potentially overwhelming number of overdue tasks.

The goal of this pattern is to turn a moment of anxiety into one of relief and empowerment.

**Interaction Flow:**

1.  **Trigger:** The system detects a login after a multi-day absence and a significant number of overdue tasks.
2.  **Greeting:** Instead of the standard dashboard, the user is presented with a full-screen, non-judgmental modal. The message is supportive: "Welcome back! Life happens. Let's get you back on track."
3.  **Diagnosis:** The wizard clearly and simply states the current situation, e.g., "You have 12 overdue tasks."
4.  **Strategic Options:** The user is presented with clear, simple choices for how to handle the overdue items. This is the core of the interaction:
    *   **Spread it Out (Recommended):** Intelligently reschedules the missed tasks over a manageable future period (e.g., the next 1-2 weeks).
    *   **Intensive Catch-up:** Adds a small number of overdue tasks to each of the next few days for users who want to catch up quickly.
    *   **Declare a Fresh Start:** Archives all overdue tasks, allowing the user to focus entirely on the upcoming schedule. This serves as an escape hatch to prevent complete abandonment of the tool.
5.  **Confirmation & Feedback:** After the user selects an option, the system provides immediate visual feedback, such as an animation of the calendar reorganizing itself. The user then lands on their newly updated, manageable dashboard for the current day.

### 2.3 Core Experience Principles

These principles, derived from our core experience design, will guide all UX/UI decisions:

-   **Guidance over Control:** The app will always offer a smart, default recommendation for any complex decision (like the "Spread it Out" option), but the user always has the final say. The app is a knowledgeable guide, not a dictator.
-   **Clarity over Clutter:** In moments of complexity, such as onboarding or rescheduling, the interface will use focused, step-by-step flows (wizards, modals) to eliminate distractions and reduce cognitive load.
-   **Effortless over Efficient:** The user's *perception* of effort is the primary concern. Even if it requires an extra click, a guided process that feels easier is preferable to a more compact but confusing one.
-   **Feedback is a Conversation:** The system must provide immediate, clear, and often visual feedback in response to user actions. This makes the application feel responsive and alive, turning a one-way interaction into a two-way conversation.


---

## 3. Visual Foundation

### 3.1 Color System

A collaborative and visual approach was taken to define the application's color system. Four distinct theme directions were generated to explore different emotional tones, each with a full palette and live UI component previews.

The themes explored were:
-   **Calm & Focused:** A serene blue palette designed to evoke trust and serenity.
-   **Academic & Traditional:** A sophisticated navy and cream palette for a prestigious, university feel.
-   **Modern & Energetic:** A vibrant green-based theme intended to feel motivating and fresh.
-   **Minimal & Clean:** A high-contrast monochrome theme designed for ultimate focus.

**Interactive Visualizations:**

An interactive HTML file has been generated to allow for deep exploration and side-by-side comparison of these themes in both light and dark modes.

-   **Color Theme Explorer:** [ux-color-themes.html](./ux-color-themes.html)

This artifact serves as the primary tool for selecting the final color direction. The user's choice and rationale will be documented here upon selection.

---

## 4. Design Direction

### 4.1 Chosen Design Approach

To make a well-informed decision on the application's fundamental layout and interaction model, a collaborative and visual exploration was conducted. Six distinct design directions were mocked up to showcase different approaches to navigation, information density, and visual style.

The explored directions were:
1.  **The Dashboard Pro:** Sidebar navigation, high information density, card-based layout.
2.  **The Zen Focus:** Sidebar navigation, spacious and minimal, list-based layout.
3.  **The Web App Standard:** Traditional top navigation, balanced density, card-based layout.
4.  **The Streamlined List:** Top navigation paired with a spacious, single-column list.
5.  **The Visual Grid:** A more graphical, grid-based layout for visualizing courses.
6.  **The Minimalist's View:** An ultra-clean, command-palette-driven interface.

**Interactive Mockups:**

An interactive HTML showcase was generated to allow for direct comparison of these six directions, including responsive previews.

-   **Design Direction Showcase:** [ux-design-directions.html](./ux-design-directions.html)

This artifact is the basis for choosing the final design direction. The user's choice and the rationale behind it will be documented here once a decision is made.

---

## 5. User Journey Flows

### 5.1 Critical User Paths

This section details the design of critical user journeys, ensuring they are intuitive, empathetic, and aligned with our core experience principles.

### Journey: Initial Study Plan Generation

This is the most critical journey for a new user, representing the core "magic moment" of the application. The chosen approach is the **"Guided Wizard"**, which prioritizes clarity and user confidence over speed, directly aligning with our "Guidance over Control" principle.

**Approach:** A multi-step, modal-based wizard that walks the user through the process, ensuring they are never overwhelmed.

**Flow Steps:**

1.  **Trigger:** User clicks "Add New Course" from the dashboard.
2.  **Step 1: Course Basics**
    *   **User Sees:** A clean modal asking for "Course Name" and "Exam Date". The date picker will prevent selecting past dates.
    *   **User Does:** Fills in the two fields and clicks "Next".
3.  **Step 2: Add Syllabus**
    *   **User Sees:** A clear choice between "Upload Syllabus File" (with accepted formats listed) and "Paste Topics Manually".
    *   **User Does:** Uploads a file or pastes text.
    *   **System Responds:** A loading indicator appears while the AI parses the content.
4.  **Step 3: Confirm Topics**
    *   **User Sees:** A list of topics extracted by the AI. Each topic is editable or deletable.
    *   **User Does:** Reviews the list, makes any necessary corrections, and clicks "Confirm Topics". This step is crucial for building trust and ensuring accuracy.
5.  **Step 4: Set Your Pace**
    *   **User Sees:** Simple, friendly questions like "How many hours can you study per week?" and "Do you study on weekends?".
    *   **User Does:** Adjusts sliders or inputs their preferences.
6.  **Step 5: Generation & Completion**
    *   **User Sees:** A final confirmation screen with a "Generate My Plan!" button. Upon clicking, a progress indicator is shown.
    *   **System Responds:** Once complete, the wizard closes, and the user is taken to their dashboard where the new course and its study plan are now visible. A success notification appears briefly.

**Rationale:** This wizard-based approach prevents the cognitive overload of a single large form, builds user trust by allowing confirmation at the AI-interaction step, and gently guides the user to a successful outcome, ensuring their first major interaction with the app is a positive and empowering one.

---

## 6. Component Library

### 6.1 Component Strategy

Our component strategy is to leverage the **Shadcn UI** library as our foundational toolkit. The vast majority of the UI (buttons, modals, inputs, menus, etc.) will be built by composing these high-quality, accessible components.

However, to deliver our unique user experience, we will develop a small number of custom, highly-specialized components. The strategy is to use the Shadcn primitives (e.g., Card, Badge, Dialog) as the building blocks for these custom components wherever possible, ensuring a consistent look and feel.

### 6.2 Custom Component Definitions

#### Component: `StudyTaskCard`

This is the most critical custom component in the application, as it's the primary point of interaction for the user's daily workflow.

-   **Purpose:** To display a single study task for the day and provide a fast, satisfying, and low-effort way for the user to update its status.

-   **Anatomy:**
    -   **Course Title:** A small, muted text element indicating the parent course (e.g., "Calculus").
    -   **Task Title:** The primary, larger text describing the study block (e.g., "Chapter 3 Problems").
    -   **Status Indicator:** A prominent, color-coded visual element (e.g., a colored dot or a small tag) that provides an at-a-glance understanding of the task's state.
    -   **Action Area:** The entire card surface will serve as the primary interactive element to encourage quick updates.

-   **States and Variants:**
    -   **Not Started (Default):** A clean, neutral card with a grey status indicator. It invites interaction without creating pressure.
    -   **In Progress:** A subtle visual shift, such as a blue indicator or border, to signify that it is the current active task.
    -   **Completed:** A highly satisfying visual transformation. The card content will be faded, the title will have a strikethrough, and a prominent green checkmark will appear. This provides positive reinforcement.
    -   **Missed:** A clear but non-judgmental state, indicated by a red status indicator, to inform the user without causing anxiety.
    -   **Hover:** The card will have a subtle lift or glow on hover to clearly communicate its interactivity.

-   **Behavior:**
    -   **Primary Interaction (Clicking the Card):** A single click on the card will cycle the status from `Not Started` -> `In Progress` -> `Completed`. This makes the most common workflow incredibly efficient.
    -   **Secondary Interaction (Marking as Missed):** To prevent accidental negative marking, marking a task as `Missed` will require a more deliberate action, such as clicking a small "x" icon that appears only on hover.

---

## 7. UX Pattern Decisions

### 7.1 Consistency Rules

To ensure a cohesive, predictable, and calm user experience, the following UX patterns will be applied consistently across the application.

#### 1. Feedback Patterns (System-to-User Communication)

-   **Success Feedback:** Non-intrusive "toast" notifications will be used (e.g., in the bottom-right corner). They will appear for 3-4 seconds and then fade automatically to confirm a successful action (e.g., "Plan Saved!") without interrupting the user's flow.
-   **Error Feedback:** For critical errors (e.g., API failure), a persistent red toast will be used that must be manually dismissed. For form validation errors, specific error messages will appear inline, directly beneath the relevant input field, providing immediate and contextual guidance.
-   **Loading Indicators:**
    -   **Initial Page/View Load:** A "skeleton" loader that mimics the shape of the upcoming content will be used. This manages expectations and makes the app feel faster.
    -   **Button/Action-Specific Load:** When an action is initiated via a button (e.g., "Generate Plan"), a spinner will appear inside the button itself, disabling it until the action is complete.

#### 2. Form Patterns (User-to-System Communication)

-   **Labels:** To maintain a clean and modern aesthetic while ensuring clarity, forms will use "floating labels." The label will appear inside the input field as a placeholder and will animate to a position above the field when the user focuses on it.
-   **Validation:** Form field validation will be triggered `onBlur` (when the user clicks or tabs away from a field). This prevents the anxiety of seeing validation errors while the user is still in the process of typing.

#### 3. Confirmation Patterns (Preventing User Error)

-   **Critical Destructive Actions (e.g., Deleting a Course):** A high-friction confirmation modal will be employed. The user must type the name of the course to enable the final "Delete" button. The dialog will also clearly state that the course can be restored for 30 days, reducing user anxiety.
-   **Minor Destructive Actions (e.g., Deleting a single study topic):** A standard, low-friction modal with a simple "Are you sure?" question and "Delete" / "Cancel" buttons will be sufficient.
-   **Reversible Actions (e.g., Marking a task as "Missed"):** No confirmation will be required for actions that can be easily undone with a single click, prioritizing a low-effort user experience.

---

## 8. Responsive Design & Accessibility

### 8.1 Responsive Strategy

The application will be designed with a "desktop-first, but mobile-aware" responsive strategy, ensuring an optimal experience on the primary target devices (desktop, laptop, tablet) while considering future mobile use. The chosen "Zen Focus" layout with a persistent sidebar will adapt across breakpoints as follows:

-   **Desktop (> 1024px):** The full sidebar with text labels and icons will be visible, providing clear, at-a-glance navigation for users on larger screens.
-   **Tablet (768px - 1024px):** The sidebar will collapse into a narrow, icon-only "rail." This preserves horizontal screen real estate while keeping the primary navigation accessible. Hovering or tapping an icon can expand the full sidebar.
-   **Mobile (< 768px):** For smaller screens, the sidebar will be completely hidden by default. A standard "hamburger" menu icon will be present in the main header, which will toggle a slide-in navigation panel. The main content area will reflow to a single-column layout.

### 8.2 Accessibility Strategy

Accessibility is a core requirement to ensure the application is usable by everyone, including individuals with disabilities.

-   **Compliance Target:** The application will adhere to the **Web Content Accessibility Guidelines (WCAG) 2.1 at a Level AA** conformance. This is the global standard for web accessibility and is a legal requirement for many educational and public-facing applications.

-   **Key Technical Requirements:**
    -   **Keyboard Navigability:** All interactive elements, including buttons, links, form inputs, and custom components, must be fully operable via a keyboard alone.
    -   **Sufficient Color Contrast:** The final color palette will be tested to ensure it meets WCAG AA contrast ratios (4.5:1 for normal text, 3:1 for large text).
    -   **Screen Reader Compatibility:** The application will use semantic HTML5 and appropriate ARIA (Accessible Rich Internet Applications) attributes to ensure that it is fully understandable and navigable by screen reader software.
    -   **Visible Focus Indicators:** All interactive elements will have a clear and highly visible focus state (e.g., an outline or ring) to help keyboard users understand where they are on the page.
    -   **Form Accessibility:** All form inputs will be properly associated with labels, and error messages will be programmatically linked to their respective fields.

By integrating these requirements from the start, we will build a more robust, inclusive, and user-friendly application for all.

---

## 9. Implementation Guidance

### 9.1 Completion Summary

The UX Design Specification is now complete. Through a collaborative, iterative process, we have defined a comprehensive and user-centric vision for the AI-Powered Personal Study Planner. This document provides a complete blueprint for developers and designers to build an application that is not only functional but also intuitive, empathetic, and aligned with the core goal of helping students feel calm, confident, and in control of their academic lives.

**Key Decisions & Deliverables:**

-   **Design System:** **Shadcn UI** was chosen for its flexibility, modern aesthetic, and strong accessibility foundation.
-   **Visual Foundation:** The **"Calm & Focused"** color theme was provisionally selected to guide the visual identity, with an interactive `ux-color-themes.html` file provided for final confirmation.
-   **Design Direction:** After exploring six distinct layouts, the **"The Zen Focus"** direction (sidebar navigation, spacious, list-based) was selected as the foundational structure. An interactive `ux-design-directions.html` file showcases these options.
-   **Core User Journeys:** Critical flows, such as the **"Initial Plan Generation"**, have been designed as guided wizards to maximize clarity and user confidence.
-   **Custom Components:** Key custom components like the `StudyTaskCard` have been defined to support the core daily user experience.
-   **UX Patterns:** Consistent patterns for feedback, forms, and confirmations have been established to ensure a predictable and reliable user experience.
-   **Responsive & Accessible Strategy:** A clear strategy is in place to ensure the application is fully responsive and meets **WCAG 2.1 Level AA** accessibility standards.

This specification, along with its accompanying interactive HTML artifacts, provides the necessary guidance to move forward into high-fidelity design and front-end development with confidence and clarity.

---

## Appendix

### Related Documents

- Product Requirements: `{{prd_file}}`
- Product Brief: `{{brief_file}}`
- Brainstorming: `{{brainstorm_file}}`

### Core Interactive Deliverables

This UX Design Specification was created through visual collaboration:

- **Color Theme Visualizer**: {{color_themes_html}}
  - Interactive HTML showing all color theme options explored
  - Live UI component examples in each theme
  - Side-by-side comparison and semantic color usage

- **Design Direction Mockups**: {{design_directions_html}}
  - Interactive HTML with 6-8 complete design approaches
  - Full-screen mockups of key screens
  - Design philosophy and rationale for each direction

### Optional Enhancement Deliverables

- **Key Screens Showcase**: [key-screens-showcase.html](./key-screens-showcase.html)
  - An interactive HTML mockup applying all design decisions to visualize key screens like the Dashboard, Course Management, and Settings pages.

<!-- Additional deliverables added here by other workflows -->

### Next Steps & Follow-Up Workflows

This UX Design Specification can serve as input to:

- **Wireframe Generation Workflow** - Create detailed wireframes from user flows
- **Figma Design Workflow** - Generate Figma files via MCP integration
- **Interactive Prototype Workflow** - Build clickable HTML prototypes
- **Component Showcase Workflow** - Create interactive component library
- **AI Frontend Prompt Workflow** - Generate prompts for v0, Lovable, Bolt, etc.
- **Solution Architecture Workflow** - Define technical architecture with UX context

### Version History

| Date     | Version | Changes                         | Author |
| -------- | ------- | ------------------------------- | ------ |
| fredag 21. november 2025 | 1.0     | Initial UX Design Specification | BIP |

---

_This UX Design Specification was created through collaborative design facilitation, not template generation. All decisions were made with user input and are documented with rationale._
