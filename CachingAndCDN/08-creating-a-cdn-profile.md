# Creating a CDN Profile in Azure

Azure Content Delivery Network (CDN) is a global caching solution designed to improve application performance and availability. It distributes content closer to end users by using a global network of edge locations. This guide covers the steps to create a CDN profile and endpoint in Azure.

---

## Azure CDN Overview

### Key Features
- **Content Caching**:
  - Supports static content (e.g., images, CSS, JavaScript) and dynamic content.
  - Reduces load times and latency for users.
- **Global Load Balancing**:
  - Distributes user requests to the closest or fastest server.
- **Web Application Firewall (WAF)**:
  - Provides enhanced security against threats.
- **Integration with Azure Services**:
  - Works with Azure Blob Storage, App Services, and custom origins.

### Azure CDN Tiers
1. **Front Door (Recommended)**:
   - Combines CDN with global load balancing and WAF.
   - Ideal for modern, scalable applications.
2. **CDN Standard and Premium (Classic)**:
   - Standard (Microsoft and Egeo): Basic CDN functionality.
   - Premium (Egeo): Advanced CDN features.

---

## Steps to Create a CDN Profile

### 1. **Search and Create a CDN Profile**
- Go to the Azure Portal.
- Search for "Azure Front Door and CDN Profiles."
- Select **+ Create**.

### 2. **Configure Profile Settings**
1. **Basics Tab**:
   - Select **Subscription**.
   - Choose a **Resource Group** or create a new one.
   - Enter a globally unique **CDN Profile Name**.
   - Choose the **Pricing Tier**:
     - Front Door Standard or Premium for modern use cases.
     - CDN Standard (Microsoft) or CDN Premium (Egeo).

2. **Review Resource Provider**:
   - Ensure the resource provider `Microsoft.CDN` is registered for the subscription.
     - Navigate to **Subscriptions > Resource Providers**.
     - Search for `Microsoft.CDN` and click **Register** if not already registered.

3. **Review and Create**:
   - Validate settings and click **Create** to deploy the profile.

---

## Creating an Endpoint

After creating a CDN profile, the next step is to configure an endpoint to serve cached content.

### Steps to Create an Endpoint

1. **Navigate to the CDN Profile**:
   - Locate your CDN profile under the selected resource group.

2. **Add an Endpoint**:
   - Click **+ Endpoint**.
   - Configure the following:
     - **Endpoint Name**: Choose a unique name (e.g., `mycdnendpoint`).
     - **Origin Type**:
       - Azure Storage Account (Static files).
       - App Service (Web applications).
       - Custom Origin (Public URLs or on-premises servers).
     - **Origin Hostname**: Specify the backend server or service.

3. **Optimization Type**:
   - General Web Delivery: Default for websites.
   - Video/Media Streaming: For large media files.
   - Large File Download: Optimized for large files like software packages.

4. **Enable HTTPS**:
   - Ensure secure delivery by enabling HTTPS (TLS/SSL).

5. **Review and Deploy**:
   - Validate settings and deploy the endpoint.

### Notes:
- **Propagation Time**:
  - Changes can take up to 10 minutes to propagate globally.
- **Custom Domain**:
  - You can configure a custom domain for the endpoint and enable HTTPS.

---

## Using Azure CDN in Your Application

To integrate Azure CDN into your application, follow these steps:

### 1. **Upload Content to Your Origin**
- Upload static files (e.g., images, JavaScript, CSS) to your configured origin (e.g., Azure Blob Storage or App Service).
- Ensure the origin is accessible by the CDN.

### 2. **Update Application URLs**
- Replace references to static content URLs in your application with the CDN endpoint URL.
  Example:
  ```html
  <img src="https://<cdn-endpoint-name>.azureedge.net/images/logo.png" />
  ```

### 3. **Test CDN Integration**
- Access your application and verify that static content is served through the CDN endpoint.
- Use browser developer tools to check the network tab and confirm CDN URLs are being used.

### 4. **Optimize Cache Settings**
- Configure cache expiration policies for static content to control how long assets are cached at edge locations.
- Use versioning in your asset URLs to handle updates (e.g., `logo-v2.png`).

---

## Summary
Azure CDN helps reduce latency and improve the performance of web applications by caching static and dynamic content. By integrating CDN endpoints into your application, you can offload traffic from your backend servers, reduce costs, and enhance user experience globally. The Front Door service offers advanced capabilities and is recommended for modern applications.
 