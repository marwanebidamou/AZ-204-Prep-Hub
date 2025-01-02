# Azure Blob Storage Operations Using C#

This document covers common Azure Blob Storage operations programmatically implemented using C#. It includes examples for retrieving properties, setting metadata, uploading, downloading, moving, and deleting blobs.

---

## Prerequisites

1. **Install Required NuGet Package:**
   ```bash
   dotnet add package Azure.Storage.Blobs
   ```
2. **Set Up Azure Storage Account:**
   - Ensure a storage account is created in Azure with necessary permissions.
   - Obtain the connection string for your storage account.

---

## C# Code Examples for Blob Operations

### Initialize Blob Service Client
```csharp
using Azure.Storage.Blobs;

string connectionString = "<your-connection-string>";
var blobServiceClient = new BlobServiceClient(connectionString);
```

---

### Upload a File to Blob Storage
```csharp
string containerName = "my-container";
string blobName = "example.txt";
string filePath = "path/to/local/example.txt";

var containerClient = blobServiceClient.GetBlobContainerClient(containerName);
await containerClient.CreateIfNotExistsAsync();

var blobClient = containerClient.GetBlobClient(blobName);
await blobClient.UploadAsync(filePath, overwrite: true);
Console.WriteLine($"File uploaded successfully to {blobClient.Uri}");
```

---

### Download a Blob from Blob Storage
```csharp
string downloadPath = "path/to/downloaded/example.txt";
await blobClient.DownloadToAsync(downloadPath);
Console.WriteLine($"File downloaded successfully to {downloadPath}");
```

---

### Retrieve Blob Properties
```csharp
var properties = await blobClient.GetPropertiesAsync();
Console.WriteLine($"Blob Size: {properties.Value.ContentLength} bytes");
Console.WriteLine($"Content Type: {properties.Value.ContentType}");
Console.WriteLine($"Last Modified: {properties.Value.LastModified}");
```

---

### Set Metadata for a Blob
```csharp
var metadata = new Dictionary<string, string>
{
    {"Category", "Documents"},
    {"Owner", "AzureUser"}
};

await blobClient.SetMetadataAsync(metadata);
Console.WriteLine("Metadata set successfully.");
```

---

### Move a Blob Between Containers
```csharp
string destinationContainerName = "destination-container";
var destinationBlobClient = blobServiceClient.GetBlobContainerClient(destinationContainerName)
                                           .GetBlobClient(blobName);

await destinationBlobClient.StartCopyFromUriAsync(blobClient.Uri);
await blobClient.DeleteAsync();
Console.WriteLine("Blob moved successfully.");
```

---

### Delete a Blob
```csharp
await blobClient.DeleteAsync();
Console.WriteLine("Blob deleted successfully.");
```

---

## Additional Examples

### List All Blobs in a Container
```csharp
await foreach (var blobItem in containerClient.GetBlobsAsync())
{
    Console.WriteLine($"Blob Name: {blobItem.Name}");
}
```

### Lease a Blob for Exclusive Access
```csharp
var leaseClient = blobClient.GetBlobLeaseClient();
var lease = await leaseClient.AcquireAsync(TimeSpan.FromSeconds(60));
Console.WriteLine($"Lease ID: {lease.LeaseId}");
await leaseClient.ReleaseAsync();
```

---

## Best Practices

1. **Secure Connection Strings:**
   - Store connection strings securely (e.g., environment variables, Azure Key Vault).

2. **Optimize Metadata:**
   - Use metadata sparingly to avoid exceeding limits.

3. **Enable Logging and Monitoring:**
   - Track operations for debugging and auditing purposes.

4. **Use Asynchronous Methods:**
   - Leverage async methods to improve performance in production environments.

---

## Learn More

- [Azure Blob Storage Documentation](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction)
- [Azure Storage Blobs Client Library for .NET](https://learn.microsoft.com/en-us/dotnet/api/overview/azure/storage.blobs-readme)
