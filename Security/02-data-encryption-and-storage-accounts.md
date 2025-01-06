# Data Encryption in Azure Storage Accounts

This section explains the key concepts of data encryption for Azure Storage Accounts, including encryption in transit and at rest. Azure provides built-in encryption mechanisms to ensure data security both during transmission and storage.

---

## Encryption in Transit
- **Definition**: Ensures that data is securely transmitted between the client and the storage account.
- **Mechanism**: Utilizes HTTPS or SSL for secure communication.
- **Configuration**: 
  - Enabled by default when creating a storage account.
  - Ensured through the **Require Secure Transfer** setting.

### Enabling Secure Transfer
- During storage account creation:
  - Navigate to the **Advanced** tab.
  - Check the **Require secure transfer for REST API operations** option (enabled by default).
- After creation:
  - Navigate to the storage account's **Configuration** settings.
  - Enable/disable secure transfer as needed.

**Best Practice**: Always enable secure transfer to protect data from interception.

---

## Encryption at Rest
- **Definition**: Data is encrypted when stored on disk.
- **Types of Encryption**:
  1. **Microsoft-Managed Keys**:
     - Default encryption option.
     - Managed transparently by Azure.
     - Requires no user intervention.
  2. **Customer-Managed Keys (CMK)**:
     - Users manage encryption keys through Azure Key Vault.
     - Provides greater control over keys.

### Configuring Encryption at Rest
1. **Microsoft-Managed Keys**:
   - No additional configuration needed.
   - Enabled by default for all storage accounts.
2. **Customer-Managed Keys**:
   - Requires Azure Key Vault.
   - Steps:
     - Create an Azure Key Vault.
     - Generate or import encryption keys.
     - Assign the storage account access to the Key Vault.

### Infrastructure Encryption
- **Definition**: Adds a second layer of encryption to data at rest.
- **Configuration**: Must be enabled during storage account creation.
  - Navigate to the **Encryption** tab.
  - Enable **Infrastructure Encryption**.
- **Use Case**: Provides additional security for highly sensitive data.

---

## Summary of Encryption Options

| Type                   | Purpose                                | Configuration            | Notes                                      |
|------------------------|----------------------------------------|--------------------------|--------------------------------------------|
| Encryption in Transit  | Protects data during transmission      | Enabled by default       | Ensure HTTPS is always used.              |
| Microsoft-Managed Keys | Default encryption for stored data     | No configuration needed  | Transparent to users.                     |
| Customer-Managed Keys  | User-controlled encryption for storage | Requires Azure Key Vault | Suitable for organizations with strict policies. |
| Infrastructure Encryption | Double encryption for sensitive data | Enabled at creation      | Cannot be modified post-creation.         |

---

## Best Practices
1. **Always Enable HTTPS**:
   - Use the **Require secure transfer** option to enforce secure communication.
2. **Use Customer-Managed Keys When Necessary**:
   - Comply with organizational policies by managing your own encryption keys.
3. **Enable Infrastructure Encryption for Critical Data**:
   - Protect against physical data access risks.
4. **Monitor and Audit**:
   - Use Azure Monitor and logging to track access to your storage account.
5. **Leverage Azure Key Vault**:
   - Centralize key management and access control.

---

## Additional Resources
- [Azure Storage Account Encryption](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption)
- [Azure Key Vault Documentation](https://learn.microsoft.com/en-us/azure/key-vault/)
- [Secure Transfer in Azure Storage](https://learn.microsoft.com/en-us/azure/storage/common/storage-require-secure-transfer)
