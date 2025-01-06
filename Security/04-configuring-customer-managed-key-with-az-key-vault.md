# Configuring Customer-Managed Keys (CMK) with Azure Key Vault

Azure provides the flexibility to use Customer-Managed Keys (CMK) for managing encryption in various services, such as SQL databases. Using CMK allows organizations to take full control of their encryption keys, enhancing security and compliance.

---

## Overview of Customer-Managed Keys

Customer-Managed Keys allow you to:
- Store encryption keys in **Azure Key Vault**.
- Rotate keys periodically to meet security policies.
- Enable fine-grained control over access to keys and encrypted data.

### Use Cases
- Enforcing strict data protection policies.
- Ensuring compliance with regulations like GDPR and HIPAA.
- Supporting double encryption by combining service-level encryption with your own managed keys.

---

## Steps to Configure CMK for SQL Databases

### 1. Create an Azure Key Vault
1. Navigate to the **Azure Portal**.
2. Search for **Key Vault** in the resource creation menu.
3. Configure the key vault:
   - Choose a **Region**.
   - Select the **Standard** or **Premium** pricing tier.
   - Enable **Purge Protection** to prevent accidental key deletion.
4. Review and create the Key Vault.

### 2. Add a Key to the Key Vault
1. Navigate to the created Key Vault.
2. Go to the **Keys** section.
3. Click **Generate/Import** to create a new key.
   - Choose **RSA** encryption with a suitable key size (e.g., 2048 bits).
   - Optionally, set an activation and expiration date.
4. Save the key.

### 3. Assign Key Vault Permissions
1. Navigate to the **Access Control (IAM)** tab in the Key Vault.
2. Add a role assignment for the SQL database's managed identity or your user account.
   - Role: **Key Vault Administrator** or **Key Vault Contributor**.
   - Assign to: The SQL server’s managed identity or your specific Azure user.

### 4. Configure SQL Database to Use CMK
1. Navigate to your SQL Server resource in the **Azure Portal**.
2. Under **Transparent Data Encryption**, select **Customer-Managed Keys**.
3. Choose the created Key Vault.
   - Select the specific key created earlier.
4. Enable **Auto-Rotation** if required.
   - Allows the SQL database to automatically use the latest version of the key upon rotation.

### 5. Validate Configuration
- Ensure that the database encryption is enabled with the selected Customer-Managed Key.
- Test key access permissions by attempting to query the database or perform encryption-related operations.

---

## Benefits of Using Customer-Managed Keys

1. **Enhanced Security**:
   - Prevent unauthorized access by storing keys in a dedicated Key Vault.
2. **Compliance**:
   - Meet regulatory requirements by controlling encryption keys.
3. **Auto-Rotation**:
   - Reduce the risk of stale keys by automating rotation.
4. **Auditability**:
   - Gain insights into key access and usage through Key Vault logs.

---

## Key Considerations

- **Purge Protection**:
  - Must be enabled to prevent accidental or malicious deletion of keys.
- **Managed Identity**:
  - Use a system-assigned or user-assigned managed identity for seamless key access.
- **Service Dependencies**:
  - Ensure all services relying on the key are updated when rotating keys.
- **Double Encryption**:
  - Consider enabling infrastructure-level encryption for an additional security layer.

---

## Additional Resources

- [Azure Key Vault Overview](https://learn.microsoft.com/en-us/azure/key-vault/key-vault-overview)
- [Key Vault Integration with Managed Identity](https://learn.microsoft.com/en-us/azure/key-vault/general/managed-identity)
- [Transparent Data Encryption](https://learn.microsoft.com/en-us/azure/sql-database/transparent-data-encryption-azure-sql)

This guide ensures that you securely manage and configure Customer-Managed Keys with Azure Key Vault, enabling advanced encryption options for your SQL databases and other Azure services.
