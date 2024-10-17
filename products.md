# Product API Documentation

## **Base URL**: `/api/v1/products`

### Authentication:  
All product-related endpoints require authentication unless stated otherwise. Provide the API key or JWT token in the request headers:  
Except:  Get All Product, Get Product by ID
```
Authorization: Bearer <token>
```

---

## **1. Create a Product**
### **Endpoint**: `POST /api/v1/products`
### **Description**: Creates a new product in the system.

### **Request Body** (JSON):
```json
{
  "name": "Sample Product",
  "description": "This is a sample product.",
  "price": 100,
  "category": "Electronics",
  "images": ["image1.jpg", "image2.jpg"],
  "stock": 50
}
```

### **Response** (201 - Created):
```json
{
  "_id": "64e8e342eb45a",
  "name": "Sample Product",
  "description": "This is a sample product.",
  "price": 100,
  "category": "Electronics",
  "images": ["image1.jpg", "image2.jpg"],
  "stock": 50,
  "ratings": 0,
  "reviews": [],
  "createdAt": "2024-10-16T12:00:00.000Z",
  "updatedAt": "2024-10-16T12:00:00.000Z"
}
```

### **Possible Errors**:
- **400 Bad Request**: Missing or invalid fields in the request body.
- **401 Unauthorized**: No valid token provided.

---

## **2. Get All Products**
### **Endpoint**: `GET /api/v1/products`
### **Description**: Retrieves all products, with optional filtering via query parameters.

### **Query Parameters** (optional):
- `category` (string) - Filters products by category.
- `minPrice` (number) - Filters products with a price greater than or equal to `minPrice`.
- `maxPrice` (number) - Filters products with a price less than or equal to `maxPrice`.
- `sort` (string) - Sort by fields, e.g., `price`, `ratings`.

### **Response** (200 - OK):
```json
[
  {
    "_id": "64e8e342eb45a",
    "name": "Sample Product",
    "description": "This is a sample product.",
    "price": 100,
    "category": "Electronics",
    "images": ["image1.jpg", "image2.jpg"],
    "stock": 50,
    "ratings": 0,
    "reviews": [],
    "createdAt": "2024-10-16T12:00:00.000Z",
    "updatedAt": "2024-10-16T12:00:00.000Z"
  }
]
```

### **Possible Errors**:
- **400 Bad Request**: Invalid query parameters.

---

## **3. Get Product by ID**
### **Endpoint**: `GET /api/v1/products/:id`
### **Description**: Fetches a product by its unique ID.

### **Path Parameters**:
- `id` (string) - The ID of the product to retrieve.

### **Response** (200 - OK):
```json
{
  "_id": "64e8e342eb45a",
  "name": "Sample Product",
  "description": "This is a sample product.",
  "price": 100,
  "category": "Electronics",
  "images": ["image1.jpg", "image2.jpg"],
  "stock": 50,
  "ratings": 0,
  "reviews": []
}
```

### **Possible Errors**:
- **404 Not Found**: Product with the given ID does not exist.

---

## **4. Update a Product**
### **Endpoint**: `PUT /api/v1/products/:id`
### **Description**: Updates an existing product’s details.

### **Request Body** (JSON):
```json
{
  "name": "Updated Product Name",
  "price": 150,
  "stock": 30
}
```

### **Response** (200 - OK):
```json
{
  "_id": "64e8e342eb45a",
  "name": "Updated Product Name",
  "description": "This is a sample product.",
  "price": 150,
  "category": "Electronics",
  "images": ["image1.jpg", "image2.jpg"],
  "stock": 30,
  "ratings": 0,
  "reviews": [],
  "updatedAt": "2024-10-17T12:00:00.000Z"
}
```

### **Possible Errors**:
- **400 Bad Request**: Invalid fields in the request body.
- **404 Not Found**: Product with the given ID does not exist.

---

## **5. Delete a Product**
### **Endpoint**: `DELETE /api/v1/products/:id`
### **Description**: Deletes a product by its ID.

### **Response** (200 - OK):
```json
{
  "message": "Product deleted successfully",
  "product": {
    "_id": "64e8e342eb45a",
    "name": "Sample Product",
    "description": "This is a sample product.",
    "price": 100,
    "category": "Electronics",
    "images": ["image1.jpg", "image2.jpg"],
    "stock": 50
  }
}
```

### **Possible Errors**:
- **404 Not Found**: Product with the given ID does not exist.

---

### **6. Add a Review**
### **Endpoint**: `POST /api/v1/products/:id/reviews`
### **Description**: Adds a new review to a product.

### **Request Body** (JSON):
```json
{
  "userId": "64e8f42be71c3",
  "name": "John Doe",
  "rating": 5,
  "comment": "Great product!"
}
```

### **Response** (200 - OK):
```json
{
  "message": "Review added successfully",
  "product": {
    "_id": "64e8e342eb45a",
    "name": "Sample Product",
    "description": "This is a sample product.",
    "price": 100,
    "category": "Electronics",
    "images": ["image1.jpg", "image2.jpg"],
    "stock": 50,
    "ratings": 5,
    "reviews": [
      {
        "userId": "64e8f42be71c3",
        "name": "John Doe",
        "rating": 5,
        "comment": "Great product!"
      }
    ]
  }
}
```

### **Possible Errors**:
- **400 Bad Request**: Missing or invalid fields in the review.

---

## Common Status Codes:
- **200 OK**: Successful response.
- **201 Created**: Resource created successfully.
- **400 Bad Request**: Invalid request data or parameters.
- **401 Unauthorized**: Authentication required or invalid token.
- **404 Not Found**: Resource not found.

---
