## UI Audit Steps 

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Settings select Org settings. 
3. In the Services section click Calendar. 
4. Verify Let your users share their calendars with people outside of 
your organization who have Office 365 or Exchange is unchecked.

## Note 
I got an error when trying to uncheck the box in Step 4 above and had to connect to Exchange Oline and run this command
```powershell
Enable-OrganizationCustomization
```

## Powershell Audit Steps 

1. Connect to Exchange Online using Connect-ExchangeOnline. 
2. Run the following Exchange Online PowerShell command:

```powershell
Set-SharingPolicy -Identity "Default Sharing Policy" -Enabled $False
```
