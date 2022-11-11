# ⚙️ net

Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

## Description

Adjust account settings.

## Usage Examples

### Add user to Administrators group

	net localgroup Administrators gerald /add

### View User information

**netuser and whoami are often monitored by EDR systems and flagged as anomalous activity.**

	net user gerald

```cmd-session
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

	whoami

#### Displaying Shares using net share

	net share

```cmd-session
Share name   Resource                        Remark

-------------------------------------------------------------------------------
C$           C:\                             Default share
IPC$                                         Remote IPC
ADMIN$       C:\WINDOWS                      Remote Admin
Company Data C:\Users\htb-student\Desktop\Company Data

The command completed successfully.
```

# References
