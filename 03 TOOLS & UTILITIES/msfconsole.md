# 💢 msfconsole

Tags: #💢
Related to: 
See also: 
Previous: [[metasploit framework]], [[Hacking Wordpress]], [[Getting Started]], [[Footprinting]]

## Description

The Metasploit Framework is an open source platform that supports vulnerability research, exploit development, and the creation of custom security tools.

## Usage Examples

### Pwn public exploit

| Command | Description |
|-|-|
| Public Exploits |  |
| `searchsploit openssh 7.2` | Search for public exploits for a web application |
| `msfconsole` | MSF: Start the Metasploit Framework |
| `search exploit eternalblue` | MSF: Search for public exploits in MSF |
| `use exploit/windows/smb/ms17_010_psexec` | MSF: Start using an MSF module |
| `show options` | MSF: Show required options for an MSF module |
| `set RHOSTS 10.10.10.40` | MSF: Set a value for an MSF module option |
| `check` | MSF: Test if the target server is vulnerable |
| `exploit` | MSF: Run the exploit on the target server is vulnerable |

### IPMI version detection

	msf6 auxiliary(scanner/ipmi/ipmi_version)

### Dump IPMI hashes

	msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)

# References