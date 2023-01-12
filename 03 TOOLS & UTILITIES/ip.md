# ⚙️ ip

Tags: #⚙️
Related to:
See also: [[ifconfig]]
Previous:

## Description

Show / manipulate routing, network devices, interfaces and tunnels.

## Usage Examples

### Show addresses assigned to all network interfaces

	ip a
	ip addr

### Check that you're connected to VPN

	ip -4 a show tun0

```text
6: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 500
    inet 10.10.10.1/23 scope global tun0
       valid_lft forever preferred_lft forever
```

As long we get our IP back, then we should be connected to the VPN network.

# References
