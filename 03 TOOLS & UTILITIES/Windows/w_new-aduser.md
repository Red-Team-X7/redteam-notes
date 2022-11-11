# ⚙️ new-aduser

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Add a user to AD and set attributes.

## Usage Examples

### Add a user to AD and set attributes

	New-ADUser -Name "first last" -Accountpassword (Read-Host -AsSecureString "Super$ecurePassword!") -Enabled $true -OtherAttributes @{'title'="Analyst";'mail'="f.last@domain.com"}

# References