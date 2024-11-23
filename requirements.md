# User Authentication
## Functional Requirements
 * Allow users to register as Guests or Hosts.
 * Support secure login with JWT-based authentication.
 * Provide endpoints for password reset and email verification.
 * Enforce strong password policies.

## Technical Requirements
### API Endpoints

`Post /api/auth/register`

### Input:

        `{
  "email": "user@example.com",
  "password": "SecurePassword123",
  "role": "guest"
}`

### Output(200 OK):

        `{
  "message": "User registered successfully",
  "userId": 1234
}`

### Validation Rules:
    * Email must follow a valid email format.
    * Password must be at least 8 characters long, include one uppercase letter, one digit, and one special character.
    * Role must be either 'guest' or 'host'.

### Performance Criteria:
    * Registration request should be processed within 200ms under normal load.

`POST /api/auth/login`

### Input:

        '{
  "email": "user@example.com",
  "password": "SecurePassword123"
}`

### Output(200 OK):
        `{
  "token": "eyJhbGciOiJIUzI1NiIsInR5..."
}`

`POST /api/auth/reset-password`

### Input:

        `{
  "email": "user@example.com"
}`

### Output(200 OK):

        `{
  "message": "Password reset email sent."
}`


# Property Management
## Functional Requirements
  * Hosts can add, edit, or delte property listings.
  * Each property must have details like title, description, location, price, and availability.
  * Hosts can upload multiple images per property.
  * Properties must support filtering by price, location, and availability.

## Technical Requirements
### API Endpoints

`POST /api/properties`

### Input:

        `{
  "title": "Cozy Apartment",
  "description": "A comfortable apartment in the city center.",
  "location": "Nairobi",
  "price_per_night": 50,
  "amenities": ["WiFi", "Kitchen"],
  "availability": {
    "start_date": "2024-01-01",
    "end_date": "2024-12-31"
  }
}`

### Output(200 OK):

        `{
  "message": "Property added successfully",
  "propertyId": 5678
}`

### Validation Rules:
  * Title must not exceed 100 characters.
  * Price must be a positive integer.
  * Availability dates must be valid (start date earlier than end date).

`PATCH /api/properties/{id}`

### Input:(Partial updates allowed)
        `{
  "price_per_night": 60,
  "availability": {
    "start_date": "2024-02-01"
  }
}`

`GET /api/properties`

    ### Querty Parameters:

        - location: Filter by location.
        - price_range: Filter by price range.
        - availability: Filter by data range.

# Booking System
## Functional Requirements
    * Guests can search for properties based on filters
    * Guests can book available properties.
    * Hosts can approve or reject booking requests.
    * Guests can cancel bookings before a specified deadline.

## Technical Requirements
### API Endpoints

`POST /api/bookings`

### Input:
        `{
  "propertyId": 5678,
  "guestId": 1234,
  "check_in_date": "2024-06-01",
  "check_out_date": "2024-06-10"
}`

### Output(200 OK):
        `{
  "message": "Booking request submitted",
  "bookingId": 9012
}`

### Validation Rules:
    * Property must be available for the selected dates.
    * Check-in date must be earlier than check-out date.
    * Guest cannot book their own property.

`GET /api/bookings/{id}`

### Output(200 OK):
        `{
  "bookingId": 9012,
  "property": {
    "title": "Cozy Apartment",
    "location": "Nairobi"
  },
  "status": "Pending"
}`

`PATCH /api/bookings/{id}`(For Hosts to Approve/Reject)

### Input:
        `{
  "status": "approved"
}`
