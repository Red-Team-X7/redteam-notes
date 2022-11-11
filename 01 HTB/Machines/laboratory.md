📦 HTB | laboratory
----
Tags: #📦
Related to: 
See also: [[nmap]], [[xclip]]
Previous: [[01 HTB/HTB]]

- [ ] official walkthrough
- [ ] ippsec

Run nmap script and version scan:

	sudo nmap -sC -sV -oA nmap/laboratory 10.129.162.52 -v

```bash
# Nmap 7.92 scan initiated Sat Jan 15 02:55:34 2022 as: nmap -sC -sV -oA nmap/laboratory 10.129.162.52
Nmap scan report for 10.129.162.52
Host is up (0.13s latency).
Not shown: 997 filtered tcp ports (no-response)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 25:ba:64:8f:79:9d:5d:95:97:2c:1b:b2:5e:9b:55:0d (RSA)
|   256 28:00:89:05:55:f9:a2:ea:3c:7d:70:ea:4d:ea:60:0f (ECDSA)
|_  256 77:20:ff:e9:46:c0:68:92:1a:0b:21:29:d1:53:aa:87 (ED25519)
80/tcp  open  http     Apache httpd 2.4.41
|_http-title: Did not follow redirect to https://laboratory.htb/
|_http-server-header: Apache/2.4.41 (Ubuntu)
443/tcp open  ssl/http Apache httpd 2.4.41 ((Ubuntu))
|_http-title: The Laboratory
| ssl-cert: Subject: commonName=laboratory.htb
| Subject Alternative Name: DNS:git.laboratory.htb
| Not valid before: 2020-07-05T10:39:28
|_Not valid after:  2024-03-03T10:39:28
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: Host: laboratory.htb; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sat Jan 15 02:56:08 2022 -- 1 IP address (1 host up) scanned in 34.53 seconds
```

Enumerate http:

	firefox 10.129.162.52	// redirects to https://laboratory.htb/

Add entry to /etc/hosts for target:

	sudo vi /etc/hosts	// 10.129.162.52 laboratory.htb

Enumerate HTTP:

	firefox 10.129.162.52	// we get the page; look for a copyright, when it was created, see if it's a wordpress site...; dexter CEO name

Look at source code:

	<Ctrl+U>	// see if it has wp/, joomla, etc. to see what it's coded in

See if it's an HTML page, PHP...

	firefox https://laboratory.htb/index.html	// we get a hit
	firefox https://laboratory.htb/index.php	// not found

From nmap scan, SSL certificate has an alternate name:

```
Subject Alternative Name: DNS:git.laboratory.htb
```

Edit /etc/hosts with git info:

	sudo vi /etc/hosts	// 10.129.162.52 laboratory.htb git.laboratory.htb

Enumerate HTTP:

	firefox https://git.laboratory.htb/	// 502 "Whoops, GitLab is taking too much time to respond."

```
IPDL protocol error: Handler returned error code!

###!!! [Parent][DispatchAsyncMessage] Error: PClientManager::Msg_ExpectFutureClientSource Processing error: message was deserialized, but the handler returned false (indicating failure)

```

References
----
<iframe width="560" height="315" src="https://www.youtube.com/embed/ozmHeApuSj8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>