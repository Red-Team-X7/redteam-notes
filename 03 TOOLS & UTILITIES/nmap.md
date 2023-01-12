# 💢 nmap

Tags: #💢
Related to: 
See also: [[nping]], [[ndiff]], [[ncat]]
Previous: [[Information Gathering]], [[Getting Started]], [[Network Enumeration with Nmap]]

## Description

Nmap (“Network Mapper”) is a free and open source (license) utility for network discovery and security auditing. Many systems and network administrators also find it useful for tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime. Nmap uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. It was designed to rapidly scan large networks, but works fine against single hosts. Nmap runs on all major computer operating systems, and official binary packages are available for Linux, Windows, and Mac OS X. In addition to the classic command-line Nmap executable, the Nmap suite includes an advanced GUI and results viewer (Zenmap), a flexible data transfer, redirection, and debugging tool (Ncat), a utility for comparing scan results (Ndiff), and a packet generation and response analysis tool (Nping).

Nmap was named “Security Product of the Year” by Linux Journal, Info World, LinuxQuestions.Org, and Codetalker Digest. It was even featured in twelve movies, including The Matrix Reloaded, Die Hard 4, Girl With the Dragon Tattoo, and The Bourne Ultimatum.

## Usage Examples

### Examine service

	sudo nmap 10.129.14.128 -sV -sC -p139,445

```text
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 15:15 CEST
Nmap scan report for sharing.inlanefreight.htb (10.129.14.128)
Host is up (0.00024s latency).

PORT    STATE SERVICE     VERSION
139/tcp open  netbios-ssn Samba smbd 4.6.2
445/tcp open  netbios-ssn Samba smbd 4.6.2
MAC Address: 00:00:00:00:00:00 (VMware)

Host script results:
|_nbstat: NetBIOS name: HTB, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-09-19T13:16:04
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.35 seconds
```

### Find FTP scripts

	find / -type f -name ftp* 2>/dev/null | grep scripts

```text
/usr/share/nmap/scripts/ftp-syst.nse
/usr/share/nmap/scripts/ftp-vsftpd-backdoor.nse
/usr/share/nmap/scripts/ftp-vuln-cve2010-4221.nse
/usr/share/nmap/scripts/ftp-proftpd-backdoor.nse
/usr/share/nmap/scripts/ftp-bounce.nse
/usr/share/nmap/scripts/ftp-libopie.nse
/usr/share/nmap/scripts/ftp-anon.nse
/usr/share/nmap/scripts/ftp-brute.nse
```

### Run Script Wildcard

	sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*

```text
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-21 00:53 CEST
Nmap scan report for 10.129.14.128
Host is up (0.00021s latency).

PORT     STATE SERVICE     VERSION
3306/tcp open  nagios-nsca Nagios NSCA
| mysql-brute: 
|   Accounts: 
|     root:<empty> - Valid credentials
|_  Statistics: Performed 45010 guesses in 5 seconds, average tps: 9002.0
|_mysql-databases: ERROR: Script execution failed (use -d to debug)
|_mysql-dump-hashes: ERROR: Script execution failed (use -d to debug)
| mysql-empty-password: 
|_  root account has empty password
| mysql-enum: 
|   Valid usernames: 
|     root:<empty> - Valid credentials
|     netadmin:<empty> - Valid credentials
|     guest:<empty> - Valid credentials
|     user:<empty> - Valid credentials
|     web:<empty> - Valid credentials
|     sysadmin:<empty> - Valid credentials
|     administrator:<empty> - Valid credentials
|     webadmin:<empty> - Valid credentials
|     admin:<empty> - Valid credentials
|     test:<empty> - Valid credentials
|_  Statistics: Performed 10 guesses in 1 seconds, average tps: 10.0
| mysql-info: 
|   Protocol: 10
|   Version: 8.0.26-0ubuntu0.20.04.1
|   Thread ID: 13
|   Capabilities flags: 65535
|   Some Capabilities: SupportsLoadDataLocal, SupportsTransactions, Speaks41ProtocolOld, LongPassword, DontAllowDatabaseTableColumn, Support41Auth, IgnoreSigpipes, SwitchToSSLAfterHandshake, FoundRows, InteractiveClient, Speaks41ProtocolNew, ConnectWithDatabase, IgnoreSpaceBeforeParenthesis, LongColumnFlag, SupportsCompression, ODBCClient, SupportsMultipleStatments, SupportsAuthPlugins, SupportsMultipleResults
|   Status: Autocommit
|   Salt: YTSgMfqvx\x0F\x7F\x16\&\x1EAeK>0
|_  Auth Plugin Name: caching_sha2_password
|_mysql-users: ERROR: Script execution failed (use -d to debug)
|_mysql-variables: ERROR: Script execution failed (use -d to debug)
|_mysql-vuln-cve2012-2122: ERROR: Script execution failed (use -d to debug)
MAC Address: 00:00:00:00:00:00 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.21 seconds
```

### Trace script

	sudo nmap -sV -p21 -sC -A 10.129.14.136 --script-trace

```text
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-19 13:54 CEST                                                                                                                                                   
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 8 [10.129.14.136:21]                                   
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 16 [10.129.14.136:21]             
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 24 [10.129.14.136:21]
NSOCK INFO [11.4640s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 32 [10.129.14.136:21]
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #1 [10.129.14.136:21] (timeout: 7000ms) EID 42
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #2 [10.129.14.136:21] (timeout: 9000ms) EID 50
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #3 [10.129.14.136:21] (timeout: 7000ms) EID 58
NSOCK INFO [11.4640s] nsock_read(): Read request from IOD #4 [10.129.14.136:21] (timeout: 11000ms) EID 66
NSE: TCP 10.10.14.4:54226 > 10.129.14.136:21 | CONNECT
NSE: TCP 10.10.14.4:54228 > 10.129.14.136:21 | CONNECT
NSE: TCP 10.10.14.4:54230 > 10.129.14.136:21 | CONNECT
NSE: TCP 10.10.14.4:54232 > 10.129.14.136:21 | CONNECT
NSOCK INFO [11.4660s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 50 [10.129.14.136:21] (41 bytes): 220 Welcome to HTB-Academy FTP service...
NSOCK INFO [11.4660s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 58 [10.129.14.136:21] (41 bytes): 220 Welcome to HTB-Academy FTP service...
NSE: TCP 10.10.14.4:54228 < 10.129.14.136:21 | 220 Welcome to HTB-Academy FTP service.
```

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

# References

[^1]: https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/nmap