# User Story: User Logout

- **Story Key:** `story-1-006`
- **Epic:** User Authentication & Onboarding
- **Title:** User Logout
- **Status:** ready-for-dev
- **Author:** BIP (Scrum Master)
- **Source Tech Spec:** `tech-spec-epic-1.md`

---

### 1. User Narrative

> **As a** logged-in user,
> **I want to** be able to log out of my account,
> **so that** I can securely end my session and protect my private information on a shared device.

---

### 2. Acceptance Criteria (AC)

1.  **Given** I am logged into the application,
    **Then** a "Logout" button or menu item must be clearly visible and accessible (e.g., within a user profile dropdown in the main navigation).

2.  **Given** I click the "Logout" button,
    **When** the action is triggered,
    **Then** the client-side `AuthManager.signOut()` function must be invoked.

3.  **Given** the `signOut` call to Supabase is successful,
    **Then** the user's session (including any JWT stored in the client) must be cleared.

4.  **Given** I have successfully logged out,
    **When** the application navigates,
    **Then** I must be redirected to the public home page or the login page.

5.  **Given** I have logged out,
    **Then** I must not be able to access any protected routes (e.g., `/dashboard`) without logging in again.

---

### 3. Technical Notes & Implementation Details

-   **Frontend Service:** All authentication logic must be handled through the `AuthManager` client-side service.
-   **API Call:** The implementation must use the `supabase.auth.signOut()` method from the `@supabase/supabase-js` library.
-   **UI Components:** The "Logout" button should be implemented using the standard **Shadcn UI** component library, likely as part of a `DropdownMenu` associated with a user avatar.
-   **State Management:** The global authentication state (managed by `zustand`) must be cleared to reflect that there is no longer an authenticated user. This will trigger UI changes, such as hiding protected navigation links.
-   **Routing:** The Next.js router must be used to handle the redirect to a public page. All protected routes must enforce authentication checks, which should now fail for the logged-out user.
-   **Error Handling:** While errors during logout are rare, the UI should not crash. If an error occurs, the state should ideally be reset to a logged-out state on the client-side regardless, to ensure the user is not "stuck" in a logged-in UI.

---

### 4. Traceability

-   **Architecture:** `solution-architecture.md` (Sec 3: Supabase Auth - JWT Management)
-   **UX Design:** `ux-design-specification.md` (Consistent placement of user controls in navigation)
-   **Technical Spec:** `tech-spec-epic-1.md` (Sec: APIs and Interfaces - `signOut`, AC6)
---

### Dev Agent Record
- **Context Reference:** `docs/sprint-artifacts/story-1-006.context.xml`
