# Common Azure CLI Commands for AZ-204 Certification

This document contains essential Azure CLI commands to assist with preparation for the AZ-204 certification exam. These commands cover scenarios like managing Azure resources, automating deployments, and configuring services.

---

## General Azure Management

### Login and Account Management
```bash
# Login to Azure
az login

# List all subscriptions
az account list --output table

# Set active subscription
az account set --subscription <subscription-id>
```

### Resource Groups
```bash
# Create a resource group
az group create --name MyResourceGroup --location eastus

# List all resource groups
az group list --output table

# Delete a resource group
az group delete --name MyResourceGroup --yes --no-wait
```

---

## Azure App Service Management

### Creating and Managing App Services
```bash
# Create an App Service plan
az appservice plan create --name MyAppPlan --resource-group MyResourceGroup --location eastus --sku S1

# Create a Web App
az webapp create --name MyWebApp --resource-group MyResourceGroup --plan MyAppPlan

# List Web Apps in a Resource Group
az webapp list --resource-group MyResourceGroup --output table

# Delete a Web App
az webapp delete --name MyWebApp --resource-group MyResourceGroup
```

---

## Azure Logic Apps

### Managing Logic Apps
```bash
# List Logic Apps in a Resource Group
az logic workflow list --resource-group MyResourceGroup --output table

# Start a Logic App
az logic workflow run trigger --resource-group MyResourceGroup --name MyLogicApp --workflow-name MyLogicApp
```

---

## Azure Storage Management

### Blob Storage
```bash
# Create a Storage Account
az storage account create --name mystorageacct --resource-group MyResourceGroup --location eastus --sku Standard_LRS --kind StorageV2

# List Storage Accounts
az storage account list --resource-group MyResourceGroup --output table

# Upload a Blob
az storage blob upload --account-name mystorageacct --container-name my-container --name myfile.txt --file /path/to/myfile.txt

# Change Blob Tier to Archive
az storage blob set-tier --account-name mystorageacct --container-name my-container --name myfile.txt --tier Archive
```

---

## Azure Functions

### Managing Azure Functions
```bash
# Create a Function App
az functionapp create --resource-group MyResourceGroup --name MyFunctionApp --storage-account mystorageacct --consumption-plan-location eastus

# List Function Apps in a Resource Group
az functionapp list --resource-group MyResourceGroup --output table

# Delete a Function App
az functionapp delete --name MyFunctionApp --resource-group MyResourceGroup
```

---

## Virtual Machines

### Managing Virtual Machines
```bash
# Create a Virtual Machine
az vm create --resource-group MyResourceGroup --name MyVM --image Win2019Datacenter --admin-username azureuser --admin-password <password>

# Start a Virtual Machine
az vm start --resource-group MyResourceGroup --name MyVM

# Stop a Virtual Machine
az vm stop --resource-group MyResourceGroup --name MyVM

# Delete a Virtual Machine
az vm delete --resource-group MyResourceGroup --name MyVM --yes
```

---

## Networking

### Managing Virtual Networks
```bash
# Create a Virtual Network
az network vnet create --resource-group MyResourceGroup --name MyVNet --address-prefix 10.0.0.0/16 --subnet-name MySubnet --subnet-prefix 10.0.1.0/24

# List Virtual Networks
az network vnet list --resource-group MyResourceGroup --output table
```

---

## Monitoring and Diagnostics

### Setting up Monitoring
```bash
# Enable Application Insights for a Web App
az webapp update --resource-group MyResourceGroup --name MyWebApp --set appInsightsEnabled=true

# Enable Diagnostics Logging for a Web App
az webapp log config --resource-group MyResourceGroup --name MyWebApp --web-server-logging filesystem
```

---

## References
- [Azure CLI Documentation](https://learn.microsoft.com/en-us/cli/azure/)