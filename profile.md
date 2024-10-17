
### User Profile API Documentation

#### Base URL
```
/api/v1/profile
```

### Endpoints

#### 1. **Get User Profile**
- **Endpoint**: `/api/v1/profile/`
- **Method**: `GET`
- **Description**: Retrieve the profile information of the authenticated user.
- **Middleware**: 
  - `verifyUserAccess`: Ensures the user is authenticated.
  - `verifyRoles(Roles.Admin)`: Only users with admin roles can access this route.
  
- **Response**:
  - **Success (200)**: Returns the user profile information.
    - **Example Response**:
    ```json
    {
      "id": "123456789",
      "name": "John Doe",
      "email": "johndoe@example.com",
      "role": "User",
      "createdAt": "2024-10-18T00:00:00Z",
      "updatedAt": "2024-10-18T00:00:00Z"
    }
    ```

- **Error (401)**: Unauthorized if the user is not authenticated.
- **Error (403)**: Forbidden if the user does not have the admin role.

#### 2. **Get User Profile by User ID**
- **Endpoint**: `/api/v1/profile/:userId`
- **Method**: `GET`
- **Description**: Retrieve the profile information for a specific user by user ID.
- **Parameters**: 
  - `userId` (path parameter): The ID of the user whose profile is being retrieved.
  
- **Middleware**: 
  - `verifyUserAccess`: Ensures the user is authenticated.
  
- **Response**:
  - **Success (200)**: Returns the user profile information.
    - **Example Response**:
    ```json
    {
      "id": "987654321",
      "name": "Jane Smith",
      "email": "janesmith@example.com",
      "role": "User",
      "createdAt": "2024-10-18T00:00:00Z",
      "updatedAt": "2024-10-18T00:00:00Z"
    }
    ```

- **Error (404)**: Not Found if the user with the specified ID does not exist.
- **Error (401)**: Unauthorized if the user is not authenticated.

#### 3. **Update User Profile**
- **Endpoint**: `/api/v1/profile/:userId`
- **Method**: `PATCH`
- **Description**: Update the profile information of a specific user by user ID.
- **Parameters**:
  - `userId` (path parameter): The ID of the user whose profile is being updated.
  
- **Request Body**: 
  - Should contain the fields to be updated.
  - **Example Request Body**:
  ```json
  {
    "name": "Jane Doe",
    "email": "janedoe@example.com"
  }
  ```

- **Middleware**: 
  - `verifyUserAccess`: Ensures the user is authenticated.

- **Response**:
  - **Success (200)**: Returns the updated user profile information.
    - **Example Response**:
    ```json
    {
      "id": "987654321",
      "name": "Jane Doe",
      "email": "janedoe@example.com",
      "role": "User",
      "createdAt": "2024-10-18T00:00:00Z",
      "updatedAt": "2024-10-18T00:00:00Z"
    }
    ```

- **Error (400)**: Bad Request if the provided data is invalid.
- **Error (404)**: Not Found if the user with the specified ID does not exist.
- **Error (401)**: Unauthorized if the user is not authenticated.

### Additional Information
- **Authentication**: All endpoints require the user to be authenticated. Ensure that your API client includes the necessary authentication headers (e.g., a JWT token) in requests.
- **Roles**: Only users with the `Admin` role can retrieve profiles of other users. Normal users can only access their profile.


