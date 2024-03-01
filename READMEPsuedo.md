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



#### PRODUCT API  

 
##### Overview:
 
     This API allows users to manage products, including inserting, retrieving, updating, and deleting product records.

#### Technologies Used:

    - Node.js
    - AWS SDK for JavaScript (v3)
    - AWS DynamoDB

#### Setup:

1. Install Node.js and npm.
2. Install dependencies: `npm install`.
3. Set up AWS credentials in the local environment or AWS configuration file.

#### Operations:

##### Create product (POST):

#### Description:

Creates a new product in the database.

#### Input:

- `name` (string): The name of the product.
- `description` (string): The description of the product.
- `price` (number): the price of the product.
- `quantity` (number): the quantity of the product.
- `unit` (number): the unit of the product in kg and piece.
- `category` (string):the category of the product.
- `image` (string):the image of the product.

#### Workflow:

1. Parse input data from the request body.
2. Generate a unique product ID.
3. Connect to the database (e.g., AWS DynamoDB).
4. Insert the product into the database.
5. Return a success message with the product ID.

#### Method: POST

#### Logic:

1. Connect to the DynamoDB database.
2. insert all product data in the database using AWS DynamoDB.

#### Request Body:

```json
{
  "name": "tv",
  "description": "Product Description",
  "price": 3000,
  "quantity": 10,
  "unit": {
    "PIECE": 10
  },
  "category": "electronics",
  "image": "https://example.com/image.jpg"
}
```

#### Responses:

- 201 Created: Product created successfully
- 400 Bad Request: Invalid request body
- 500 Internal Server Error: Error response.


##### Get All product (GET)

#### Description:

Retrieves all product stored in the database.

#### Workflow:

1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve all product from the database.
3. Return the list of product.

#### Response:

- **Status Code:** 200 (OK)
- **Body:** JSON array containing details of all product.

#### Logic:

1. Connect to the database.
2. Retrieve all product from the database using AWS DynamoDB.

#### Example Response:-

```json
[
    {
        "image": {
            "S": "C:\\Users\\Hi\\Pictures\\Screenshots\\Screenshot 2024-01-16 161402.png"
        },
        "unit": {
            "M": {
                "kg": {
                    "N": 50
                }
            }
        },
        "quantity": {
            "N": 50
        },
        "productId": "8c2af27c-1ce4-400b-b4e1-0117bfc7d0cf",
        "price": {
            "N": 50
        },
        "name": {
            "S": "washine machine"
        },
        "description": {
            "S": "Updated Product Description"
        },
        "category": {
            "S": "electronics"
        }
    },
    {
        "image": {
            "S": "C:\\Users\\Hi\\Pictures\\Screenshots\\Screenshot 2024-01-16 161402.png"
        },
        "unit": {
            "M": {
                "kg": {
                    "N": "50"
                }
            }
        },
        "quantity": {
            "N": "50"
        },
        "productId": "77cb44bb-cc53-43c7-b9d1-75ae7502ab9a",
        "price": {
            "N": "200"
        },
        "name": {
            "S": "apple"
        },
        "description": {
            "S": "Updated Product Description"
        },
        "category": {
            "S": "fruits"
        }
    }
]
```

#### Responses:

- 200 OK: Successful response with the product data
- 404 Not Found: Product with the specified ID not found
- 500 Internal Server Error: Error response.


##### Get product By ID (GET):

#### Description:

Retrieves a specific product from the database based on its unique product ID.

#### Input:

- `id`: Unique identifier of the product to retrieve.

#### Workflow:

1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve the product with the specified ID from the database.
3. Return the product details if found.

#### path parameters:

- `id`: Unique identifier of the product to retrieve.

#### Response:

- **Status Code:** 200 (OK) if the product is found.
- **Body:** JSON object containing details of the product.

#### Logic:

1. Connect to the database.
2. Retrieve the product with the specified ID from the database using AWS DynamoDB.

#### Example Response:-

```json
{
        "image": {
            "S": "C:\\Users\\Hi\\Pictures\\Screenshots\\Screenshot 2024-01-16 161402.png"
        },
        "unit": {
            "M": {
                "kg": {
                    "N": 50
                }
            }
        },
        "quantity": {
            "N": 50
        },
        "productId": "8c2af27c-1ce4-400b-b4e1-0117bfc7d0cf",
        "price": {
            "N": 50
        },
        "name": {
            "S": "washine machine"
        },
        "description": {
            "S": "Updated Product Description"
        },
        "category": {
            "S": "electronics"
        }     
}
```
#### Responses:

- 200 OK: Successful response with the product data
- 404 Not Found: Product with the specified ID not found
- 500 Internal Server Error: Error response.


##### Update product (PUT):

#### Description:

Updates the details of an existing product in the database based on its unique product ID.

#### Input
- `name` (string): The name of the product.
- `description` (string): The description of the product.
- `price` (number): the price of the product.
- `quantity` (number): the quantity of the product.
- `unit` (number): the unit of the product in kg and piece.
- `category` (string):the category of the product.
- `image` (string):the image of the product.

#### Workflow
1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve the existing product details based on the provided product ID.
3. Update the specified fields of the product with the new values.
4. Save the updated product details in the database.
5. Return a success message with the updated product details.

#### path parameters:

- `id`: Unique identifier of the product to update the data.

#### Logic:

1. Connect to the database.
2. Retrieve the product with the specified ID from the database using AWS DynamoDB.

#### Request Body:-

```json
{
        "image": {
            "S": "C:\\Users\\Hi\\Pictures\\Screenshots\\Screenshot 2024-01-16 161402.png"
        },
        "unit": {
            "M": {
                "kg": {
                    "N": 50
                }
            }
        },
        "quantity": {
            "N": 50
        },
        "productId": "8c2af27c-1ce4-400b-b4e1-0117bfc7d0cf",
        "price": {
            "N": 50
        },
        "name": {
            "S": "washine machine"
        },
        "description": {
            "S": "Updated Product Description"
        },
        "category": {
            "S": "electronics"
        }     
}
```
   
#### Responses:

- 200 OK: Product updated successfully
- 404 Not Found: Product with the specified ID not found
- 500 Internal Server Error: Error response.


##### Delete product (DELETE):

#### Description:

Deletes an existing product from the database based on its unique product ID.

#### Input:

- `id`: Unique identifier of the product to delete.

#### Workflow:

1. Connect to the database (e.g., AWS DynamoDB).
2. Check if the product exists based on the provided product ID.
3. If the product exists, delete it from the database.
4. Return a success message indicating the deletion.

#### path Parameters:

- `id`: Unique identifier of the product to delete.

#### Response:

- **Status Code:** 204 (No Content) if the product is deleted successfully.
- **Body:** None

#### Logic
1. Connect to the database.
2. Check if the product exists based on the provided product ID.
3. If the product exists, delete it from the database.

#### Example Request

``` http

http://localhost:3000/dev/Products/f92c4124-f6ad-468d-bf1b-3e7bd1eccd0e

```

#### Responses:

- 204 No Content: Product deleted successfully  
- 404 Not Found: Product with the specified ID not found  
- 500 Internal Server Error: Error response.


# SearchCart Function

## Logic

1. Initialize DynamoDB Document Client:
   - Create an instance of the DynamoDB Document Client from the AWS SDK, specifying the region and endpoint.

2. Define the search function:
   - Define an asynchronous function named `search`.
   - Log the start of the search function.
   - Construct a `params` object specifying the TableName as 'cart'.
   - Log the scanning of the DynamoDB table.
   - Use the `scan` method of the DynamoDB Document Client to scan the specified DynamoDB table.
   - Await the response from the scan operation.
   - If successful:
     - Log the successful search and return a response object with status code 200 OK.
     - Include the retrieved items from DynamoDB in the response body.
   - If an error occurs during the scan operation:
     - Log the error.
     - Return a response object with status code 500 Internal Server Error.
     - Include an error message in the response body indicating the failure to retrieve data from DynamoDB.

3. Export the search function:
   - Export the `search` function to make it accessible from other modules.



# GetItemById Function

## Logic

1. Configure the AWS SDK:
   - Import the AWS SDK.
   - Configure the AWS SDK to use the local DynamoDB endpoint by updating the AWS configuration with the region and endpoint details.

2. Initialize DynamoDB Document Client:
   - Create an instance of the DynamoDB Document Client from the AWS SDK.

3. Define the getItemById function:
   - Define an asynchronous function named `getItemById` which takes an `event` parameter.
   - Extract the 'itemid' from the path parameters of the incoming request.
   - Construct a `params` object specifying the TableName as 'cart' and the Key as the 'itemid'.
   - Try to retrieve the item from DynamoDB using the `get` method of the DynamoDB Document Client.
   - If the item is not found:
     - Return a response object with status code 404 Not Found.
     - Include a message indicating that the item was not found.
   - If successful:
     - Return a response object with status code 200 OK.
     - Include the retrieved item in the response body.
   - If an error occurs during the retrieval:
     - Log the error.
     - Return a response object with status code 500 Internal Server Error.
     - Include an error message in the response body indicating the failure to retrieve the item from DynamoDB.

4. Export the getItemById function:
   - Export the `getItemById` function to make it accessible from other modules.



# InsertItem Function

## Logic

1. Configure the AWS SDK:
   - Import the AWS SDK.
   - Configure the AWS SDK to use the local DynamoDB endpoint by updating the AWS configuration with the region and endpoint details.

2. Initialize DynamoDB Document Client:
   - Create an instance of the DynamoDB Document Client from the AWS SDK.

3. Define the insert function:
   - Define an asynchronous function named `insert` which takes an `event` parameter.
   - Parse the request body from the event to extract the data to be inserted into DynamoDB.
   - Construct a `params` object specifying the TableName as 'cart' and the Item as the parsed request body.
   - Try to insert data into the DynamoDB table using the `put` method of the DynamoDB Document Client.
   - If successful:
     - Return a response object with status code 200 OK.
     - Include a message indicating successful data insertion in the response body.
   - If an error occurs during the insertion:
     - Log the error.
     - Return a response object with status code 500 Internal Server Error.
     - Include an error message in the response body indicating the failure to insert data into DynamoDB.

4. Export the insert function:
   - Export the `insert` function to make it accessible from other modules.



# UpdateQuantity Function

## Logic

1. Configure the AWS SDK:
   - Import the AWS SDK.
   - Configure the AWS SDK to use the local DynamoDB endpoint by updating the AWS configuration with the region and endpoint details.

2. Initialize DynamoDB Document Client:
   - Create an instance of the DynamoDB Document Client from the AWS SDK.

3. Define the updateQuantity function:
   - Define an asynchronous function named `updateQuantity` which takes an `event` parameter.
   - Extract the 'itemid' from the path parameters of the incoming request.
   - Parse the request body from the event to extract the updated quantity.
   - Construct a `params` object specifying the TableName as 'cart', the Key as the 'itemid', and the UpdateExpression to update the quantity.
   - Try to update the quantity in DynamoDB using the `update` method of the DynamoDB Document Client.
   - If successful:
     - Return a response object with status code 200 OK.
     - Include the updated item in the response body.
   - If an error occurs during the update:
     - Log the error.
     - Return a response object with status code 500 Internal Server Error.
     - Include an error message in the response body indicating the failure to update the quantity in DynamoDB.

4. Export the updateQuantity function:
   - Export the `updateQuantity` function to make it accessible from other modules.



# DeleteCart Function

## Logic

1. Import the AWS SDK:
   - Import the AWS SDK to use its functionalities.

2. Set DynamoDB Local endpoint:
   - Create an instance of the `AWS.Endpoint` class with the endpoint URL for DynamoDB Local.
   - Update the AWS configuration to set the region to 'localhost' and specify the DynamoDB endpoint URL.

3. Create a DynamoDB DocumentClient:
   - Instantiate a DynamoDB DocumentClient from the AWS SDK to interact with DynamoDB.

4. Define the deleteCart function:
   - Define an asynchronous function named `deleteCart` which takes an `event` parameter.
   - Extract the 'itemid' from the path parameters of the incoming request.
   - Define the parameters for the delete operation, specifying the TableName as 'cart' and the Key as the 'itemid'.
   - Try to delete the item from the DynamoDB table using the `delete` method of the DocumentClient.
   - If successful:
     - Return a response object with status code 200 OK.
     - Include a message indicating successful deletion and the deleted item data in the response body.
   - If an error occurs during the deletion:
     - Return a response object with status code 500 Internal Server Error.
     - Include an error message indicating the failure to delete the item in the response body.

5. Export the deleteCart function:
   - Export the `deleteCart` function to make it accessible from other modules.
