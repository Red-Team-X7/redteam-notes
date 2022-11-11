# ⚙️ whoami

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

Displays user, group and privileges information for the user who is currently logged on to the local system. If used without parameters, whoami displays the current domain and user name.

## Usage Examples

### View User information

**netuser and whoami are often monitored by EDR systems and flagged as anomalous activity.**

	net user gerald

```
User name                    gerald
Full Name                    
Comment                      
User's comment               
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            ?13/?07/?2020 09:26:56
Password expires             Never
Password changeable          ?13/?07/?2020 09:26:56
Password required            No
User may change password     Yes

Workstations allowed         All
Logon script                 
User profile                 
Home directory               
Last logon                   ?25/?12/?2021 20:07:42

Logon hours allowed          All

Local Group Memberships      *Administrators       *Users                
Global Group memberships     *None                 
The command completed successfully.
```

	whoami /user

```powershell-session
USER INFORMATION
----------------

User Name           SID
=================== =============================================
ws01\bob S-1-5-21-674899381-4069889467-2080702030-1002
```

# References
