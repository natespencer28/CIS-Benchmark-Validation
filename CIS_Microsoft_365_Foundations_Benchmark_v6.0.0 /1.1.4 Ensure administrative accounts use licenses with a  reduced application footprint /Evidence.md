## 🛠️ Audit Steps

1. Navigate to Microsoft 365 admin center https://admin.microsoft.com. 
2. Click to expand Users select Active users. 
3. Sort by the Licenses column. 
4. For each user account in an administrative role verify the account is assigned a 
license that is not associated with applications i.e. (Microsoft Entra ID P1, 
Microsoft Entra ID P2). 
o If an organization uses PIM to elevate a daily driver account to privileged 
levels, this control and licensing requirement can be considered satisfied.

***IN THIS SCENARIO I DON'T HAVE ENTRA ID P1 OR P2 SO I LEFT MY ADMIN ACCOUNT UNLICENSED TO SATISFY THIS BENCHMARK***

<img width="820" height="168" alt="image" src="https://github.com/user-attachments/assets/7f5662df-5ef1-48c6-a888-1aa159fe5d81" />

## 🛠️ Audit Steps via Powershell
