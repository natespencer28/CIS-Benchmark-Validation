## 🛠️ Audit Steps

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Teams & groups select Active teams & groups. 
3. On the Active teams and groups page, check that no groups have the status 
'Public' in the privacy column. 


## 🛠️ Audit Steps via Powershell

1. Connect to the Microsoft Graph service using Connect-MgGraph -Scopes "Group.Read.All". 
2. Run the following Microsoft Graph PowerShell command:

```powershell
Get-MgGroup -All | where {$_.Visibility -eq "Public"} | select 
DisplayName,Visibility
```
3. Ensure Visibility is Private for each group. 

##Before##

<img width="897" height="213" alt="image" src="https://github.com/user-attachments/assets/c5e6af53-8b5d-4ebc-9647-a203f3de4276" />

##After##

<img width="905" height="291" alt="image" src="https://github.com/user-attachments/assets/d4e682f6-2ac4-4ebc-b605-4d9293f731ed" />






