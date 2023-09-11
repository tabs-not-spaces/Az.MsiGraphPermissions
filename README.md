# Az.MsiGraphPermissions 1.0.0.1

Want to apply Graph Permissions / Roles to a Managed Service Identity in Azure? Now you can!

This module only exists to patch this missing feature from the AAD Managed Identity UI. Hopefully this will not be needed for long!

## How to install

```PowerShell
Install-Module Az.MsiGraphPermissions
```

## How to use

```PowerShell
Connect-AzAccount -Tenant "powers-hell.com" -UseDeviceAuthentication
$token = Get-AzAccessToken -ResourceUrl "https://graph.microsoft.com"
$roles = @(
    "DeviceManagementApps.ReadWrite.All", 
    "DeviceManagementConfiguration.Read.All", 
    "DeviceManagementManagedDevices.Read.All", 
    "DeviceManagementRBAC.Read.All", 
    "DeviceManagementServiceConfig.ReadWrite.All", 
    "GroupMember.Read.All"
)
Add-GraphPermissionToMsi -ApplicationName "MyObviouslyCoolApp" -GraphApiPermission $roles -Token $token.Token
```

In the above example we get our auth token using the Az.Accounts module, but any MSAL solution can be leveraged.

Once auth is granted, using the managed service identity name, supply a list of Graph API permissions by **name** and watch the magic happen.

If the MSI already has the supplied permissions you will be notified.

## Features to come

- View current applied permissions / roles
- Remove current applied permissions / roles
- Output the results of `Add-GraphPermissionToMsi` as an object

## Want to contribute?

Fork away, this module probably wont live long, but the feature list above would be a great opportunity to work on for anyone new to PowerShell / Azure.