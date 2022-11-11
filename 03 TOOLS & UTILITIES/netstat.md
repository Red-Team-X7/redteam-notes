# ⚙️ netstat

Tags: #⚙️
Related to:
See also: [[ss]]
Previous: [[Getting Started]]


## Description

Print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships.

## Usage Examples

### Display kernel routing tables

	netstat -rn

```
Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.0.1     0.0.0.0         UG        0 0          0 XXX
XXX.XXX.0.0     0.0.0.0         255.255.0.0     U         0 0          0 XXX
XXX.XXX.0.0     0.0.0.0         255.255.255.0   U         0 0          0 XXX
```

### Show PID, program name, and state

	netstat -antupe

```
-n		// Show numerical addresses instead of trying to determine symbolic host, port or user names.
-a		// Show both listening and non-listening sockets.
-p		// Show the PID and name of the program to which each socket belongs.
-t		// tcp
-u		// udp
-e		// extend - display additional information; use twice for maximum detail.
```

###  Show PID, program name, state, and more

	netstat -nap

```
-n		// Show numerical addresses instead of trying to determine symbolic host, port or user names.
-a		// Show both listening and non-listening sockets.
-p		// Show the PID and name of the program to which each socket belongs.
```

### Show listening sockets

	netstat -lnp

```
-l		// Show only listening sockets.
-n		// Show numerical addresses instead of trying to determine symbolic host, port or user names.
-p		// Show the PID and name of the program to which each socket belongs.
```

	netstat -lnp | grep 8001

```
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp6       0      0 :::8001                 :::*                    LISTEN      30315/chisel
```


# References