# ⚙️ ipcalc

Tags: #⚙️
Related to: [[whois]]
See also: 
Previous: [[OSINT - Corporate Recon]]

## Description

ipcalc  takes  an IPv4 address and netmask and calculates the resulting broadcast, network, Cisco wildcard mask, and host range. By giving a second netmask, you can design sub- and supernetworks. It is also intended to be a teaching tool and presents the results as easy-to-understand binary values.

## Usage Examples

### Calculate IP info

	ipcalc 10.10.10.10/24  

```text
Address:   10.10.10.10          00001010.00001010.00001010. 00001010
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
=>
Network:   10.10.10.0/24        00001010.00001010.00001010. 00000000
HostMin:   10.10.10.1           00001010.00001010.00001010. 00000001
HostMax:   10.10.10.254         00001010.00001010.00001010. 11111110
Broadcast: 10.10.10.255         00001010.00001010.00001010. 11111111
Hosts/Net: 254                   Class A, Private Internet
```

# References