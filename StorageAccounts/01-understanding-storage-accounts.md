
# Understanding Azure Storage Accounts

Azure Storage Accounts provide scalable, durable, and secure storage solutions for modern applications. This document focuses on Blob Storage as part of Azure Storage Accounts and explores the options, pricing tiers, and redundancy features available.

---

## Key Types of Storage in Azure

1. **Managed Disks:**
   - Fixed-price storage designed for virtual machines.
   - Reserved storage paid per month regardless of usage.
   - Typical use case: Virtual Machine disk storage.

2. **Blob Storage:**
   - Cost-efficient storage for unstructured data such as files and media.
   - Pay-as-you-go model based on storage and access.
   - Typical use case: Storing and retrieving large amounts of unstructured data.

---

## Blob Storage Overview
Blob Storage is the most cost-effective way to store files in Azure. It supports:
- **General Purpose v2 (GPv2):** Standard storage with various access tiers.
- **Premium Storage:** High-performance storage with lower latency.

### Pricing Tiers
1. **Hot:**
   - Optimized for frequent access.
   - Cost example: ~2.1 cents/GB/month in East US.

2. **Cool:**
   - Optimized for infrequent access.
   - Cost example: ~1 cent/GB/month.

3. **Archive:**
   - Optimized for rarely accessed data.
   - Requires rehydration to access.

### Regional Pricing Variations
- Pricing varies by region.
- Example: Storage in Brazil costs more (~3.3 cents/GB/month) compared to East US (~2.1 cents/GB/month).

---

## Storage Redundancy Options
Azure offers multiple redundancy options to ensure high availability and durability:

1. **Locally Redundant Storage (LRS):**
   - Keeps three copies within the same data center.
   - Cost-effective but no geographic protection.

2. **Zone-Redundant Storage (ZRS):**
   - Keeps copies in multiple availability zones within the same region.
   - Ensures higher fault tolerance than LRS.

3. **Geo-Redundant Storage (GRS):**
   - Stores six copies: three locally and three in a paired region.
   - Provides geographic disaster recovery.

4. **Geo-Zone Redundant Storage (GZRS):**
   - Combines ZRS and GRS for ultimate durability.
   - Stores three zone-redundant copies locally and three copies in a paired region.

5. **Read-Access Geo-Redundant Storage (RA-GRS):**
   - Similar to GRS but allows read access to secondary copies.
   - Suitable for read-heavy workloads needing high availability.

---


## Blob Storage Types

Azure Blob Storage supports three distinct types of blobs, each tailored to different scenarios:

### 1. Block Blobs

**Overview**:  
Block blobs are designed for storing large files such as text and binary data.

**Key Features**:
- Data is divided into blocks, which can be uploaded independently.
- Ideal for storing documents, images, videos, and backups.

**Use Cases**:
- Uploading large files in chunks.
- Storing unstructured data efficiently.

---

### 2. Append Blobs

**Overview**:  
Append blobs are optimized for scenarios where data needs to be added sequentially.

**Key Features**:
- Supports append-only operations; existing data cannot be modified.
- Each blob can grow up to 4.75 TiB in size.

**Use Cases**:
- Storing logs from virtual machines or applications.
- Audit trails and streaming data.

---

### 3. Page Blobs

**Overview**:  
Page blobs are designed for workloads requiring frequent updates to data.

**Key Features**:
- Data is organized into 512-byte pages.
- Supports random read/write operations.
- Can store up to 8 TiB of data.

**Use Cases**:
- Storing virtual hard disk (VHD) files for Azure virtual machines.
- Databases and scenarios requiring frequent updates.

---

### Quick Comparison of Blob Types

| **Blob Type**    | **Use Case**                   | **Max Size** | **Key Characteristics**                                     |
|-------------------|--------------------------------|--------------|-------------------------------------------------------------|
| **Block Blobs**   | Text/binary data storage       | 4.75 TiB     | Uploaded in blocks, best for large file uploads.            |
| **Append Blobs**  | Sequential data logging       | 4.75 TiB     | Optimized for appending operations, existing data immutable.|
| **Page Blobs**    | Random read/write workloads   | 8 TiB        | Used for frequently updated data like virtual disk storage. |

---
## Creating a Storage Account

### Azure Portal
1. Go to **Create a Resource** > **Storage Accounts**.
2. Configure the following:
   - **Subscription:** Select your subscription.
   - **Resource Group:** Create or choose an existing resource group.
   - **Storage Account Name:** Choose a unique name.
   - **Region:** Select a region.
   - **Performance:** Choose Standard or Premium.
   - **Redundancy:** Choose from LRS, ZRS, GRS, or GZRS.
   - **Primary Service:** Select Blob, Table, Queue, or File storage.
   - **Read Access to Data in Regional Unavailability:** Enable if required.
3. Click **Review + Create** and then **Create**.

### Azure CLI
```bash
az storage account create \  
  --name <storage-account-name> \  
  --resource-group <resource-group-name> \  
  --location <region> \  
  --sku <redundancy-option> \  
  --kind StorageV2
```

---

## Advanced Settings

### HTTPS and Access Control
- **HTTPS Required:** Ensures secure communication over REST API.
- **Public Access:** Enable if public file access is required.
- **Account Key Access:** Use keys for full admin rights or disable in favor of Azure Active Directory.

### TLS Settings
- Enable TLS 1.2 for enhanced security.

### Data Lake Storage
- For big data analytics requiring petabytes or exabytes of storage.
- Supports hierarchical namespace, true folders, and file-level access control.

### Access Tiers
1. **Hot Tier:**
   - Default tier for frequently accessed data.

2. **Cool Tier:**
   - Suitable for infrequently accessed data, saving ~50% on storage costs.

3. **Archive Tier:**
   - Cheapest option for rarely accessed data with higher retrieval costs.

---

## Additional Notes
- **Access Tiers:** Adjust access tiers based on data usage patterns to optimize costs.
- **Encryption:** Data is encrypted at rest by default.
- **Networking:** Configure virtual networks and firewalls for secure access.

---

## Learn More
- [Azure Storage Pricing](https://azure.microsoft.com/en-us/pricing/details/storage/)
- [Azure Storage Documentation](https://learn.microsoft.com/en-us/azure/storage/)
