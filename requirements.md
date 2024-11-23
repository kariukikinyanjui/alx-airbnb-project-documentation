# 1. User Authentication
## Funcational Requirements
 * Allow users to register as Guests or Hosts.
 * Support secure login with JWT-based authentication.
 * Provide endpoints for password reset and email verification.
 * Enforce strong password policies.

## Technical Requirements
### API Endpoints
    1. POST /api/auth/register
        ### Input:
            ```{
  "email": "user@example.com",
  "password": "SecurePassword123",
  "role": "guest"
}```

        ### Output(201 Created):
            ```{
  "message": "User registered successfully",
  "userId": 1234
}```

### Validation Rules:
    - Email must follow a valid email format.
    - Password must be at least 8 characters long, include one uppercase letter, one digit, and one special character.
    - Role must be either 'guest' or 'host'.

### Performance Criteria:
    - Registration request should be processed within 200ms under normal load

    2. POST /api/auth/reset-password
        ### Input:
            ```{
  "email": "user@example.com",
  "password": "SecurePassword123"
}```

        ### Output(201 Created):
            ```{
  "token": "eyJhbGciOiJIUzI1NiIsInR5..."
}```

    3. POST /api/auth/reset-password
        ### Input:
            ```{
  "email": "user@example.com"
}```

        ### Output(201 Created):
            ```
                {
  "message": "Password reset email sent."
}
```

