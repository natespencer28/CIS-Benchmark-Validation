## 🛠️ Audit Steps

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Users select Active users. 
3. Sort by the Licenses column. 
4. For each user account in an administrative role verify the account is assigned a 
license that is not associated with applications i.e. (Microsoft Entra ID P1, 
Microsoft Entra ID P2). 
o If an organization uses PIM to elevate a daily driver account to privileged 
levels, this control and licensing requirement can be considered satisfied.

***IN THIS SCENARIO I DON'T HAVE ENTRA ID P1 OR P2 SO I LEFT MY ADMIN ACCOUNT UNLICENSED TO SATISFY THIS BENCHMARK AND WOULD USE PIM FOR THE ANORAK@READYP1.ORG ACCOUNT***

<img width="820" height="168" alt="image" src="https://github.com/user-attachments/assets/7f5662df-5ef1-48c6-a888-1aa159fe5d81" />

## 🛠️ Audit Steps via Powershell

1. Connect to Microsoft Graph using Connect-MgGraph -Scopes 
"RoleManagement.Read.Directory","User.Read.All" 
2. Run the following PowerShell script:

```powershell
$DirectoryRoles = Get-MgDirectoryRole 
 
# Get privileged role IDs 
$PrivilegedRoles = $DirectoryRoles | Where-Object { 
    $_.DisplayName -like "*Administrator*" -or $_.DisplayName -eq "Global 
Reader" 
} 
 
# Get the members of these various roles 
$RoleMembers = $PrivilegedRoles | ForEach-Object { Get-MgDirectoryRoleMember -DirectoryRoleId $_.Id } | 
    Select-Object Id -Unique 
 
# Retrieve details about the members in these roles 
$PrivilegedUsers = $RoleMembers | ForEach-Object { 
    Get-MgUser -UserId $_.Id -Property UserPrincipalName, DisplayName, Id 
} 
 
$Report = [System.Collections.Generic.List[Object]]::new() 
 
foreach ($Admin in $PrivilegedUsers) { 
    $License = $null 
    $License = (Get-MgUserLicenseDetail -UserId $Admin.id).SkuPartNumber 
join ", " 
    $Object = [pscustomobject][ordered]@{ 
        DisplayName           = $Admin.DisplayName 
        UserPrincipalName     = $Admin.UserPrincipalName 
        License               = $License 
    } 
    $Report.Add($Object) 
} 
 
$Report
```
## Ouput of Powershell

<img width="534" height="96" alt="image" src="https://github.com/user-attachments/assets/8e2ea314-ca5b-4374-af8e-5a0934ba5641" />

