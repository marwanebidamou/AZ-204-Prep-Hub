# Monitor and Analyze Metrics, Logs, and Traces

Azure Monitor, integrated with Application Insights, provides deep insights into your application's performance and health. This guide explores how to utilize Azure Monitor and Application Insights for monitoring and analyzing metrics, logs, and traces.

---

## Accessing Application Insights in Azure Monitor

1. **Navigate to Azure Monitor**:
   - Search for **Azure Monitor** in the Azure Portal.
   - Select **Insights > Applications**.

2. **Select Your Application**:
   - Choose the application you want to monitor.
   - Navigate to the **Application Insights** pane for detailed metrics and insights.

3. **Overview Dashboard**:
   - View high-level metrics such as:
     - Failed requests.
     - Server response time.
     - Availability.
     - Server requests.
   - Use the time range filter to zoom in on specific hours or days.

---

## Application Dashboard

- **Dashboard Creation**:
  - Click **Application Dashboard** from the overview pane.
  - Automatically creates a shared dashboard specific to the application.
  - Includes tiles for metrics, making it easy to monitor at a glance.

- **Shared Access**:
  - Share this dashboard with team members for collaborative monitoring.

---

## Monitoring Application Availability

### Setting Up Availability Tests

1. **Create a Test**:
   - Name the test (e.g., `test1`).
   - Specify the endpoint (e.g., homepage URL).
   - Configure the following options:
     - **Frequency**: 5, 10, or 15 minutes.
     - **Locations**: Select Azure Data Center locations.
     - **Request Type**: HTTP GET.
     - **Success Criteria**: HTTP status code 200.

2. **Alerts**:
   - Configure alert rules to notify when availability tests fail.

3. **Result Visualization**:
   - Availability metrics are plotted over time to monitor uptime and detect failures.

---

## Performance Analysis

1. **Performance Tab**:
   - View scatterplots showing response times for your application.
   - Example metrics:
     - Response times: 8ms, 10ms, etc.
     - Average response time.

2. **Live Metrics**:
   - Enables real-time monitoring of application performance.
   - Note: Requires additional setup if unavailable.

---

## Application Map

- Visualize application components and their interactions.
- Metrics include:
  - Node response times.
  - Number of calls to the application.
- Filter data by specific time periods for detailed analysis.

---

## Extending Application Insights

- **Auto-Instrumentation**:
  - Automatically collects metrics, requests, and dependencies without requiring code changes.
  - Supported platforms include .NET Framework, .NET Core, Java, Node.js, and some Python environments.

- **Manual Instrumentation**:
  - Use the Application Insights SDK to add custom telemetry for advanced monitoring needs.

---

## Summary

Application Insights within Azure Monitor provides robust tools for understanding application performance and availability. From setting up availability tests to analyzing detailed performance metrics, it empowers teams to identify and resolve issues proactively. Utilize auto-instrumentation or SDK-based customization depending on your application's platform and needs.
