## 1.3.1 (L1) Ensure the 'Password expiration policy' is set to 'Set 
passwords to never expire (recommended)'

## 📌 Control Objective
When a new group is created in the Administration panel, the default privacy value of the group is "Public". (In this case, ‘public’ means accessible to the identities within the organization without requiring group owner authorization to join.)

## 🔎 Description
Shared mailboxes are used when multiple people need access to the same mailbox, such as a company information or support email address, reception desk, or other function that might be shared by multiple people.

## 🧠 Rationale
Explain why this control matters, including: The intent of the shared mailbox is the only allow delegated access from other mailboxes. An admin could reset the password, or an attacker could potentially gain access to the shared mailbox allowing the direct sign-in To prevent this, block sign-in for the account that is associated with the shared mailbox.
