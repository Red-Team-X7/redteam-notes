# ⚙️ new-adgroup

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Create a new security group with accompanying attributes.

## Usage Examples

### Create a new security group named "name" with the accompanying attributes

	New-ADGroup -Name "name" -SamAccountName analysts -GroupCategory Security -GroupScope Global -DisplayName "Security Analysts" -Path "CN=Users,DC=domain,DC=local" -Description "Members of this group are Security Analysts under the IT OU"

# References