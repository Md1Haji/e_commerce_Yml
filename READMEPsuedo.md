# E-Commerce System

# Order Management API

## Description
This API provides endpoints to manage orders in an e-commerce system, including creating, retrieving, updating, and deleting orders.

## Technologies Used
- Node.js
- AWS SDK for JavaScript (v3)
- AWS DynamoDB

## Setup
1. Install Node.js and npm.
2. Install dependencies: `npm install`.
3. Set up AWS credentials in the local environment or AWS configuration file.

## Operations

### Create Order

#### Description
Creates a new order in the system.

#### Input
- `customerName`: Name of the customer placing the order.
- `products`: Array of products in the order.
- `totalPrice`: Total price of the order.
- `createdAt`: Timestamp indicating when the order was created.

#### Workflow
1. Parse input data from the request body.
2. Generate a unique order ID.
3. Connect to the database (e.g., AWS DynamoDB).
4. Insert the order into the database.
5. Return a success message with the order ID.

#### Request Body
```json
{
  "customerName": "John Doe",
  "products": [
    {
      "productId": "1",
      "quantity": 2
    },
    {
      "productId": "2",
      "quantity": 1
    }
  ],
  "totalPrice": 27.97,
  "createdAt": "2024-02-28T12:00:00Z",  
  "status": "confirmed"
}
```

### Get All Orders

#### Description
Retrieves all orders stored in the system.

#### Workflow
1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve all orders from the database.
3. Return the list of orders.

#### Response
- **Status Code:** 200 (OK)
- **Body:** JSON array containing details of all orders.

#### Logic
1. Connect to the database.
2. Retrieve all orders from the database using AWS DynamoDB.

#### Example Response
```json
[
  {
    "orderId": "12345",
    "customerName": "John Doe",
    "products": [
      {
        "productId": "1",
        "quantity": 2
      },
      {
        "productId": "2",
        "quantity": 1
      }
    ],
    "totalPrice": 27.97,
    "createdAt": "2024-02-28T12:00:00Z",
    "status": "confirmed"
  },
  {
    "orderId": "67890",
    "customerName": "Jane Smith",
    "products": [
      {
        "productId": "3",
        "quantity": 1
      }
    ],
    "totalPrice": 14.99,
    "createdAt": "2024-02-28T13:00:00Z",
    "status": "cancelled"
  }
]

```

### Get Order By ID

#### Description
Retrieves a specific order from the system based on its unique order ID.

#### Input
- `orderId`: Unique identifier of the order to retrieve.

#### Workflow
1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve the order with the specified ID from the database.
3. Return the order details if found.

#### Request Parameters
- `orderId`: Unique identifier of the order to retrieve.

#### Response
- **Status Code:** 200 (OK) if the order is found.
- **Body:** JSON object containing details of the order.

#### Logic
1. Connect to the database.
2. Retrieve the order with the specified ID from the database using AWS DynamoDB.

#### Example Response
```json
{
  "orderId": "12345",
  "customerName": "John Doe",
  "products": [
    {
      "productId": "1",
      "quantity": 2
    },
    {
      "productId": "2",
      "quantity": 1
    }
  ],
  "totalPrice": 27.97,
  "createdAt": "2024-02-28T12:00:00Z",
  "status": "confirmed"
}
```

### Update Order

#### Description
Updates the details of an existing order in the system based on its unique order ID.

#### Input
- `orderId`: Unique identifier of the order to update.
- `customerName`: Updated name of the customer placing the order (optional).
- `products`: Updated array of products in the order (optional).
- `totalPrice`: Updated total price of the order (optional).
- `status`: Updated status of the order (optional).

#### Workflow
1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve the existing order details based on the provided order ID.
3. Update the specified fields of the order with the new values.
4. Save the updated order details in the database.
5. Return a success message with the updated order details.

#### Request Body
```json
{
  "orderId": "12345",
  "customerName": "Updated Customer Name",
  "products": [
    {
      "productId": "1",
      "quantity": 3
    }
  ],
  "totalPrice": 35.99,
  "status": "confirmed"
}
```
### Delete Order

#### Description
Deletes an existing order from the system based on its unique order ID.

#### Input
- `orderId`: Unique identifier of the order to delete.

#### Workflow
1. Connect to the database (e.g., AWS DynamoDB).
2. Check if the order exists based on the provided order ID.
3. If the order exists, delete it from the database.
4. Return a success message indicating the deletion.

#### Request Parameters
- `orderId`: Unique identifier of the order to delete.

#### Response
- **Status Code:** 204 (No Content) if the order is deleted successfully.
- **Body:** None

#### Logic
1. Connect to the database.
2. Check if the order exists based on the provided order ID.
3. If the order exists, delete it from the database.

#### Example Request
```http
DELETE /orders/12345
```


# Update Order Status

## Description
The "Update Order Status" functionality allows users to modify the status of an existing order.

## Input
- `orderId`: The unique identifier of the order to be updated.
- `status`: The new status of the order (e.g., confirmed, cancelled, completed, closed).

## Workflow
1. Send a POST request to the designated endpoint (`/updateOrderStatus`).
2. Include the `orderId` and `status` in the request body as JSON data.
3. The system updates the status of the specified order in the database.
4. Return a confirmation message indicating the successful update of the order status.

## Request Body
```json
{
  "orderId": "12345",
  "status": "confirmed"
}
```


# POST METHOD: TO INSERT INVENTORY DETAILS IN THE DYNAMODB DATABASE.

## RESEARCH

 --> I referred dynamodb tutorials and stack overflow website.

## LOGIC

 1. METHOD: POST

 2. ENDPOINT: /inventory 

 3. Created the node js serverless aws lambda function that will insert the inventory details into the database.

 4. connect to database.

 5. Configure AWS credentials and DynamoDB endpoint.

 6. Extract product_id and availableQuantity from the requestBody.

 7. Define parameters for putting an item into the 'inventory' table.

 8.  Insert the item into the 'inventory' table.

 9. If the insert is successful, return a success response with status code 200 and the inserted data.

 10.  If there's an error during the insert, catch the error, log it, and return an error response with status code 500 and an error message 
    in the body.

 

## SUMMARY:

-->In this appilcation we are using node js serverless code to inventory details by required details from the postman.



 

# PUT METHOD: TO UPDATE INVENTORY DETAILS IN TO THE DATABASE.

## RESEARCH

 --> I referred dynamodb tutorials and stack overflow website.

## LOGIC

 1. METHOD: PUT

 2. ENDPOINT: /inventory/{inventory_id}

 3. Created the node js serverless aws lambda function that will update the inventory details.

 4. connect to database.
    
 5. Configure AWS credentials and DynamoDB endpoint.

 6. Extract updateQuantity from the requestBody.
 
 7. Retrieve inventory_id from pathparameters.

 8. Define parameters for updating an item in the 'inventory' table.

 9. Try to update the item in the DynamoDB table using the defined parameters.

 10. If the update is successful, return a success response with status code 200 and the updated item attributes in the body.

 11. If there's an error during the update, catch the error, log it, and return an error response with status code 500 and an error message 
    in the body.

## SUMMARY:

-->In this appilcation we are using node js serverless code to update quantity details.




# GET METHOD: TO GET ALL INVENTORY DETAILS.

## RESEARCH

 --> I referred dynamodb tutorials and stack overflow website.

## LOGIC

 1. METHOD: GET

 2. ENDPOINT: /inventory

 3. Created the node js serverless aws lambda function that will get all inventory details.

 4. connect to database.
  
 5. Configure AWS credentials and DynamoDB endpoint.

 6. Define parameters for scanning all items in the 'inventory' table.

 7. Try to scan all items in the DynamoDB table using the defined parameters.

 8. If the scan is successful, return a success response with status code 200 and the scanned items in the body.

 9. If there's an error during the scan, catch the error, and return an error response with status code 500 and an error message in the body.

 

## SUMMARY:

-->In this appilcation we are using node js serverless code to get all inventory details.
    


# GET METHOD: TO GET INVENTORY DETAILS FOR PARTICULAR INVENTORY_ID

## RESEARCH

 --> I referred dynamodb tutorials and stack overflow website.

## LOGIC

 1. METHOD: GET

 2. ENDPOINT: /inventory/{inventory_id}

 3. Created the node js serverless aws lambda function that will get inventory details particular id.

 4. connect to database.
  
 5. Configure AWS credentials and DynamoDB endpoint.

 6. Extract the inventory ID from the path parameters of the event.

 7. Define parameters for scanning all items in the 'inventory' table.

 8. Try to scan all items in the DynamoDB table using the defined parameters.

 9. If the scan is successful, return a success response with status code 200 and the scanned items in the body.

 10. If there's an error during the scan, catch the error, and return an error response with status code 500 and an error message in the body.


## SUMMARY:

-->In this appilcation we are using go serverless code to get inventory details of a particular id.


# DELETE METHOD: TO DELETE INVENTORY DETAILS OF PARTICULAR INVENTORY_ID

## RESEARCH

 --> I referred dynamodb tutorials and stack overflow website.

## LOGIC

 1. METHOD: DELETE

 2. ENDPOINT: /inventory/{inventory_id}

 3. Created the node js serverless aws lambda function that will delete inventory details of particular id.

 4. connect to database.
  
 5. Configure AWS credentials and DynamoDB endpoint.

 6. Extract the inventory ID from the path parameters of the event.

 7. Try to delete a product from the 'inventory' table based on the provided inventory ID.

 8. If the deletion is successful, return a success response with status code 200 and a message indicating the successful deletion, along with any deleted data.

 9. If there's an error during the deletion process, catch the error, and return an error response with status code 500 and an error message indicating the failure to delete the item.


## SUMMARY:

-->In this appilcation we are using node js serverless code to delete inventory details of a particular id.




