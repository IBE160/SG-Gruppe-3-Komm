# User Story: Password Recovery (Forgot Password)

- **Story Key:** `story-1-005`
- **Epic:** User Authentication & Onboarding
- **Title:** Password Recovery (Forgot Password)
- **Status:** ready-for-dev
- **Author:** BIP (Scrum Master)
- **Source Tech Spec:** `tech-spec-epic-1.md`

---

### 1. User Narrative

> **As a** user who has forgotten my password,
> **I want to** request a password reset link to be sent to my email address,
> **so that** I can regain access to my account by setting a new password.

---

### 2. Acceptance Criteria (AC)

1.  **Given** I am on the login page,
    **Then** a "Forgot Password?" link must be clearly visible.

2.  **Given** I click the "Forgot Password?" link,
    **When** the UI updates,
    **Then** I must be presented with a form asking for my registered email address.

3.  **Given** I enter my registered email address and submit the form,
    **When** the action is triggered,
    **Then** the client-side `AuthManager.sendPasswordReset(email)` function must be invoked.

4.  **Given** the `sendPasswordReset` call to Supabase is successful,
    **When** I check my email inbox,
    **Then** I must find an email from the application containing a unique, single-use password reset link.

5.  **Given** I click the password reset link in the email,
    **Then** I must be redirected to a secure page within the application dedicated to setting a new password.

6.  **Given** I am on the password reset page,
    **When** I enter and confirm a new password that meets the application's security requirements,
    **Then** my account credentials in Supabase must be securely updated with the new password.

7.  **Given** my password has been successfully reset,
    **Then** I must be redirected to the login page with a success notification (e.g., a toast) stating, "Your password has been updated. Please log in."

---

### 3. Technical Notes & Implementation Details

-   **Frontend Service:** All authentication logic must be handled through the `AuthManager` client-side service.
-   **API Call:** The "request reset" functionality must use the `supabase.auth.resetPasswordForEmail()` method. The password update will be handled by Supabase's built-in UI/flow when the user clicks the link.
-   **UI Components:** The forms and inputs for requesting the reset and setting the new password must use the standard **Shadcn UI** component library.
-   **Routing:**
    -   A new route (e.g., `/auth/forgot-password`) should be created for the form that collects the user's email.
    -   A new route (e.g., `/auth/update-password`) must be created to handle the password update. This page will be accessed via the link from the email and will process the reset token provided by Supabase in the URL.
-   **State Management:** The UI should provide clear feedback during the process. For example, the "Send Reset Link" button should be disabled with a loading spinner while the API call is in progress.
-   **Error Handling:** The UI must display a clear error message if the password reset request fails (e.g., email not found, rate limiting). For security reasons, it is often best practice to show a generic success message ("If an account with that email exists, a reset link has been sent") to prevent user enumeration. This should be confirmed as the desired behavior.

---

### 4. Traceability

-   **Architecture:** `solution-architecture.md` (Sec 3: Supabase Auth)
-   **UX Design:** `ux-design-specification.md` (Sec 7: Form Patterns, Feedback Patterns)
-   **Technical Spec:** `tech-spec-epic-1.md` (Sec: APIs and Interfaces - `sendPasswordReset`, AC7, AC8)
---

### Dev Agent Record
- **Context Reference:** `docs/sprint-artifacts/story-1-005.context.xml`
