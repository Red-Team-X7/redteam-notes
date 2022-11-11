# 🤖 cmd.exe
Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]]

## Description

## Usage Examples

### Get client-side software inventory
	dir /s “c:\Program Files” > inventory.txt
	dir /s “c:\Program Files (x86)” >> inventory.txt

### Disable firewall
	netsh advfirewall set allprofiles state off

### Get network settings

	ipconfig				// See network settings.
	ipconfig /displaydns	// See Windows DNS cache.

### Add a user

	net user											// List local users.
	net localgroup										// List local groups.
	net localgroup administrators						// List member of local admin group.
	net user [logon_name] [password] /add				// Add a user.
	net localgroup administrators [logon_name] /add		// Put the user in the local admin group.

### List running processes

	tasklist

### Show command help

	hostname /?

# References