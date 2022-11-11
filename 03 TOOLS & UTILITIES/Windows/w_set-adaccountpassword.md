# ⚙️ set-adaccountpassword

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Set the password of an AD user to the password specified.

## Usage Examples

### Set the password of an AD user to the password specified

	Set-ADAccountPassword -Identity <'name'> -Reset -NewPassword (ConvertTo-SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)

# References