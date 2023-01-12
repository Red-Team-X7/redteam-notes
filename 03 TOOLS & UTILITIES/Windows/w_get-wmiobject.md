# ⚙️ get-wmiobject

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

## Usage Examples

### Get information about the operating system

	Get-WmiObject -Class win32_OperatingSystem

```text
Version    BuildNumber
-------    -----------
10.0.19041 19041
```

	Get-WmiObject -Class Win32_OperatingSystem | select SystemDirectory,BuildNumber,SerialNumber,Version | ft

```text
SystemDirectory     BuildNumber SerialNumber            Version
---------------     ----------- ------------            -------
C:\Windows\system32 19041       00123-00123-00123-AAOEM 10.0.19041
```

# References