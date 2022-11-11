# ⚙️ ftp

Tags: #⚙️
Related to:
See also:
Previous: [[Getting Started]], [[Footprinting]]

## Description

Internet file transfer program.

## Usage Examples

### Interact with the FTP service on the target

	ftp <FQDN/IP>

### Anonymous passive mode login and file download

	ftp -p 10.10.110.100	// anonymous:anonymous
	ls
	cd Transfer
	cd Incoming
	get todo.txt
	exit

# References