
# Azure Durable Functions Guide

## Prerequisites
- An active Azure account.
- Basic knowledge of Azure Functions.
- Familiarity with Node.js and npm (Node Package Manager).

---

## Setting Up Durable Functions

### Step 1: Create or Access Your Function App
1. Log in to the Azure portal.
2. Navigate to your **Function App**.
3. In the **Development Tools** section, select **App Service Editor**.

### Step 2: Open App Service Editor
- The App Service Editor provides a Visual Studio Code-like environment.
- In the editor, locate the `wwwroot` folder. This contains all the files for your Function App, including existing HTTP and Timer trigger functions.

### Step 3: Create `package.json`
1. Open the **Console** from the development tools.
2. Navigate to the `wwwroot` directory:
   ```bash
   cd wwwroot
   ```
3. Create a `package.json` file:
   ```bash
   touch package.json
   ```
4. Open the `package.json` file in the editor and add the following minimal configuration:
   ```json
   {
       "name": "my-function-app",
       "version": "1.0.0"
   }
   ```
5. Save the file.

---

### Step 4: Install Durable Functions
1. In the console, install the `durable-functions` npm package:
   ```bash
   npm install durable-functions
   ```
2. Verify the installation by checking your `package.json` file:
   ```json
   {
       "name": "my-function-app",
       "version": "1.0.0",
       "dependencies": {
           "durable-functions": "^x.x.x"
       }
   }
   ```
3. Ensure a `node_modules` folder is created in the `wwwroot` directory, which contains the installed dependencies.

---

## Building Your First Durable Function

### Define an Orchestrator Function
1. Create a new file, `orchestrator.js`:
   ```bash
   touch orchestrator.js
   ```
2. Add the following code:
   ```javascript
   const df = require("durable-functions");

   module.exports = df.orchestrator(function* (context) {
       const outputs = [];
       outputs.push(yield context.df.callActivity("Hello", "Tokyo"));
       outputs.push(yield context.df.callActivity("Hello", "Seattle"));
       outputs.push(yield context.df.callActivity("Hello", "London"));

       return outputs;
   });
   ```

### Define an Activity Function
1. Create a new file, `activity.js`:
   ```bash
   touch activity.js
   ```
2. Add the following code:
   ```javascript
   module.exports = async function (context) {
       return `Hello, ${context.bindings.name}!`;
   };
   ```

---

## Testing Your Durable Functions
1. Deploy your changes to Azure.
2. Trigger the orchestrator function via HTTP or other supported triggers.
3. Monitor execution using Azure Monitor or Application Insights.

---

## Additional Resources
- [Azure Durable Functions Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview)
- [Node.js and Durable Functions Sample Code](https://github.com/Azure/azure-functions-durable-js)

---
