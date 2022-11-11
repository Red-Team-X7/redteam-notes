# ⚙️ netstat

Tags: #⚙️
Related to:
See also:
Previous:

## Description

Print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

## Usage Examples

### Check active connections and find executables

	netstat -o
	
Compare PID with running services:

	tasklist | findstr <PID>	// and would see SERVER.EXE running on port 4444.
	
### Check for locally running services

	netstat -ant | findstr LIST

```
-n	// Displays addresses and port numbers in numerical form.
-a	// Displays all connections and listening ports.
-t	// Displays the current connection offload state.
```

```
TCP    127.0.0.1:4444         0.0.0.0:0              LISTENING       InHost
```

# References