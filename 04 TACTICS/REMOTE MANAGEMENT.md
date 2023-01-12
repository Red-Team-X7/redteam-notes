# 🔥 remote management

Tags: #🔥
Related to: [[ssh]], [[ssh-audit]], [[rdp-sec-check]], [[xfreerdp]], [[evil-winrm]], [[impacket-wmiexec]], [[nmap]], [[nc]], [[rsync]], [[cpan]], [[remmina]]
See also:
Previous: [[TACTICS]], [[Footprinting]]

## Description

## Cheatsheet

####  Linux Remote Management

| **Command** | **Description** |
| --- | --- |
| `ssh-audit.py <FQDN/IP>` | Remote security audit against the target SSH service. |
| `ssh <user>@<FQDN/IP>` | Log in to the SSH server using the SSH client. |
| `ssh -i private.key <user>@<FQDN/IP>` | Log in to the SSH server using private key. |
| `ssh <user>@<FQDN/IP> -o PreferredAuthentications=password` | Enforce password-based authentication. |

#### Windows Remote Management

| **Command** | **Description** |
| --- | --- |
| `rdp-sec-check.pl <FQDN/IP>` | Check the security settings of the RDP service. |
| `xfreerdp /u:<user> /p:"<password>" /v:<FQDN/IP>` | Log in to the RDP server from Linux. |
| `evil-winrm -i <FQDN/IP> -u <user> -p <password>` | Log in to the WinRM server. |
| `wmiexec.py <user>:"<password>"@<FQDN/IP> "<system command>"` | Execute command using the WMI service. |

#### Dangerous Settings

##### SSH

| **Setting** | **Description** |
| --- | --- |
| `PasswordAuthentication yes` | Allows password-based authentication. |
| `PermitEmptyPasswords yes` | Allows the use of empty passwords. |
| `PermitRootLogin yes` | Allows to log in as the root user. |
| `Protocol 1` | Uses an outdated version of encryption. |
| `X11Forwarding yes` | Allows X11 forwarding for GUI applications. |
| `AllowTcpForwarding yes` | Allows forwarding of TCP ports. |
| `PermitTunnel` | Allows tunneling. |
| `DebianBanner yes` | Displays a specific banner when logging in. |

##### R-Services

| **Command** | **Service Daemon** | **Port** | **Transport Protocol** | **Description** |
| --- | --- | --- | --- | --- |
| `rcp` | `rshd` | 514 | TCP | Copy a file or directory bidirectionally from the local system to the remote system (or vice versa) or from one remote system to another. It works like the `cp` command on Linux but provides `no warning to the user for overwriting existing files on a system`. |
| `rsh` | `rshd` | 514 | TCP | Opens a shell on a remote machine without a login procedure. Relies upon the trusted entries in the `/etc/hosts.equiv` and `.rhosts` files for validation. |
| `rexec` | `rexecd` | 512 | TCP | Enables a user to run shell commands on a remote machine. Requires authentication through the use of a `username` and `password` through an unencrypted network socket. Authentication is overridden by the trusted entries in the `/etc/hosts.equiv` and `.rhosts` files. |
| `rlogin` | `rlogind` | 513 | TCP | Enables a user to log in to a remote host over the network. It works similarly to `telnet` but can only connect to Unix-like hosts. Authentication is overridden by the trusted entries in the `/etc/hosts.equiv` and `.rhosts` files. |

## Usage Examples

### SSH

#### Default Configuration

	cat /etc/ssh/sshd_config  | grep -v "#" | sed -r '/^\s*$/d'

```text
Include /etc/ssh/sshd_config.d/*.conf
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding yes
PrintMotd no
AcceptEnv LANG LC_*
Subsystem       sftp    /usr/lib/openssh/sftp-server
```

#### SSH-Audit

	git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit
	./ssh-audit.py 10.129.14.132

```text
# general
(gen) banner: SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.3
(gen) software: OpenSSH 8.2p1
(gen) compatibility: OpenSSH 7.4+, Dropbear SSH 2018.76+
(gen) compression: enabled (zlib@openssh.com)                                   

# key exchange algorithms
(kex) curve25519-sha256                     -- [info] available since OpenSSH 7.4, Dropbear SSH 2018.76                            
(kex) curve25519-sha256@libssh.org          -- [info] available since OpenSSH 6.5, Dropbear SSH 2013.62
(kex) ecdh-sha2-nistp256                    -- [fail] using weak elliptic curves
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(kex) ecdh-sha2-nistp384                    -- [fail] using weak elliptic curves
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(kex) ecdh-sha2-nistp521                    -- [fail] using weak elliptic curves
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(kex) diffie-hellman-group-exchange-sha256 (2048-bit) -- [info] available since OpenSSH 4.4
(kex) diffie-hellman-group16-sha512         -- [info] available since OpenSSH 7.3, Dropbear SSH 2016.73
(kex) diffie-hellman-group18-sha512         -- [info] available since OpenSSH 7.3
(kex) diffie-hellman-group14-sha256         -- [info] available since OpenSSH 7.3, Dropbear SSH 2016.73

# host-key algorithms
(key) rsa-sha2-512 (3072-bit)               -- [info] available since OpenSSH 7.2
(key) rsa-sha2-256 (3072-bit)               -- [info] available since OpenSSH 7.2
(key) ssh-rsa (3072-bit)                    -- [fail] using weak hashing algorithm
                                            `- [info] available since OpenSSH 2.5.0, Dropbear SSH 0.28
                                            `- [info] a future deprecation notice has been issued in OpenSSH 8.2: https://www.openssh.com/txt/release-8.2
(key) ecdsa-sha2-nistp256                   -- [fail] using weak elliptic curves
                                            `- [warn] using weak random number generator could reveal the key
                                            `- [info] available since OpenSSH 5.7, Dropbear SSH 2013.62
(key) ssh-ed25519                           -- [info] available since OpenSSH 6.5
...SNIP...
```

#### Change Authentication Method

	ssh -v cry0l1t3@10.129.14.132 -o PreferredAuthentications=password

```text
OpenSSH_8.2p1 Ubuntu-4ubuntu0.3, OpenSSL 1.1.1f  31 Mar 2020
debug1: Reading configuration data /etc/ssh/ssh_config
...SNIP...
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Next authentication method: password
cry0l1t3@10.129.14.132's password:
```

### Rsync

#### Scanning for Rsync

	sudo nmap -sV -p 873 127.0.0.1

```text
Starting Nmap 7.92 ( https://nmap.org ) at 2022-09-19 09:31 EDT
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0058s latency).

PORT    STATE SERVICE VERSION
873/tcp open  rsync   (protocol version 31)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 1.13 seconds
```

#### Probing for Accessible Shares

	nc -nv 127.0.0.1 873

```text
(UNKNOWN) [127.0.0.1] 873 (rsync) open
@RSYNCD: 31.0
@RSYNCD: 31.0
#list
dev            	Dev Tools
@RSYNCD: EXIT
```

#### Enumerating an Open Share

	rsync -av --list-only rsync://127.0.0.1/dev

```text
receiving incremental file list
drwxr-xr-x             48 2022/09/19 09:43:10 .
-rw-r--r--              0 2022/09/19 09:34:50 build.sh
-rw-r--r--              0 2022/09/19 09:36:02 secrets.yaml
drwx------             54 2022/09/19 09:43:10 .ssh

sent 25 bytes  received 221 bytes  492.00 bytes/sec
total size is 0  speedup is 0.00
```

#### Sync Files to Attacker Machine

	rsync -av rsync://127.0.0.1/dev
	rsync -av rsync://127.0.0.1/dev -e ssh
	rsync -av rsync://127.0.0.1/dev -e ssh -p2222

### R-Services

#### Scanning for R-Services

	sudo nmap -sV -p 512,513,514 10.0.17.2

```text
Starting Nmap 7.80 ( https://nmap.org ) at 2022-12-02 15:02 EST
Nmap scan report for 10.0.17.2
Host is up (0.11s latency).

PORT    STATE SERVICE    VERSION
512/tcp open  exec?
513/tcp open  login?
514/tcp open  tcpwrapped

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 145.54 seconds
```

##### Sample .rhosts File

>Note: The `hosts.equiv` file is recognized as the global configuration regarding all users on a system, whereas `.rhosts` provides a per-user configuration.

	cat .rhosts

```text
htb-student     10.0.17.5
+               10.0.17.10
+               +
```

As we can see from this example, both files follow the specific syntax of `<username> <ip address>` or `<username> <hostname>` pairs. Additionally, the `+` modifier can be used within these files as a wildcard to specify anything. In this example, the `+` modifier allows any external user to access r-commands from the `htb-student` user account via the host with the IP address `10.0.17.10`.

#### Logging in Using rlogin

	rlogin 10.0.17.2 -l htb-student

```text
Last login: Fri Dec  2 16:11:21 from localhost

[htb-student@localhost ~]$
```

#### Listing Authenticated Users Using rwho

	rwho

```text
root         web01:pts/0 Dec  2 21:34
htb-student  workstn01:tty1  Dec  2 19:57  2:25
```

### RDP

#### Nmap

	nmap -sV -sC 10.129.201.248 -p3389 --script rdp*

```text
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-06 15:45 CET
Nmap scan report for 10.129.201.248
Host is up (0.036s latency).

PORT     STATE SERVICE       VERSION
3389/tcp open  ms-wbt-server Microsoft Terminal Services
| rdp-enum-encryption: 
|   Security layer
|     CredSSP (NLA): SUCCESS
|     CredSSP with Early User Auth: SUCCESS
|_    RDSTLS: SUCCESS
| rdp-ntlm-info: 
|   Target_Name: ILF-SQL-01
|   NetBIOS_Domain_Name: ILF-SQL-01
|   NetBIOS_Computer_Name: ILF-SQL-01
|   DNS_Domain_Name: ILF-SQL-01
|   DNS_Computer_Name: ILF-SQL-01
|   Product_Version: 10.0.17763
|_  System_Time: 2021-11-06T13:46:00+00:00
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.26 seconds
```

In addition, we can use `--packet-trace` to track the individual packages and inspect their contents manually. We can see that the `RDP cookies` (`mstshash=nmap`) used by Nmap to interact with the RDP server can be identified by `threat hunters` and various security services such as [Endpoint Detection and Response](https://en.wikipedia.org/wiki/Endpoint_detection_and_response) (`EDR`), and can lock us out as penetration testers on hardened networks.

	nmap -sV -sC 10.129.201.248 -p3389 --packet-trace --disable-arp-ping -n

```text
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-06 16:23 CET
SENT (0.2506s) ICMP [10.10.14.20 > 10.129.201.248 Echo request (type=8/code=0) id=8338 seq=0] IP [ttl=53 id=5122 iplen=28 ]
SENT (0.2507s) TCP 10.10.14.20:55516 > 10.129.201.248:443 S ttl=42 id=24195 iplen=44  seq=1926233369 win=1024 <mss 1460>
SENT (0.2507s) TCP 10.10.14.20:55516 > 10.129.201.248:80 A ttl=55 id=50395 iplen=40  seq=0 win=1024
SENT (0.2517s) ICMP [10.10.14.20 > 10.129.201.248 Timestamp request (type=13/code=0) id=8247 seq=0 orig=0 recv=0 trans=0] IP [ttl=38 id=62695 iplen=40 ]
RCVD (0.2814s) ICMP [10.129.201.248 > 10.10.14.20 Echo reply (type=0/code=0) id=8338 seq=0] IP [ttl=127 id=38158 iplen=28 ]
SENT (0.3264s) TCP 10.10.14.20:55772 > 10.129.201.248:3389 S ttl=56 id=274 iplen=44  seq=2635590698 win=1024 <mss 1460>
RCVD (0.3565s) TCP 10.129.201.248:3389 > 10.10.14.20:55772 SA ttl=127 id=38162 iplen=44  seq=3526777417 win=64000 <mss 1357>
NSOCK INFO [0.4500s] nsock_iod_new2(): nsock_iod_new (IOD #1)
NSOCK INFO [0.4500s] nsock_connect_tcp(): TCP connection requested to 10.129.201.248:3389 (IOD #1) EID 8
NSOCK INFO [0.4820s] nsock_trace_handler_callback(): Callback: CONNECT SUCCESS for EID 8 [10.129.201.248:3389]
Service scan sending probe NULL to 10.129.201.248:3389 (tcp)
NSOCK INFO [0.4830s] nsock_read(): Read request from IOD #1 [10.129.201.248:3389] (timeout: 6000ms) EID 18
NSOCK INFO [6.4880s] nsock_trace_handler_callback(): Callback: READ TIMEOUT for EID 18 [10.129.201.248:3389]
Service scan sending probe TerminalServerCookie to 10.129.201.248:3389 (tcp)
NSOCK INFO [6.4880s] nsock_write(): Write request for 42 bytes to IOD #1 EID 27 [10.129.201.248:3389]
NSOCK INFO [6.4880s] nsock_read(): Read request from IOD #1 [10.129.201.248:3389] (timeout: 5000ms) EID 34
NSOCK INFO [6.4880s] nsock_trace_handler_callback(): Callback: WRITE SUCCESS for EID 27 [10.129.201.248:3389]
NSOCK INFO [6.5240s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 34 [10.129.201.248:3389] (19 bytes): .........4.........
Service scan match (Probe TerminalServerCookie matched with TerminalServerCookie line 13640): 10.129.201.248:3389 is ms-wbt-server.  Version: |Microsoft Terminal Services|||

...SNIP...

NSOCK INFO [6.5610s] nsock_write(): Write request for 54 bytes to IOD #1 EID 27 [10.129.201.248:3389]
NSE: TCP 10.10.14.20:36630 > 10.129.201.248:3389 | 00000000: 03 00 00 2a 25 e0 00 00 00 00 00 43 6f 6f 6b 69    *%      Cooki
00000010: 65 3a 20 6d 73 74 73 68 61 73 68 3d 6e 6d 61 70 e: mstshash=nmap
00000020: 0d 0a 01 00 08 00 0b 00 00 00  

...SNIP...

NSOCK INFO [6.6820s] nsock_write(): Write request for 57 bytes to IOD #2 EID 67 [10.129.201.248:3389]
NSOCK INFO [6.6820s] nsock_trace_handler_callback(): Callback: WRITE SUCCESS for EID 67 [10.129.201.248:3389]
NSE: TCP 10.10.14.20:36630 > 10.129.201.248:3389 | SEND
NSOCK INFO [6.6820s] nsock_read(): Read request from IOD #2 [10.129.201.248:3389] (timeout: 5000ms) EID 74
NSOCK INFO [6.7180s] nsock_trace_handler_callback(): Callback: READ SUCCESS for EID 74 [10.129.201.248:3389] (211 bytes)
NSE: TCP 10.10.14.20:36630 < 10.129.201.248:3389 | 
00000000: 30 81 d0 a0 03 02 01 06 a1 81 c8 30 81 c5 30 81 0          0  0
00000010: c2 a0 81 bf 04 81 bc 4e 54 4c 4d 53 53 50 00 02        NTLMSSP
00000020: 00 00 00 14 00 14 00 38 00 00 00 35 82 8a e2 b9        8   5
00000030: 73 b0 b3 91 9f 1b 0d 00 00 00 00 00 00 00 00 70 s              p
00000040: 00 70 00 4c 00 00 00 0a 00 63 45 00 00 00 0f 49  p L     cE    I
00000050: 00 4c 00 46 00 2d 00 53 00 51 00 4c 00 2d 00 30  L F - S Q L - 0
00000060: 00 31 00 02 00 14 00 49 00 4c 00 46 00 2d 00 53  1     I L F - S
00000070: 00 51 00 4c 00 2d 00 30 00 31 00 01 00 14 00 49  Q L - 0 1     I
00000080: 00 4c 00 46 00 2d 00 53 00 51 00 4c 00 2d 00 30  L F - S Q L - 0
00000090: 00 31 00 04 00 14 00 49 00 4c 00 46 00 2d 00 53  1     I L F - S
000000a0: 00 51 00 4c 00 2d 00 30 00 31 00 03 00 14 00 49  Q L - 0 1     I
000000b0: 00 4c 00 46 00 2d 00 53 00 51 00 4c 00 2d 00 30  L F - S Q L - 0
000000c0: 00 31 00 07 00 08 00 1d b3 e8 f2 19 d3 d7 01 00  1
000000d0: 00 00 00

...SNIP...
```


#### RDP Security Check - Installation

	sudo cpan

```text
Loading internal logger. Log::Log4perl recommended for better logging

CPAN.pm requires configuration, but most of it can be done automatically.
If you answer 'no' below, you will enter an interactive dialog for each
configuration option instead.

Would you like to configure as much as possible automatically? [yes] yes


Autoconfiguration complete.

commit: wrote '/root/.cpan/CPAN/MyConfig.pm'

You can re-run configuration any time with 'o conf init' in the CPAN shell

cpan shell -- CPAN exploration and modules installation (v2.27)
Enter 'h' for help.


cpan[1]> install Encoding::BER

Fetching with LWP:
http://www.cpan.org/authors/01mailrc.txt.gz
Reading '/root/.cpan/sources/authors/01mailrc.txt.gz'
............................................................................DONE
...SNIP...
```

#### RDP Security Check

	git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check
	./rdp-sec-check.pl 10.129.201.248

```text
Starting rdp-sec-check v0.9-beta ( http://labs.portcullis.co.uk/application/rdp-sec-check/ ) at Sun Nov  7 16:50:32 2021

[+] Scanning 1 hosts

Target:    10.129.201.248
IP:        10.129.201.248
Port:      3389

[+] Checking supported protocols

[-] Checking if RDP Security (PROTOCOL_RDP) is supported...Not supported - HYBRID_REQUIRED_BY_SERVER
[-] Checking if TLS Security (PROTOCOL_SSL) is supported...Not supported - HYBRID_REQUIRED_BY_SERVER
[-] Checking if CredSSP Security (PROTOCOL_HYBRID) is supported [uses NLA]...Supported

[+] Checking RDP Security Layer

[-] Checking RDP Security Layer with encryption ENCRYPTION_METHOD_NONE...Not supported
[-] Checking RDP Security Layer with encryption ENCRYPTION_METHOD_40BIT...Not supported
[-] Checking RDP Security Layer with encryption ENCRYPTION_METHOD_128BIT...Not supported
[-] Checking RDP Security Layer with encryption ENCRYPTION_METHOD_56BIT...Not supported
[-] Checking RDP Security Layer with encryption ENCRYPTION_METHOD_FIPS...Not supported

[+] Summary of protocol support

[-] 10.129.201.248:3389 supports PROTOCOL_SSL   : FALSE
[-] 10.129.201.248:3389 supports PROTOCOL_HYBRID: TRUE
[-] 10.129.201.248:3389 supports PROTOCOL_RDP   : FALSE

[+] Summary of RDP encryption support

[-] 10.129.201.248:3389 supports ENCRYPTION_METHOD_NONE   : FALSE
[-] 10.129.201.248:3389 supports ENCRYPTION_METHOD_40BIT  : FALSE
[-] 10.129.201.248:3389 supports ENCRYPTION_METHOD_128BIT : FALSE
[-] 10.129.201.248:3389 supports ENCRYPTION_METHOD_56BIT  : FALSE
[-] 10.129.201.248:3389 supports ENCRYPTION_METHOD_FIPS   : FALSE

[+] Summary of security issues

rdp-sec-check v0.9-beta completed at Sun Nov  7 16:50:33 2021
```

#### Initiate an RDP Session

	xfreerdp /u:cry0l1t3 /p:"P455w0rd!" /v:10.129.201.248

```text
[16:37:47:135] [95319:95320] [INFO][com.freerdp.core] - freerdp_connect:freerdp_set_last_error_ex resetting error state
[16:37:47:135] [95319:95320] [INFO][com.freerdp.client.common.cmdline] - loading channelEx rdpdr
[16:37:47:135] [95319:95320] [INFO][com.freerdp.client.common.cmdline] - loading channelEx rdpsnd
[16:37:47:135] [95319:95320] [INFO][com.freerdp.client.common.cmdline] - loading channelEx cliprdr
[16:37:47:447] [95319:95320] [INFO][com.freerdp.primitives] - primitives autodetect, using optimized
[16:37:47:453] [95319:95320] [INFO][com.freerdp.core] - freerdp_tcp_is_hostname_resolvable:freerdp_set_last_error_ex resetting error state
[16:37:47:453] [95319:95320] [INFO][com.freerdp.core] - freerdp_tcp_connect:freerdp_set_last_error_ex resetting error state
[16:37:47:523] [95319:95320] [INFO][com.freerdp.crypto] - creating directory /home/cry0l1t3/.config/freerdp
[16:37:47:523] [95319:95320] [INFO][com.freerdp.crypto] - creating directory [/home/cry0l1t3/.config/freerdp/certs]
[16:37:47:523] [95319:95320] [INFO][com.freerdp.crypto] - created directory [/home/cry0l1t3/.config/freerdp/server]
[16:37:47:599] [95319:95320] [WARN][com.freerdp.crypto] - Certificate verification failure 'self signed certificate (18)' at stack position 0
[16:37:47:599] [95319:95320] [WARN][com.freerdp.crypto] - CN = ILF-SQL-01
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - @           WARNING: CERTIFICATE NAME MISMATCH!           @
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - The hostname used for this connection (10.129.201.248:3389) 
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - does not match the name given in the certificate:
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - Common Name (CN):
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] -      ILF-SQL-01
[16:37:47:600] [95319:95320] [ERROR][com.freerdp.crypto] - A valid certificate for the wrong name should NOT be trusted!
Certificate details for 10.129.201.248:3389 (RDP-Server):
        Common Name: ILF-SQL-01
        Subject:     CN = ILF-SQL-01
        Issuer:      CN = ILF-SQL-01
        Thumbprint:  b7:5f:00:ca:91:00:0a:29:0c:b5:14:21:f3:b0:ca:9e:af:8c:62:d6:dc:f9:50:ec:ac:06:38:1f:c5:d6:a9:39
The above X.509 certificate could not be verified, possibly because you do not have
the CA certificate in your certificate store, or the certificate has expired.
Please look at the OpenSSL documentation on how to add a private CA to the store.


Do you trust the above certificate? (Y/T/N) y

[16:37:48:801] [95319:95320] [INFO][com.winpr.sspi.NTLM] - VERSION ={
[16:37:48:801] [95319:95320] [INFO][com.winpr.sspi.NTLM] -      ProductMajorVersion: 6
[16:37:48:801] [95319:95320] [INFO][com.winpr.sspi.NTLM] -      ProductMinorVersion: 1
[16:37:48:801] [95319:95320] [INFO][com.winpr.sspi.NTLM] -      ProductBuild: 7601
[16:37:48:801] [95319:95320] [INFO][com.winpr.sspi.NTLM] -      Reserved: 0x000000
```

### WinRM

#### Nmap WinRM

	nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n

```text
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-06 16:31 CET
Nmap scan report for 10.129.201.248
Host is up (0.030s latency).

PORT     STATE SERVICE VERSION
5985/tcp open  http    Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.34 seconds
```

	evil-winrm -i 10.129.201.248 -u Cry0l1t3 -p P455w0rD!

```text
Evil-WinRM shell v3.3

Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine

Data: For more information, check Evil-WinRM Github: https://github.com/Hackplayers/evil-winrm#Remote-path-completion

Info: Establishing connection to remote endpoint

*Evil-WinRM* PS C:\Users\Cry0l1t3\Documents>
```

### WMI

#### Footprint WMI

	impacket-wmiexec Cry0l1t3:"P455w0rD!"@10.129.201.248 "hostname"

```text
Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] SMBv3.0 dialect used
ILF-SQL-01
```

# Resources

### Native Powershell WinRM

https://docs.microsoft.com/en-us/powershell/module/microsoft.wsman.management/test-wsman?view=powershell-7.2