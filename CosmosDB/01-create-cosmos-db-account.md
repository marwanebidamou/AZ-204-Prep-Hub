# Azure Cosmos DB Overview

Azure Cosmos DB is a globally distributed, multi-model database service provided by Microsoft Azure. It supports multiple APIs and offers comprehensive solutions for various data storage and retrieval needs.

---

## Key Features of Azure Cosmos DB

### Multi-Model Database
- **NoSQL Database:** Stores JSON documents.
- **Graph Database:** Supports Gremlin API for graph data.
- **Column-Family Database:** Compatible with Cassandra.
- **Table Storage:** Enterprise-grade table storage.
- **Relational Database:** PostgreSQL API for relational data storage.

### Global Distribution
- Built for global availability with multi-region support.
- Features geo-redundancy and multi-region writes.
- Low-latency access to data worldwide.

### High Availability and Scalability
- **99.999% availability SLA** for multi-region accounts.
- Elastic scalability for throughput and storage.
- Designed for high-speed read and write operations.

---

## Creating a Cosmos DB Account

1. **Navigate to Azure Portal:**
   - Go to **Create a Resource** > **Databases** > **Azure Cosmos DB**.

2. **Choose API:**
   - **NoSQL:** Ideal for new projects requiring JSON document storage.
   - **PostgreSQL:** For relational data needs.
   - **MongoDB:** For applications migrating from MongoDB.
   - **Cassandra:** For apps using Cassandra API.
   - **Gremlin:** For graph data storage.
   - **Table:** For Azure Table Storage migration.

3. **Set Basic Configuration:**
   - Choose **Subscription** and **Resource Group**.
   - Provide a globally unique account name.
   - Select a geographic **Region** for the database.

4. **Select Capacity Mode:**
   - **Provisioned Throughput:** Predefined request units per second.
   - **Serverless:** Pay-as-you-go based on usage.
   - Enable **Free Tier** (1,000 RU/s and 25GB storage free per subscription).

5. **Global Distribution Settings:**
   - Enable geo-redundancy for automatic multi-region replication.
   - Optionally configure multi-region writes.

6. **Review and Create:**
   - Validate all settings and deploy the Cosmos DB account.

---

## Working with Data in Cosmos DB

### Adding a Database and Container

1. Go to the **Data Explorer** in the Azure Portal.
2. Click **New Container**.
3. Set database and container names.
4. Configure throughput (shared or dedicated).
5. Add partition keys for optimized storage.



### Consistency Levels

1. **Strong:** Guaranteed consistency across replicas.
2. **Bounded Staleness:** Configurable lag for reads.
3. **Session:** Consistency within a session.
4. **Consistent Prefix:** Reads never see out-of-order writes.
5. **Eventual:** High availability with minimal latency.

---

## Best Practices

1. **Partitioning:**
   - Choose a partition key that evenly distributes data.

2. **Throughput Management:**
   - Use **Auto-Scale** to handle unpredictable workloads.

3. **Monitoring:**
   - Use **Azure Monitor** to track performance and costs.

4. **Indexing Policy:**
   - Customize indexing to optimize query performance.

5. **Security:**
   - Enable **Azure Active Directory** for secure access.
   - Use **VNet** and **Private Endpoints** to restrict access.

---

## Resources

- [Azure Cosmos DB Documentation](https://learn.microsoft.com/en-us/azure/cosmos-db/)
- [Best Practices for Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/best-practices)
- [Consistency Levels](https://learn.microsoft.com/en-us/azure/cosmos-db/consistency-levels)
- [Pricing Details](https://azure.microsoft.com/en-us/pricing/details/cosmos-db/)
