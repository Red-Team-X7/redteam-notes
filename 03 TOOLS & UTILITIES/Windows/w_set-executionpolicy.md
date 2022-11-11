# ⚙️ set-executionpolicy

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

Set PowerShell execution policies.

## Usage Examples

### Set the PowerShell execution policy to bypass for the current session

	Set-ExecutionPolicy Bypass -Scope Process

```powershell-session
Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

# References