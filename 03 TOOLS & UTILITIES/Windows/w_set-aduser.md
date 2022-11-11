# ⚙️ set-aduser

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Force a user to change their password at next logon attempt.

## Usage Examples

### Force a user to change their password at next logon attempt

	Set-ADUser -Identity amasters -ChangePasswordAtLogon $true

# References