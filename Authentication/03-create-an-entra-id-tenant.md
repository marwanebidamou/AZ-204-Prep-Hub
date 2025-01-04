# Creating an Entra ID Tenant

In this guide, we walk through the steps to create an **Entra ID (formerly Azure Active Directory)** tenant for testing and learning purposes. This tenant will not be associated with a subscription, meaning it won't support resource creation but will allow us to explore security and identity management concepts.

---

## Why Create a New Tenant?

- **Testing and Development**: A separate tenant enables safe experimentation without impacting production or corporate environments.
- **Focus on Security Concepts**: While no resources can be created without a subscription, we can still explore **users**, **groups**, **roles**, and **app registrations**.

---

## Types of Tenants

When creating a tenant, you can choose between:
1. **Microsoft Entra ID**:
   - Ideal for enterprise-grade identity management.
   - Suitable for managing employees and application access.
2. **Business-to-Consumer (B2C)**:
   - Allows users to log in via social accounts (e.g., LinkedIn, Google, Facebook).
   - Useful for applications targeting external consumers.

For this example, we’ll create an **Azure Active Directory tenant**.

---

## Step-by-Step Guide to Creating an Entra ID Tenant

### 1. **Start the Creation Process**
   - Navigate to **Entra ID** in the Azure portal.
   - Under **Manage Tenants**, select **Create**.

### 2. **Choose Directory Type**
   - Select **Azure Active Directory** (default option).

### 3. **Provide Basic Information**
   - **Organization Name**: Provide a unique and meaningful name (e.g., `Azure User Group Organization`).
   - **Domain Name**: Choose a domain prefix (e.g., `azureusergroup.onmicrosoft.com`).
     - The `onmicrosoft.com` domain is assigned by default until a custom domain is added.
     - Example user: `joe@azureusergroup.onmicrosoft.com`.
   - **Region**: Choose your data residency location based on compliance requirements (e.g., Europe for GDPR).

### 4. **Review and Create**
   - Confirm the provided details.
   - Click **Create** to initiate the process.
   - Tenant creation may take up to 15 minutes.

---

## Accessing the New Tenant

Once the tenant is created:
1. Click the provided link to open the tenant.
2. Log in if prompted.
3. View tenant details, including:
   - **Primary Domain**: Use for user creation and roles.
   - **Global Administrator Role**: As the creator, you have full administrative control.
4. Note: Resource creation is not possible without an associated subscription.

---

## Key Features of the New Tenant

- **Cost-Free**: Operates under the free tier unless upgraded to a premium plan.
- **Global Administrator Access**: Full control to manage users, roles, and app registrations.
- **Focus on Security and Identity**: Explore authentication and authorization without affecting live systems.

---

## Next Steps

The focus now shifts to:
- **App Registrations**: Setting up applications to use Entra ID for authentication.
- **Authentication and Authorization**: Working with Microsoft Graph and shared access signatures (SAS).

---

## Summary

Creating an **Entra ID tenant** provides a controlled environment to learn and test Azure’s identity and access management features. This setup is ideal for exploring **users**, **roles**, and **app registrations**, laying the foundation for secure application development.

---

## Resources

- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/azure/active-directory/)
- [How to Create a Tenant in Azure](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/)
- [Azure Active Directory B2C](https://learn.microsoft.com/en-us/azure/active-directory-b2c/)
