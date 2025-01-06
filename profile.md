### **User Profile API Documentation**

This document explains the **GET** and **PATCH** endpoints for managing user profiles in the system. User profiles are created during registration with limited details. Additional fields like `address`, `phoneNumber`, and `gender` are updated later using the **PATCH** endpoint. Users can view their complete profile with the **GET** endpoint.

---

### **Base URL**
`https://one00daysofcoding.onrender.com`

---

### **1. GET /profile**

#### **Description**
Retrieve the full profile of the authenticated user.

#### **Endpoint**
`GET /user/v1/profile/`

#### **Headers**
- **Authorization**: `Bearer <token>` (Required)

#### **Response**
- **Success (200)**
  ```json
  {
    "status": "success",
    "data": {
      "id": "userId123",
      "firstname": "John",
      "lastname": "Doe",
      "email": "john.doe@example.com",
      "phoneNumber": "1234567890",
      "address": "123 Main St",
      "gender": "male"
    }
  }
  ```
- **Error (401 Unauthorized)**
  ```json
  {
    "status": "failed",
    "message": "Unauthorized access. No valid user found",
    "statusCode": 401
  }
  ```

---

### **2. PATCH /user/v1/profile//:userId**

#### **Description**
Update the authenticated user's profile. This endpoint allows updating fields like `firstname`, `lastname`, `phoneNumber`, `email`, `address`, and `gender`. 

#### **Endpoint**
`PATCH /profile/:userId`

#### **Headers**
- **Authorization**: `Bearer <token>` (Required)

#### **Body Parameters**
| Field         | Type     | Required | Description                              |
|---------------|----------|----------|------------------------------------------|
| firstname     | string   | Optional | The user's first name.                  |
| lastname      | string   | Optional | The user's last name.                   |
| phoneNumber   | string   | Optional | The user's phone number.                |
| email         | string   | Optional | The user's email address.               |
| address       | string   | Optional | The user's address.                     |
| gender        | string   | Optional | The user's gender (`male` or `female`). |

#### **Validation Rules**
- **Gender** must be either `male` or `female`.
- Fields not in the allowed list (`firstname`, `lastname`, `phoneNumber`, `email`, `address`, `gender`) are rejected with an error.

#### **Response**
- **Success (200)**
  ```json
  {
    "status": "success",
    "message": "Profile updated successfully",
    "statusCode": 200
  }
  ```
- **Error (400 Bad Request)**
  - Invalid fields:
    ```json
    {
      "status": "failed",
      "message": "Invalid fields: fieldName",
      "statusCode": 400
    }
    ```
  - Invalid gender:
    ```json
    {
      "status": "Validation failed",
      "message": {
        "field": "gender",
        "details": "invalidGenderValue is not a valid option. Please enter either 'male' or 'female' as the gender"
      }
    }
    ```
- **Error (403 Forbidden)**
  ```json
  {
    "message": "Access denied"
  }
  ```

- **Error (404 Not Found)**
  ```json
  {
    "status": "failed",
    "message": "User not found",
    "statusCode": 404
  }
  ```

---

### **Authentication & Authorization**
- Both endpoints require authentication using the `verifyUserAccess` middleware to ensure only authenticated users can access their profiles.
- The **PATCH** endpoint also checks that the `userId` in the URL matches the authenticated user's ID.

---

### **Usage Notes**
1. **GET**: Fetch all available details of the authenticated user, including updated fields.
2. **PATCH**: Only updates provided fields; unmodified fields retain their original values.
3. Any invalid or unexpected field in the request body for **PATCH** will result in a validation error.

For further clarification, feel free to reach out!
