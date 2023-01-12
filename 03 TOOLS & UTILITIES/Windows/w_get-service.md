# ⚙️ get-service

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

cmdlet to view running services.

## Usage Examples

### Get the status of services

	Get-Service | ? {$_.Status -eq "Running"} | select -First 2 |fl

```text
Name                : AdobeARMservice
DisplayName         : Adobe Acrobat Update Service
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess

Name                : Appinfo
DisplayName         : Application Information
Status              : Running
DependentServices   : {}
ServicesDependedOn  : {RpcSs, ProfSvc}
CanPauseAndContinue : False
CanShutdown         : False
CanStop             : True
ServiceType         : Win32OwnProcess, Win32ShareProcess
```

# References