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


### Conditional Access Policy Configuration Audit

- **Users:** All users  
- **Cloud apps or actions:** Office 365 (Select apps)  
- **Conditions → Client apps:** Browser only  
- **Session:** Use app-enforced restrictions  
- **Enable Policy:** On

<img width="480" height="118" alt="image" src="https://github.com/user-attachments/assets/7451da19-ca4e-4d72-82f7-4a31008a8e26" />

## Powershell Script
Connect to Microsoft Graph using Connect-MgGraph -Scopes 
"Policy.Read.All": 
```powershell
$Caps = Get-MgIdentityConditionalAccessPolicy -All | 
    Where-Object { 
$_.SessionControls.ApplicationEnforcedRestrictions.IsEnabled } 
$CapReport = [System.Collections.Generic.List[Object]]::new()     
# Filter to policies with "Use app enforced restrictions" enabled 
 
# Loop through policies and generate a per policy report. 
foreach ($policy in $Caps) { 
    $Name = $policy.DisplayName 
    $Users = $policy.Conditions.Users.IncludeUsers 
    $Targets = $policy.Conditions.Applications.IncludeApplications 
    $ClientApps = $policy.Conditions.ClientAppTypes 
    $Restrictions = 
$policy.SessionControls.ApplicationEnforcedRestrictions.IsEnabled 
    $State = $policy.State 
 
    $CountPass = $Targets.count -eq 1 -and $ClientApps.count -eq 1 
    $Pass = $Targets -eq 'Office365' -and $ClientApps -eq 'browser' -and 
            $Restrictions -and $CountPass -and $State -eq 'enabled' 
 
    $obj = [PSCustomObject]@{ 
        DisplayName             = $Name 
        AuditState              = if ($Pass) { "PASS" } else { "FAIL" } 
        IncludeUsers            = $Users 
        IncludeApplications     = $Targets 
        ClientAppTypes          = $ClientApps 
        AppEnforcedRestrictions = $Restrictions 
        State                   = $State 
    } 
    $CapReport.Add($obj) 
} 
 
if ($Caps) { 
    $CapReport 
} else { 
    Write-Host "** FAIL **: There are no qualifying conditional access 
policies." 
}
```



