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

# User API Documentation

## Register New User

[Previous register documentation remains the same...]

## Login User

`POST /users/login`

Authenticates a user and returns a token.

### Request Body

````json
{
  "email": "john@email.com", // Required, valid email
  "password": "secret123"

  // Required, min 6 characters
## Logout User

`POST /users/logout`

Logs out the authenticated user by invalidating the token.

### Request Headers

```json
{
  "Authorization": "Bearer jwt_token_here" // Required, valid JWT token
}
````

Responses
Success Response
Code: 200 OK

{
"message": "Successfully logged out"
}

Error Response
Code: 401 Unauthorized

{
"message": "Invalid token or token expired"
}

Security Features
Token is invalidated on the server side
JWT token expires in 24 hours
}

```

Validation Rules
email: Required, must be valid email format
password: Required, minimum 6 characters
Responses
Success Response
Code: 200 OK

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

Error Responses
Code: 401 Unauthorized

{
"message": "Invalid email or password"
}

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
Password comparison using bcrypt
JWT token expires in 24 hours
Password is excluded from response
```

Captain Endpoints
Register New Captain
POST /captains/register

Creates a new captain account and returns an authentication token.

Request Body

{
"fullname": {
"firstname": "Jane", // Required, min 3 characters
"lastname": "Smith" // Optional, min 3 characters if provided
},
"email": "jane@example.com", // Required, valid email, min 5 characters, unique
"password": "secret123", // Required, min 6 characters
"vehicle": {
"color": "Red", // Required, min 3 characters
"plate": "ABC1234", // Required, min 3 characters
"capacity": 4, // Required, minimum 1
"vehicleType": "car" // Required, one of ["car", "motorcycle", "auto"]
}
}

Validation Rules
fullname.firstname: Required, minimum 3 characters
fullname.lastname: Optional, minimum 3 characters if provided
email: Required, valid email format, minimum 5 characters, unique
password: Required, minimum 6 characters
vehicle.color: Required, minimum 3 characters
vehicle.plate: Required, minimum 3 characters
vehicle.capacity: Required, numeric, minimum 1
vehicle.vehicleType: Required, one of "car", "motorcycle", "auto"

Responses

Success

Code: 201 Created

Content:

{
"token": "jwt_token_here",
"captain": {
"\_id": "captain_id",
"fullname": {
"firstname": "Jane",
"lastname": "Smith"
},
"email": "jane@example.com",
"status": "inactive",
"vehicle": {
"color": "Red",
"plate": "ABC1234",
"capacity": 4,
"vehicleType": "car"
}
}
}

Error

Code: 400 Bad Request

Content:

{
"errors": [
{
"msg": "Invalid vehicle type",
"param": "vehicle.vehicleType",
"location": "body"
}
]
}

Model Structure Description
The Captain model has the following structure:

fullname (object)
firstname (string): Required, minimum 3 characters
lastname (string): Optional, minimum 3 characters
email (string): Required, unique, minimum 5 characters
password (string): Required, hashed using bcrypt
socketId (string): Optional, used for real-time communication
status (string): Enum of ["active", "inactive"], default is "inactive"
vehicle (object)
color (string): Required, minimum 3 characters
plate (string): Required, minimum 3 characters
capacity (number): Required, minimum value of 1
vehicleType (string): Required, one of ["car", "motorcycle", "auto"]
location (object)
latitude (number): Optional
longitude (number): Optional

Security Features
Password is hashed using bcrypt (10 rounds)
JWT token expires in 24 hours
Password is excluded from captain object in responses
Notes
Email addresses must be unique in the system
Vehicle information is required for captains
status indicates the captain's availability
Token is required for authenticated endpoints
socketId is used for real-time communication
