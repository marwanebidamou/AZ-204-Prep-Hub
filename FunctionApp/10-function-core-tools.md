
# Using Azure Function Core Tools

This document provides step-by-step guidance for creating, testing, and deploying Azure Functions using Azure Function Core Tools.

---

## Overview
Azure Function Core Tools allow developers to:
- Create, test, and manage Azure Functions locally or within the Azure Cloud Shell.
- Work with various function templates (HTTP triggers, Durable Functions, Blob storage, etc.).
- Deploy Azure Functions to the Azure platform directly.

---

## Prerequisites
- Installed Azure Function Core Tools on your local machine or access to the Azure Cloud Shell.
- An active Azure account.
- Basic knowledge of JavaScript and Azure Functions.

---

## Setting Up a Local Function

### Step 1: Create a Project Directory
1. Create a directory for your function:
   ```bash
   mkdir my-test-function
   cd my-test-function
   ```

### Step 2: Initialize the Directory
1. Use the `func init` command to initialize the directory:
   ```bash
   func init
   ```
2. Choose the runtime environment when prompted (e.g., JavaScript).

### Step 3: Create a Function
1. Create a new function:
   ```bash
   func new
   ```
2. Choose a template from the list (e.g., HTTP trigger).
3. Name your function (e.g., `DemoFunction`).

---

## Testing Functions Locally

### Step 1: Start the Local Server
1. Start the function runtime locally:
   ```bash
   func start
   ```
2. The function will be available at `http://localhost:7071`.

### Step 2: Test the Function
1. Use `curl` to test the function:
   ```bash
   curl http://localhost:7071/api/DemoFunction?name=YourName
   ```
2. Verify the response:
   ```
   Hello YourName, this HTTP triggered function executed successfully.
   ```

---

## Deploying Functions to Azure

### Step 1: Create an Azure Function App
1. Use the Azure CLI to create a function app:
   ```bash
   az functionapp create --resource-group <ResourceGroupName>      --consumption-plan-location <Location>      --runtime node      --name <FunctionAppName>      --storage-account <StorageAccountName>
   ```

### Step 2: Publish the Function
1. Deploy the function to Azure:
   ```bash
   func azure functionapp publish <FunctionAppName>
   ```

---

## Additional Features

### Debugging Functions
- Use the `func start` command to debug locally.
- Integrate with Visual Studio Code for enhanced debugging capabilities.

### Using Logs
- View logs in the Azure portal under the **Monitor** section of your Function App.
- Access real-time logs locally using the Core Tools.

---

## Notes
- **Cloud Shell Access:** All commands can be executed within the Azure Cloud Shell without additional installation.
- **Asynchronous Operations:** Use the `&` symbol to run background processes and maintain access to the terminal.

---

## Additional Resources
- [Azure Functions Core Tools Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/functions-run-local)
- [Azure CLI Documentation](https://learn.microsoft.com/en-us/cli/azure/)
