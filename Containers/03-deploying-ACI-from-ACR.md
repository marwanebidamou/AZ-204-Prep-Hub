
# Deploying an Application to Azure Container Instances (ACI) from Azure Container Registry (ACR)

## Overview
This document outlines the process of setting up an Azure Container Registry (ACR), managing container images, and deploying containerized applications to Azure Container Instances (ACI). This guide uses Azure CLI, Azure Portal, and best practices for container deployment.

---

## 1. Setting Up Azure Container Registry (ACR)

### Using Azure CLI
1. **Login to Azure:**
   ```bash
   az login
   ```
2. **Create a Resource Group:**
   ```bash
   az group create --name <resource-group-name> --location <location>
   ```
3. **Create the Container Registry:**
   ```bash
   az acr create --resource-group <resource-group-name>      --name <acr-name> --sku Basic
   ```

### Using Azure Portal
1. Navigate to **Azure Portal**.
2. Click **Create a Resource** > **Containers** > **Container Registry**.
3. Provide the required details:
   - **Resource Group:** Select or create one.
   - **Registry Name:** Enter a unique name.
   - **SKU:** Select Basic.
4. Click **Review + Create** and then **Create**.

---

## 2. Pushing Images to Azure Container Registry

### Steps
1. **Build Your Docker Image:**
   ```bash
   docker build -t <image-name>:<tag> .
   ```
2. **Login to ACR:**
   ```bash
   az acr login --name <acr-name>
   ```
3. **Tag the Docker Image:**
   ```bash
   docker tag <image-name>:<tag> <acr-name>.azurecr.io/<image-name>:<tag>
   ```
4. **Push the Image to ACR:**
   ```bash
   docker push <acr-name>.azurecr.io/<image-name>:<tag>
   ```

### Verify in Azure Portal
1. Navigate to your **Container Registry** resource in Azure.
2. Go to **Repositories** and verify the pushed image.

---

## 3. Enabling Admin Access for Testing

1. In the Azure Portal, go to your **Container Registry**.
2. Under **Settings**, navigate to **Access Keys**.
3. Enable the **Admin User** toggle.
4. Copy the **username** and **passwords** for deployment purposes.

> **Note:** Remember to disable or regenerate credentials after testing.

---

## 4. Deploying to Azure Container Instances (ACI)

### Using Azure Portal
1. Navigate to **Azure Portal** > **Create a Resource** > **Containers** > **Container Instances**.
2. Provide the container instance details:
   - **Resource Group:** Use the same as your container registry for convenience.
   - **Name:** Specify a unique name for the instance.
   - **Image Source:** Select **Azure Container Registry** and choose the desired image and tag.
   - **DNS Label:** Define a custom DNS label for public access (e.g., `my-container-app`).
3. Click **Review + Create** and then **Create**.

### Validate Deployment
1. After deployment, go to the resource page for the container instance.
2. Copy the **fully qualified domain name (FQDN)** or **IP address**.
3. Open a browser and paste the URL to verify the application is running.

---

## 5. Monitoring and Logs

- Check logs in the Azure Portal under the **Container** section.
- Logs display pull status, deployment details, and runtime metrics like uptime and restarts.

---

## Notes
- Containers in ACR can be deployed to any platform supporting containers, such as AWS, Google Cloud, or Kubernetes.
- Use the Azure CLI or PowerShell for automated and scriptable deployments.

---

This guide provides a streamlined approach to container deployment using Azure services, making it easy to deploy, manage, and scale applications efficiently.
