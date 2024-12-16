
# Order Management API

This API provides endpoints for managing user orders, including viewing order history, retrieving specific order details, cancelling orders, and getting order status options.

##base: `https://one00daysofcoding.onrender.com`

## Endpoints

| HTTP Method | Endpoint                                     | Description                    |
|-------------|---------------------------------------------|--------------------------------|
| `GET`      | `/api/v1/orders/history`                    | Get order history for a user   |
| `GET`      | `/api/v1/orders/:orderId`                   | Get details of a specific order|
| `POST`     | `/api/v1/orders/:orderId/cancel`            | Cancel a specific order        |
| `GET`      | `/api/v1/orders/status-options`             | Retrieve order status options  |

---

## Order History

### Description
Retrieves the order history for the currently authenticated user.

### Endpoint
```
GET /api/v1/orders/history
```

### Example Request
```http
GET base/api/v1/orders/history
Authorization: Bearer <user-token>
```

### Response
```json
{
  "orders": [
    {
      "_id": "676039543a80ea2ffc355b91",
      "userId": "1234567890",
      "productDetails": { "name": "Polystar Smart TV", "price": 300 },
      "status": "Delivered",
      "orderDate": "2024-06-10T12:00:00Z"
    },
    {
      "_id": "676039543a80ea2ffc355b92",
      "userId": "1234567890",
      "productDetails": { "name": "Microwave Oven", "price": 150 },
      "status": "Pending",
      "orderDate": "2024-06-15T15:00:00Z"
    }
  ]
}
```

---

## Order Details

### Description
Retrieves details of a specific order based on its ID.

### Endpoint
```
GET /api/v1/orders/:orderId
```

### Example Request
```http
GET base/api/v1/orders/676039543a80ea2ffc355b91
```

### Response
```json
{
  "order": {
    "_id": "676039543a80ea2ffc355b91",
    "userId": "1234567890",
    "productDetails": { "name": "Polystar Smart TV", "price": 300 },
    "status": "Delivered",
    "orderDate": "2024-06-10T12:00:00Z"
  }
}
```

---

## Cancel Order

### Description
Cancels a specific order if its status is `Pending`. Additional details (phone, reason, more information) are required for cancellation.

### Endpoint
```
POST /api/v1/orders/:orderId/cancel
```

### Request Payload
| Field     | Type   | Required | Description                       |
|-----------|--------|----------|-----------------------------------|
| `phone`   | string | Yes      | Phone number for contact          |
| `reason`  | string | Yes      | Reason for cancellation           |
| `moreInfo`| string | No       | Additional information (optional) |

### Example Request
```http
POST https://one00daysofcoding.onrender.com/api/v1/orders/676039543a80ea2ffc355b91/cancel
Content-Type: application/json

{
  "phone": "123-456-7890",
  "reason": "No longer needed",
  "moreInfo": "Found a better deal."
}
```

### Response
```json
{
  "message": "Order canceled successfully",
  "order": {
    "id": "676039543a80ea2ffc355b91",
    "status": "Cancelled",
    "cancellationDetails": {
      "phone": "123-456-7890",
      "reason": "No longer needed",
      "moreInfo": "Found a better deal.",
      "cancelledAt": "2024-06-16T10:30:00Z"
    }
  }
}
```

### Error Responses
- **400 Bad Request**: If required fields are missing.
  ```json
  { "message": "Phone number is required" }
  ```
- **404 Not Found**: If the order does not exist.
- **400 Bad Request**: If the order is not `Pending`.
  ```json
  { "message": "Only pending orders can be canceled" }
  ```

---

## Order Status Options

### Description
Retrieves available order status options.

### Endpoint
```
GET /api/v1/orders/status-options
```

### Example Request
```http
GET https://one00daysofcoding.onrender.com/api/v1/orders/status-options
```

### Response
```json
{
  "statusOptions": ["Pending", "Delivered", "Cancelled"]
}
```

---

### Cancellation Schema
The following schema is used to validate cancellation requests:

```typescript
const cancelOrderSchema = Joi.object({
  phone: Joi.string().required().messages({ 'any.required': 'Phone number is required' }),
  reason: Joi.string().required().messages({ 'any.required': 'Cancellation reason is required' }),
  moreInfo: Joi.string().optional(),
});
```
