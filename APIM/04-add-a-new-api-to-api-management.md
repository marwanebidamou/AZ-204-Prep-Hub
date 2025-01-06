# Adding a New API to Azure API Management

Azure API Management (APIM) enables you to add, manage, and secure APIs efficiently. This guide demonstrates how to add a new API to APIM using an Azure Function as the backend. By following these steps, you can integrate your APIs seamlessly into the APIM ecosystem and take advantage of its robust features.

---

## Step-by-Step Guide to Adding a New API

### 1. **Navigate to API Management**
1. Open the Azure Portal.
2. Navigate to your API Management instance.
3. Click on **APIs** in the left-hand menu.
4. Click **Add API** to start adding a new API.

### 2. **Choose the API Type**
APIM supports various API types. Choose the one that fits your scenario:

- **HTTP**: Create a new API with custom configuration.
- **WebSocket**: For real-time, bidirectional communication.
- **GraphQL**: For managing GraphQL APIs.
- **OpenAPI Specification**: Import an existing API specification.
- **Logic Apps, Function Apps, App Services, or Container Apps**: Directly connect existing Azure resources.

### 3. **Add an Azure Function App API**
1. **Select Function App**:
   - From the API type selection, choose **Function App**.
   - Click **Browse** to search for your Function App.
   - Select the Function App you want to integrate.

2. **Select Functions**:
   - A list of available functions in the selected Function App will appear.
   - Choose the functions to include in the API.
   - Click **Select** to proceed.

3. **Provide API Details**:
   - **Name**: Enter a meaningful name for your API.
   - **API URL Suffix**: Define the suffix for the API endpoint (e.g., `my-api`).
   - **API Version** (optional): Specify if this is a new version of an existing API.

4. Click **Create** to finalize the API addition.

### 4. **Define API Operations**
1. Navigate to the newly created API.
2. Select an operation (e.g., `GET` or `POST`).
3. Define operation details:
   - **Name**: Give the operation a meaningful name.
   - **Request Parameters**:
     - Add query or header parameters as needed.
     - Define parameter types (e.g., `string`, `integer`).
     - Mark required parameters if applicable.
   - **Response**: Configure expected response codes and content types.

4. Save your changes.

### 5. **Test the API**
1. Navigate to the **Test** tab.
2. Select the operation to test (e.g., `GET`).
3. Provide required parameters and headers.
4. Click **Send** to execute the request.
5. Review the response details, including status codes and payloads.

---

## Benefits of Adding APIs to APIM
1. **Unified Management**: Aggregate multiple APIs into a single platform.
2. **Secure Exposure**: Leverage authentication, throttling, and IP filtering.
3. **Scalability**: Handle growing demand with APIM’s performance features.
4. **Enhanced Documentation**: Automatically generate and publish API documentation.
5. **Monitoring and Analytics**: Use built-in tools to monitor API usage and performance.

---

## Example: Testing an API

### Scenario
- You’ve added a Function App API.
- The `GET /resource` operation requires a query parameter `name`.

### Steps
1. Go to the **Test** tab of the API.
2. Enter the query parameter:
   - **Name**: `name`
   - **Value**: `Scott`
3. Click **Send**.
4. Verify the response:
   - Status Code: `200 OK`
   - Response Body: `{ "message": "Hello, Scott" }`

---

## Best Practices
1. **Use Meaningful Names**:
   - Ensure APIs and operations have clear, descriptive names.
2. **Define Parameters Clearly**:
   - Specify all required parameters and provide defaults where applicable.
3. **Secure APIs**:
   - Implement authentication and IP filtering policies.
4. **Test Extensively**:
   - Use the Test tab and external tools like Postman for robust testing.
5. **Monitor Usage**:
   - Enable metrics and diagnostics to track performance and troubleshoot issues.

---

## Conclusion
Adding APIs to Azure API Management streamlines API lifecycle management, ensuring scalability, security, and usability. By integrating services like Function Apps and applying APIM features, you can optimize the API experience for developers and end-users alike.

