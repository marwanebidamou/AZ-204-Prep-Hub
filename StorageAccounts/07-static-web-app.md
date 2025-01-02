# Azure Static Web Apps Overview

Azure Static Web Apps is a hosting service for static web applications. It is designed to host HTML, JavaScript, CSS, and images while integrating with serverless APIs like Azure Functions for backend functionality.

---

## What are Static Web Apps?

- **Static Content:** Hosts static assets such as HTML, JavaScript, and CSS without server-side code execution.
- **Serverless Backend:** Automatically creates and integrates Azure Functions for backend operations.
- **Cost-Effective:** Includes a free tier with features like custom domains and SSL.
- **Scalable:** Ideal for personal projects, testing, and lightweight production workloads.

---

## Key Features

### Hosting Plans

- **Free Plan:**
  - 100 GB bandwidth per month.
  - Includes custom domains and SSL.
  - Limited to three staging environments.

- **Standard Plan:**
  - Increased app size and bandwidth.
  - Private endpoints and staging environments.
  - Supports authentication options.

### Deployment Options

- Deploy directly from **GitHub** repositories.
- Continuous deployment using GitHub Actions.
- Manual deployment options for custom workflows.

---

## Creating a Static Web App

1. **Navigate to the Azure Portal:**
   - Select **Create a Resource** > **Static Web Apps**.

2. **Fill Basic Information:**
   - Choose a **Subscription**.
   - Create or select a **Resource Group** (e.g., `staticwebapp`).
   - Specify the **Name** of the app.
   - Choose a **Plan** (e.g., Free Plan).
   - Select a **Region**.

3. **Connect to GitHub:**
   - Authenticate to GitHub and authorize Azure.
   - Select the repository containing your static site code.
   - Choose the **branch** and **build configuration**.

4. **Review and Create:**
   - Validate the information and click **Create**.

---

## Example: Deploying a Vanilla JavaScript App

1. Clone the repository `Demo-vanilla-app` from GitHub or create a static site with an `index.html` and `style.css` file.
2. Deploy the app using the Azure Static Web App interface.
3. Access the deployed app via the generated URL (e.g., `https://<random-name>.azurestaticapps.net`).

---

## Managing Static Web Apps

### Custom Domains
- Configure custom domains with SSL certificates.
- Add domains via the Azure portal.

### Staging Environments
- Use up to three staging environments for testing.
- Link staging environments to different branches in GitHub.

### Integrated Backend APIs
- Automatically deploy Azure Functions for backend logic.
- Functions are deployed in a separate API environment but linked to the static app.

### Monitoring
- Use **Azure Monitor** and **Application Insights** for traffic and performance analysis.

---

## Best Practices

1. **Use GitHub for Deployment:**
   - Simplifies version control and continuous integration.

2. **Optimize for Performance:**
   - Minify CSS, JavaScript, and HTML.
   - Use caching headers for static assets.

3. **Integrate APIs Smartly:**
   - Use Azure Functions for serverless backend logic.

4. **Secure Custom Domains:**
   - Always enable SSL for secure connections.

---

## Resources
- [Azure Static Web Apps Documentation](https://learn.microsoft.com/en-us/azure/static-web-apps/)
- [Custom Domains in Static Web Apps](https://learn.microsoft.com/en-us/azure/static-web-apps/custom-domain)
