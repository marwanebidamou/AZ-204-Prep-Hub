
# Creating a Cosmos DB Collection (Container)

In Azure Cosmos DB, collections (also called containers) are fundamental units for storing data within a database. This guide walks you through creating a database and container in Cosmos DB.

---

## Steps to Create a Container

### 1. **Access the Data Explorer**
- Navigate to the **Data Explorer** section in the Cosmos DB account.
- Choose between:
  - **Sample Data:** Creates a pre-filled container with example data.
  - **New Container:** Allows you to define your own container and database.

---

### 2. **Define a Database**
- Click on **New Container** to create both a database and a container.
- **Database ID:** Assign a unique name for the database, e.g., `DB1`.
- **Throughput Allocation:**
  - Assign **Request Units (RUs):** Choose between 100 to 1000 RUs for shared throughput.
  - Optionally enable **Autoscale:** Automatically adjusts throughput based on demand.

---

### 3. **Define a Container**
- **Container ID:** Specify a name for the container, e.g., `cars`.
- **Partition Key:**
  - Select a field to partition your data for scalability and efficient querying.
  - **Good Examples:** Fields with limited and diverse values like `make` (e.g., BMW, Toyota).
  - **Avoid:** Fields with too many unique values (e.g., VIN, license plate) or static values (e.g., year).

---

### 4. **Optional Settings**
- **Unique Keys:** Define unique constraints for specific fields, such as VIN for cars.
- **Database Operations:** Enable features like stored procedures, triggers, and user-defined functions.

---

## Example Configuration

| Parameter              | Value                    |
|------------------------|--------------------------|
| Database ID            | `DB1`                   |
| Throughput             | 1000 RUs (Autoscale)    |
| Container ID           | `cars`                  |
| Partition Key          | `/make`                 |
| Unique Key (Optional)  | `/VIN`                  |

---

## Querying the Container
Once created, you can query the container using SQL-like syntax. Cosmos DB supports a SQL API for querying JSON data.

### Example Query
```sql
SELECT * FROM C
```
- **`C`**: Alias for the current container (e.g., `cars`).
- Retrieves all items from the container.

---

## Key Considerations
1. **Throughput Costs:**
   - Throughput is billed hourly based on the RUs assigned to the database or container.
   - Free tier accounts allow up to 1000 RUs without charges.

2. **Partition Key:**
   - A well-chosen partition key is crucial for scalability and performance.
   - Avoid highly unique or static fields.

3. **Database Features:**
   - Stored Procedures: Automate tasks within the database.
   - Triggers: Perform actions in response to events.
   - User-Defined Functions: Add custom logic to your queries.

---

## Example Use Case
For a container storing car information:
- **Partition Key:** `/make`
- **Unique Key:** `/VIN`
- Queries can efficiently filter cars by make and retrieve specific entries using unique identifiers.

---

## Next Steps
After creating the container:
- Insert sample data into the container.
- Experiment with querying and advanced features like stored procedures and triggers.

---
