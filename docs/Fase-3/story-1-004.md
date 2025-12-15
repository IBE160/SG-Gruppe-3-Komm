# User Story: Secure User Login

- **Story Key:** `story-1-004`
- **Epic:** User Authentication & Onboarding
- **Title:** Secure User Login
- **Status:** ready-for-dev
- **Author:** BIP (Scrum Master)
- **Source Tech Spec:** `tech-spec-epic-1.md`

---

### 1. User Narrative

> **As a** registered and verified user,
> **I want to** log in to my account securely using my email and password,
> **so that** I can access my personalized dashboard and study plans.

---

### 2. Acceptance Criteria (AC)

1.  **Given** I am on the application's login page,
    **Then** the UI must display a form with fields for "Email" and "Password," and a "Log In" button.

2.  **Given** I have entered my correct credentials for a verified account,
    **When** I click the "Log In" button,
    **Then** the client-side `AuthManager.signIn(credentials)` function must be invoked.

3.  **Given** the `signIn` call to Supabase is successful,
    **Then** the application must receive a valid JWT session, which is stored securely in the client.

4.  **Given** I have successfully logged in,
    **When** the application navigates,
    **Then** I must be redirected to my personal dashboard page.

5.  **Given** I attempt to log in with incorrect credentials,
    **Then** the login must fail, and a clear error message (e.g., "Invalid login credentials") must be displayed on the login form.

6.  **Given** I attempt to log in with a correct password but an unverified email address,
    **Then** the login must fail, and a message must be displayed informing me that my email needs to be verified, as per `story-1-002` and `story-1-003`.

---

### 3. Technical Notes & Implementation Details

-   **Frontend Service:** All authentication logic must be handled through the `AuthManager` client-side service.
-   **API Call:** The implementation must use the `supabase.auth.signInWithPassword()` method from the `@supabase/supabase-js` library.
-   **UI Components:** The login form, its inputs, and buttons must be built using the standard **Shadcn UI** component library. Form validation (`onBlur`, floating labels) should follow the UX specification.
-   **State Management:** The global authentication state (managed by `zustand`) must be updated with the user's session information upon successful login.
-   **Routing:** The Next.js router must be used to handle the redirect to the dashboard upon successful login. Protected routes (like the dashboard) must be inaccessible to unauthenticated users.
-   **Error Handling:** The UI must gracefully handle and display specific error messages for invalid credentials and other login failures.

---

### 4. Traceability

-   **Architecture:** `solution-architecture.md` (Sec 3: Supabase Auth, Component Diagram)
-   **UX Design:** `ux-design-specification.md` (Sec 7: Form Patterns, Error Feedback)
-   **Technical Spec:** `tech-spec-epic-1.md` (Sec: APIs and Interfaces - `signIn`, AC4)
---

### Dev Agent Record
- **Context Reference:** docs/sprint-artifacts/story-1-004.context.xml