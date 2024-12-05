# User Registration API Documentation

## Register New User

`POST /users/register`

Creates a new user account and returns an authentication token.

### Request Body

```json
{
  "fullname": {
    "firstname": "John", // Required, min 3 characters
    "lastname": "Doe" // Optional, min 3 characters if provided
  },
  "email": "john@email.com", // Required, min 5 characters, unique
  "password": "secret123" // Required, min 6 characters
}
```

Validation Rules
fullname.firstname: Required, minimum 3 characters
fullname.lastname: Optional, minimum 3 characters if provided
email: Required, must be valid email format, minimum 5 characters, must be unique
password: Required, minimum 6 characters

Responses
Success Response
Code: 201 Created

{
"token": "jwt_token_here",
"user": {
"\_id": "user_id",
"fullname": {
"firstname": "John",
"lastname": "Doe"
},
"email": "john@email.com"
}
}

Error Response
Code: 400 Bad Request

{
"errors": [
{
"msg": "Invalid email",
"param": "email",
"location": "body"
}
]
}

Security Features
Password is hashed using bcrypt (10 rounds)
JWT token expires in 24 hours
Password is excluded from user object in responses
Notes
Email addresses must be unique in the system
Token is required for authenticated endpoints
Socket ID field is optional and used for real-time communication
