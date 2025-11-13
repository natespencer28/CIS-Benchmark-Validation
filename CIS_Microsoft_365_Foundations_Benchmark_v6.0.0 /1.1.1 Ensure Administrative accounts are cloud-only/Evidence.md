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
```powershell
# Add recommended PowerShell or Graph commands
# Example:
Get-MgUser -Filter "OnPremisesSyncEnabled eq true"








