# ⚙️ get-adcomputer

Tags: #⚙️
Related to:
See also:
Previous: [[Introduction to Active Directory]]

## Description

Checks for a computer and view its properties.

## Usage Examples

### Check for a computer named "name" and view its properties

	Get-ADComputer -Identity "name" -Properties * | select CN,CanonicalName,IPv4Address

# References