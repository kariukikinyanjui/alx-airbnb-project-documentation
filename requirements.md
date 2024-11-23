# User Authentication
## Functional Requirements
 * Allow users to register as Guests or Hosts.
 * Support secure login with JWT-based authentication.
 * Provide endpoints for password reset and email verification.
 * Enforce strong password policies.

## Technical Requirements
### API Endpoints

`Post /api/auth/register`
    * Input
        `{
  "email": "user@example.com",
  "password": "SecurePassword123",
  "role": "guest"
}`
