# Understanding Azure Durable Functions

Azure Durable Functions extend Azure Functions by enabling the creation of stateful, long-running workflows within a serverless environment. This capability allows developers to define complex orchestrations and manage state without provisioning or managing infrastructure.

## Key Concepts

### 1. Stateless vs. Stateful Functions

- **Stateless Functions**: Traditional Azure Functions are stateless, designed to execute a specific task quickly in response to a trigger (e.g., HTTP request, timer, blob creation). They are short-lived and do not maintain state between executions.

- **Stateful Functions**: Durable Functions introduce statefulness, allowing functions to maintain context and state across multiple executions. This is essential for implementing complex workflows that require tracking progress over time.

### 2. Durable Functions Components

Durable Functions comprise three primary components:

- **Client Function**: Initiates the workflow, typically triggered by an external event such as an HTTP request or a timer.

- **Orchestrator Function**: Manages the workflow's control flow, determining the sequence of activities and maintaining state. It can call other functions and manage their execution order.

- **Activity Function**: Performs discrete tasks within the workflow, such as calling external APIs, processing data, or interacting with storage services.

## Durable Functions Patterns

Durable Functions support several patterns for building complex workflows:

### 1. Function Chaining

In this pattern, functions execute sequentially, with each function's output serving as the input for the next. The orchestrator ensures that each function completes before the next begins.

![Function chaining](https://learn.microsoft.com/en-us/azure/azure-functions/durable/media/durable-functions-concepts/function-chaining.png " Function chaining")

```csharp
[FunctionName("Chaining")]
public static async Task<object> Run(
    [OrchestrationTrigger] IDurableOrchestrationContext context)
{
    try
    {
        var x = await context.CallActivityAsync<object>("F1", null);
        var y = await context.CallActivityAsync<object>("F2", x);
        var z = await context.CallActivityAsync<object>("F3", y);
        return  await context.CallActivityAsync<object>("F4", z);
    }
    catch (Exception)
    {
        // Error handling or compensation goes here.
    }
}
```

### 2. Fan-Out/Fan-In

This pattern involves executing multiple functions in parallel (fan-out) and then aggregating their results (fan-in). The orchestrator waits for all parallel tasks to complete before proceeding.
![ Fan out/fan in](https://learn.microsoft.com/en-us/azure/azure-functions/durable/media/durable-functions-concepts/fan-out-fan-in.png " Fan out/fan in")
```csharp
[FunctionName("FanOutFanIn")]
public static async Task Run(
    [OrchestrationTrigger] IDurableOrchestrationContext context)
{
    var parallelTasks = new List<Task<int>>();

    // Get a list of N work items to process in parallel.
    object[] workBatch = await context.CallActivityAsync<object[]>("F1", null);
    for (int i = 0; i < workBatch.Length; i++)
    {
        Task<int> task = context.CallActivityAsync<int>("F2", workBatch[i]);
        parallelTasks.Add(task);
    }

    await Task.WhenAll(parallelTasks);

    // Aggregate all N outputs and send the result to F3.
    int sum = parallelTasks.Sum(t => t.Result);
    await context.CallActivityAsync("F3", sum);
}
```

### 3. Asynchronous HTTP APIs

Durable Functions can manage long-running operations by providing an endpoint that clients can poll to check the status of an operation, allowing for asynchronous processing without client-side timeouts.

![Async HTTP APIs](https://learn.microsoft.com/en-us/azure/azure-functions/durable/media/durable-functions-concepts/async-http-api.png "Async HTTP APIs")


### 4. Monitor Pattern

This pattern implements a recurring process in a workflow, such as polling for a condition to be met. The orchestrator can wait, check the condition, and repeat as necessary.

![Monitor](https://learn.microsoft.com/en-us/azure/azure-functions/durable/media/durable-functions-concepts/monitor.png
"Monitor")

```csharp
[FunctionName("MonitorJobStatus")]
public static async Task Run(
    [OrchestrationTrigger] IDurableOrchestrationContext context)
{
    int jobId = context.GetInput<int>();
    int pollingInterval = GetPollingInterval();
    DateTime expiryTime = GetExpiryTime();

    while (context.CurrentUtcDateTime < expiryTime)
    {
        var jobStatus = await context.CallActivityAsync<string>("GetJobStatus", jobId);
        if (jobStatus == "Completed")
        {
            // Perform an action when a condition is met.
            await context.CallActivityAsync("SendAlert", jobId);
            break;
        }

        // Orchestration sleeps until this time.
        var nextCheck = context.CurrentUtcDateTime.AddSeconds(pollingInterval);
        await context.CreateTimer(nextCheck, CancellationToken.None);
    }

    // Perform more work here, or let the orchestration end.
}
```

### 5. Human Interaction

Workflows often require human input or approval. Durable Functions can pause execution, waiting for an external event (e.g., an approval) before continuing.

![ Human Interaction](https://learn.microsoft.com/en-us/azure/azure-functions/durable/media/durable-functions-concepts/approval.png " Human Interaction")

```csharp
[FunctionName("ApprovalWorkflow")]
public static async Task Run(
    [OrchestrationTrigger] IDurableOrchestrationContext context)
{
    await context.CallActivityAsync("RequestApproval", null);
    using (var timeoutCts = new CancellationTokenSource())
    {
        DateTime dueTime = context.CurrentUtcDateTime.AddHours(72);
        Task durableTimeout = context.CreateTimer(dueTime, timeoutCts.Token);

        Task<bool> approvalEvent = context.WaitForExternalEvent<bool>("ApprovalEvent");
        if (approvalEvent == await Task.WhenAny(approvalEvent, durableTimeout))
        {
            timeoutCts.Cancel();
            await context.CallActivityAsync("ProcessApproval", approvalEvent.Result);
        }
        else
        {
            await context.CallActivityAsync("Escalate", null);
        }
    }
}
```

## Benefits of Durable Functions

- **State Management**: Automatically manages state, eliminating the need for external storage or complex state management code.

- **Long-Running Workflows**: Supports workflows that can run for extended periods, beyond the typical timeout limits of standard functions.

- **Error Handling and Compensation**: Provides robust error handling and the ability to define compensation logic to revert or mitigate the effects of failed operations.

- **Scalability**: Inherits the scalability of Azure Functions, automatically scaling out to meet demand.

## Considerations

- **Deterministic Code**: Orchestrator functions must be deterministic; they should produce the same output given the same input and should not perform I/O operations directly.

- **Latency**: While Durable Functions manage state efficiently, there may be some latency due to state persistence and retrieval.

- **Pricing**: Billing is based on the execution time and resource consumption of the functions, so long-running workflows may incur higher costs.

## Getting Started

To begin using Durable Functions:

1. **Install the Durable Functions Extension**: Ensure your Azure Functions project includes the Durable Functions extension.

2. **Define Functions**: Create client, orchestrator, and activity functions as per your workflow requirements.

3. **Deploy and Monitor**: Deploy your functions to Azure and use the Azure portal to monitor executions and diagnose issues.

For detailed guidance and tutorials, refer to the [official Azure Durable Functions documentation][1].

[1]: https://learn.microsoft.com/en-us/azure/azure-functions/durable/
