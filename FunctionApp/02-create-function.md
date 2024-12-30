# Creating an Azure Function with an HTTP Trigger

Azure Functions enable serverless computing, allowing you to execute code in the cloud without managing infrastructure. This guide explains how to create a simple HTTP-triggered function directly in the Azure portal.

## Steps to Create an Azure Function

### 1. **Create a Function App**
   - Navigate to the Azure portal and create a Function App.
   - Once created, go to the resource overview for details, including the app's URL.

### 2. **Navigate to the Functions Section**
   - Select the **Functions** option under your Function App.
   - Click on **Create** to start adding a new function.

### 3. **Select a Development Option**
   Azure provides various development options:
   - **In-portal development** (used in this guide).
   - Local development with Visual Studio Code, Visual Studio, or other editors, which you can later publish to Azure.

### 4. **Choose a Template**
   - Azure Functions offers templates for different trigger types. Common triggers include:
     - **HTTP request** (used in this guide).
     - Timer trigger (scheduled functions).
     - Storage queue or blob triggers.
     - Cosmos DB document changes, etc.
   - Select the **HTTP trigger** template.

### 5. **Configure the Function**
   - Provide a function name (e.g., `MyFirstFunction`).
   - Set the authorization level (e.g., Function, Admin, or Anonymous).
   - Click **Create** to generate the function.

### 6. **Review Function Code**
   - After creation, the portal provides default function code and configuration files. You can edit them as needed.

---

## Example: HTTP-Triggered Function

This example demonstrates a simple HTTP-triggered Azure Function that responds with a personalized message.

### Default `index.js` Code
```javascript
module.exports = async function (context, req) {
    context.log('HTTP trigger function processed a request.');

    const name = req.query.name || (req.body && req.body.name);
    const responseMessage = name
        ? `Hello, ${name}. This HTTP triggered function executed successfully.`
        : "This HTTP triggered function executed successfully. Please pass a name in the query string or in the request body.";

    context.res = {
        // status: 200, /* Defaults to 200 */
        body: responseMessage
    };
};
```

### Default `function.json` Configuration
```json
{
    "bindings": [
        {
            "authLevel": "function",
            "type": "httpTrigger",
            "direction": "in",
            "name": "req",
            "methods": ["get", "post"]
        },
        {
            "type": "http",
            "direction": "out",
            "name": "res"
        }
    ]
}
```

### Testing the Function

1. **Get the Function URL**
   - Go to the function in the Azure portal.
   - Select **Get Function URL** and copy it.

2. **Run in Browser or Postman**
   - For a GET request: Append `?name=YourName` to the URL and paste it into your browser.
   - For a POST request: Use a tool like Postman to send a JSON body (e.g., `{ "name": "YourName" }`).

3. **Expected Output**
   - Without a name: 
     ```
     This HTTP triggered function executed successfully. Please pass a name in the query string or in the request body.
     ```
   - With a name:
     ```
     Hello, YourName. This HTTP triggered function executed successfully.
     ```

---

## Key Concepts

### Triggers
Triggers define how a function is invoked. Examples include:
- **HTTP Trigger**: Responds to HTTP requests.
- **Timer Trigger**: Executes on a schedule.
- **Queue Trigger**: Listens for messages in a queue.

### Bindings
Bindings are declarative ways to interact with other Azure services.
- **Input Binding**: Reads data (e.g., blob storage file).
- **Output Binding**: Writes data (e.g., sends a message to a queue).

---

## Notes
- HTTP-triggered functions can be configured for different security levels:
  - **Anonymous**: No authentication required.
  - **Function**: Requires a function key.
  - **Admin**: Requires an admin key.

- Azure Functions operate on a consumption plan, allowing up to 1 million free executions per month.

- This simple example can be extended to integrate with services like Blob Storage, Cosmos DB, or queues to build powerful workflows.
