# Deploying an Azure Web App from Azure Container Registry

## Overview
This document outlines the steps to deploy a containerized application into an Azure Web App from Azure Container Registry (ACR). Azure Web App provides additional options for scaling and production-ready features compared to Azure Container Instances (ACI).

---

## 1. Setting Up the Azure Web App

### Using Azure Portal
1. **Create a New Web App:**
   - Navigate to the **Azure Portal**.
   - Click **Create a Resource** > **Web App**.
   - Provide the following details:
     - **Resource Group:** Select or create one.
     - **Name:** Enter a unique name for your app (e.g., `SampleWebApp12345`).
     - **Publish:** Select **Docker Container**.
     - **Operating System:** Select **Linux**.
     - **Region:** Choose a preferred region.
    

2. **Configure Container Settings:**
   - Choose **Azure Container Registry (ACR)** as the image source.
   - Select the desired image and tag from your ACR.
   - Skip optional configurations like **Networking** or **Application Insights** unless needed.

3. **Review and Create:**
   - Review the summary and pricing estimate.
   - Click **Create** to deploy the Web App.

---

## 2. Accessing the Deployed Web App

### Steps
1. Once the deployment is complete, click **Go to Resource**.
2. Copy the provided **URL** for the Web App.
3. Paste the URL into a browser to view your application.
   - You should see the containerized app running with its content (e.g., "Hello there from containers").

---

## 3. Key Differences Between Azure Container Instance (ACI) and Azure Web App
- **Azure Container Instance (ACI):**
  - Simpler and faster to deploy.
  - Limited to a maximum of 4 running instances.
  - Ideal for lightweight, short-term deployments.

- **Azure Web App:**
  - Offers advanced scaling options (e.g., scaling up/out with premium plans).
  - Supports integration with backups and other Azure services.
  - Suitable for production-grade containerized applications.
  - More options for managing app complexity and configurations.

---

## Notes
- **Admin Account:** Ensure the admin account for ACR is enabled for seamless integration.
- **Scaling Options:** Azure Web App allows scaling for higher workloads and complex scenarios.
- **Deletion:** Clean up resources after testing to avoid unnecessary charges.

This document highlights the deployment process for containers into Azure Web App, showcasing its advanced features and suitability for scalable, production-ready applications.
