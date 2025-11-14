## 🛠️ Remediation Steps

### **The Audit**

Step 1 - Ensure a policy and procedure is in place at the organization: 
• FIDO2 Security Keys should be locked in a secure separate fireproof location. 
• Passwords should be at least 16 characters, randomly generated and MAY be 
separated in multiple pieces to be joined on emergency. 

Step 2 - Ensure two emergency access accounts are defined: 
1. Navigate to Microsoft 365 admin center https://admin.microsoft.com 
2. Expand Users > Active Users 
3. Inspect the designated emergency access accounts and ensure the following: 
o The accounts are named correctly, and do NOT identify with a particular 
person. 
o The accounts use the default .onmicrosoft.com domain and not the 
organization's. 
o The accounts are cloud-only. 
o The accounts are unlicensed. 
o The accounts are assigned the Global Administrator directory role. 
Step 3 - Ensure at least one account is excluded from all conditional access 
rules: 
1. Navigate Microsoft Entra admin center https://entra.microsoft.com/ 
2. Expand Protection > Conditional Access. 
3. Inspect the conditional access rules. 
4. Ensure one of the emergency access accounts is excluded from all rules.


### **The Evidence**

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






















