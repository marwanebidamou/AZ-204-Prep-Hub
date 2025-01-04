# Registering an Application in Entra ID (Azure Active Directory)

To enable your application to authenticate users via Entra ID (formerly Azure AD), you must register the application. This process creates a unique identity for your app within Entra ID and allows it to interact with the identity provider.

---

## Steps to Register an Application in Entra ID

### 1. **Navigate to App Registrations**
1. Open the Azure Portal and go to **Azure Active Directory**.
2. Select **App Registrations** from the left-hand menu.

### 2. **Create a New Registration**
1. Click on `+ New Registration`.
2. Fill in the details:
   - **Name**: Provide a meaningful name for your application, e.g., `Sample Login App`.
   - **Supported Account Types**: Choose how users can access the application:
     - **Accounts in this organizational directory only** (Single-tenant).
     - **Accounts in any organizational directory** (Multi-tenant).
     - **Accounts in any directory and personal Microsoft accounts** (e.g., Outlook.com, Hotmail).
   - **Redirect URI**: Leave it blank for now if you're not ready to set it up. This URI will be the endpoint where authentication responses are sent.
3. Click `Register`.

---

### 3. **Access Application Details**
Once the registration is complete:
- **Application (client) ID**: A unique identifier for your application.
- **Directory (tenant) ID**: Identifies the Entra ID tenant.
- **Quickstart Guides**: Found in the `Quickstart` section, offering sample code and configurations based on your application's type.

---

## Configuring Redirect URI

Redirect URIs define where authentication tokens are sent after user authentication. For local development:
- Use `https://localhost:44321/` (or the port used by your local server).

### Steps to Add or Update Redirect URI:
1. Go to **Authentication** in the application settings.
2. Under **Redirect URIs**, add your desired URI.
3. Save the changes.

---

## Sample Code and Quickstart

### Using .NET Core
1. In the **Quickstart** section:
   - Select the type of application (e.g., Web App).
   - Choose the desired framework (e.g., .NET Core).
2. Download the sample code provided.
3. Extract the code to a directory close to the root (to avoid path errors).
4. Open the project in **Visual Studio** or your preferred IDE.

The sample application will:
- Use Entra ID as the identity provider.
- Include configuration for testing on `localhost`.

---

## Testing the Application Locally

1. Open the downloaded project in Visual Studio.
2. Build and run the application.
3. Use the redirect URI (e.g., `https://localhost:44321/`) to test the login process.
4. Validate that the application can:
   - Authenticate users via Entra ID.
   - Handle authentication tokens.

---

## Next Steps

- **Explore Authentication Flows**:
  - Implement OAuth 2.0 or OpenID Connect for authentication.
- **Configure Permissions**:
  - Grant API permissions for Microsoft Graph or other APIs.
- **Deploy to Azure**:
  - Once tested locally, deploy the application to Azure for production use.

---

## Resources

- [Register an App with Entra ID](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)
- [Quickstart for .NET Apps](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-v2-aspnet-core-webapp)
- [Redirect URI Documentation](https://learn.microsoft.com/en-us/azure/active-directory/develop/reply-url)

---
