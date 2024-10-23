

### **Reviews Endpoint Documentation**
## Base URL
The base URL for all project endpoints is:
```
https://one00daysofcoding.onrender.com/
```
## Auth Section
Endpoint:
```
https://one00daysofcoding.onrender.com/v1/products/
```

#### **1. Add a Review**
- **Endpoint**: `POST /:id/reviews`
- **Description**: Adds a review to a specific product.
- **Parameters**:
  - `id` (URL param): The ID of the product to which the review is being added.
  - **Body** (JSON):
    - `userId` (string, required): The ID of the user adding the review.
    - `name` (string, optional): The name of the reviewer (defaulted if omitted).
    - `rating` (number, required): The rating for the product (must be between 1 and 5).
    - `comment` (string, required): A text comment about the product.
  
- **Validation**:
  - All fields are validated using Joi.
  - `userId` is required.
  - `rating` must be between 1 and 5.
  - `comment` is required.
  
- **Response**:
  - `201 Created`: If the review is successfully added.
  - `400 Bad Request`: If the validation fails, with an appropriate error message.

- **Example Request**:
  ```json
  {
    "userId": "60b6e777fcd3d50015bb3f72",
    "rating": 4,
    "comment": "Great product!"
  }
  ```

#### **2. Get All Reviews for a Product**
- **Endpoint**: `GET /:id/reviews`
- **Description**: Retrieves all reviews for a specific product.
- **Parameters**:
  - `id` (URL param): The ID of the product whose reviews are being fetched.
  
- **Response**:
  - `200 OK`: Returns a list of reviews for the product.
  - `400 Bad Request`: If the product ID is invalid or the product is not found.
  
- **Example Response**:
  ```json
  {
    "status": true,
    "reviews": [
      {
        "userId": "60b6e777fcd3d50015bb3f72",
        "name": "John Doe",
        "rating": 4,
        "comment": "Great product!"
      },
      {
        "userId": "60b6e777fcd3d50015bb3f73",
        "name": "Jane Doe",
        "rating": 5,
        "comment": "Excellent quality."
      }
    ]
  }
  ```

#### **3. Update a Review**
- **Endpoint**: `PUT /:productId/reviews/:reviewId`
- **Description**: Updates a specific review for a product.
- **Parameters**:
  - `productId` (URL param): The ID of the product.
  - `reviewId` (URL param): The ID of the review to update.
  - **Body** (JSON):
    - `userId` (string, required): The ID of the user updating the review.
    - `name` (string, optional): The name of the reviewer (optional).
    - `rating` (number, optional): The updated rating for the product (must be between 1 and 5).
    - `comment` (string, required): The updated comment for the product.
  
- **Validation**:
  - `userId` is required.
  - `rating` must be between 1 and 5 if provided.
  - `comment` is required.

- **Response**:
  - `200 OK`: If the review is successfully updated.
  - `400 Bad Request`: If validation fails.
  - `404 Not Found`: If the review or product is not found.

- **Example Request**:
  ```json
  {
    "userId": "60b6e777fcd3d50015bb3f72",
    "rating": 5,
    "comment": "Updated review: Amazing product!"
  }
  ```

#### **4. Delete a Review**
- **Endpoint**: `DELETE /:productId/reviews/:reviewId`
- **Description**: Deletes a specific review from a product.
- **Parameters**:
  - `productId` (URL param): The ID of the product.
  - `reviewId` (URL param): The ID of the review to delete.
  
- **Response**:
  - `200 OK`: If the review is successfully deleted.
  - `404 Not Found`: If the review or product is not found.

- **Example Response**:
  ```json
  {
    "status": true,
    "message": "Review deleted successfully"
  }
  ```

---
