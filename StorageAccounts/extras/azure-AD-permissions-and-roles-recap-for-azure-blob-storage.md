**Azure AD Permissions and Roles Recap for Azure Blob Storage and Microsoft Graph (AZ-204)**

### **Azure Blob Storage Permissions via Azure AD**
Azure Blob Storage uses Azure Role-Based Access Control (RBAC) to manage permissions. Key roles and their permissions are outlined below:

#### **Roles for Azure Blob Storage**

1. **Storage Blob Data Owner**
   - Full access to Azure Storage blobs and containers.
   - Permissions include read, write, delete, and manage access control (IAM).
   - **When to Use**: Assign to users or applications that require complete control over blob data, including managing permissions.

2. **Storage Blob Data Contributor**
   - Read, write, and delete blob data.
   - Cannot manage access permissions.
   - **When to Use**: Use for applications or users that need to modify blob data but should not have permission to manage IAM roles.

3. **Storage Blob Data Reader**
   - Read-only access to blob data.
   - **When to Use**: Ideal for scenarios where applications or users only need to view or download blob data.

4. **Storage Blob Data Delegator**
   - Grants access to Azure AD users to impersonate the storage account for delegated access (used with Azure AD and OAuth).
   - **When to Use**: Required for scenarios where OAuth 2.0 is leveraged for delegated access.

#### **Key Features of Azure AD Authentication for Blob Storage**
- **Managed Identities**: Used to grant secure access without managing credentials.
- **OAuth 2.0 Tokens**: Access tokens are issued by Azure AD to access blob data.
- **Conditional Access Policies**: Additional security measures, such as IP restrictions and MFA, can be enforced.

#### **Steps to Assign Azure Blob Roles**
1. Navigate to the Azure Storage account.
2. Go to **Access Control (IAM)**.
3. Click **Add role assignment**.
4. Choose the desired role (e.g., Storage Blob Data Contributor).
5. Select the user, group, or managed identity and assign the role.

---

### **Microsoft Graph Permissions via Azure AD**
Microsoft Graph uses OAuth 2.0 to authorize access to resources. Permissions can be delegated (on behalf of a user) or application-level (without user context).

#### **Permission Types**
1. **Delegated Permissions**
   - Required when an application needs to act on behalf of a user.
   - Example: Reading a user’s calendar or profile.
   - **When to Use**: Use for scenarios where a user’s specific data or context is required, such as personal calendar or email access.

2. **Application Permissions**
   - Required when an application acts independently of a user.
   - Example: Reading all user profiles in an organization.
   - **When to Use**: Suitable for backend services or daemons that need organizational data without user context.

#### **Common Microsoft Graph Permissions**

1. **User.Read**
   - Read the signed-in user’s profile.
   - **When to Use**: For applications that display user profile information after login.

2. **User.ReadBasic.All**
   - Read basic profiles of all users in the directory.
   - **When to Use**: For applications that require access to basic details of multiple users.

3. **Group.Read.All** / **Group.ReadWrite.All**
   - Read all groups / Read and write all groups.
   - **When to Use**: Use when the application needs to query or manage group memberships.

4. **Files.Read** / **Files.ReadWrite**
   - Read user files / Read and write user files.
   - **When to Use**: For applications accessing OneDrive or SharePoint content.

5. **Directory.Read.All** / **Directory.ReadWrite.All**
   - Read directory data / Read and write directory data.
   - **When to Use**: For administrative tools that interact with Azure AD directory data.

6. **Mail.Read** / **Mail.ReadWrite**
   - Read user mail / Read and write user mail.
   - **When to Use**: For email applications accessing user mailboxes.

7. **Sites.Read.All** / **Sites.ReadWrite.All**
   - Read all SharePoint sites / Read and write all SharePoint sites.
   - **When to Use**: For SharePoint-integrated applications needing site or file access.

8. **user_impersonation**
   - Allows the application to access resources on behalf of the signed-in user.
   - **When to Use**: Common in scenarios like accessing Azure APIs or Key Vault on behalf of a user.

#### **Admin Consent**
- Certain permissions, such as **Directory.Read.All**, require admin consent as they expose organizational-level data.
- Admin consent is granted via Azure Portal or through a consent URL.

#### **Steps to Assign Microsoft Graph Permissions**
1. Register the application in Azure AD.
2. Navigate to **API Permissions**.
3. Click **Add a permission**.
4. Choose **Microsoft Graph** and select the desired permissions.
5. (If needed) Grant admin consent for organization-wide permissions.

---

### **Best Practices for Managing Permissions and Roles**

1. **Follow the Principle of Least Privilege**
   - Assign only the permissions and roles necessary for users or applications.

2. **Use Managed Identities**
   - Leverage managed identities to securely access Azure Blob Storage and Microsoft Graph without managing credentials.

3. **Audit Role Assignments**
   - Regularly review role assignments and permissions via Azure AD Activity Logs and Access Reviews.

4. **Implement Conditional Access**
   - Enforce conditional access policies for added security, such as MFA or location-based restrictions.

5. **Monitor with Azure Monitor and Security Center**
   - Track activities and detect anomalies in access patterns for Azure Blob Storage and Microsoft Graph resources.

---

This recap provides an overview of key Azure AD permissions and roles essential for Azure Blob Storage and Microsoft Graph scenarios, tailored to AZ-204 exam preparation.

