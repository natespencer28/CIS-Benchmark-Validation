## 🛠️ Remediation Steps

### **Option A: Admin Center**

1. Navigate to Microsoft Entra admin center https://entra.microsoft.com/. 
2. Click to expand Identity > Users and select All users. 
3. To the right of the search box click the Add filter button. 
4. Add the On-premises sync enabled filter with the value set to Yes and click 
Apply. 
5. Verify that no user accounts in administrative roles are present in the filtered list.

<img width="1189" height="324" alt="image" src="https://github.com/user-attachments/assets/67099826-da10-47f6-9d16-b10ddc8a1327" />


### **Option B: PowerShell / Graph API**

[1.1.1.ps1](https://github.com/natespencer28/M365_Automation/blob/main/1.1.1.ps1)

## Step 1 Connect to Microsoft Graph 
-Connect-MgGraph -Scopes "RoleManagement.Read.Directory","User.Read.All" 
## Step 2. Run the following PowerShell script: 

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
Get-MgUser -UserId $_.Id -Property UserPrincipalName, DisplayName, Id, 
OnPremisesSyncEnabled 
} 
$PrivilegedUsers | Where-Object { $_.OnPremisesSyncEnabled -eq $true } |  
ft DisplayName,UserPrincipalName,OnPremisesSyncEnabled
```

## Step 3. The script will output any hybrid users that are also members of privileged roles. 
If nothing returns, then no users with that criteria exist. 

<img width="674" height="382" alt="image" src="https://github.com/user-attachments/assets/bbd89f1a-506c-4ad7-887c-239ed382a46d" />






















