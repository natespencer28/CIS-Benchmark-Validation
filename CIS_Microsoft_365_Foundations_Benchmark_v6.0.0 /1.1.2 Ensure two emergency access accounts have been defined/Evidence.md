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
  - The accounts are named correctly, and do NOT identify with a particular person. 
  - The accounts use the default .onmicrosoft.com domain and not the organization's. 
  - The accounts are cloud-only.
  - The accounts are unlicensed.
  - The accounts are assigned the Global Administrator directory role.

Step 3 - Ensure at least one account is excluded from all conditional access 
rules: 
1. Navigate Microsoft Entra admin center https://entra.microsoft.com/ 
2. Expand Protection > Conditional Access. 
3. Inspect the conditional access rules. 
4. Ensure one of the emergency access accounts is excluded from all rules.


### **The Evidence**

  ✅ The accounts are named correctly, and do NOT identify with a particular person.
  ✅ The accounts use the default .onmicrosoft.com domain and not the organization's.
  ✅ The accounts are cloud-only.
  ✅ The accounts are unlicensed.
  ✅ The accounts are assigned the Global Administrator directory role.
  ✅ The accounts are excluded from CA Policies.

<img width="655" height="209" alt="image" src="https://github.com/user-attachments/assets/b9560aa4-0a30-4bf6-a235-3c02c09a5c52" />




















