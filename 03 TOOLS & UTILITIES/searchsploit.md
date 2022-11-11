# 💢 searchsploit
Tags: #💢
Related to: 
See also: 
Previous: [[Exploitation Tools]], [[Getting Started]]

---
## Description

Exploit Database Archive Search.

## Usage Examples

### Install

	sudo apt install exploitdb -y

### Search for exploits

	searchsploit opennetadmin

```
OpenNetAdmin 18.1.1 - Command Injection Exploit (Metasploit)	| php/webapps/47772.rb
OpenNetAdmin 18.1.1 - Remote Code Execution						| php/webapps/47691.sh
```

Examine exploit using $PAGER:

	searchsploit -x php/webapps/47691.sh

Copy exploit to the current working directory:

	searchsploit -m php/webapps/47691.sh

### Update

	searchsploit -u
	
---
## References
- [[]]