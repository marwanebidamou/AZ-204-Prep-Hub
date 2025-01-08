# Common PowerShell Commands for AZ-204 Certification

This document includes essential PowerShell commands to help you prepare for the AZ-204 certification exam. These commands cover common scenarios like managing Azure resources, automating deployments, and configuring services.

---

## General Azure Management

### Login and Account Management
```powershell
# Login to Azure
Connect-AzAccount

# List all subscriptions
Get-AzSubscription

# Set active subscription
Set-AzContext -SubscriptionId <subscription-id>
```

### Resource Groups
```powershell
# Create a resource group
New-AzResourceGroup -Name "MyResourceGroup" -Location "East US"

# List all resource groups
Get-AzResourceGroup

# Delete a resource group
Remove-AzResourceGroup -Name "MyResourceGroup"
```

---

## Azure App Service Management

### Creating and Managing App Services
```powershell
# Create an App Service plan
New-AzAppServicePlan -Name "MyAppPlan" -ResourceGroupName "MyResourceGroup" -Location "East US" -Tier "Standard" -NumberofWorkers 1

# Create a Web App
New-AzWebApp -Name "MyWebApp" -ResourceGroupName "MyResourceGroup" -AppServicePlan "MyAppPlan"

# List Web Apps in a Resource Group
Get-AzWebApp -ResourceGroupName "MyResourceGroup"

# Delete a Web App
Remove-AzWebApp -Name "MyWebApp" -ResourceGroupName "MyResourceGroup"
```

---

## Azure Logic Apps

### Managing Logic Apps
```powershell
# List Logic Apps in a Resource Group
Get-AzLogicApp -ResourceGroupName "MyResourceGroup"

# Start a Logic App
Start-AzLogicApp -ResourceGroupName "MyResourceGroup" -Name "MyLogicApp"

# Stop a Logic App
Stop-AzLogicApp -ResourceGroupName "MyResourceGroup" -Name "MyLogicApp"
```

---

## Azure Storage Management

### Blob Storage
```powershell
# Create a Storage Account
New-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorageacct" -Location "East US" -SkuName "Standard_LRS" -Kind "StorageV2"

# Get Storage Account Context
$ctx = (Get-AzStorageAccount -ResourceGroupName "MyResourceGroup" -Name "mystorageacct").Context

# List Blobs in a Container
Get-AzStorageBlob -Container "my-container" -Context $ctx

# Upload a Blob
Set-AzStorageBlobContent -File "file-path" -Container "my-container" -Blob "myfile.txt" -Context $ctx

# Change Blob Tier to Archive
Set-AzStorageBlobTier -BlobName "myfile.txt" -Container "my-container" -Tier "Archive" -Context $ctx
```

---

## Azure Functions

### Managing Azure Functions
```powershell
# Create a Function App
New-AzFunctionApp -ResourceGroupName "MyResourceGroup" -Name "MyFunctionApp" -StorageAccountName "mystorageacct" -AppServicePlan "MyAppPlan"

# List Function Apps in a Resource Group
Get-AzFunctionApp -ResourceGroupName "MyResourceGroup"

# Delete a Function App
Remove-AzFunctionApp -Name "MyFunctionApp" -ResourceGroupName "MyResourceGroup"
```

---

## Virtual Machines

### Managing Virtual Machines
```powershell
# Create a Virtual Machine
New-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM" -Location "East US" -Image "Win2019Datacenter" -Credential (Get-Credential)

# Start a Virtual Machine
Start-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM"

# Stop a Virtual Machine
Stop-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM"

# Delete a Virtual Machine
Remove-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyVM"
```

---

## Networking

### Managing Virtual Networks
```powershell
# Create a Virtual Network
New-AzVirtualNetwork -ResourceGroupName "MyResourceGroup" -Name "MyVNet" -AddressPrefix "10.0.0.0/16" -Location "East US"

# Create a Subnet
Add-AzVirtualNetworkSubnetConfig -Name "MySubnet" -AddressPrefix "10.0.1.0/24" -VirtualNetwork $vnet

# List Virtual Networks
Get-AzVirtualNetwork -ResourceGroupName "MyResourceGroup"
```

---

## Monitoring and Diagnostics

### Setting up Monitoring
```powershell
# Enable Application Insights for a Web App
Set-AzWebApp -ResourceGroupName "MyResourceGroup" -Name "MyWebApp" -EnableApplicationInsights $true

# Enable Diagnostics Logging for a Web App
Set-AzWebApp -ResourceGroupName "MyResourceGroup" -Name "MyWebApp" -HttpLoggingEnabled $true
```

---

## References
- [Azure PowerShell Documentation](https://learn.microsoft.com/en-us/powershell/azure/)