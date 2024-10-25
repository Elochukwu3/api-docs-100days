### API Documentation for Delivery Address Feature

## Base URL
The base URL for all project endpoints is:
```
https://one00daysofcoding.onrender.com/
```
#### 1. **Create a New Delivery Address**
   - **Endpoint:** `POST /v1/delivery/address`
   - **Description:** Adds a new delivery address for the authenticated user.
   - **Authorization:** Requires Bearer token.
   - **sample url**: ``
https://one00daysofcoding.onrender.com/v1/delivery/address
``
   - **Request Body:**
     ```json
     {
       "firstName": "Bruce",
       "lastName": "Doe",
       "phoneNumber": "08012345678",
       "streetAddress": "123 Main Street",
       "directions": "Near the mall",  // Optional
       "lga": "Ikeja",
       "city": "Lagos",
       "state": "Lagos"
     }
     ```
   - **Response:**
     - **Status:** 201 Created
     - **Response Body:**
       ```json
       {
         "message": "Delivery address added successfully",
         "address": {
           "_id": "603d214f77f354001f6e9f8a",
           "firstName": "John",
           "lastName": "Doe",
           "phoneNumber": "08012345678",
           "streetAddress": "123 Main Street",
           "directions": "Near the mall",
           "lga": "Ikeja",
           "city": "Lagos",
           "state": "Lagos",
           "user": "603d210f77f354001f6e9f88"
         }
       }
       ```

#### 2. **Get All Delivery Addresses**
   - **Endpoint:** `GET /v1/delivery/address`
   - **Description:** Retrieves all delivery addresses associated with the authenticated user.
   - **Authorization:** Requires Bearer token.
   - **sample url**: ``
https://one00daysofcoding.onrender.com/v1/delivery/address
``
   - **Response:**
     - **Status:** 200 OK
     - **Response Body:**
       ```json
       {
         "status": "success",
         "addresses": [
           {
             "_id": "603d214f77f354001f6e9f8a",
             "firstName": "John",
             "lastName": "Doe",
             "phoneNumber": "08012345678",
             "streetAddress": "123 Main Street",
             "directions": "Near the mall",
             "lga": "Ikeja",
             "city": "Lagos",
             "state": "Lagos",
             "user": "603d210f77f354001f6e9f88"
           },
           {
             "_id": "603d214f77f354001f6e9f8b",
             "firstName": "Jane",
             "lastName": "Doe",
             "phoneNumber": "08087654321",
             "streetAddress": "456 Side Road",
             "lga": "Yaba",
             "city": "Lagos",
             "state": "Lagos",
             "user": "603d210f77f354001f6e9f88"
           }
         ]
       }
       ```

#### 3. **Update a Delivery Address**
   - **Endpoint:** `PUT /v1/delivery/address/:id`
   - **Description:** Updates a specific delivery address for the authenticated user.
   - **Authorization:** Requires Bearer token.
   - **sample url:** ``
https://one00daysofcoding.onrender.com/v1/delivery/address/.......
``
   - **Request Body (Optional Fields):**
     ```json
     {
       "firstName": "Updated Name",
       "phoneNumber": "08123456789",
       "lga": "Victoria Island"
     }
     ```
   - **Response:**
     - **Status:** 200 OK
     - **Response Body:**
       ```json
       {
         "message": "Delivery address updated successfully",
         "address": {
           "_id": "603d214f77f354001f6e9f8a",
           "firstName": "Updated Name",
           "lastName": "Doe",
           "phoneNumber": "08123456789",
           "streetAddress": "123 Main Street",
           "directions": "Near the mall",
           "lga": "Victoria Island",
           "city": "Lagos",
           "state": "Lagos",
           "user": "603d210f77f354001f6e9f88"
         }
       }
       ```

#### 4. **Delete a Delivery Address**
   - **Endpoint:** `DELETE /v1/delivery/address/:id`
   - **Description:** Deletes a specific delivery address for the authenticated user.
   - **Authorization:** Requires Bearer token.
   - **Response:**
     - **Status:** 200 OK
     - **Response Body:**
       ```json
       {
         "message": "Delivery address deleted successfully"
       }
       ```
#### 5. Get Delivery Address by ID

**Endpoint:** `GET /v1/delivery/address/:id`
**Description:** Fetch a specific delivery address by its ID. The user must be authenticated.
**Request Parameters:**- `id` (string, required): The ID of the delivery address.
**Authentication:** Requires user authentication (`req.user` is used to validate ownership).
**Response:**
- **200 OK:**  
  Returns the delivery address object if found.
  ```json
  {
    "status": true,
    "address": {
      "firstName": "John",
      "lastName": "Doe",
      "phoneNumber": "+1234567890",
      "streetAddress": "123 Street Name",
      "directions": "Near the park",
      "lga": "Local Government Area",
      "city": "City Name",
      "state": "State Name"
    }
  }
  ```

- **401 Unauthorized:**  
  If the user is not authenticated or the address does not belong to the user.
  ```json
  {
    "status": false,
    "message": "Unauthorized access"
  }
  ```

- **404 Not Found:**  
  If the delivery address with the specified `id` is not found.
  ```json
  {
    "status": false,
    "message": "Address not found"
  }
  ```
  
### Note on `req.user` for Authenticated Routes

For all delivery address routes, `req.user` is used to identify the logged-in user. This means that users must be authenticated to add, update, get, or delete their addresses.

- **How it works:**  
  The `req.user` object contains the user's ID and is used to link delivery addresses to the correct user.
  
- **Key point:**  
  If `req.user` is not available (i.e., the user is not logged in), a `401 Unauthorized` error will be returned.
---
