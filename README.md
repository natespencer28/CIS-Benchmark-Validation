## CIS-Benchmark-Validation

CIS, or the Center for Internet Security, has developed CIS Benchmarks to provide best practices for defending against cyber threats across various technology domains. These benchmarks cover over 25 vendor product families, including M365, with the goal of identifying security gaps to protect systems in an ever-evolving threat landscape.

The CIS Benchmark for M365 Environments is located above. 

## 1.1.1 (L1) Ensure Administrative accounts are cloud-only 

**Description**

Administrative accounts are special privileged accounts that could have varying levels 
of access to data, users, and settings. Regular user accounts should never be utilized 
for administrative tasks and care should be taken, in the case of a hybrid environment, 
to keep administrative accounts separate from on-prem accounts.

**Remediation**

Remediation will require first identifying the privileged accounts that are synced from on
premises and then creating a new cloud-only account for that user. Once a replacement 
account is established, the hybrid account should have its role reduced to that of a non
privileged user or removed depending on the need. 

**Evidence** 
