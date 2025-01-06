# Azure Cache for Redis: Scaling Overview

Scaling Azure Cache for Redis is an essential feature that allows applications to adapt to changing workloads by adjusting the memory and features of the cache. Understanding how scaling works, its limitations, and the supported paths is key to leveraging this capability effectively.

---

## Key Points of Scaling Azure Cache for Redis

### 1. **Scaling Options**
- **Within a Tier**: You can scale **up** between different sizes of the same tier (e.g., Basic C0 → Basic C1 → Basic C2).
- **Across Tiers**:
  - Upgrade from **Basic** to **Standard**.
  - Upgrade from **Standard** to **Premium**.
  - **Note**: You cannot scale directly from Basic to Premium; the transition must be incremental (Basic → Standard → Premium).

### 2. **No Scaling Down**
- Scaling **down** (reducing memory or downgrading tiers) is **not supported**.
- This limitation requires careful planning when selecting the initial tier and size of the cache to avoid over-provisioning.

---

## Example Scaling Process

### Scenario
You have a **Basic C0** tier cache (250 MB memory) and need to increase capacity.

### Steps:
1. Navigate to the **Scaling** option in the Azure portal for your Redis cache instance.
2. Select a higher tier or size:
   - Example: Scale from **Basic C0** to **Basic C1** (1 GB memory).
3. Confirm your selection.
4. The scaling process begins and typically a few minutes.

---

## Key Scaling Features

### Restrictions and Path
- Once you scale to a higher size (e.g., Basic C1), you **cannot return** to the lower size (e.g., Basic C0).
- Scaling across tiers requires stepwise progression:
  - Example: **Basic** → **Standard** → **Premium**.

### Indicators in the Azure Portal
- The interface provides **visual indicators** of available scaling options:
  - **Available tiers/sizes**: Highlighted in color.
  - **Unavailable options**: Grayed out with a notice (e.g., "Cannot scale down").

---

## Considerations

1. **Memory Allocation**:
   - Each tier offers progressively larger memory sizes.
   - Higher tiers unlock advanced features such as clustering and persistence.

2. **Downtime**:
   - Scaling involves provisioning a new cache instance.
   - Allow for brief interruptions during the transition.

3. **Planning Ahead**:
   - Ensure the initial configuration aligns with anticipated growth, as scaling down is not possible.

---

### Summary

Azure Cache for Redis scaling is a powerful tool for managing application performance and adapting to demand. By understanding its tier-based progression, lack of downward scalability, and the implications of scaling decisions, developers can effectively utilize Redis Cache for dynamic workloads.
