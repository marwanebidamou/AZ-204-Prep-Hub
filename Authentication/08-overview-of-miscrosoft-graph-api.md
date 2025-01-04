# Working with Microsoft Graph API

Microsoft Graph API provides a unified REST API and client libraries to interact programmatically with Microsoft Cloud services. It enables developers to access resources and build solutions leveraging Microsoft 365, Azure Active Directory, and other related services.

![Microsoft Graph](https://learn.microsoft.com/en-us/graph/images/microsoft-graph.png "Microsoft Graph")
---

## Overview of Microsoft Graph

### Supported Services
- **Microsoft 365:**
  - Access email, calendars, contacts, and Office suite features.
- **Azure Active Directory:**
  - Manage users, groups, and roles programmatically.
- **Security Services:**
  - Leverage threat analytics and advanced threat protection.
- **Other Services:**
  - Dynamics 365, Intune, and Windows services.

### Use Cases
- **User Management:**
  - Query and manage users and their relationships within Azure AD.
- **Calendar and Email:**
  - Automate workflows using Outlook emails, contacts, and calendar events.
- **Dynamic Relationships:**
  - Explore relationships between entities like users, groups, and resources using the "graph" concept.

---

## Setting Up Microsoft Graph API in Visual Studio

### Prerequisites
1. **Active Azure AD Tenant:**
   - Ensure you have a tenant with registered users.
2. **Application Registration:**
   - Register an application in Entra ID for API permissions.

### Steps to Configure the Environment
1. **Register Your Application:**
   - Go to **App Registrations** in Entra ID.
   - Create a new app registration.
   - Add **Microsoft Graph API** permissions (e.g., `User.Read.All` for querying users).
   - Generate a **client secret** and note down the client ID, tenant ID, and secret.

2. **Set Up Visual Studio Project:**
   - Open **Visual Studio**.
   - Create a **.NET Core Console App**.
   - Install the **Microsoft Graph SDK** using NuGet:
     ```bash
     dotnet add package Microsoft.Graph
     dotnet add package Microsoft.Graph.Auth
     ```

3. **Authenticate with Microsoft Graph:**
   - Use the client credentials flow for authentication.

---

## Example: Query Azure AD Users with Microsoft Graph

Below is an example of a .NET application to list users in an Azure AD tenant.

### Code Implementation

```csharp
using Microsoft.Graph;
using Microsoft.Identity.Client;
using System;
using System.Net.Http.Headers;
using System.Threading.Tasks;

class Program
{
    private static string tenantId = "<Your-Tenant-ID>";
    private static string clientId = "<Your-Client-ID>";
    private static string clientSecret = "<Your-Client-Secret>";

    static async Task Main(string[] args)
    {
        var client = GetAuthenticatedGraphClient();
        var users = await client.Users.Request().GetAsync();

        Console.WriteLine("Users in Azure AD:");
        foreach (var user in users)
        {
            Console.WriteLine($"User: {user.DisplayName}, Email: {user.Mail}");
        }
    }

    private static GraphServiceClient GetAuthenticatedGraphClient()
    {
        var confidentialClient = ConfidentialClientApplicationBuilder
            .Create(clientId)
            .WithClientSecret(clientSecret)
            .WithAuthority(new Uri($"https://login.microsoftonline.com/{tenantId}"))
            .Build();

        var authProvider = new DelegateAuthenticationProvider(async (requestMessage) =>
        {
            var authResult = await confidentialClient.AcquireTokenForClient(new[] { "https://graph.microsoft.com/.default" }).ExecuteAsync();
            requestMessage.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
        });

        return new GraphServiceClient(authProvider);
    }
}
```

### Key Features in the Code
1. **Authentication:**
   - Uses **ConfidentialClientApplicationBuilder** for app-level authentication.
   - Acquires an access token for Microsoft Graph.
2. **GraphServiceClient:**
   - Simplifies interaction with the Microsoft Graph API.
   - Makes API calls, such as `client.Users.Request().GetAsync()` to fetch user data.

---

## Best Practices

1. **Least Privilege Access:**
   - Grant only the necessary permissions (e.g., `User.Read.All` or `Group.Read.All`).
2. **Secure Secrets:**
   - Store client secrets securely using Azure Key Vault or environment variables.
3. **Pagination:**
   - Handle large datasets by using the `NextPageRequest` for paginated results.
4. **Error Handling:**
   - Implement robust error handling to manage API rate limits and transient failures.

---

## Resources

- [Microsoft Graph API Overview](https://learn.microsoft.com/en-us/graph/overview)
- [Graph SDK for .NET](https://learn.microsoft.com/en-us/graph/sdks/sdks-overview)
- [Azure AD App Registration Guide](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)

This example demonstrates the power and flexibility of the Microsoft Graph API, showcasing its ability to integrate seamlessly with Azure Active Directory and other Microsoft services.
