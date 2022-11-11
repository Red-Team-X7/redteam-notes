# 😈 Information Gathering

Tags: #😈
Related to: 
See also: 
Previous: [[KALI]]

1. [[DNS Analysis]]
2. [[IDS & IPS Identification]]
3. [[Live Host Identification]]
4. [[Network & Port Scanners]]
5. [[OSINT Analysis]]
6. [[Route Analysis]]
7. [[SMB Analysis]]
8. [[SMTP Analysis]]
9. [[SNMP Analysis]]
10. [[SSL Analysis]]

[[dmitry]]
[[ike-scan]]
[[legion]]
[[maltego]]
[[netdiscover]]
[[nmap]]
[[recon-ng]]
[[spiderfoot]]

[[p0f]]

## Error codes [^1]

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

# References
[^1]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes