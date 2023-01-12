# ⚙️ reg

Tags: #⚙️
Related to:
See also:
Previous: [[Windows Fundamentals]]

## Description

View information about a registry entry.

## Usage Examples

### View information about a registry key while logged into the system

	reg query HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run

```text
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
    SecurityHealth    REG_EXPAND_SZ    %windir%\system32\SecurityHealthSystray.exe
    RTHDVCPL    REG_SZ    "C:\Program Files\Realtek\Audio\HDA\RtkNGUI64.exe" -s
    Greenshot    REG_SZ    C:\Program Files\Greenshot\Greenshot.exe
```

### View information about a registry key running under the current user while logged in to a system

	reg query HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
    OneDrive    REG_SZ    "C:\Users\bob\AppData\Local\Microsoft\OneDrive\OneDrive.exe" /background
    OPENVPN-GUI    REG_SZ    C:\Program Files\OpenVPN\bin\openvpn-gui.exe
    Docker Desktop    REG_SZ    C:\Program Files\Docker\Docker\Docker Desktop.exe
```

# References