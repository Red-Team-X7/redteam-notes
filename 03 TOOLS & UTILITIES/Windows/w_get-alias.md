# ⚙️ get-alias

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

List PowerShell aliases

## Usage Examples

### List PowerShell aliases

	get-alias

```text
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           % -> ForEach-Object
Alias           ? -> Where-Object
Alias           ac -> Add-Content
Alias           asnp -> Add-PSSnapin
Alias           cat -> Get-Content
Alias           cd -> Set-Location
Alias           CFS -> ConvertFrom-String                          3.1.0.0    Microsoft.PowerShell.Utility
Alias           chdir -> Set-Location
Alias           clc -> Clear-Content
Alias           clear -> Clear-Host
Alias           clhy -> Clear-History
Alias           cli -> Clear-Item
Alias           clp -> Clear-ItemProperty
```

### Get the aliases for a cmdlet

	Get-Alias -Name "Show-Files"

```text
CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           Show-Files
```

# References