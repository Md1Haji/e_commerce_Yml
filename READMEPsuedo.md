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


### Update Order Status

#### Description
The "Update Order Status" functionality allows users to modify the status of an existing order.

## Input
- `orderId`: The unique identifier of the order to be updated.
- `status`: The new status of the order (e.g., confirmed, cancelled, completed, closed).

#### Workflow
1. Send a POST request to the designated endpoint (`/updateOrderStatus`).
2. Include the `orderId` and `status` in the request body as JSON data.
3. The system updates the status of the specified order in the database.
4. Return a confirmation message indicating the successful update of the order status.

#### Request Body
```json
{
  "orderId": "12345",
  "status": "cancell"
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

### Create product (POST):

#### Description:

Creates a new product in the database.

#### Input:

- name (string): The name of the product.
- description (string): The description of the product.
- price (number): the price of the product.
- quantity (number): the quantity of the product.
- unit (number): the unit of the product in kg and piece.
- category (string):the category of the product.
- image (string):the image of the product.

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
1. 201 Created: Product created successfully
2. 400 Bad Request: Invalid request body
3. 500 Internal Server Error: Error response.


### Get All product (GET)

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
1. 200 OK : Successful response with the product data
2. 404 Not Found : Product with the specified ID not found
3. 500 Internal Server Error : Error response.


### Get product By ID (GET):

#### Description:

Retrieves a specific product from the database based on its unique product ID.

#### Input:

- id: Unique identifier of the product to retrieve.

#### Workflow:

1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve the product with the specified ID from the database.
3. Return the product details if found.

#### path parameters:

- id: Unique identifier of the product to retrieve.

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
1. 200 OK: Successful response with the product data
2. 404 Not Found: Product with the specified ID not found
3. 500 Internal Server Error: Error response.


### Update product (PUT):

#### Description:

Updates the details of an existing product in the database based on its unique product ID.

#### Input
- name (string): The name of the product.
- description (string): The description of the product.
- price (number): the price of the product.
- quantity (number): the quantity of the product.
- unit (number): the unit of the product in kg and piece.
- category (string):the category of the product.
- image (string):the image of the product.

#### Workflow
1. Connect to the database (e.g., AWS DynamoDB).
2. Retrieve the existing product details based on the provided product ID.
3. Update the specified fields of the product with the new values.
4. Save the updated product details in the database.
5. Return a success message with the updated product details.

#### path parameters:

- id: Unique identifier of the product to update the data.

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
1. 200 OK: Product updated successfully
2. 404 Not Found: Product with the specified ID not found
3. 500 Internal Server Error: Error response.


### Delete product (DELETE):

#### Description:

Deletes an existing product from the database based on its unique product ID.

#### Input:

- id: Unique identifier of the product to delete.

#### Workflow:

1. Connect to the database (e.g., AWS DynamoDB).
2. Check if the product exists based on the provided product ID.
3. If the product exists, delete it from the database.
4. Return a success message indicating the deletion.

#### path Parameters:

- id: Unique identifier of the product to delete.

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

1.200 No Content: Product deleted successfully  
2.404 Not Found: Product with the specified ID not found  
3.500 Internal Server Error: Error response.

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



### CUSTOMERS PSUDO CODE 

##  Customeradd -

1. Import required modules: AWS SDK and uuid

2. Configure AWS SDK to connect to local DynamoDB instance

3. Create a DynamoDB DocumentClient instance

4. Define a Lambda function named insertCustomer to insert customer data into DynamoDB

5. Parse the incoming event body to extract customer details

6. Generate a unique customer ID using uuidv4()

7. Construct parameters for DynamoDB put operation:
   - Define TableName as 'Customer'
   - Set Item with customer_Id and customer_details

8. Execute DynamoDB put operation using the DocumentClient instance and the constructed parameters

9. If the put operation is successful:
   - Return a success response with status code 200 and a message indicating successful insertion
   - If an error occurs during the put operation:
   - Return an error response with status code 500 and a message indicating the error encountered

##  CustomerGetAll - 

1. Import the AWS SDK module.

2. Configure the AWS SDK to connect to the local DynamoDB instance.

3. Create a DynamoDB DocumentClient instance.

4. Define a Lambda function named getAllCustomer to retrieve all customer data from DynamoDB.

5. Try the following:
   a. Construct parameters for a DynamoDB scan operation:
      - Set TableName as 'Customer'.
   b. Execute the DynamoDB scan operation using the DocumentClient instance and the constructed parameters.
   c. Store the result items in a variable named customer.

6. If the scan operation is successful:
   - Return a success response with status code 200 and the retrieved customer data in the response body.
   - If an error occurs during the scan operation:
   - Return an error response with status code 500 and a message indicating the error encountered.

##  CustomerGetById -

1. Import the AWS SDK module.

2. Configure the AWS SDK to connect to the local DynamoDB instance.

3. Create a DynamoDB DocumentClient instance.

4. Define a Lambda function named getCustomerById to retrieve a customer's data by ID from DynamoDB.

5. Extract the customer ID from the event's path parameters.

6. If the customer ID is missing:
   - Return a response with status code 400 and a message indicating that the customer ID is required.

7. Construct parameters for a DynamoDB get operation:
   - Set TableName as 'Customer'.
   - Set Key with the extracted customer ID.

8. Try the following:
   a. Execute the DynamoDB get operation using the DocumentClient instance and the constructed parameters.
   b. Store the retrieved item data in a variable named data.

9. If the get operation is successful:
   - Return a success response with status code 200 and the retrieved customer data in the response body.
   
10. If an error occurs during the get operation:
   - Return an error response with status code 500 and a message indicating the error encountered.

##  CustomerUpdateById -

1. Import the AWS SDK module.

2. Configure the AWS SDK to connect to the local DynamoDB instance.

3. Create a DynamoDB DocumentClient instance.

4. Define a Lambda function named updateCustomer to update customer data in DynamoDB.

5. Try the following:
   a. Extract the customer ID from the event's path parameters.
   b. Parse the request body to extract the updated customer details.
   
6. Define parameters for a DynamoDB update operation:
   a. Set TableName as 'Customer'.
   b. Set Key with the extracted customer ID.
   c. Define an UpdateExpression to set the customer_details attribute.
   d. Define ExpressionAttributeValues to specify the new customer details.
   e. Set ReturnValues as 'ALL_NEW' to return the updated item.

7. Execute the DynamoDB update operation using the DocumentClient instance and the constructed parameters.

8. If the update operation is successful:
   - Return a success response with status code 200 and a message indicating the successful update along with the updated item data.
   
9. If an error occurs during the update operation:
   - Return an error response with status code 500 and a message indicating the error encountered.

##  CustomerDeleteById -

1. Import the AWS SDK module.

2. Configure the AWS SDK to connect to the local DynamoDB instance.

3. Create a DynamoDB DocumentClient instance.

4. Define a Lambda function named deleteCustomer to delete customer data from DynamoDB.

5. Try the following:
   a. Extract the customer ID from the event's path parameters.
   b. Check if the customer ID is provided in the path parameters. If not, return a 400 Bad Request response.

6. Define parameters for a DynamoDB delete operation:
   a. Set TableName as 'Customer'.
   b. Set Key with the extracted customer ID.

7. Execute the DynamoDB delete operation using the DocumentClient instance and the constructed parameters.

8. If the delete operation is successful:
   - Return a success response with status code 200 and a message indicating the successful deletion of the customer.

9. If an error occurs during the delete operation:
   - Return an error response with status code 500 and a message indicating the error encountered during deletion.

#  dynamodb lambda API
 
## Overview
- The API's pseudo code includes logic for inserting, retrieving, updating, and deleting customer data in a DynamoDB 'Customer' table, emphasizing CRUD operations and error handling.
 
# InsertCustomer Function

## Logic

- **Parse the incoming event to extract the request body.**
- **Extract the value from the request body: details.**
- **Generate a unique identifier (e.g., customer_Id) using uuidv4.**
- **Create a DynamoDB `params` object with the following:**
  - TableName: 'Customer'
  - Item: Object containing customer_Id and details.
- **Use the DynamoDB `post` method to insert the data into the 'Customer' table.**
- **If successful:**
  - Return a response with status code 200 OK.
  - Include a success message in the response body.
- **If an error occurs:**
  - Return a response with status code 500 Internal Server Error.
  - Include an error message in the response body.

# GetCustomerById Function

## Logic

- **Extract the value from the path parameters: customer_Id.**
- **If customer_Id is missing:**
   - Return a response with status code 400 Bad Request.
   - Include a message indicating that Customer ID is required.
- **Create a DynamoDB `params` object with the following:**
   - TableName: 'Customer'
   - Key: Object containing customer_Id.
- **Try to get data from DynamoDB using the `get` method.**
- **If successful:**
   - Return a response with status code 200 OK.
   - Include the retrieved customer data in the response body.
- **If an error occurs:**
   - Return a response with status code 500 Internal Server Error.
   - Include an error message in the response body.

# GetAllCustomer Function

## Logic

- **Create a DynamoDB `params` object with the following:**
   - TableName: 'Customer'
- **Try to scan data from DynamoDB using the `scan` method.**
- **If successful:**
   - Return a response with status code 200 OK.
   - Include the list of all customer data in the response body.
- **If an error occurs:**
   - Return a response with status code 500 Internal Server Error.
   - Include an error message in the response body.

# UpdateCustomer Function

## Logic

- **Extract the value from the path parameters: customer_Id.**
- **Parse the incoming event to extract the request body.**
- **Extract the updated value from the request body: details.**
- **Create a DynamoDB `params` object with the following:**
   - TableName: 'Customer'
   - Key: Object containing customer_Id.
   - UpdateExpression: 'SET details = :details'
   - ExpressionAttributeValues: { ':details': details }
   - ReturnValues: 'ALL_NEW'
- **Try to update data in DynamoDB using the `update` method.**
- **If successful:**
   - Return a response with status code 200 OK.
   - Include a message and the updated customer data in the response body.
- **If an error occurs:**
   - Return a response with status code 500 Internal Server Error.
   - Include an error message in the response body.

# DeleteCustomer Function

## Logic

- **Extract the value from the path parameters: customer_Id.**
- **If customer_Id is missing:**
   - Return a response with status code 400 Bad Request.
   - Include a message indicating that Customer ID is required.
- **Create a DynamoDB `params` object with the following:**
   - TableName: 'Customer'
   - Key: Object containing customer_Id.
- **Try to delete data from DynamoDB using the `delete` method.**
- **If successful:**
   - Return a response with status code 200 OK.
   - Include a success message in the response body.
- **If an error occurs:**
   - Return a response with status code 500 Internal Server Error.
   - Include an error message in the response body.
