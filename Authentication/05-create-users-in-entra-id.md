# Creating Users in Entra ID (Azure Active Directory)

Entra ID (formerly Azure Active Directory) allows you to create and manage users within your organization’s tenant. These users can authenticate to applications and services integrated with Entra ID.

---

## Steps to Create Users in Entra ID

### 1. **Creating a New User**
A **new user** is a full member of the tenant and has permissions based on their assigned roles and groups.

#### Steps:
1. Navigate to the **Users** section in the Entra ID portal.
2. Click on `+ New User` and select `Create User`.
3. Fill in the required details:
   - **User Name**: This will follow the default domain name (e.g., `john.doe@yourdomain.onmicrosoft.com`).
   - **Name**: Provide the user's full name.
   - **Password**: You can auto-generate or set a custom password.
4. (Optional) Assign the user to specific groups or roles.
5. Click `Create` to complete the process.

#### Example:
Creating a user named John Doe:
- **User Name**: `john.doe@yourdomain.onmicrosoft.com`
- **Password**: Auto-generated.

---

### 2. **Creating a Guest User**
A **guest user** is an external user invited to join the tenant. Guest users are ideal for collaboration with external partners or contractors.

#### Steps:
1. Navigate to the **Users** section in the Entra ID portal.
2. Click on `+ New User` and select `Invite User`.
3. Provide the external user's email address (e.g., `sally.doe@example.com`).
4. (Optional) Add a personal invitation message.
5. Click `Invite` to send the email invitation.

#### Key Features of Guest Users:
- Guest users receive an invitation email to join the tenant.
- Guest accounts are labeled as **Guest** in the directory.
- Guest users may have limited permissions compared to tenant members.
- Guest accounts are not synchronized with on-premises Active Directory.

---

## Managing Created Users

1. **Assigning Roles and Groups**:
   - Users can be added to specific roles (e.g., developer, HR administrator) and groups.
   - Roles determine permissions within the tenant.

2. **Monitoring and Auditing**:
   - Use **Access Reviews** to periodically review and validate user access, especially for guest users.

---

## Example Use Case

- **Internal User**: John Doe is created as a full member of the tenant with access to specific internal resources.
- **External Guest**: Sally Doe is invited as a guest to collaborate on a shared project. She receives an email, registers her account, and gains limited access to tenant resources.

---

## Best Practices for Managing Users

1. **Strong Passwords**: Auto-generate passwords to enforce security.
2. **Guest User Reviews**: Regularly review guest user access to ensure it remains relevant.
3. **Custom Domains**: Configure a custom domain (e.g., `@companyname.com`) for a professional user experience.
4. **Role-Based Access**: Assign roles to limit permissions and reduce security risks.

---

## Next Steps

With users created in your tenant, you can proceed to integrate authentication into your applications. For example:
- John Doe can log into a web application using Entra ID authentication.
- Guest users like Sally can access shared resources securely.

For more information:
- [Entra ID Users Documentation](https://learn.microsoft.com/en-us/azure/active-directory/fundamentals/add-users-azure-active-directory)
- [Manage Guest Users in Entra ID](https://learn.microsoft.com/en-us/azure/active-directory/external-identities/what-is-b2b)

---
