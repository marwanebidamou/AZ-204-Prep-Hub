# Creating an Azure Web App  

This guide walks you through the process of creating an Azure Web App using the Azure Portal, Azure CLI, and Azure PowerShell. It includes all prerequisites and provides step-by-step instructions.  

---

## 1. Overview  
Azure Web Apps are part of the Azure App Service offering. They allow you to deploy and manage scalable web applications in various languages and frameworks such as .NET, Java, Node.js, Python, and more.  

### Key Features:
- Managed hosting environment  
- Continuous deployment support  
- Scalability and high availability  


---

## 2. Prerequisites  

### Tools and Versions
- **Azure CLI:** Ensure you have Azure CLI installed and up-to-date (use `az --version` to check).  
- **Azure PowerShell:** Install and configure Azure PowerShell (`Get-Module -ListAvailable Az` to verify).  


### Resources
- An active Azure Subscription.  
- An existing or new **Resource Group** and **App Service Plan**.  

---

## 3. Create a Web App via Azure Portal  

### Steps:
1. **Log in to Azure Portal:**  
   Navigate to [Azure Portal](https://portal.azure.com).  

2. **Navigate to App Services:**  
   Search for and select **App Services** from the search bar.  

3. **Click on "Create":**  
   Click the **Create** button to start creating a new Web App.  

4. **Fill in the Basics:**
   - **Subscription:** Choose your subscription.  
   - **Resource Group:** Select an existing one or create a new resource group.  
   - **Name:** Provide a globally unique name for your Web App.  
   - **Runtime Stack:** Choose the runtime (e.g., .NET, Node.js, Python).  
   - **Region:** Choose the region closest to your users.  
   - **Publish Option:** Select whether you want to deploy your app as **Code** or in a **Container**.  

5. **Configure Hosting:**
   - **Plan:** Choose an existing App Service Plan or create a new one based on your performance and pricing needs.  

6. **Review and Create:**  
   - Review your settings, and click **Create** to deploy your Web App.  

---

## 4. Create a Web App via Azure CLI  

### Prerequisites:
- Install and configure Azure CLI.  
- Ensure you’re signed in:  
  ```bash
  az login
  ```

### Commands to Create a Web App:

#### Creating a Web App for Code Deployment:
```bash
az webapp create --resource-group <RESOURCE_GROUP_NAME> \
  --plan <APP_SERVICE_PLAN_NAME> \
  --name <WEB_APP_NAME> \
  --runtime <RUNTIME>
```

#### Creating a Web App for Container Deployment:
```bash
az webapp create --resource-group <RESOURCE_GROUP_NAME> \
  --plan <APP_SERVICE_PLAN_NAME> \
  --name <WEB_APP_NAME> \
  --deployment-container-image-name <IMAGE_NAME>
```

#### Using `az webapp up` for Quick Deployment:
1. **Create a Local Folder:**
   ```bash
   mkdir MyWebApp
   cd MyWebApp
   ```
2. **Clone a Sample Repository:**
   ```bash
   git clone https://github.com/Azure-Samples/html-docs-hello-world .
   ```
3. **Deploy the App:**
   ```bash
   az webapp up --name <WEB_APP_NAME>
   ```
   - Azure will automatically create a resource group and App Service Plan if they do not exist.  
   - Replace `<WEB_APP_NAME>` with your desired app name.  

---

## 5. Create a Web App via Azure PowerShell  

### Prerequisites:
- Install and configure Azure PowerShell.  
- Ensure you’re signed in:  
  ```powershell
  Connect-AzAccount
  ```

### Commands to Create a Web App:

#### Creating a Resource Group:
```powershell
New-AzResourceGroup -Name <RESOURCE_GROUP_NAME> -Location <LOCATION>
```

#### Creating an App Service Plan:
```powershell
New-AzAppServicePlan -ResourceGroupName <RESOURCE_GROUP_NAME> -Name <APP_SERVICE_PLAN_NAME> \
  -Location <LOCATION> -Tier Free
```

#### Creating a Web App:
```powershell
New-AzWebApp -ResourceGroupName <RESOURCE_GROUP_NAME> -Name <WEB_APP_NAME> \
  -Location <LOCATION> -AppServicePlan <APP_SERVICE_PLAN_NAME>
```

---

## 6. Verify Deployment  

### Using the Azure Portal:
1. Go to **App Services** in the Azure Portal.  
2. Select your Web App to open its dashboard.  
3. Browse your Web App by clicking on the **URL** in the overview.  

### Using Azure CLI:
```bash
az webapp browse --name <WEB_APP_NAME> --resource-group <RESOURCE_GROUP_NAME>
```

### Using Azure PowerShell:
```powershell
Get-AzWebApp -ResourceGroupName <RESOURCE_GROUP_NAME> -Name <WEB_APP_NAME>
```

---

## 7. Next Steps  

- Set up Continuous Deployment with Azure DevOps or GitHub.  
- Configure custom domains and SSL.  
- Monitor and scale your Web App.  

For more details, refer to the [official Azure Web App documentation](https://learn.microsoft.com/en-us/azure/app-service/).
