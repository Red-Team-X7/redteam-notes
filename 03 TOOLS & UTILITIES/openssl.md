# ⚙️ openssl

Tags: #⚙️
Related to:
See also:
Previous: [[Getting Started]]

## Description

OpenSSL command line program.

## Usage Examples

### Interact with the FTP service on the target using encrypted connection

	openssl s_client -connect <FQDN/IP>:21 -starttls ftp	

### Connect to IMAPS service

	openssl s_client -connect <FQDN/IP>:imaps	

### Connect to POP3s service

	openssl s_client -connect <FQDN/IP>:pop3s	

# References



[[Footprinting]]