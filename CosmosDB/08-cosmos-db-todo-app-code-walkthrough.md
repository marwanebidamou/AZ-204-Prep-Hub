# Cosmos DB Todo App: Code Walkthrough

The Azure Cosmos DB .NET Core Todo App is a sample application that demonstrates how to integrate Cosmos DB into an ASP.NET Core MVC application. This walkthrough dissects the code structure and highlights the interaction with Cosmos DB.

---

## Overview of the Application

This application follows the **Model-View-Controller (MVC)** architecture and provides a simple CRUD interface for managing a to-do list. The Cosmos DB service acts as the backend database.

### Repository Location
- GitHub Repository: [Azure-Samples/cosmos-dotnet-core-todo-app](https://github.com/Azure-Samples/cosmos-dotnet-core-todo-app)

### Application Structure
- **Controllers:** Handle user requests and define application logic.
- **Models:** Define the structure of data.
- **Views:** Represent the UI and render data for the user.

---

## Code Walkthrough

### 1. **Model: ToDoItem.cs**
Defines the data structure for a to-do item.

```csharp
public class ToDoItem
{
    public string Id { get; set; } // Unique identifier
    public string Name { get; set; } // Task name
    public string Description { get; set; } // Task description
    public bool IsComplete { get; set; } // Completion status
}
```

### 2. **Controller: ItemController.cs**
Handles HTTP requests and interactions with the Cosmos DB service.

#### Index Action
Retrieves and displays all items.

```csharp
public async Task<IActionResult> Index()
{
    var items = await _cosmosDbService.GetItemsAsync();
    return View(items);
}
```

- **_cosmosDbService:** Interface for Cosmos DB interactions.
- **GetItemsAsync:** Fetches all items from the database.

#### Create Action
Displays the form for adding a new item.

```csharp
public IActionResult Create()
{
    return View();
}
```

Handles form submission and adds the item to the database.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> Create(ToDoItem item)
{
    if (ModelState.IsValid)
    {
        await _cosmosDbService.AddItemAsync(item);
        return RedirectToAction(nameof(Index));
    }
    return View(item);
}
```

#### Edit Action
Displays the form for editing an existing item.

```csharp
public async Task<IActionResult> Edit(string id)
{
    var item = await _cosmosDbService.GetItemAsync(id);
    return View(item);
}
```

Handles form submission to update the item.

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<IActionResult> Edit(ToDoItem item)
{
    if (ModelState.IsValid)
    {
        await _cosmosDbService.UpdateItemAsync(item);
        return RedirectToAction(nameof(Index));
    }
    return View(item);
}
```

#### Delete Action
Deletes an item by ID.

```csharp
public async Task<IActionResult> Delete(string id)
{
    await _cosmosDbService.DeleteItemAsync(id);
    return RedirectToAction(nameof(Index));
}
```

### 3. **Cosmos DB Service: CosmosDbService.cs**
This service contains methods for CRUD operations on Cosmos DB.

#### Initialization

```csharp
public CosmosDbService(CosmosClient dbClient, string databaseName, string containerName)
{
    _container = dbClient.GetContainer(databaseName, containerName);
}
```

#### Methods

- **GetItemsAsync:**
  Retrieves all items from the container.
  
  ```csharp
  public async Task<IEnumerable<ToDoItem>> GetItemsAsync()
  {
      var query = _container.GetItemQueryIterator<ToDoItem>(new QueryDefinition("SELECT * FROM c"));
      var results = new List<ToDoItem>();
      while (query.HasMoreResults)
      {
          var response = await query.ReadNextAsync();
          results.AddRange(response);
      }
      return results;
  }
  ```

- **AddItemAsync:**
  Inserts a new item into the container.

  ```csharp
  public async Task AddItemAsync(ToDoItem item)
  {
      await _container.CreateItemAsync(item, new PartitionKey(item.Id));
  }
  ```

- **UpdateItemAsync:**
  Updates an existing item in the container.

  ```csharp
  public async Task UpdateItemAsync(ToDoItem item)
  {
      await _container.UpsertItemAsync(item, new PartitionKey(item.Id));
  }
  ```

- **DeleteItemAsync:**
  Deletes an item from the container.

  ```csharp
  public async Task DeleteItemAsync(string id)
  {
      await _container.DeleteItemAsync<ToDoItem>(id, new PartitionKey(id));
  }
  ```

### 4. **Configuration: appsettings.json**
Contains the Cosmos DB configuration details.

```json
{
  "CosmosDb": {
    "Account": "<Your-CosmosDB-Account-URI>",
    "Key": "<Your-CosmosDB-Key>",
    "DatabaseName": "ToDoList",
    "ContainerName": "Items"
  }
}
```

### 5. **Startup.cs**
Registers the Cosmos DB service.

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<ICosmosDbService>(InitializeCosmosClientInstanceAsync(Configuration.GetSection("CosmosDb")).GetAwaiter().GetResult());
}

private static async Task<CosmosDbService> InitializeCosmosClientInstanceAsync(IConfigurationSection configurationSection)
{
    string account = configurationSection["Account"];
    string key = configurationSection["Key"];
    string databaseName = configurationSection["DatabaseName"];
    string containerName = configurationSection["ContainerName"];

    CosmosClient client = new CosmosClient(account, key);
    CosmosDbService cosmosDbService = new CosmosDbService(client, databaseName, containerName);

    var database = await client.CreateDatabaseIfNotExistsAsync(databaseName);
    await database.Database.CreateContainerIfNotExistsAsync(containerName, "/id");

    return cosmosDbService;
}
```

---

## How to Run the Application

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Azure-Samples/cosmos-dotnet-core-todo-app.git
   ```

2. **Configure Cosmos DB:**
   - Update `appsettings.json` with your Cosmos DB account details.

3. **Build and Run:**
   - Open the solution in Visual Studio.
   - Build the solution.
   - Run the application locally.

4. **Deploy to Azure (Optional):**
   - Publish the application to an Azure App Service.

---

## Key Takeaways
- **Integration:** Demonstrates seamless integration with Azure Cosmos DB.
- **Scalability:** Showcases best practices for building scalable cloud applications.
- **CRUD Operations:** Provides a clean implementation of CRUD operations using the Cosmos DB SDK.

---

## Resources
- [Azure Cosmos DB Documentation](https://learn.microsoft.com/en-us/azure/cosmos-db/)
- [Azure Cosmos DB SDK for .NET](https://learn.microsoft.com/en-us/azure/cosmos-db/sql-api-sdk-dotnet)
- [GitHub Repository](https://github.com/Azure-Samples/cosmos-dotnet-core-todo-app)
