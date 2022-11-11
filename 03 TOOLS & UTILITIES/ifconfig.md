# ⚙️ ifconfig

Tags: #⚙️
Related to:
See also: [[ip]]
Previous: [[Getting Started]]

## Description

Configure a network interface.

## Usage Examples

### Get IP/Subnet

	ifconfig

```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.16.1.100  netmask 255.255.255.0  broadcast 172.16.1.255
        inet6 fe80::250:56ff:feb9:bcff  prefixlen 64  scopeid 0x20<link>
        ether 00:50:56:b9:bc:ff  txqueuelen 1000  (Ethernet)
        RX packets 1312723  bytes 282279120 (282.2 MB)
        RX errors 0  dropped 29  overruns 0  frame 0
        TX packets 2192918  bytes 664647759 (664.6 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

### Check routing table

	sudo netstat -rn

```shell-session
[sudo] password for user: 

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.195.2   0.0.0.0         UG        0 0          0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG        0 0          0 tun0
192.168.1.0   0.0.0.0         255.255.255.0   U         0 0          0 eth0
```


# References

[^1]: https://gtfobins.github.io/
