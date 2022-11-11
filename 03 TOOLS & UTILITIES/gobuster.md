# 💢 gobuster

Tags: #💢
Related to:
See also:
Previous: [[Web Crawlers & Directory Bruteforce]], [[Getting Started]]

## Description

Gobuster is a tool used to brute-force:

-   URIs (directories and files) in web sites.
-   DNS subdomains (with wildcard support).

Because I wanted:

1.  something that didn’t have a fat Java GUI (console FTW).
2.  to build something that just worked on the command line.
3.  something that did not do recursive brute force.
4.  something that allowed me to brute force folders and multiple extensions at once.
5.  something that compiled to native on multiple platforms.
6.  something that was faster than an interpreted script (such as Python).
7.  something that didn’t require a runtime.
8.  use something that was good with concurrency (hence Go).
9.  to build something in Go that wasn’t totally useless.

## Usage Examples

```shell-session
Usage:
  gobuster [command]

Available Commands:
  dir         Uses directory/file enumeration mode
  dns         Uses DNS subdomain enumeration mode
  fuzz        Uses fuzzing mode
  help        Help about any command
  s3          Uses aws bucket enumeration mode
  version     shows the current version
  vhost       Uses VHOST enumeration mode
```

	gobuster dir -u 10.129.1.145 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster-root.out
	
### Enumerate files and directories through proxychains

	gobuster dir --proxy socks5://127.0.0.1:1080 --url http://172.16.1.13/ -w /usr/share/wordlists/dirb/common.txt

```shell-session
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

### Enumerate files and directories

	gobuster dir -u http://10.10.10.121/ -w /usr/share/dirb/wordlists/common.txt

```shell-session
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            http://10.10.10.121/
[+] Threads:        10
[+] Wordlist:       /usr/share/dirb/wordlists/common.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/12/11 21:47:25 Starting gobuster
===============================================================
/.hta (Status: 403)
/.htpasswd (Status: 403)     // forbidden
/.htaccess (Status: 403)
/index.php (Status: 200)     // resource request successful
/server-status (Status: 403)
/wordpress (Status: 301)     // redirected, not a failure
===============================================================
2020/12/11 21:47:46 Finished
===============================================================
```

### Enumerate files extensions

```shell-session
-x, --extensions	// File extension(s) to search for (will take too long
					// if you don't know what extensions are on the server)
```

### Enumerate DNS

	gobuster dns -d inlanefreight.com -w /usr/share/SecLists/Discovery/DNS/namelist.txt

```shell-session
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Domain:     inlanefreight.com
[+] Threads:    10
[+] Timeout:    1s
[+] Wordlist:   /usr/share/SecLists/Discovery/DNS/namelist.txt
===============================================================
2020/12/17 23:08:55 Starting gobuster
===============================================================
Found: blog.inlanefreight.com
Found: customer.inlanefreight.com
Found: my.inlanefreight.com
Found: ns1.inlanefreight.com
Found: ns2.inlanefreight.com
Found: ns3.inlanefreight.com
===============================================================
2020/12/17 23:10:34 Finished
===============================================================
```

# References
https://github.com/OJ/gobuster