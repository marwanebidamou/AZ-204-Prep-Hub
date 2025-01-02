
# Uploading and Securing Files in an Azure Storage Account

Azure Blob Storage provides an efficient way to store unstructured data, but ensuring secure access is equally critical. This guide explains how to upload files to a blob storage account, configure security settings, and share access safely.

---

## Uploading Files to Blob Storage

### Steps to Upload Files via Azure Portal
1. **Access Your Storage Account:**
   - Navigate to **Storage Accounts** in the Azure Portal.
   - Open your storage account and click on **Containers**.

2. **Create a New Container:**
   - Click **+ Container**.
   - Provide a name for the container (e.g., `first-container`).
   - Select access level:
     - **Private:** Secure, requires credentials.
     - **Blob:** Public read access to blobs only.
     - **Container:** Public read access to container and blobs.

3. **Upload Files:**
   - Open the container and click **Upload**.
   - Choose a file from your local machine.
   - Optional: Select **Overwrite** if a file with the same name exists.
   - Click **Upload** to transfer the file to Azure.

4. **Verify Upload:**
   - Confirm the file appears in the container.
   - Check properties such as access tier, blob type, and file size.

---

## Secure Access to Blob Storage

### Access Keys
- **Access Keys Overview:**
  - Two keys (Key 1 and Key 2) are provided for full administrative access.
  - Keep these keys secure and avoid sharing them.

- **Key Rotation:**
  - Rotate keys periodically for enhanced security.
  - Set reminders for key rotation (e.g., every 60 days).

- **Connection Strings:**
  - Use connection strings in applications to authenticate with storage accounts.

### Shared Access Signatures (SAS)
- **What is SAS?**
  - A URL-based access mechanism allowing fine-grained access to specific blobs or containers.

- **Generating SAS:**
  1. Go to the container or blob and select **Generate SAS**.
  2. Configure permissions (e.g., read-only).
  3. Set expiry dates (e.g., 1 month).
  4. Optionally restrict access by IP address.
  5. Copy the generated SAS token or URL for use.

- **Using SAS:**
  - Append the SAS token to the blob URL for authenticated access.

- **Warning:**
  - SAS tokens cannot be directly revoked.
  - To revoke SAS access:
    1. Rotate the signing key.
    2. Use **Stored Access Policies** for revocable SAS management.

---

## Example: Generating and Using a SAS URL
1. Navigate to a blob.
2. Generate a SAS with read-only access for 30 days.
3. Copy the SAS token or URL.
4. Use the URL to access the blob securely.

**URL Structure:**
```
https://<storage-account-name>.blob.core.windows.net/<container-name>/<blob-name>?<sas-token>
```

---

## Advanced Access Management

### Stored Access Policies
- **Overview:**
  - Stored Access Policies allow revocable access management.
  - Link SAS tokens to a policy for controlled and flexible access revocation.

- **Steps to Create Stored Access Policy:**
  1. Define a policy on a container.
  2. Link SAS tokens to this policy.
  3. Revoke the policy to disable all associated SAS tokens.

---

## Notes
1. **Default Access Levels:** Use private containers for sensitive data.
2. **Sharing Best Practices:** Avoid sharing keys or long-lived SAS tokens.
3. **Programmatic Access:** Use Azure SDKs or REST APIs for secure integration.

---

## Learn More
- [Azure Blob Storage Documentation](https://learn.microsoft.com/en-us/azure/storage/blobs/)
- [Azure Storage Security](https://learn.microsoft.com/en-us/azure/storage/common/storage-security-guide/)
- [Azure Shared Access Signature (SAS)](https://learn.microsoft.com/en-us/azure/storage/common/storage-sas-overview)
