
# Creating a Durable Function in Azure

This guide details the steps to create and test a durable function in Azure using Node.js. Durable Functions enable complex workflows with stateful orchestration, making them ideal for long-running or multi-step processes.

---

## Prerequisites
- **Azure Function App** with Durable Functions enabled.
- **Node.js** environment with npm access.
- Basic understanding of Azure Functions and orchestration patterns.

---

## Durable Functions Overview
Durable Functions consist of three key components:
1. **Client Function**: Initiates the durable workflow.
2. **Orchestrator Function**: Manages the sequence of tasks (traffic cop).
3. **Activity Function**: Performs specific tasks as part of the workflow.

---

## Steps to Create a Durable Function

### Step 1: Create the Client Function
The client function starts the durable workflow by calling the orchestrator function.

1. Go to the **Functions** section in the Azure portal.
2. Click **+ Add** to create a new function.
3. Search for **Durable Functions** templates.
4. Select the **Orchestration Client** template.
5. Configure the client:
   - **Name**: `StartFunction`
   - **Trigger**: HTTP
   - **Authorization**: Function-level key
6. Click **Add** to create the function.

### Code for Client Function
The client function starts the orchestrator function:
```javascript
const df = require("durable-functions");

module.exports = async function (context, req) {
    const client = df.getClient(context);
    const instanceId = await client.startNew(req.params.functionName, undefined, req.body);

    context.log(`Started orchestration with ID = '${instanceId}'.`);

    return client.createCheckStatusResponse(context.bindingData.req, instanceId);
};
```

---

### Step 3: Create the Orchestrator Function
The orchestrator manages the workflow by calling activity functions.

1. Add a new function and select the **Orchestration** template.
2. Name the function `OrchestratorFunction`.
3. Modify the orchestrator code:
   ```javascript
   const df = require("durable-functions");

   module.exports = df.orchestrator(function* (context) {
       const outputs = [];
       outputs.push(yield context.df.callActivity("ActivityFunction", "How are you?"));
       outputs.push(yield context.df.callActivity("ActivityFunction", "What is your name?"));
       outputs.push(yield context.df.callActivity("ActivityFunction", "What do you do?"));
       return outputs;
   });
   ```

---

### Step 4: Create the Activity Function
The activity function performs the tasks specified by the orchestrator.

1. Add a new function and select the **Activity** template.
2. Name the function `ActivityFunction`.
3. Modify the activity function code:
   ```javascript
   module.exports = async function (context) {
       const question = context.bindings.questionText;
       return `Response to "${question}"`;
   };
   ```

4. Update `function.json`:
   ```json
   {
       "bindings": [
           {
               "name": "questionText",
               "type": "activityTrigger",
               "direction": "in"
           }
       ]
   }
   ```

---

## Testing the Durable Function

### Step 1: Trigger the Client Function
1. Navigate to **StartFunction**.
2. Click **Get Function URL** and copy the URL.
3. Append the orchestrator function name as a query parameter:
   ```
   ?functionName=OrchestratorFunction
   ```
4. Use a tool like Postman or a browser to send an HTTP POST request to the function.

### Step 2: Monitor the Orchestrator
1. Use the `createCheckStatusResponse` URLs from the client response to:
   - Check the status of the orchestration.
   - Retrieve the output after completion.

### Sample Output
```json
{
    "instanceId": "abcd1234",
    "runtimeStatus": "Completed",
    "output": [
        "Response to 'How are you?'",
        "Response to 'What is your name?'",
        "Response to 'What do you do?'"
    ]
}
```

---

## Key Features
- **Stateful Workflows**: Orchestrator remembers the state across multiple activity calls.
- **Parallel Execution**: Combine multiple activities using fan-out and fan-in patterns.
- **Long-Running Workflows**: Durable functions can handle workflows spanning days, weeks, or even months.

---

## Additional Resources
- [Azure Durable Functions Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview)
- [Orchestrator and Activity Function Examples](https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-types)
