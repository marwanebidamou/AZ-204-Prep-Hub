# Auto Scaling Azure App Service

Auto scaling in Azure App Service enables your application to automatically adjust its resources to meet varying demand, ensuring optimal performance and cost efficiency.

## Scaling Up vs. Scaling Out

- **Scaling Up**: Upgrading to a higher pricing tier (e.g., from S1 to S2) to access more CPU, memory, and features. This approach has a maximum limit based on the highest available tier. 

- **Scaling Out**: Adding more instances of your app within the same pricing tier to distribute load. This method offers greater flexibility and can handle increased traffic more effectively.

## Manual Scaling

You can manually adjust the number of instances for your app:

1. **Navigate to your App Service in the Azure Portal**.

2. **Select "Scale out (App Service plan)"** from the left-hand menu.

3. **Use the slider** to set the desired number of instances.

4. **Click "Save"** to apply the changes.

This approach is straightforward but requires manual intervention to adjust to traffic changes.

## Automatic Scaling

Automatic scaling adjusts the number of instances based on predefined rules or schedules, ensuring your app responds to demand fluctuations without manual input.

### Enabling Automatic Scaling

1. **Navigate to your App Service in the Azure Portal**.

2. **Select "Scale out (App Service plan)"** from the left-hand menu.

3. **Choose "Automatic"**.

4. **Set the "Maximum burst" value** to define the upper limit of instances. 

5. **Click "Save"** to apply the settings.

### Configuring Auto-Scale Rules

You can define rules based on metrics such as CPU usage, memory usage, or request queue length:

1. **In the "Scale out" settings**, select "Add a rule".

2. **Choose a metric** (e.g., CPU Percentage).

3. **Set the condition** (e.g., "Greater than 70%").

4. **Define the action** (e.g., "Increase count by 1").

5. **Set the cooldown period** to prevent rapid scaling actions.

6. **Add a corresponding scale-in rule** to decrease instances when demand drops.

7. **Click "Add"**, then "Save" to apply the rules.

### Scheduling Auto-Scale

For predictable workloads, you can schedule scaling:

1. **In the "Scale out" settings**, select "Add a scale condition".

2. **Define the time range** and days.

3. **Set the minimum and maximum instance counts** for this period.

4. **Click "Add"**, then "Save" to apply the schedule.

## Considerations

- **Resource Limits**: Ensure that connected resources (e.g., databases) can handle the increased load when scaling out. Automatic scaling allows you to set the maximum number of instances your App Service Plan can scale to, helping to prevent overwhelming backend systems.

- **Instance Warm-Up**: Use pre-warmed instances to reduce cold start times during scaling. Pre-warmed instances act as a buffer during HTTP scale and activation events.

- **Pricing**: Be aware that scaling out increases costs linearly with the number of instances. For example, if your App Service Plan costs $0.20/hour for one instance, scaling out to two instances would cost $0.40/hour.

## Additional Resources

- [How to enable automatic scaling - Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/manage-automatic-scaling)

- [Scale up features and capacities - Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/manage-scale-up)

- [Azure App Service Automatic Scaling](https://techcommunity.microsoft.com/blog/appsonazureblog/azure-app-service-automatic-scaling/2983300)
