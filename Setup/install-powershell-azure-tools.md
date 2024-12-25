
# Installing PowerShell 7 and Azure Tools on Windows

This guide provides step-by-step instructions to install PowerShell 7 and the Azure PowerShell module on a Windows machine.

---

## Step 1: Install PowerShell 7

1. Download the PowerShell 7 installer from the [official GitHub releases page](https://github.com/PowerShell/PowerShell/releases).
   - Look for the `.msi` file for Windows (e.g., `PowerShell-7.x.x-win-x64.msi`).
2. Run the downloaded installer and follow these steps:
   - Accept the license agreement.
   - Choose the installation folder (or keep the default).
   - Ensure the option to **Add PowerShell to PATH** is checked.
3. Complete the installation and open PowerShell 7 by searching for `pwsh` in the Start menu.

---

## Step 2: Install the Azure PowerShell Module

1. Open PowerShell 7.
2. Run the following command to install the Azure PowerShell module:
   ```powershell
   Install-Module -Name Az -Scope CurrentUser -Repository PSGallery -Force
   ```
3. After installation, verify the module is installed by running:
   ```powershell
   Get-Module -Name Az -ListAvailable
   ```

   This will list all the Azure modules available, confirming the installation was successful.

---

## Step 3: Connect to Your Azure Account

1. Open PowerShell 7.
2. Use the following command to sign in to your Azure account:
   ```powershell
   Connect-AzAccount
   ```
3. A browser window will open asking you to sign in. Enter your Azure credentials to authenticate.
4. Once authenticated, PowerShell will display information about your active subscription.

To verify the connection, run:
```powershell
Get-AzSubscription
```

This command will list all subscriptions associated with your Azure account.

### Troubleshooting
If `Connect-AzAccount` fails with an authentication error (e.g., related to WAM or redirect URIs), try using device code authentication:
```powershell
Connect-AzAccount -UseDeviceAuthentication
```
This will provide a device login code and URL to authenticate in your browser.


---

## Step 4: Update the Azure Module (Optional)

To ensure you have the latest features and fixes, update the Azure module periodically:
```powershell
Update-Module -Name Az
```

---

## Notes
- PowerShell 7 is required for optimal performance and compatibility with the latest Azure tools.
- Use `pwsh` to launch PowerShell 7 instead of the default Windows PowerShell.

You’re now ready to manage Azure resources using PowerShell and prepare for the AZ-204 certification!
