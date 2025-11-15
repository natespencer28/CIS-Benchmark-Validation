**🛠️ Audit Steps**

1. Navigate to the Microsoft 365 admin center https://admin.microsoft.com 
2. Select Roles > Role assignments. 
3. Select the Global Administrator role from the list and click on Assigned. 
4. Review the list of Global Administrators. 
o If there are groups present, then inspect each group and its members. 
o Take note of the total number of Global Administrators in and outside of 
groups. 
5. Ensure the number of Global Administrators is between two and four.

<img width="375" height="199" alt="image" src="https://github.com/user-attachments/assets/df57939b-5af1-44b5-a08e-eb180ef4874a" />


🛠️ Audit Steps using Powershell 

1. Connect to Microsoft Graph using Connect-MgGraph -Scopes 
Directory.Read.All 
2. Run the following PowerShell script:


<img width="587" height="82" alt="image" src="https://github.com/user-attachments/assets/1862b6fe-a3c6-4a8a-88c3-aa784fdac5f5" />

