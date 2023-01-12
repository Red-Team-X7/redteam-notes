# ⚙️ get-mpcomputerstatus

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

Check which Defender protection settings are enabled.

## Usage Examples

### Check which Defender protection settings are enabled

	Get-MpComputerStatus | findstr "True"

```text
AMServiceEnabled                : True
AntispywareEnabled              : True
AntivirusEnabled                : True
BehaviorMonitorEnabled          : True
IoavProtectionEnabled           : True
IsTamperProtected               : True
NISEnabled                      : True
OnAccessProtectionEnabled       : True
RealTimeProtectionEnabled       : True
```

# References