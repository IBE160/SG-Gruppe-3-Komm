# Epic Technical Specification: User Authentication & Onboarding

Date: 2025-12-08
Author: BIP
Epic ID: 1
Status: Draft

---

## Overview

This document provides the technical specification for Epic 1: User Authentication & Onboarding. The primary goal is to implement a secure and user-friendly system for users to create accounts, log in, and manage their credentials. This epic is foundational to the application, as it establishes the user's identity and ensures that all their data is stored securely and is accessible only to them. The implementation will leverage Supabase for its robust, built-in authentication services, including user registration, login, and password recovery, aligning with our strategy to use managed services to accelerate development.

## Objectives and Scope

**In-Scope:**
-   New user registration with email and password.
-   Post-registration email verification.
-   Ability for users to resend the verification email.
-   Secure login for registered and verified users.
-   "Forgot Password" functionality with an email-based reset link.
-   User logout capability.

**Out-of-Scope:**
-   Social login (e.g., Google, GitHub).
-   Single Sign-On (SSO) integrations.
-   Two-Factor Authentication (2FA).
-   User profile management (e.g., changing email, password from a settings page).

## System Architecture Alignment

This epic directly implements a core component of the solution architecture. It will utilize **Supabase Auth** as the primary authentication provider, as specified in the architecture document.

-   **Data Model:** The `public.users` table will be used to store basic user profile information, linked directly to the `auth.users` table managed by Supabase. Every new registration will create an entry in both tables.
-   **Security:** All authentication logic will be handled by Supabase's GoTrue service, which manages secure password hashing, JWT generation, and email delivery for verification and resets. Row Level Security (RLS) policies, as defined in the architecture, will be enforced on all tables, using the `auth.uid()` from the JWT to ensure users can only access their own data.
-   **Frontend:** The Next.js frontend will interact with Supabase via the official `supabase-js` client library, which provides convenient methods for all authentication flows (`signUp`, `signInWithPassword`, `signOut`, etc.).

## Detailed Design

### Services and Modules

| Service/Module | Responsibility | Owner |
| :--- | :--- | :--- |
| **Next.js Frontend** | Handles all UI for authentication (registration, login, forgot password forms). | Frontend Team |
| **Supabase Auth** | Manages user creation, credential verification, session management (JWTs), and email sending. | Supabase (Managed) |
| **`AuthManager` (Client-side)** | A dedicated module/service in the Next.js app to wrap the `supabase-js` client, manage auth state (e.g., via Zustand), and handle redirects. | Frontend Team |

### Data Models and Contracts

The data model for this epic is defined in the solution architecture. It primarily concerns the `users` table.

```sql
-- Users Table: Stores user information, linked to Supabase Auth.
CREATE TABLE public.users (
    id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
    full_name TEXT,
    created_at TIMESTAMPTZ DEFAULT NOW()
);
```
-   **Contract:** Any operation that creates a user via `Supabase Auth` will result in a corresponding entry in `auth.users`, which in turn allows for the creation of an entry in `public.users`. The `id` field serves as a foreign key, ensuring integrity.

### APIs and Interfaces

Interaction will be primarily with the `supabase-js` client library. The `AuthManager` module will expose methods that wrap these calls.

```typescript
// Example interface for the AuthManager service
interface IAuthManager {
  signUp(credentials: { email, password }): Promise<{ user, error }>;
  signIn(credentials: { email, password }): Promise<{ session, error }>;
  signOut(): Promise<{ error }>;
  sendPasswordReset(email: string): Promise<{ error }>;
  resendVerification(email: string): Promise<{ error }>;
  onAuthStateChange(callback: (session: Session | null) => void): Subscription;
}
```

### Workflows and Sequencing

1.  **New User Registration:**
    -   User fills out and submits the registration form in the Next.js app.
    -   The `AuthManager` calls `supabase.auth.signUp({ email, password })`.
    -   Supabase creates the user in the `auth.users` table (with `confirmed_at` as null) and sends a verification email.
    -   The frontend displays a "Please verify your email" message.

2.  **User Login:**
    -   User submits the login form.
    -   `AuthManager` calls `supabase.auth.signInWithPassword({ email, password })`.
    -   Supabase verifies credentials and returns a JWT session.
    -   `AuthManager` stores the session and redirects the user to the dashboard. The JWT will be used for all subsequent authenticated requests.

3.  **Password Reset:**
    -   User enters their email in the "Forgot Password" form.
    -   `AuthManager` calls `supabase.auth.resetPasswordForEmail(email)`.
    -   Supabase sends a password reset link to the user's email.
    -   The user clicks the link, is taken to a reset page, and provides a new password. Supabase securely updates the user's credentials.

## Non-Functional Requirements

### Performance

-   Authentication-related actions (login, registration) should provide feedback to the user (e.g., loading indicator) and complete within 3 seconds on a standard broadband connection, as per the PRD.
-   The client-side `AuthManager` should load and initialize asynchronously so as not to block the initial page render.

### Security

-   All authentication will be managed by Supabase Auth, leveraging its secure handling of passwords (hashed and salted) and other credentials.
-   User sessions will be managed via JWTs issued by Supabase. The frontend will store the JWT securely and send it in the Authorization header for all API requests.
-   Email verification is mandatory. Users cannot log in until their email is verified, preventing sign-ups with fraudulent email addresses.
-   Password reset links will be single-use and expire after a short period (Supabase default is 24 hours).
-   Row Level Security (RLS) must be enabled on all tables containing user data, with policies that restrict access to data owned by the authenticated user (`auth.uid()`).

### Reliability/Availability

-   The authentication service relies on Supabase's availability. The system should handle potential Supabase outages gracefully by displaying an informative error message to the user.
-   Email delivery for verification and password resets depends on the underlying email provider configured in Supabase. The system should include a "Resend Verification" feature as a fallback.

### Observability

-   All successful and failed login attempts should be logged for security monitoring purposes (handled by Supabase Auth logs).
-   The frontend should log any errors encountered during authentication flows to a monitoring service (e.g., Sentry, LogRocket) to aid in debugging.

## Dependencies and Integrations

| Dependency | Type | Purpose |
| :--- | :--- | :--- |
| **`@supabase/supabase-js`** | NPM Package | Official client library for interacting with Supabase services (Auth, Database). |
| **`zustand`** | NPM Package | For managing the global authentication state (e.g., current user, session). |
| **Shadcn UI** | Component Library | Provides the UI components for building forms (Input, Button) and modals. |

## Acceptance Criteria (Authoritative)

1.  **AC1:** A new user can create an account using a valid email and a password.
2.  **AC2:** After registering, the user receives an email with a verification link.
3.  **AC3:** A user who has not verified their email is shown an option to resend the verification email.
4.  **AC4:** A registered and verified user can log in with their email and password.
5.  **AC5:** An unauthenticated user cannot access protected routes (e.g., the dashboard).
6.  **AC6:** A logged-in user can successfully log out, terminating their session.
7.  **AC7:** A user who has forgotten their password can request a password reset link via email.
8.  **AC8:** Clicking the reset link allows the user to set a new password.

## Traceability Mapping

| AC | Spec Section(s) | Component(s)/API(s) | Test Idea |
| :--- | :--- | :--- | :--- |
| **AC1** | APIs and Interfaces | `AuthManager.signUp` | Unit test `signUp` call; Integration test registration form. |
| **AC2** | Workflows and Sequencing | Supabase Email Template | E2E test: register and check email inbox (mocked). |
| **AC3** | APIs and Interfaces | `AuthManager.resendVerification` | Integration test the "Resend" button functionality. |
| **AC4** | APIs and Interfaces | `AuthManager.signIn` | Unit test `signIn` call; Integration test login form. |
| **AC5** | System Arch. Alignment | Next.js Middleware/Router | E2E test: try to access `/dashboard` when not logged in. |
| **AC6** | APIs and Interfaces | `AuthManager.signOut` | Integration test the "Logout" button. |
| **AC7** | APIs and Interfaces | `AuthManager.sendPasswordReset` | Integration test the "Forgot Password" form. |
| **AC8** | Workflows and Sequencing | Supabase Reset Page | E2E test: complete the password reset flow. |

## Risks, Assumptions, Open Questions

-   **Risk:** Email deliverability issues (verification/reset emails being marked as spam).
    -   **Mitigation:** Ensure Supabase is configured with a reputable email provider (e.g., SendGrid, SES) if the built-in provider is insufficient.
-   **Assumption:** The default Supabase email templates are sufficient for the MVP.
-   **Question:** What is the desired session length for a user?
    -   **Next Step:** Assume Supabase default (1 hour, refreshed automatically) for now. Revisit if user feedback indicates it's too short/long.

## Test Strategy Summary

-   **Unit Tests:** Create unit tests for the `AuthManager` service to mock `supabase-js` calls and verify correct handling of responses and errors.
-   **Component Tests:** Test the Registration, Login, and Forgot Password forms in isolation to ensure correct state handling and validation.
-   **Integration/E2E Tests:** Use a testing framework like Cypress or Playwright to simulate full user flows:
    -   A user signs up, receives a (mocked) verification email, clicks the link, and logs in.
    -   A logged-in user logs out.
    -   A user requests a password reset and completes the flow.
-   **Security Testing:** Verify that RLS policies are effective by writing tests (e.g., using Supabase's test helpers) that attempt to access another user's data and assert that the request fails.
