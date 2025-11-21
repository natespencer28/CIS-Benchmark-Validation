## 1.3.2 (L2) Ensure 'Idle session timeout' is set to '3 hours (or less)' 
for unmanaged devices 

## 📌 Control Objective
Idle session timeout allows the configuration of a setting which will timeout inactive 
users after a pre-determined amount of time.

## 🔎 Description
 When a user reaches the set idle timeout 
session, they'll get a notification that they're about to be signed out. They must choose 
to stay signed in or they'll be automatically signed out of all Microsoft 365 web apps. 
Combined with a Conditional Access rule this will only impact unmanaged devices. 

## 🧠 Rationale
Ending idle sessions through an automatic process can help protect sensitive company 
data and will add another layer of security for end users who work on unmanaged 
devices that can potentially be accessed by the public. 

## Note 

To ensure that idle timeouts affect only unmanaged devices, both steps 1 and 2 
must be completed. Otherwise managed devices will also be impacted by the timeout 
policy.

Step 1 - Configure Idle session timeout in UI 

Step 2 - Ensure the Conditional Access policy is in place In UI 
