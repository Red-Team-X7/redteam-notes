# ⚙️ tcpdump

Tags: #⚙️ 
Related to: [[tshark]]
See also:
Previous: [[Intro to Network Traffic Analysis]]

## Description

Dump traffic on a network

## Usage Examples

### Dump traffic without converting names

	sudo tcpdump -i tun0 -nn net 10.10.10

## Expressions

	Protocol: ether, ip, ipv6, arp, rarp, tcp, udp  
 
	Type:  
			host [host]  
			net [network]  
			port [portnum]  
			portrange [start-end]  

	Direction:  
			src  
			dst  

	Use "and" or "or" to combine them.  
	Use "not" to negate.  

	Wrap in parenthesis to group elements together.

## Options

    -n
			Use numbers instead of names for machines.
    
    -nn
			" " and ports (in latest versions
        	-n and -nn are the same).
    
    -i[int]
        	sniff on particular interface
        	(-D lists interfaces).
    
    -v
        	Be verbose (show TTL, IP ID, Total Length,
        	IP options, ...)
    
    -w
        	Dump packets to a file.
        	(use -r to read file later).
    
    -x
        	Print hex and ASCII
    
    -A
			Print ASCII (doesn't work in all versions...
   			consider -X instead).

---
## References
- https://www.tcpdump.org
- https://www.winpcap.org/windump/default.htm