## UI Audit Steps

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Settings then select Org settings. 
3. Under Services select Microsoft Forms. 
4. Ensure the checkbox labeled Add internal phishing protection is checked 
under Phishing protection. 

## Audit in Powershell

1. Connect to the Microsoft Graph service using Connect-MgGraph -Scopes 
"OrgSettings-Forms.Read.All". 
2. Run the following Microsoft Graph PowerShell commands:
```powershell
$uri = 'https://graph.microsoft.com/beta/admin/forms/settings' 
Invoke-MgGraphRequest -Uri $uri | select isInOrgFormsPhishingScanEnabled
```
3. Ensure isInOrgFormsPhishingScanEnabled is 'True'. 

## UI Evidence

<img width="595" height="839" alt="image" src="https://github.com/user-attachments/assets/b1bf5c56-e2c5-43b8-805b-a0ff6be44d85" />


## Powershell Evidence

<img width="723" height="132" alt="image" src="https://github.com/user-attachments/assets/2826df51-d44e-4dc2-9ba9-9a7aa14438f4" />
