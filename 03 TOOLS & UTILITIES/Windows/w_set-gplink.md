# ⚙️ set-gplink

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Link a GPO for use to a specific OU or security group.

## Usage Examples

### Link a GPO for use to a specific OU or security group

	Set-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" -LinkEnabled Yes

# References