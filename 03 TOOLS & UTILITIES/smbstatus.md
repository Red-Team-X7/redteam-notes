# ⚙️ smbstatus

Tags: #⚙️
Related to: [[smbclient]]
See also:
Previous:

## Description

Report on current Samba connections.

## Usage Examples

### Check on SMB connections

	smbstatus

```text
Samba version 4.11.6-Ubuntu
PID     Username     Group        Machine                                   Protocol Version  Encryption           Signing              
----------------------------------------------------------------------------------------------------------------------------------------
75691   sambauser    samba        10.10.14.4 (ipv4:10.10.14.4:45564)      SMB3_11           -                    -                    

Service      pid     Machine       Connected at                     Encryption   Signing     
---------------------------------------------------------------------------------------------
notes        75691   10.10.14.4   Do Sep 23 00:12:06 2021 CEST     -            -           

No locked files
```

# References