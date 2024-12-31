# Adding Delays to Functions Using `moment` in Node.js

This document explains how to add delays to orchestrated durable functions in Node.js by leveraging the `moment` module.

---

## Prerequisites
- A working Azure Function App set up with Durable Functions.
- Node.js environment with npm access.
- Basic understanding of orchestrator functions in Azure Durable Functions.

---

## Overview
Adding delays between steps in a durable function allows for precise control over the timing of task execution. Using the `moment` library, we can create timers in orchestrator functions. This ensures that resources are released while the function waits, optimizing performance and costs.

---

## Steps to Add Delays

### Step 1: Install `moment`
1. Open the Azure portal and navigate to your **Function App**.
2. Scroll down to **Development Tools** and open the **Console**.
3. Install the `moment` library:
   ```bash
   npm install moment
   ```
4. Optionally, install `typescript` for additional benefits:
   ```bash
   npm install typescript
   ```

### Step 2: Update the Orchestrator Function
1. Navigate to the **Code + Test** section of your orchestrator function.
2. Include the `moment` module by requiring it:
   ```javascript
   const moment = require("moment");
   ```

3. Modify the orchestrator code to include delays:
   ```javascript
   const df = require("durable-functions");
   const moment = require("moment");

   module.exports = df.orchestrator(function* (context) {
       const outputs = [];

       // Add first step
       outputs.push(yield context.df.callActivity("AskQuestion", "How are you?"));

       // Wait for 1 hour
       const firstDeadline = moment.utc().add(1, 'hours').toDate();
       yield context.df.createTimer(firstDeadline);

       // Add second step
       outputs.push(yield context.df.callActivity("AskQuestion", "What is your name?"));

       // Wait for 1 more hour
       const secondDeadline = moment.utc().add(1, 'hours').toDate();
       yield context.df.createTimer(secondDeadline);

       // Add third step
       outputs.push(yield context.df.callActivity("AskQuestion", "What do you do?"));

       return outputs;
   });
   ```

### Step 3: Key Points About `createTimer`
- **Resource Optimization:** 
  The `createTimer` function allows Azure to hibernate the orchestrator and release resources until the timer completes.
- **Syntax:** 
  - **Node.js:** `context.df.createTimer(date)`
  - **C#:** `context.createTimer(date)`
  - **Python:** `context.create_timer(date)`

- **Avoid Blocking Code:**
  Do not use blocking functions like `setTimeout` or `sleep` as they consume resources unnecessarily.

### Step 4: Deploy and Test
1. Deploy the modified orchestrator function to Azure.
2. Trigger the function using the appropriate client.
3. Monitor the function's execution in **Monitor** or **Application Insights**.

---

## Notes
- **Maximum Function Duration:**
  Azure Durable Functions now support long-running orchestrations without a fixed duration limit, enabling workflows that span days, weeks, or even months.
- **State Management:**
  Durable functions manage state seamlessly, even during extended delays, ensuring consistent execution.

---

## Additional Resources
- [Azure Durable Functions Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-overview)
- [Moment.js Documentation](https://momentjs.com/)
