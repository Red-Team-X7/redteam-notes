# ⚙️ invoke-wmimethod

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

Call methods of WMI objects

## Usage Examples

### Rename a file

	Invoke-WmiMethod -Path "CIM_DataFile.Name='C:\users\public\spns.csv'" -Name Rename -ArgumentList "C:\Users\Public\kerberoasted_users.csv"

```powershell-session
__GENUS          : 2
__CLASS          : __PARAMETERS
__SUPERCLASS     :
__DYNASTY        : __PARAMETERS
__RELPATH        :
__PROPERTY_COUNT : 1
__DERIVATION     : {}
__SERVER         :
__NAMESPACE      :
__PATH           :
ReturnValue      : 0
PSComputerName   :
```

# References