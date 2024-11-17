## USER CART ENDPOINT
`base url: https://one00daysofcoding.onrender.com/`
1. **Get Cart Items**
   - **Endpoint**: `GET /cart/v1`
   - **Description**: Retrives all the products that have been added to the cart with their quantites, image of product, size of that specific product, price of specific product and total price of all products added to the cart
   - **Request parameters**:
       - **userId** (this is optional cause it will be sent automatically when user successfully logs in and sessions are active)
    - **Response**:
        - **( 200 - Success )**:
          ```json
          {
            "userId": "id",
            "items": [
                {
                  "productId": "ID of the specific product in the cart collection",
                  "quantity": "Quantity of the product",
                  "size": "Size of the product",
                  "price": "Price of the product",
                  "image": "Image of the product"
                }
            ],
          "totalamount": "Total price of all product in the cart"
          }
          ```
        - **( 401 - Unauthorised)**: This when a specific person is not allowed to access the endpoint because probably the user id can't be found.

2. **Add Product to Cart**
   - **Endpoint**: `POST /cart/v1`
   - **Description**: Adds a product to the cart with the quantity, image, size of the product selected by the user
   - **Request parameters**:
     - **userId**  (this is optional cause it will be sent automatically when user successfully logs in and sessions are active)
     - **req body**
         ```json
         {
           "productId" : "ID of the product",
           "quantity": "Quantity of the product",
           "size": "Size of the product",
           "price": "Price of the product",
           "image": "Image of the product"
         }
         ```
   - **Response**:
       - **(201 - Created )**:
           ```json
           {
              "message": "Product successfully added to cart!" 
           }
           ```
       - **(500 - Server error )**:
         ```json
           {
              "message": "Error adding product to cart" 
           }
           ```
       - **( 401 - Unauthorised)**: This when a specific person is not allowed to access the endpoint because probably the user id can't be found.
3. **Updating product in cart**:
     - **Endpoint**: `PUT /cart/v1`
     - **Description**: Updates a product in the cart to change the quantity of the product selected by the user
     - **Request parameters**:
       - **userId**  (this is optional cause it will be sent automatically when user successfully logs in and sessions are active)
       - **req body**
         ```json
         {
           "productId" : "ID of the specific product user want to update",
           "quantity" : "Providing the updated quantity user wants to get"
         }
         ```
     -  **Response**:
        - **(200 - Success )**:
           ```json
           {
              "message": "Product successfully added to cart!" 
           }
           ```
        - **(500 - Server error )**:
           ```json
             {
                "message": "Error updating product to cart" 
             }
           ```
         - **( 401 - Unauthorised)**: This when a specific person is not allowed to access the endpoint because probably the user id can't be found.
4. **Deleting a product in the cart**:
      - **Endpoint**: `DELETE /cart/v1`
     - **Description**: Deletes a product in the cart
     - **Request parameters**:
       - **userId**  (this is optional cause it will be sent automatically when user successfully logs in and sessions are active)
       - **req body**
         ```json
         {
           "productId" : "ID of the specific product user want to update"
         }
         ```
     -  **Response**:
        - **(200 - Success )**:
           ```json
           {
              "message": "Product successfully deleted from cart!" 
           }
           ```
        - **(500 - Server error )**:
           ```json
             {
                "message": "Error deleting product from cart" 
             }
           ```
         - **( 401 - Unauthorised)**: This when a specific person is not allowed to access the endpoint because probably the user id can't be found.
      



        
       
           

       
         
            
           
      
          
