# Using Application Quickstart to Code an Application with Entra ID

The Microsoft Identity Platform provides a Quickstart feature to help developers integrate authentication into their applications. In this guide, we'll walk through setting up and running a sample application that uses Entra ID (formerly Azure AD) for user authentication.

---

## Understanding the Authentication Flow
![Quickstart Application](https://registeredapps.hosting.portal.azure.net/registeredapps/Content/1.0.2896.1143/Quickstarts/en/media/quickstart-v2-aspnet-core-webapp/aspnetcorewebapp-intro.svg "Quickstart Application")
1. **User Accesses the Website**: The client navigates to your application.
2. **Redirection to Entra ID**: The application redirects the client to the Microsoft Identity Platform for authentication.
3. **User Login**: The user provides their credentials.
4. **Token Issuance**: Upon successful authentication, the Identity Platform issues an **access token** and redirects the client back to your website.
5. **Token Validation**: The client sends the access token to your application, where it's validated for further access.

---

## Steps to Use the Quickstart Application
### 1. **Download the Quickstart Code**
- Navigate to the **Quickstart** section in your application's settings in the Azure Portal.
- Choose your application type (e.g., `.NET Core Web App`) and download the provided sample code.

### 2. **Open the Project in Visual Studio**
1. Extract the downloaded `.zip` file to a local directory.
2. Open the solution file in **Visual Studio**.
3. Trust the project when prompted.

---

### 3. **Explore the Key Files**
#### **Program.cs**
- Contains the main entry point for the application.
- Initializes the **HostBuilder** and sets the startup class.

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

#### **Startup.cs**
- Configures services and middleware for the application.
- Adds authentication middleware to enable user sign-ins.

```csharp
public class Startup
{
    public Startup(IConfiguration configuration)
    {
        Configuration = configuration;
    }

    public IConfiguration Configuration { get; }

    // This method gets called by the runtime. Use this method to add services to the container.
    // <Configure_service_ref_for_docs_ms>
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddAuthentication(OpenIdConnectDefaults.AuthenticationScheme)
            .AddMicrosoftIdentityWebApp(Configuration.GetSection("AzureAd"));

        services.AddControllersWithViews(options =>
        {
            var policy = new AuthorizationPolicyBuilder()
                .RequireAuthenticatedUser()
                .Build();
            options.Filters.Add(new AuthorizeFilter(policy));
        });
        services.AddRazorPages()
            .AddMicrosoftIdentityUI();
    }
    // </ Configure_service_ref_for_docs_ms >

    // This method gets called by the runtime. Use this method to configure the HTTP request pipeline.
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
        else
        {
            app.UseExceptionHandler("/Home/Error");
            // The default HSTS value is 30 days. You may want to change this for production scenarios, see https://aka.ms/aspnetcore-hsts.
            app.UseHsts();
        }
        app.UseHttpsRedirection();
        app.UseStaticFiles();

        app.UseRouting();
        // <endpoint_map_ref_for_docs_ms>
        app.UseAuthentication();
        app.UseAuthorization();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllerRoute(
                name: "default",
                pattern: "{controller=Home}/{action=Index}/{id?}");
            endpoints.MapRazorPages();
        });
        // </endpoint_map_ref_for_docs_ms>
    }
}
```

#### **appsettings.json**
- Contains application settings, including the **client ID** and **tenant ID**.

```json
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "your-tenant.onmicrosoft.com",
    "ClientId": "your-client-id",
    "TenantId": "your-tenant-id",
    "CallbackPath": "/signin-oidc"
  }
}
{
    "AzureAd": {
        "Instance": "https://login.microsoftonline.com/",
        "Domain": "your-tenant.onmicrosoft.com",
        "TenantId": "your-tenant-id",
        "ClientId": "your-client-id",
        "CallbackPath": "/signin-oidc"
    }
}
```

---

### 4. **Run the Application Locally**
1. Start the application in Visual Studio (default local URL: `https://localhost:44321`).
2. The application redirects to the Microsoft Identity Platform for sign-in.

---

### 5. **Sign In with Entra ID**
- Use a test account (e.g., `John Doe`) or your global administrator account.
- Grant the application the requested permissions, such as reading the Azure AD profile.
- Upon successful login, the app displays a personalized greeting (e.g., "Hello, [username]").

---

## Features Demonstrated

- **Redirect URI**: Handles the token response after login.
- **Authentication Middleware**: Validates access tokens to ensure secure access.
- **Azure AD Permissions**: Demonstrates the use of user consent for app permissions.

---

## Key Takeaways

- The Quickstart provides a solid starting point for integrating Entra ID authentication into applications.
- Sample code is preconfigured to work with your tenant and client ID.
- Authentication flow follows the OAuth 2.0/OpenID Connect standards.

---

## Resources

- [Microsoft Identity Platform Overview](https://learn.microsoft.com/en-us/azure/active-directory/develop/)
- [Quickstart: Configure a .NET Core Web App](https://learn.microsoft.com/en-us/azure/active-directory/develop/quickstart-v2-aspnet-core-webapp)
- [ASP.NET Core Razor Pages](https://learn.microsoft.com/en-us/aspnet/core/razor-pages/)

---
