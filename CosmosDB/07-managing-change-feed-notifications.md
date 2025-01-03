# Managing Change Feed Notifications in Azure Cosmos DB

Azure Cosmos DB provides a feature called **Change Feed** that enables real-time event-driven architecture. The change feed captures inserts and updates to items within a Cosmos DB container, making it ideal for:

- Event-driven applications.
- Real-time analytics.
- Data synchronization across systems.

---

## How Change Feed Works

The change feed provides a chronological log of changes (insertions and updates) to items in a Cosmos DB container. Deleted items are **not captured**. The change feed can be accessed programmatically using:

- **Azure Functions with Cosmos DB Trigger.**
- **SDKs** for custom solutions.

---

## Setting Up a Cosmos DB Trigger in Azure Functions

### Steps to Create a Change Feed Trigger:

1. **Create a New Function App:**
   - Navigate to Azure Portal.
   - Create a new Function App.

2. **Add a Cosmos DB Trigger:**
   - Open the Function App.
   - Select `+ Add Function`.
   - Choose `Azure Cosmos DB trigger` as the function template.

3. **Configure the Trigger:**
   - Provide a meaningful name (e.g., `ChangeFeedProcessor`).
   - Link it to an existing Cosmos DB account.
   - Specify the **database** and **container** to monitor (e.g., `QuestionsDB` and `Employee`).
   - Define the **leases container**, used by Azure Functions to track processing state.
     - If not already available, the leases container is automatically created.

4. **Deploy and Test:**
   - Add logic to the function to handle change feed events.
   - Use the Azure Functions Log tab to monitor triggers.

---

## Example: Cosmos DB Trigger with Azure Functions

Below is a simple example of an Azure Function triggered by the Cosmos DB change feed.

```csharp
using System;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;

public static class ChangeFeedProcessor
{
    [FunctionName("ChangeFeedProcessor")]
    public static void Run(
        [CosmosDBTrigger(
            databaseName: "QuestionsDB",
            collectionName: "Employee",
            ConnectionStringSetting = "CosmosDBConnection",
            LeaseCollectionName = "leases")] IReadOnlyList<dynamic> changes,
        ILogger log)
    {
        if (changes != null && changes.Count > 0)
        {
            foreach (var document in changes)
            {
                log.LogInformation($"Document modified: {document}");
                log.LogInformation($"Document ID: {document.id}");
            }
        }
    }
}
```

### Key Features of the Trigger Code:
- **CosmosDBTrigger Attribute:**
  - Specifies the database, container, and leases container.
  - `ConnectionStringSetting` links to the Cosmos DB account.
- **Logger:**
  - Outputs information about the changed document.

---

## Change Feed with SDKs

Developers can also use the Cosmos DB SDK to access the change feed programmatically. This approach allows for greater customization.

### Example with .NET SDK:

```csharp
using Microsoft.Azure.Cosmos;
using System;
using System.Threading.Tasks;

class Program
{
    private static readonly string EndpointUri = "<Your-CosmosDB-Endpoint>";
    private static readonly string PrimaryKey = "<Your-CosmosDB-Key>";

    private static readonly string DatabaseId = "QuestionsDB";
    private static readonly string ContainerId = "Employee";

    static async Task Main(string[] args)
    {
        using (CosmosClient client = new CosmosClient(EndpointUri, PrimaryKey))
        {
            Container container = client.GetContainer(DatabaseId, ContainerId);

            FeedIterator<dynamic> iterator = container.GetChangeFeedIterator<dynamic>(
                ChangeFeedStartFrom.Now(),
                ChangeFeedMode.Incremental);

            while (iterator.HasMoreResults)
            {
                foreach (var change in await iterator.ReadNextAsync())
                {
                    Console.WriteLine($"Change detected for document: {change}");
                }
            }
        }
    }
}
```

### Features:
- **ChangeFeedStartFrom:**
  - Specifies where to start reading changes (e.g., from now or a point in time).
- **ChangeFeedMode:**
  - Determines the mode of reading (incremental or full).

---

## Best Practices

1. **Leases Container:**
   - Always ensure a dedicated leases container is configured to track change feed progress.
2. **Partition Key Awareness:**
   - Optimize change feed queries by considering partition key design.
3. **Avoid Overloading:**
   - Monitor request units (RUs) consumption to prevent throttling.
4. **Handle Deletions:**
   - Use soft deletes (e.g., `isDeleted: true`) to track deletions.

---

## Use Cases

- **Event-Driven Architectures:** Trigger workflows or notifications.
- **Real-Time Analytics:** Process and analyze changes as they happen.
- **Data Synchronization:** Sync data across systems or regions.

---

## Resources

- [Azure Cosmos DB Change Feed Documentation](https://learn.microsoft.com/en-us/azure/cosmos-db/change-feed)
- [Azure Functions Cosmos DB Trigger Documentation](https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2)
- [Cosmos DB SDKs](https://learn.microsoft.com/en-us/azure/cosmos-db/sql/sql-sdk-overview)
