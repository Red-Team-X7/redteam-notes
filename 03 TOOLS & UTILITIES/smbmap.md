# 💢 smbmap

Tags: #💢
Related to:
See also:
Previous: [[SMB Analysis]], [[00 KALI/Password Attacks]] [[Footprinting]]

## Description

SMBMap allows users to enumerate samba share drives across an entire domain. List share drives, drive permissions, share contents, upload/download functionality, file name auto-download pattern matching, and even execute remote commands. This tool was designed with pen testing in mind, and is intended to simplify searching for potentially sensitive data across large networks.

## Usage Examples

### Enumerate SMB shares

	smbmap -H <FQDN/IP>

# References