## ORDER ENDPOINT

`base url: https://one00daysofcoding.onrender.com/`
1. **Get Order History**  
   - **Endpoint**: `GET /api/v1/orders/history`
   - **Description**: Retrieves the list of past orders for a user, including order details such as date, status, total amount, payment method, and delivery address.
   - **Request Parameters**: 
     - `userId` (optional if using sessions or JWT tokens with user data)
   - **Response**: Returns an array of orders with fields like `orderDate`, `status`, `total`, `paymentMethod`, `orderNo`, `quantity`, and `deliveryAddress`.

2. **Get Order Details**  
   - **Endpoint**: `GET /api/v1/orders/:orderId`
   - **Description**: Retrieves detailed information about a specific order by its ID.
   - **Request Parameters**: 
     - `orderId` (in the URL)
   - **Response**: Returns detailed information about the order, including product details, order status, payment method, delivery address, and quantity.

3. **Cancel Order**  
   - **Endpoint**: `POST /api/v1/orders/:orderId/cancel`
   - **Description**: Cancels an order that is still in the "Pending" status. Only orders that haven’t been processed or shipped can be canceled.
   - **Request Parameters**: 
     - `orderId` (in the URL)
   - **Response**: Confirmation of the cancellation or an error if the order cannot be canceled (e.g., already delivered or in progress).

4. **Get Order Status Options**  
   - **Endpoint**: `GET /api/v1/orders/status-options`
   - **Description**: Retrieves possible status options for filtering orders (e.g., `Pending`, `Delivered`, `Cancelled`). This can be used for filter dropdowns.
   - **Request Parameters**: None
   - **Response**: Array of possible status values (e.g., `["Pending", "Delivered", "Cancelled"]`).
still updating....
