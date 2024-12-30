
# Azure Functions Timer Trigger

Azure Functions' timer trigger allows you to execute functions on a predefined schedule, making it ideal for tasks like periodic data cleanup or regular report generation.

## Creating a Timer Trigger Function

1. **Add a New Function**:
   - In your Function App, navigate to the **Functions** section and select **Create**.
   - Choose **Develop in portal** and select the **Timer trigger** template.

2. **Configure the Timer Trigger**:
   - **Function Name**: Assign a meaningful name to your function.
   - **Schedule**: Define the execution schedule using a CRON expression.

## Understanding CRON Expressions

CRON expressions in Azure Functions follow the format:

```
{second} {minute} {hour} {day} {month} {day-of-week}
```

For example, to run a function every five minutes:

```
0 */5 * * * *
```

This expression signifies:

- **Second**: `0` (at the start of the minute)
- **Minute**: Every 5 minutes (`*/5`)
- **Hour**, **Day**, **Month**, **Day-of-Week**: Every time (`*`)

For more details on CRON expressions, refer to the [Timer trigger for Azure Functions documentation](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer).

## Sample Function Code

Here's a basic example of a timer-triggered function in JavaScript:

```javascript
module.exports = async function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if (myTimer.isPastDue) {
        context.log('Timer function is running late!');
    }

    context.log('Timer trigger function ran at', timeStamp);
};
```

In this function, `myTimer.isPastDue` checks if the function is running later than scheduled, which can occur if a previous execution was delayed.

## Testing the Timer Trigger Function

Since timer-triggered functions execute based on the defined schedule, manual testing can be challenging. To facilitate testing:

- **Modify the Schedule**: Temporarily set the CRON expression to a short interval (e.g., every minute) during development.
- **Manual Invocation**: You can manually trigger the function using administrative tools or APIs. For guidance, see [Manually run a non HTTP-triggered function](https://learn.microsoft.com/en-us/azure/azure-functions/functions-manually-run-non-http).

## Monitoring and Logs

Azure Functions provides monitoring tools to track executions:

- **Invocations Tab**: View recent function invocations and their outcomes.
- **Application Insights**: If configured, offers detailed telemetry data.

For comprehensive monitoring capabilities, refer to the [Azure Functions monitoring documentation](https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitoring).

## Additional Resources

- [Timer trigger for Azure Functions](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer)
- [Azure Functions Node.js developer guide](https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node)

