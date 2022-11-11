# ⚙️ netsh

Tags: #⚙️
Related to:
See also:
Previous:

## Description

Network shell (netsh) is a command-line utility that allows you to configure and display the status of various network communications server roles and components after they are installed on computers running Windows Server.

## Usage Examples

### Port forward

	netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=3333 connectaddress=127.0.0.1 connectport=4444 protocol=tcp

```
The command forwards the connection from port 3333 on 0.0.0.0 to port 4444 on localhost, allowing us to access the  service. Let's validate the vulnerability by sending more than 1024 bytes of data in the password field.
```

# References
