# What is an Entra ID Tenant?

In the world of **Microsoft Entra ID** (formerly Azure Active Directory), a **tenant** is a fundamental concept that defines the security context and organizational boundary for users, groups, roles, and applications.

---

## Key Concepts

### 1. **User**
A **user** is an identity with a user ID and password that logs into Azure services. Every user belongs to at least one tenant.

### 2. **Tenant**
- A **tenant** is the unit of Entra ID that represents a specific instance of the directory service.
- It defines the security context, policies, and organizational settings for its users and resources.
- A user can belong to **multiple tenants**, but they operate independently.

### 3. **Global Administrator**
- The **Global Administrator** is the top-level role in a tenant, with permissions to manage users, groups, roles, and applications within the tenant.

---

## Viewing and Managing Tenants

### Switching Between Tenants
- Users can belong to multiple tenants.
- To switch tenants:
  1. Click your profile picture in the top-right corner.
  2. Select **Switch Directory**.
  3. Choose the desired tenant from the list.

### Default Directory
- Each user has a **default directory** assigned when they log into Azure.
- The default directory context determines the user’s permissions and access to resources.

---

## Tenant Characteristics

### 1. **Subscription Dependency**
- A tenant can exist without a subscription, but it cannot create Azure resources unless linked to an Azure subscription.
- If a tenant lacks a subscription, you'll encounter a message like:
  - "Don't have a subscription? Sign up for one."
- Subscriptions enable resource creation within the tenant.

### 2. **Permissions**
- **Global Administrator**: Full control over the tenant (create users, assign roles, manage applications).
- **Role-Based Permissions**: Granular roles such as Printer Administrator, Report Reader, etc., with specific privileges.

### 3. **Free vs. Premium Plans**
- By default, tenants operate on a **free tier**.
- Premium plans offer advanced features, such as additional security and analytics.

---

## Creating a New Tenant

Creating a new tenant is often recommended for experimentation or development to avoid affecting production environments.

### Steps to Create a Tenant:
1. Navigate to **Manage Tenants** in Entra ID.
2. Click **Create**.
3. Follow the setup process to define the new tenant.

### Why Create a New Tenant?
- To gain **Global Administrator** access for learning or testing purposes.
- To avoid impacting sensitive or production environments.

---

## Best Practices

1. **Use a Separate Tenant for Development**:
   - Avoid testing in production or corporate environments.
   - Create a personal tenant for experimentation.

2. **Leverage Role-Based Access Control (RBAC)**:
   - Assign roles to users based on their responsibilities.
   - Limit access to sensitive data and applications.

3. **Understand Subscription Dependencies**:
   - Ensure the tenant has an active subscription to create and manage resources.

---

## Summary

An **Entra ID tenant** is the foundation for managing users, roles, and resources in Microsoft Azure. Whether for personal use, development, or production, tenants define the security and organizational context. For developers, having a personal tenant as a **Global Administrator** allows safe experimentation without impacting sensitive environments.

---

## Resources

- [Microsoft Entra ID Documentation](https://learn.microsoft.com/en-us/azure/active-directory/)
- [Create and Manage Tenants](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/)
- [Azure Subscription Overview](https://learn.microsoft.com/en-us/azure/cost-management-billing/manage/create-subscription)
