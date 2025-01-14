# Multitenancy and App Registration in Microsoft Entra ID (Azure Active Directory)

Azure Active Directory (now Microsoft Entra ID) supports building multitenant applications that can be accessed and used by multiple organizations. This document focuses on the relationship between **application objects** and **service principals** in a multitenant application scenario.

---

## **1. Key Concepts**

### **a. Application Object**
- A **global definition** of an application stored in the **home tenant** (where the app is registered).
- Includes:
  - Application metadata such as redirect URIs, API permissions, and app roles.
  - Identifies the app uniquely with a **Client ID** (App ID).

### **b. Service Principal**
- A **local representation** of an application in a specific tenant.
- Created automatically when an app is granted access to a tenant.
- Enables the application to authenticate and access resources in that tenant.

### **c. Multitenant Applications**
- Applications configured to accept users from multiple tenants.
- Marked as multitenant during registration in the Azure portal.
- Generates service principals in each consumer tenant when accessed.

---

## **2. Relationship Between Application Objects and Service Principals**

### **a. Single Application Object and Multiple Service Principals**
- A multitenant app has **one application object** (in the home tenant).
- **Service principals** are created in each tenant that the app interacts with.

### Example:
1. App1 is registered in Tenant A.
2. A user from Tenant B accesses App1.
3. A **service principal** for App1 is created in Tenant B.

| **Entity**         | **Scope**        | **Purpose**                                         |
|--------------------|------------------|---------------------------------------------------|
| Application Object | Home Tenant      | Defines the app globally.                         |
| Service Principal  | Consumer Tenants | Enables app access in specific consumer tenants. |

---

## **3. Exam Tip: Key Relationships to Remember**
- Multitenant apps have **one application object** and **multiple service principals**.
- Service principals are created dynamically in consumer tenants when the app is accessed.

### Incorrect Scenarios:
- **Multiple Application Objects**: A multitenant app has only one application object.
- **Single Service Principal**: There are multiple service principals, one per tenant.

---

## **4. Steps to Create a Multitenant Application**

### **Step 1: Register the Application**
1. In the Azure portal, go to **Azure Active Directory** > **App Registrations** > **New Registration**.
2. Set "Supported account types" to **Multitenant**.
3. Configure redirect URIs and permissions.

### **Step 2: Define API Permissions**
1. Assign Microsoft Graph or custom API permissions.
2. Grant admin consent in the home tenant.

### **Step 3: Test Multitenancy**
1. Share the app URL with a user from another tenant.
2. Verify that a service principal is created in the consumer tenant.

---

## **5. Practical Use Cases**
- **SaaS Applications**:
  - Enable multiple organizations to use a single hosted instance of the application.
- **B2B Collaboration**:
  - Allow external users from partner organizations to authenticate with their own Azure AD accounts.

---

## **6. Additional Notes**
- **Admin Consent**: Some permissions may require tenant admin approval before a service principal is created.
- **Branding**: Customize app branding in the Azure portal to make it recognizable across tenants.
- **Token Validation**:
  - Validate tokens issued by Microsoft Entra ID to ensure they are from authorized tenants.

---

## **7. Exam Questions to Expect**
- Identify the relationship between application objects and service principals.
- Configure a multitenant app for authentication.
- Troubleshoot scenarios where service principals are not created.

---

By understanding the relationship between application objects and service principals, as well as configuring multitenant apps, you can build scalable and secure applications for multiple organizations.

