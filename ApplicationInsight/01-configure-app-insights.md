# Configuring an Application to Use Application Insights

Azure Application Insights is a powerful extension of Azure Monitor that provides Application Performance Management (APM) features. It helps developers monitor applications across development, testing, and production stages, providing detailed telemetry, metrics, and live monitoring capabilities.

---

## What is Application Insights?

### Key Features
- **Application Performance Monitoring**:
  - Understand how your application performs in real-time.
  - Track errors, incidents, and anomalies.
- **Detailed Telemetry**:
  - Get metrics on requests, dependencies, and live metrics.
  - Understand user behavior, popular features, and usage patterns.
- **Integration with DevOps**:
  - Works with GitHub and Azure DevOps for deployment tracking.
- **Availability Monitoring**:
  - Detects application failures and helps pinpoint issues.
- **Autoinstrumentation**:
  - Automatically collects telemetry without requiring code changes (supported for specific platforms).

### Supported Environments for Autoinstrumentation
- **Languages**:
  - .NET Framework, .NET Core/.NET, Java, Node.js, and Python.
- **Deployment Scenarios**:
  - App Services (Windows/Linux), Docker (Linux), Virtual Machines, and Azure Kubernetes Service (AKS).
- **Limitations**:
  - Certain platforms and deployment types may not support autoinstrumentation (e.g., .NET Core in Docker on Linux).

---

## Steps to Enable and Use Application Insights

### 1. **Enable Application Insights During Resource Creation**
- When creating a resource (e.g., a Web App), navigate to the **Monitoring** section.
- Ensure **Application Insights** is enabled (default setting).
- Choose an existing Application Insights resource or create a new one.

### 2. **Enable Application Insights for Existing Applications**
1. Navigate to your resource in the Azure Portal.
2. Under the **Monitoring** section, select **Application Insights**.
3. Enable it and associate it with an existing or new Application Insights resource.

### 3. **Integrating Application Insights SDK**
- Add the Application Insights SDK to your application for custom telemetry:
  1. In Visual Studio, open **NuGet Package Manager**.
  2. Search for and install `Microsoft.ApplicationInsights.Web`.
  3. Use the SDK to track custom events, metrics, and telemetry in your code.

```csharp
using Microsoft.ApplicationInsights;

var telemetryClient = new TelemetryClient();
telemetryClient.TrackEvent("Custom Event");
telemetryClient.TrackMetric("Custom Metric", value);
telemetryClient.TrackException(exception);
```

### 4. **Deploying a Web App with Application Insights**
1. Create a new .NET Core Web App in Visual Studio.
2. Build the solution.
3. Publish to Azure:
   - Choose **App Service** as the target.
   - Select the app service resource created earlier.
   - Deploy the application.

---

## Viewing Application Insights Metrics

Once the application is deployed:

1. Navigate to the **Application Insights** resource linked to your app in the Azure Portal.
2. Explore the following insights:
   - **Live Metrics**: Monitor application performance in real-time.
   - **Failures**: View error logs and track exceptions.
   - **Usage Analytics**: Understand how users interact with your application.
   - **Performance Metrics**: Analyze dependency performance, request rates, and response times.
3. Use the **Application Map** to visualize the flow of requests and dependencies in your app.

---

## Summary
Application Insights integrates seamlessly with Azure resources, providing powerful monitoring and diagnostic capabilities. Whether using autoinstrumentation or integrating the SDK for custom telemetry, Application Insights is an invaluable tool for understanding and improving application performance.
