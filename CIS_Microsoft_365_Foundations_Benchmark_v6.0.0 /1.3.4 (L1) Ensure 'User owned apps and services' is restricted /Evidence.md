## UI Audit Steps

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Settings > Org settings. 
3. In Services select User owned apps and services. 
4. Verify Let users access the Office Store and Let users start trials 
on behalf of your organization are not checked.

## Audit in Powershell

1. Connect to the Microsoft Graph service using Connect-MgGraph -Scopes 
"OrgSettings-AppsAndServices.Read.All". 
2. Run the following Microsoft Graph PowerShell command:

```powershell
$Uri = "https://graph.microsoft.com/beta/admin/appsAndServices/settings" 
Invoke-MgGraphRequest -Uri $Uri
```
3. Ensure both isOfficeStoreEnabled and isAppAndServicesTrialEnabled 
are False.

## UI Evidence

<img width="607" height="706" alt="image" src="https://github.com/user-attachments/assets/5ee2cfaf-363b-4982-88d8-17177f9c2159" />

## Powershell Evidence

<img width="887" height="160" alt="image" src="https://github.com/user-attachments/assets/bb469c84-798c-42c2-b243-841b0d83ef15" />
