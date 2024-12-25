
# Azure App Service Plan

An **Azure App Service Plan** defines the set of compute resources for your web app, API, or mobile backend in Azure App Service. It determines the region, operating system, instance size, and pricing tier. 

### Key Features:
- **Shared Resources**: Apps under the same plan share compute resources.
- **Scaling**: Offers manual and automatic scaling options based on pricing tiers.
- **Pricing Tiers**: Tailored to workloads, from development/testing to high-demand production.

---

## Pricing Tiers Overview

Azure App Service Plans are organized into three major categories:

### 1. **Dev/Test**  
- For less demanding workloads, suitable for development and testing.
- **Plans**: Free, Shared.
- **Limitations**:
  - No custom domains.
  - Limited scaling and features.

### 2. **Production**  
- Designed for most production workloads.
- **Plans**: Basic, Standard, PremiumV2, PremiumV3.
- Features include:
  - Custom domains (starting from Basic).
  - Manual scaling (Basic).
  - Auto-scaling and rule-based scaling (Premium P1 and higher).
  - Staging slots and daily backups.
  - Zone redundancy support (Premium P0 and higher).

### 3. **Isolated**  
- Dedicated hosting with no other customers sharing the machine.
- Ideal for highly secure workloads.
- **Plans**: Isolated and IsolatedV2.
- Higher costs due to dedicated resources and isolation.

---

## Legacy Plans
Some legacy plans, such as Standard (S1, S2, S3) and Premium (V1, V2), are still available but not recommended by Microsoft for new workloads.  
- **Standard Plans**: Now considered part of the legacy offering.  
- **Premium V1/V2**: Available but surpassed by PremiumV3 for performance and scalability.

---

## Performance Details

Azure provides a relative measure of performance using **Azure Compute Units (ACU)**:  
- **Baseline (100 ACU)**: Standard S1 Plan.  
- **Performance Scaling**: PremiumV2 (210 ACU) offers 110% faster performance compared to S1.  
- **Doubling Effect**:  
  - S1 → S2: Doubles CPU and memory.  
  - S2 → S3: Another doubling of resources.

> **Disk Space** and **Scaling Instances** remain constant within the same pricing tier.

---

## Feature Comparison (Highlights)

| Feature                     | Free/Shared | Basic  | Standard | PremiumV2 | PremiumV3 | Isolated |
|-----------------------------|-------------|--------|----------|-----------|-----------|----------|
| **Custom Domains**          | ❌          | ✅      | ✅        | ✅         | ✅         | ✅        |
| **Manual Scaling**          | ❌          | ✅      | ✅        | ✅         | ✅         | ✅        |
| **Auto Scaling**            | ❌          | ❌      | ❌        | ✅ (P1)    | ✅         | ✅        |
| **Daily Backups**           | ❌          | ❌      | ✅        | ✅         | ✅         | ✅        |
| **Staging Slots**           | ❌          | ❌      | ✅ (5)    | ✅         | ✅         | ✅        |
| **Zone Redundancy**         | ❌          | ❌      | ❌        | ✅ (P0)    | ✅         | ✅        |

---

## Creating an App Service Plan

### Azure Portal:
1. Log in to [Azure Portal](https://portal.azure.com).
2. Search for **App Service Plans** and click **Create**.
3. Fill in required fields:
   - **Subscription**
   - **Resource Group**
   - **Name**
   - **Region**
   - **Operating System**
   - **Pricing Tier**
4. Review and click **Create**.

### Azure CLI:
```bash
az appservice plan create --name <PLAN_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --location <REGION> \
  --sku <PRICING_TIER> \
  --is-linux
```

---

## Next Steps
1. **Deploy Apps**: Add your apps to the App Service Plan.
2. **Optimize Costs**: Select the tier that best fits your workload and scale appropriately.
3. **Monitor Performance**: Use Azure Monitor and Application Insights for insights.

For more details, refer to the [official documentation](https://learn.microsoft.com/en-us/azure/app-service/overview-hosting-plans).  
