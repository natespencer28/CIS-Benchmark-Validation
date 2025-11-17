🛠️ Audit Steps

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com/ 
2. Click to expand Teams & groups and select Shared mailboxes. 
3. Take note of all shared mailboxes. 
4. Click to expand Users and select Active users. 
5. Select a shared mailbox account to open its properties pane, and review. 
6. Ensure the text under the name reads Sign-in blocked. 
7. Repeat for any additional shared mailboxes.
   
🛠️ Audit Steps via Powershell

1. Connect to Exchange Online using Connect-ExchangeOnline 
2. Connect to Microsoft Graph using Connect-MgGraph -Scopes 
"User.Read.All" 
3. Run the following PowerShell commands:
```powershell
$MBX = Get-EXOMailbox -RecipientTypeDetails SharedMailbox -ResultSize 
Unlimited 
$MBX | ForEach-Object { Get-MgUser -UserId $_.ExternalDirectoryObjectId ` -Property DisplayName, UserPrincipalName, AccountEnabled } |  
Format-Table DisplayName, UserPrincipalName, AccountEnabled
```
4. Ensure AccountEnabled is set to False for all Shared Mailboxes.

## Evidence in my Tenant

## UI

<img width="551" height="160" alt="image" src="https://github.com/user-attachments/assets/bb0bdb94-67de-4073-87e9-18160675f0e2" />

## Powershell 

<img width="971" height="185" alt="image" src="https://github.com/user-attachments/assets/18b85cad-9912-4a55-94c3-61f9a9eb126c" />

Remediation Steps: 

1. Connect to Microsoft Graph using Connect-MgGraph -Scopes 
"User.ReadWrite.All" 
2. Connect to Exchange Online using Connect-ExchangeOnline. 
3. To disable sign-in for a single account:

```powershell
$MBX = Get-EXOMailbox -Identity TestUser@example.com 
Update-MgUser -UserId $MBX.ExternalDirectoryObjectId -AccountEnabled:$false
```


