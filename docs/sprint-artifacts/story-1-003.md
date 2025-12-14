# User Story: Resend Verification Email

- **Story Key:** `story-1-003`
- **Epic:** User Authentication & Onboarding
- **Title:** Resend Verification Email
- **Status:** ready-for-dev
- **Author:** BIP (Scrum Master)
- **Source Tech Spec:** `tech-spec-epic-1.md`

---

### 1. User Narrative

> **As a** user who has not yet verified their email,
> **I want to** be able to request a new verification email,
> **so that** I can complete my account registration if the original email was lost or delayed.

---

### 2. Acceptance Criteria (AC)

1.  **Given** I am on a page that informs me my email is unverified (e.g., after a failed login attempt),
    **Then** a "Resend Verification Email" button or link must be clearly visible.

2.  **Given** I click the "Resend Verification Email" button,
    **When** the action is triggered,
    **Then** the client-side `AuthManager.resendVerification(email)` function must be invoked with my email address.

3.  **Given** the `resendVerification` call to Supabase is successful,
    **When** I check my email inbox,
    **Then** I must find a new verification email from the application.

4.  **Given** I have requested to resend the verification email,
    **When** the UI updates,
    **Then** a non-intrusive toast notification must appear, stating "A new verification email has been sent."
    -   *UX Spec Ref:* The toast should appear for 3-4 seconds before fading automatically.

5.  **Given** I click the link in the newly received email,
    **Then** my account must be successfully verified, as per the flow defined in `story-1-002`.

---

### 3. Technical Notes & Implementation Details

-   **Frontend Service:** All authentication logic must be handled through the `AuthManager` client-side service.
-   **API Call:** The implementation must use the `supabase.auth.resend()` method (or equivalent, check latest `@supabase/supabase-js` v2 docs for the exact method, which may be `resend({ type: 'signup', email })`) wrapped in our `AuthManager`.
-   **UI Components:** The button and feedback notifications must be built using the standard **Shadcn UI** component library.
-   **State Management:** The UI should provide clear feedback during the resend process. The "Resend" button should be disabled and show a loading spinner while the API call is in progress to prevent multiple submissions.
-   **Error Handling:** A separate story will cover detailed error handling (e.g., rate limiting). However, the UI should display a clear error toast if the resend request fails for any reason.
-   **Dependencies:** This story is dependent on the registration flow (`story-1-001`) and the existence of a UI state for unverified users (e.g., from `story-1-002`'s login-prevention logic).

---

### 4. Traceability

-   **Architecture:** `solution-architecture.md` (Sec 3: Supabase Auth)
-   **UX Design:** `ux-design-specification.md` (Sec 7: Feedback Patterns)
-   **Technical Spec:** `tech-spec-epic-1.md` (Sec: APIs and Interfaces - `resendVerification`, AC3)
---

### Dev Agent Record
- **Context Reference:** docs/sprint-artifacts/story-1-003.context.xml