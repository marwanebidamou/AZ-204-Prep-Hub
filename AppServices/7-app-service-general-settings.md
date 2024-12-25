# Azure App Service General Settings

Azure App Service provides a range of configurable settings to manage the behavior and environment of your web applications. These settings can be accessed and modified through the Azure Portal under the **Configuration** section of your App Service.

## Accessing General Settings

1. **Navigate to Your App Service**:
   - In the [Azure Portal](https://portal.azure.com), go to **App Services** and select your app.

2. **Open Configuration**:
   - In the left-hand menu, select **Configuration**.

3. **General Settings Tab**:
   - Within the **Configuration** page, select the **General settings** tab.

## Configurable Settings

### Stack Settings

Define the runtime stack and version for your application:

- **.NET Versions**:
  - Choose from multiple versions, including .NET 6, .NET 5, .NET Core, and ASP.NET 4.

- **Platform Architecture**:
  - Select between 32-bit and 64-bit architectures.

- **Managed Pipeline Mode**:
  - Options include **Integrated** and **Classic**, similar to IIS settings.

### Debugging and Monitoring

- **Remote Debugging**:
  - Enable to attach Visual Studio for remote debugging sessions.
  - Note: Remote debugging should be used temporarily and turned off when not in use for security reasons.

- **Web Sockets**:
  - Enable or disable Web Sockets support for real-time applications.

- **Always On**:
  - Keep the app loaded even when idle to reduce cold start times.

### Security Settings

- **HTTPS Only**:
  - Redirect all HTTP requests to HTTPS to ensure secure communication.

- **TLS Version**:
  - Specify the minimum TLS version (e.g., TLS 1.2) for secure connections.

- **Client Certificate Mode**:
  - Configure client certificate requirements for incoming requests.

### Session Affinity

- **ARR Affinity**:
  - Enable or disable Application Request Routing (ARR) Affinity, which ensures a user's session is consistently routed to the same instance.

### Default Documents

Specify the default documents that the app service looks for when a request is made to the root URL.

- **Configuration**:
  - Add or remove default documents and set their priority order.

### Virtual Applications and Directories

Map virtual paths to physical directories within your app or to external storage:

- **Virtual Directories**:
  - Create virtual directories that map to physical paths in your app.

- **Virtual Applications**:
  - Define virtual applications with their own configuration settings.

### Handler Mappings

Customize how specific file extensions or URLs are processed by the server:

- **Configuration**:
  - Add custom script processors to handle requests for specific file extensions.

## Application and Connection Strings

Manage application settings and connection strings securely:

- **Application Settings**:
  - Define key-value pairs that are injected into your application’s environment variables.
  - These settings override configurations in your application's configuration files, providing a secure way to manage sensitive information.

- **Connection Strings**:
  - Configure database connection strings that your application can use.
  - These are encrypted at rest and can be managed separately from your application code.

For more detailed information, refer to the official Azure documentation on [App Service Configuration](https://learn.microsoft.com/en-us/azure/app-service/configure-common).

 
