## UI Audit Steps
1. Navigate to the Microsoft 365 admin center https://admin.microsoft.com/. 
2. Click to expand Settings Select Org settings. 
3. Click Security & Privacy tab. 
4. Select Idle session timeout. 
5. Verify Turn on to set the period of inactivity for users to be 
signed off of Microsoft 365 web apps is set to 3 hours (or less). 


## Audit Steps in Powershell
Connect to Microsoft Graph using Connect-MgGraph -Scopes 
"Policy.Read.All"

```powershell
$TimeoutPolicy = Get-MgPolicyActivityBasedTimeoutPolicy 
$BenchmarkTimeSpan = [TimeSpan]::Parse('03:00:00') # 3 hours 
if ($TimeoutPolicy) { 
$PolicyDefinition = $TimeoutPolicy.Definition | ConvertFrom-Json 
$Timeout = 
$PolicyDefinition.ActivityBasedTimeoutPolicy.ApplicationPolicies[0].WebSessionIdleTimeout 
$TimeSpan = [TimeSpan]::Parse($Timeout) 
$TimeoutReadable = "{0} days, {1} hours, {2} minutes" ` -f $TimeSpan.Days, $TimeSpan.Hours, $TimeSpan.Minutes  
if ($TimeSpan -le $BenchmarkTimeSpan) { 
Write-Host "** PASS ** Timeout is set to $TimeoutReadable." 
} else { 
Write-Host "** FAIL ** Timeout is too long. It is set to 
$TimeoutReadable." 
} 
} else { 
Write-Host "** FAIL **: Idle session timeout is not configured." 
}  
```


## Evidence in my Tenant 

## UI Evidence 

<img width="561" height="408" alt="image" src="https://github.com/user-attachments/assets/88201053-e531-4687-a894-82262d390cf4" />



## Powershell Evidence



