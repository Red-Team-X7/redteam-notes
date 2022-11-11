# ⚙️ add-computer

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Add a computer to the domain using the credentials specified.

## Usage Examples

### Add a new computer to the domain using the credentials specified

	Add-Computer -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\HTB-student_adm' -Restart`


### Remotely add a computer to a domain

	Add-Computer -ComputerName 'name' -LocalCredential '.\localuser' -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\htb-student_adm' -Restart

# References