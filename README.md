## CIS-Benchmark-Validation

CIS, or the Center for Internet Security, has developed CIS Benchmarks to provide best practices for defending against cyber threats across various technology domains. These benchmarks cover over 25 vendor product families, including M365, with the goal of identifying security gaps to protect systems in an ever-evolving threat landscape.

The CIS Benchmark for M365 Environments is located above. 

# **1.1.1 (L1) Ensure Administrative Accounts Are Cloud-Only**

## 🔎 Description
Administrative accounts are privileged identities with elevated access to data, users, and critical configuration settings.  
To maintain strong identity hygiene:

- **Regular user accounts should never be used for administrative operations.**
- In hybrid environments, **admin accounts must remain cloud-only** to prevent compromise via on-premises systems.
- Separation of duties ensures compromised hybrid identities cannot escalate to cloud-level control.

Maintaining cloud-only administrative accounts reduces attack surface and aligns with Zero Trust principles.

---

## 🛠️ Remediation

### **1. Identify Hybrid-Synced Privileged Accounts**
Locate administrative accounts that originate from on-prem Active Directory and are synced to Entra ID.

You can do this using:
- **Entra ID Admin Center** → *Users* → *Directory synced* filter  
- **PowerShell (Microsoft Graph):**
  ```powershell
  Get-MgUser -Filter "OnPremisesSyncEnabled eq true" | 
    Where-Object { $_.UserType -eq "Member" }

