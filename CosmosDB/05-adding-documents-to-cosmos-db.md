
# Adding Documents to Azure Cosmos DB

Azure Cosmos DB stores data in a JSON format and allows you to add documents programmatically or via its intuitive Data Explorer interface. Below are detailed steps and explanations for adding documents to a Cosmos DB container.

---

## Creating Documents in Data Explorer

### Steps to Add a Document
1. **Navigate to Your Container:**
   - Go to **Data Explorer** in the Cosmos DB account.
   - Select the database and container (e.g., `db1 > cars`).

2. **Create a New Item:**
   - Click on the **New Item** button.

3. **Input JSON Data:**
   - Enter data in JSON format. For example:
     ```json
     {
       "id": "1",
       "make": "bmw",
       "model": "X1",
       "vin": "123456",
       "color": "black",
       "doors": 4
     }
     ```
   - The `id` field must be unique within the container.

4. **Save the Document:**
   - Click **Save** to store the document in the container.

5. **System-Generated Properties:**
   - Cosmos DB automatically adds system properties:
     - `_rid`: A unique identifier for the row.
     - `_ts`: Timestamp of document creation.
     - `_etag`, `_self`, and others for internal use.

---

## Enforcing Unique Keys
- Unique keys ensure data integrity by preventing duplicates.
- Example: If `vin` is defined as a unique key, attempting to add another document with the same `vin` will result in an error:
  ```json
  {
    "id": "2",
    "make": "bmw",
    "model": "X1",
    "vin": "123456", // Duplicate unique key
    "color": "blue",
    "doors": 4
  }
  ```
  **Error:** `Entity already exists in the system.`

---

## Adding Multiple Documents
1. Create additional documents by modifying unique fields such as `id` and `vin`.
   ```json
   {
     "id": "2",
     "make": "honda",
     "model": "civic",
     "vin": "789010",
     "color": "green",
     "doors": 4
   }
   ```
   ```json
   {
     "id": "3",
     "make": "mazda",
     "model": "miata",
     "vin": "654321",
     "color": "red",
     "doors": 2
   }
   ```
2. Save each document after making the necessary changes.

---

## Querying Data in Data Explorer

### Query Syntax
1. **View All Documents:**
   - Default query:
     ```sql
     SELECT * FROM c
     ```
   - Returns all documents in a single JSON array.

2. **Filter with WHERE Clause:**
   - Retrieve specific documents:
     ```sql
     SELECT * FROM c WHERE c.make = "bmw"
     ```
     Example Output:
     ```json
     [
       {
         "id": "1",
         "make": "bmw",
         "model": "X1",
         "vin": "123456",
         "color": "black",
         "doors": 4
       }
     ]
     ```

3. **Query Non-Partitioned Fields:**
   - Query fields not part of the partition key:
     ```sql
     SELECT * FROM c WHERE c.model = "miata"
     ```

---

## Notes and Best Practices
- **Programmatic Insertion:** Use SDKs (e.g., .NET, JavaScript) for real-world applications to add and query data.
- **Partition Key:** Design efficient partition keys to optimize performance.
- **Request Units (RUs):**
  - Each query and operation consumes RUs.
  - Example: A query might consume 2 RUs, allowing approximately 500 queries per second on a container with 1000 RUs.

---

## Conclusion
The Cosmos DB Data Explorer is a powerful tool for quick data entry and queries. For production use, it is recommended to interact with the database programmatically using the Cosmos DB SDKs.
