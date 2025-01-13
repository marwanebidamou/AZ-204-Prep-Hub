# Azure Storage Lifecycle Policy

Azure Storage Lifecycle Management provides an automated, policy-driven approach to manage the lifecycle of your data, enabling cost optimization by moving or deleting data based on its usage patterns. Below is a comprehensive guide covering lifecycle policies for all Azure Storage types.

---

## **1. Overview of Azure Storage Lifecycle Policy**
- **Purpose**: Automate the movement of data between tiers (Hot, Cool, Archive) or delete it based on conditions.
- **Supported Blob Types**:
  - Block blobs: Supports all actions, including `enableAutoTierToHotFromCool`, `tierToCool`, `tierToArchive`, and `delete`.
  - Append blobs: Supports only the `delete` action.
  - Page blobs: Not supported by lifecycle management.

---

## **2. Components of Lifecycle Policies**
### **Filters**
1. **Blob Type**: Specify the blob type the rule applies to.
2. **PrefixMatch**:
   - Defines the scope of blobs based on prefixes.
   - Starts with the **container name**.
3. **Blob Index Tag**:
   - Enables filtering using custom metadata tags.

### **Actions**
1. **Move**: Transition block blobs between tiers (Hot -> Cool -> Archive).
2. **Delete**: Remove blobs permanently (applies to both block and append blobs).

---

## **3. Lifecycle Policy for Block Blobs**
### Example:
```json
{
  "rules": [
    {
      "name": "moveToCoolTier",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": ["blockBlob"],
          "prefixMatch": ["container1/", "container2/folder/"]
        },
        "actions": {
          "baseBlob": {
            "tierToCool": {
              "daysAfterModificationGreaterThan": 30
            }
          }
        }
      }
    }
  ]
}
```
- **Key Points**:
  - Moves block blobs to the Cool tier after 30 days.
  - Filters by prefix to limit the scope.

---

## **4. Lifecycle Policy for Append Blobs**
### Example:
```json
{
  "rules": [
    {
      "name": "deleteOldAppendBlobs",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": ["appendBlob"],
          "prefixMatch": ["logs/append/"],
          "tags": {
            "logCategory": "application"
          }
        },
        "actions": {
          "baseBlob": {
            "delete": {
              "daysAfterModificationGreaterThan": 365
            }
          }
        }
      }
    }
  ]
}
```
- **Key Points**:
  - Deletes append blobs under the specified prefix after 1 year.
  - Filters by custom tags (e.g., `logCategory`).

---

## **5. Lifecycle Policy for Page Blobs**
### Note:
- Currently, **page blobs are not supported** by Azure Lifecycle Management.
- Use manual or custom scripts for managing page blob lifecycles.

---

## **6. Using Blob Index Tags**
- Tags allow filtering based on metadata.
- Example:
```json
{
  "rules": [
    {
      "name": "archiveTaggedBlobs",
      "enabled": true,
      "type": "Lifecycle",
      "definition": {
        "filters": {
          "blobTypes": ["blockBlob"],
          "tags": {
            "Environment": "Production",
            "Project": "AzureMigration"
          }
        },
        "actions": {
          "baseBlob": {
            "tierToArchive": {
              "daysAfterModificationGreaterThan": 90
            }
          }
        }
      }
    }
  ]
}
```
- Moves blobs with specific tags to the Archive tier after 90 days.

---

## **7. Tips for Configuring Lifecycle Policies**
1. **Start Small**: Test with a limited scope using `prefixMatch` or tags.
2. **Monitor Costs**: Evaluate savings and potential retrieval costs when using Cool/Archive tiers.
3. **Review Logs**: Use Azure Monitor to track lifecycle policy application.
4. **Update Regularly**: Adjust policies based on usage patterns and data retention needs.

---

## **8. Common Use Cases**
1. **Log Data Management**:
   - Move infrequently accessed logs to Cool or Archive tiers.
   - Delete logs after compliance retention period.
2. **Backup Storage**:
   - Store backups in Archive tier.
   - Transition to Cool tier for quicker retrieval if needed.
3. **Data Archiving**:
   - Retain historical datasets in Archive for regulatory requirements.
4. **Cost Optimization**:
   - Transition blobs from Hot to Cool tier to reduce storage costs.

---

## **9. Tools and References**
- **Azure Portal**: Configure lifecycle management policies through the UI.
- **Azure CLI**:
  - Create policies: `az storage account management-policy create`
  - Show policies: `az storage account management-policy show`

- **Azure Resource Manager (ARM) Templates**:
  - Define lifecycle policies as part of infrastructure as code.

- **Microsoft Documentation**:
  - [Azure Blob Lifecycle Management](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-lifecycle-management-concepts)

---

By using lifecycle policies effectively, you can reduce costs, improve operational efficiency, and ensure compliance with data retention requirements.

