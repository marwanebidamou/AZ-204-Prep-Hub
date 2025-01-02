# Using AzCopy to Manage Azure Blob Storage

AzCopy is a command-line utility for efficiently copying and managing data between Azure Blob Storage containers, storage accounts, or even other cloud services. This guide explains how to use AzCopy to transfer files programmatically within Azure.

---

## Overview of AzCopy

### Key Features:
- Supports transferring data between:
  - Azure Blob Storage containers.
  - Azure Storage Accounts.
  - Other cloud services like Amazon S3 or Google Cloud.
- Transfers occur directly on Azure servers, avoiding local download/upload cycles.
- Cross-platform availability (Linux, Windows, MacOS).

### Benefits:
- Avoids bandwidth overhead for local systems.
- Ideal for large-scale transfers (e.g., terabytes or petabytes).
- Supports Azure Active Directory (AAD) authentication and Shared Access Signatures (SAS).

---

## Setting Up AzCopy

### Installation:
- Download AzCopy for your operating system from [Azure Storage Tools](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

### Verifying Installation:
```bash
azcopy --version
```

---

## Transferring Files with AzCopy

### Example Scenario:
We aim to copy a file from `first-container` to `second-container` in the same storage account.

### Prerequisites:
1. **Storage Account and Containers:**
   - A source container (`first-container`) with an existing file (e.g., `example.mp4`).
   - A destination container (`second-container`).
2. **Generate SAS Tokens:**
   - SAS tokens provide scoped access to the source and destination.
   - Ensure appropriate permissions (e.g., read for source, write for destination).

### Generate SAS Tokens:
1. Navigate to the Azure Portal.
2. Select the desired container.
3. Use the **Shared Access Signature (SAS)** option to generate tokens.
4. Copy the SAS token and append it to the storage URL:
   ```
   https://<storage-account>.blob.core.windows.net/<container-name>/<file-name>?<SAS-token>
   ```

### AzCopy Command Format:
```bash
azcopy copy "<source-URL-with-SAS-token>" "<destination-URL-with-SAS-token>"
```

### Example Command:
```bash
azcopy copy "https://myaccount.blob.core.windows.net/first-container/example.mp4?<source-SAS-token>" "https://myaccount.blob.core.windows.net/second-container/example.mp4?<destination-SAS-token>"
```

### Output:
- AzCopy provides a transfer summary:
  - Number of transfers completed.
  - Final job status (e.g., Completed).

Verify the transfer by checking the destination container.

---

## Advanced Scenarios

### Copying Between Different Storage Accounts
- Include SAS tokens for both source and destination URLs.
- Example:
  ```bash
  azcopy copy "https://sourceaccount.blob.core.windows.net/source-container/example.mp4?<source-SAS-token>" "https://destinationaccount.blob.core.windows.net/destination-container/example.mp4?<destination-SAS-token>"
  ```

### Using Azure Active Directory (AAD) for Authentication
1. Configure AAD authentication for your storage account.
2. Use AAD credentials with AzCopy:
   ```bash
   azcopy login
   ```
3. Use AAD-based access to perform transfers:
   ```bash
   azcopy copy "https://myaccount.blob.core.windows.net/first-container/example.mp4" "https://myaccount.blob.core.windows.net/second-container/example.mp4"
   ```

### Transferring Large Data Sets
- Use AzCopy for transferring terabytes or petabytes efficiently.
- Example command with recursive flag:
  ```bash
  azcopy copy "https://myaccount.blob.core.windows.net/first-container?<SAS-token>" "https://myaccount.blob.core.windows.net/second-container?<SAS-token>" --recursive=true
  ```

---

## Best Practices
1. **Use SAS Tokens Wisely:**
   - Generate SAS tokens with minimal required permissions and validity duration.
   - Revoke SAS tokens by regenerating storage account keys if needed.
2. **Monitor Transfers:**
   - Use logs or output summaries to track progress and troubleshoot issues.
3. **Automate Transfers:**
   - Schedule AzCopy commands using scripts for periodic transfers.

---

## Learn More
- [AzCopy Documentation](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)
- [Azure Blob Storage Overview](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)
