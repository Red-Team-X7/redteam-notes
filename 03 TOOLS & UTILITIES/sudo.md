# ⚙️ sudo

Tags: #⚙️ 
Related to: 
See also: 
Previous: 

## Description

Print real and effective user and group IDs.

## Usage Examples

### Execute the command as root (Administrator)

	sudo <command>	

### Print real and effective user and group IDs

	sudo -l	// the user is able to execute /bin/bash as any other user apart from root

```
-l	// If no command is specified, list the allowed (and forbidden) commands for the invoking user (or the user specified by the -U option) on the current host. A longer list format is used if this option is specified multiple times and the security policy supports a verbose output format.
```

```
Matching Defaults entries for ben on DANTE-NIX04:
    env_keep+="LANG LANGUAGE LINGUAS LC_* _XKB_CHARSET", env_keep+="XAPPLRESDIR XFILESEARCHPATH
    XUSERFILESEARCHPATH", secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin, mail_badpass

User ben may run the following commands on DANTE-NIX04:
    (ALL, !root) /bin/bash
```

### Run command as user

	sudo -u julian /bin/bash	// Welcometomyblog

```
-u	// Run the command as a user other than the default target user (usually root).
```

### Add a new sudo user

	adduser cry0l1t3
	usermod -aG sudo cry0l1t3
	su - cry0l1t3

```shell-session
Password: 

[cry0l1t3@VPS ~]$
```

# References