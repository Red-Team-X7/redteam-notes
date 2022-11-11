# ⚙️ scp

Tags: #⚙️
Related to:
See also:
Previous: [[Getting Started]]

## Description

OpenSSH secure file copy.

## Usage Examples

### Copy file to victim machine

	scp linenum.sh user@remotehost:/tmp/linenum.sh
	
	scp pspy-master.zip floris@10.129.162.241:/tmp

### Copy files to victim machine

```
scp -i <ssh-private-key> -r <directory to transfer> <username>@<IP/FQDN>:<path>
```

	scp -i ~/.ssh/cry0l1t3 -r ~/Pentesting cry0l1t3@VPS:~/

# References