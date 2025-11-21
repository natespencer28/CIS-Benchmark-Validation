## UI Audit Steps
1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Settings select Org Settings. 
3. Click on Security & privacy. 
4. Select Password expiration policy ensure that Set passwords to never 
expire (recommended) has been checked. 
To audit using PowerShell:

## Audit Steps in Powershell
1. Connect to the Microsoft Graph service using Connect-MgGraph -Scopes 
"Domain.Read.All". 
2. Run the following Microsoft Online PowerShell command:
```powershell
   Get-MgDomain | ft id,PasswordValidityPeriodInDays 
```
3. Verify the value returned for valid domains is 2147483647

## Evidence in my Tenant 

## UI Evidence 

<img width="495" height="227" alt="image" src="https://github.com/user-attachments/assets/be2b0da1-3eb5-4885-9b3a-f7dab007cc99" />


## Powershell Evidence

<img width="694" height="326" alt="image" src="https://github.com/user-attachments/assets/df690ae3-addc-4463-8a4b-58ad82a5803f" />

