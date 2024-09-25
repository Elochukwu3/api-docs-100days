

---

# 100daysOfCoding API Documentation

## Base URL
The base URL for all project endpoints is:
```
https://100daysofcoding-production.up.railway.app/
```
## Auth Section
Endpoint:
```
https://100daysofcoding-production.up.railway.app/auth/v1
```
API Key:
```
a4f5c6d7e8a9b10c11d12e13f14b15c16d17e18f19a20b21c22d23e24f25g26
```

## Authentication Endpoints

### 1. Register User
- **Endpoint**: `/register`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "firstname": "string",
    "lastname": "string",
    "state": "string",
    "email": "string",
    "password": "string",
    "confirmPassword:"string"
  }
  ```
- **Responses**:
  - **201 Created**: User registered successfully.
  - **400 Bad Request**: Input validation error.
  - **409 Conflict**: User with the provided email already exists.

### 2. Verify OTP
- **Endpoint**: `/verify-otp`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "otp": "string"
  }
  ```
- **Responses**:
  - **200 OK**: OTP verified successfully.
  - **400 Bad Request**: OTP does not match or has expired.

### 3. Login User
- **Endpoint**: `/login`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "email": "string",
    "password": "string"
  }
  ```
- **Responses**:
  - **200 OK**: Login successful, returns user info and tokens.
  - **401 Unauthorized**: Invalid credentials.

### 4. Refresh Token
- **Endpoint**: `/refresh-token`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "refreshToken": "string"
  }
  ```
- **Responses**:
  - **200 OK**: New access token returned.
  - **403 Forbidden**: Invalid or expired refresh token.

### 5. Change Password
- **Endpoint**: `/change-password`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "oldPassword": "string",
    "newPassword": "string"
  }
  ```
- **Responses**:
  - **200 OK**: Password changed successfully.
  - **401 Unauthorized**: Old password is incorrect.

### 6. Request Password Reset
- **Endpoint**: `/request-password-reset`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "email": "string"
  }
  ```
- **Responses**:
  - **200 OK**: Reset email sent successfully.
  - **404 Not Found**: User not found.

### 7. Verify Reset OTP
- **Endpoint**: `/verify-reset-otp`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "otp": "string"
  }
  ```
- **Responses**:
  - **200 OK**: OTP verified for password reset.
  - **400 Bad Request**: OTP is invalid or has expired.

### 8. Reset Password
- **Endpoint**: `/reset-password`
- **Method**: `POST`
- **Request Body**:
  ```json
  {
    "newPassword": "string"
  }
  ```
- **Responses**:
  - **200 OK**: Password reset successfully.
  - **400 Bad Request**: Invalid request.

## Middleware
- **CORS**: Configured to allow specific origins.
- **Session Handling**: Using MongoDB to store sessions.

## Logging
- **Morgan**: Used for logging HTTP requests and errors.

## Error Handling
- Custom error handler for managing application errors.

---
