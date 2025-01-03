# Cosmos DB Keys and Security

Azure Cosmos DB uses claims-based authentication to control access to the database. This method ensures that access is granted only to those who possess the necessary keys and have network connectivity to the database URL.

---

## Key Concepts of Cosmos DB Authentication

### 1. **Primary and Secondary Keys**
- **Primary Key:**
  - Used for most access scenarios, including read and write operations.
  - Recommended as the main key for application integrations.

- **Secondary Key:**
  - Acts as a backup key.
  - Useful during key rotation to ensure zero downtime.

### 2. **Read-Only Keys**
- Separate set of keys dedicated to read-only access.
- Prevents modifications to the database content.
- Ideal for scenarios where data needs to be accessed without risk of accidental changes.

---

## Key Management

### Viewing Keys
- Navigate to the **Keys** section in the Cosmos DB account settings.
- Select **Show Primary Key** or **Show Secondary Key** to view the respective keys.

### Key Rotation
- **Why Rotate Keys?**
  - Enhanced security through periodic updates.
  - Necessary after personnel changes or potential breaches.

- **How to Rotate Keys:**
  1. Switch applications to use the secondary key.
  2. Regenerate the primary key.
  3. Update applications to use the new primary key.
  4. Regenerate the secondary key if needed.

- **Effect of Key Rotation:**
  - The old key is immediately invalidated.
  - Only those with the updated key retain access.

---

## Best Practices for Key Security
1. **Control Access:**
   - Do not share keys broadly.
   - Use secure storage solutions like Azure Key Vault to manage keys.

2. **Key Rotation Policy:**
   - Regularly rotate keys (e.g., every 3-6 months).
   - Rotate keys immediately after detecting a potential security breach.

3. **Use Read-Only Keys When Possible:**
   - Assign read-only keys to users or systems that do not require write access.

4. **Implement Role-Based Access Control (RBAC):**
   - Use Azure Active Directory (AAD) for fine-grained access control.
   - Assign roles to applications and users based on their access needs.

---

## Claims-Based Authentication Workflow
1. **Obtain Key:**
   - Retrieve the primary or secondary key from the Cosmos DB account.
2. **Access Database:**
   - Use the key and database URL to authenticate.
3. **Key Validation:**
   - Cosmos DB validates the key and grants access based on permissions.

---

## Additional Resources
- [Azure Cosmos DB Security Best Practices](https://learn.microsoft.com/en-us/azure/cosmos-db/security-best-practices)
- [Azure Key Vault for Key Management](https://learn.microsoft.com/en-us/azure/key-vault/)
- [Role-Based Access Control (RBAC) in Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/how-to-setup-rbac)