# Introduction to Entra ID

Microsoft Azure offers **Entra ID** as a powerful identity management service to handle authentication for your applications. Entra ID, previously known as Azure Active Directory (Azure AD or AAD), provides a unified platform for identity as a service, allowing applications to use Azure as their authentication provider.

---

## What is Entra ID?

Entra ID is the new branding for Azure's identity management service. It falls under the broader **Microsoft Entra** umbrella, which includes several services for identity and access management. The primary function of Entra ID is to:

- Manage user authentication.
- Support on-premises and cloud synchronization.
- Enable secure access to applications and resources.

---

## Key Features of Entra ID

### 1. **User Management**
- Manage users with on-premises credentials synchronized to the cloud.
- Provide single sign-on (SSO) capabilities.
- Allow users to authenticate with the same credentials across all applications.

### 2. **Group Management**
- Organize users into groups based on roles or departments (e.g., accounting, marketing, sales).
- Groups simplify permission assignment and management.

### 3. **Role-Based Access Control (RBAC)**
- Assign roles to users (e.g., Developer, Manager, HR Administrator).
- Use roles to define access permissions for resources and applications.

### 4. **Administrative Units**
- Divide the organization into smaller, manageable units (e.g., by geography or department).
- Assign administrators with permissions specific to their unit (e.g., Europe team admin, North America team admin).

### 5. **App Registrations**
- Register applications with Entra ID to use it as an authentication provider.
- Use app registrations to enable:
  - Secure sign-ins for users.
  - Permissions and role-based access for applications.

### 6. **Custom Domains**
- Assign custom domains for your organization instead of using the default `*.onmicrosoft.com` domain.

### 7. **Password Management**
- Enable self-service password resets or restrict password management options.
- Improve user experience while maintaining security.

---

## Getting Started with Entra ID

### Accessing Entra ID
You can access Entra ID through:
- **Azure Portal**: Navigate via "All Services" or directly from your dashboard.
- **Pinned Menu**: Add Entra ID for quick access.

### Navigation in Entra ID
The key sections under **Manage** include:
- **Users**: Manage individual accounts and credentials.
- **Groups**: Organize users into logical units.
- **Roles**: Define and assign access permissions.
- **App Registrations**: Set up your applications to use Entra ID for authentication.
- **Administrative Units**: Segment your organization for focused management.
- **Domain Management**: Add custom domains for branding.

---

## Why Use Entra ID?

Entra ID provides a **centralized identity service** for organizations, making it easier to manage users and secure access to resources. Developers can integrate Entra ID into applications to leverage:
- Secure and seamless authentication.
- Centralized user and permission management.
- Compatibility with both cloud-native and on-premises environments.

---

## Upcoming Sections

In this course, we'll explore:
1. **App Registrations**: Learn how to register an application with Entra ID.
2. **Role and Group Management**: Understand how to assign permissions effectively.
3. **On-Premises Integration**: Discover ways to synchronize existing credentials with the cloud.

---

## Resources

- [Microsoft Entra Overview](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/)
- [Entra ID Documentation](https://learn.microsoft.com/en-us/azure/active-directory/)
- [App Registrations in Entra ID](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app)
- [Manage Roles and Permissions](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

