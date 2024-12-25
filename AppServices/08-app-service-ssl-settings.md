# Azure App Service SSL/TLS Settings

Azure App Service provides robust SSL/TLS settings to help secure your web applications. This guide covers the key SSL/TLS configuration options available in Azure App Service, including enabling HTTPS, configuring TLS versions, and managing SSL certificates.

## Enforcing HTTPS

To ensure all traffic to your web app is encrypted, you can enforce HTTPS:

1. **Navigate to your App Service in the Azure Portal.**
2. **Select `TLS/SSL settings` from the left-hand menu.**
3. **In the `Protocol Settings` section, set `HTTPS Only` to `On`.**

This setting ensures that any HTTP requests are redirected to HTTPS, providing a secure communication channel for your users.

## Configuring TLS Versions

Transport Layer Security (TLS) protocols encrypt data transmitted over the network. Azure App Service allows you to specify the minimum TLS version to be used:

1. **Within the `TLS/SSL settings` of your App Service, locate the `Protocol Settings` section.**
2. **Set the `Minimum TLS Version` to your desired version (e.g., `1.2`).**

Setting a higher minimum TLS version enhances security by ensuring that only clients supporting the specified version or higher can connect.

## Managing SSL Certificates

To bind a custom domain to your App Service with SSL, you'll need to upload and configure an SSL certificate.

### Uploading a Private Key Certificate (.pfx)

1. **In your App Service, select `TLS/SSL settings` > `Private Key Certificates (.pfx)`.**
2. **Click `Upload Certificate`.**
3. **Browse and select your `.pfx` file, enter the certificate password, and click `Upload`.**

Once uploaded, the certificate will appear in the list of Private Key Certificates.

### Binding the Certificate to a Custom Domain

1. **In `TLS/SSL settings`, navigate to the `Bindings` section.**
2. **Click `Add TLS/SSL Binding`.**
3. **Select your custom domain from the dropdown.**
4. **Choose the uploaded certificate from the `Private Certificate Thumbprint` dropdown.**
5. **Select the TLS/SSL type (`SNI SSL` is recommended for most scenarios).**
6. **Click `Add Binding`.**

This binds the SSL certificate to your custom domain, enabling secure HTTPS traffic.

## Using App Service Managed Certificates

Azure App Service offers free managed certificates for custom domains, suitable for many scenarios. However, these certificates have limitations, such as not supporting wildcard certificates or naked domains. For more advanced scenarios, consider purchasing an App Service Certificate.

### Adding a Managed Certificate

1. **In your App Service, select `TLS/SSL settings` > `Private Key Certificates (.pfx)`.**
2. **Click `Create App Service Managed Certificate`.**
3. **Select the custom domain you wish to secure.**
4. **Click `Create`.**

After creation, bind the certificate to your custom domain as described in the previous section.

## Additional Resources

For more detailed information, refer to the official Azure documentation:

- [Add and manage TLS/SSL certificates in Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/configure-ssl-certificate)
- [Secure a custom DNS name with a TLS/SSL binding in Azure App Service](https://learn.microsoft.com/en-us/azure/app-service/configure-ssl-bindings)
- [Add and manage App Service certificates](https://learn.microsoft.com/en-us/azure/app-service/configure-ssl-app-service-certificate)

By properly configuring these SSL/TLS settings, you enhance the security of your Azure App Service applications, ensuring encrypted communication between your app and its users.