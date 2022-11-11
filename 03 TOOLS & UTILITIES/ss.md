# ⚙️ ss
Tags: #⚙️ 
Related to: 
See also: [[netstat]]
Previous: [[ ]]

---
## Description

Used to dump socket statistics. It allows showing information similar to netstat. It can display more TCP and state information than other tools.
	   
## Usage Examples

Find SUID files:

	find / -perm -4000 -ls 2>/dev/null	// nothing interesting

Find user's files:

	find / -user jimmy -ls 2>/dev/null

```

   286763      4 drwxrwx---   2 jimmy    internal     4096 Nov 23  2019 /var/www/internal
   282830      4 -rwxrwxr-x   1 jimmy    internal      339 Nov 23  2019 /var/www/internal/main.php
     2644      4 -rwxrwxr-x   1 jimmy    internal      185 Nov 23  2019 /var/www/internal/logout.php
     1387      4 -rwxrwxr-x   1 jimmy    internal     3229 Nov 22  2019 /var/www/internal/index.php
```
	
Are we missing something...?

### Show socket statistics

	ss -lntp

```
State         Recv-Q         Send-Q                  Local Address:Port                    Peer Address:Port         
LISTEN        0              128                     127.0.0.53%lo:53                           0.0.0.0:*            
LISTEN        0              128                           0.0.0.0:22                           0.0.0.0:*            
LISTEN        0              80                          127.0.0.1:3306                         0.0.0.0:*            
LISTEN        0              128                         127.0.0.1:52846                        0.0.0.0:*            
LISTEN        0              128                              [::]:22                              [::]:*            
LISTEN        0              128                                 *:80                                 *:*
```

	127.0.0.1:52846 <= high port number

---
## References
- [[]]