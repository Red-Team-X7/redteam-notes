# 🔥 SMTP

Tags: #🔥
Related to: [[telnet]], [[nmap]], [[smtp-user-enum]]
See also:
Previous: [[TACTICS]], [[Footprinting]]

## Description

## Cheatsheet

| **Command** | **Description** |
| --- | --- |
| `telnet <FQDN/IP> 25` |

#### Dangerous Settings

```text
mynetworks = 0.0.0.0/0
```

## Usage Examples

### Default Configuration

	cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"

```text
smtpd_banner = ESMTP Server 
biff = no
append_dot_mydomain = no
readme_directory = no
compatibility_level = 2
smtp_tls_session_cache_database = btree:${data_directory}/smtp_scache
myhostname = mail1.inlanefreight.htb
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
smtp_generic_maps = hash:/etc/postfix/generic
mydestination = $myhostname, localhost 
masquerade_domains = $myhostname
mynetworks = 127.0.0.0/8 10.129.0.0/16
mailbox_size_limit = 0
recipient_delimiter = +
smtp_bind_address = 0.0.0.0
inet_protocols = ipv4
smtpd_helo_restrictions = reject_invalid_hostname
home_mailbox = /home/postfix
```

### Telnet - Connect

	telnet 10.129.14.128 25

```text
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 
```

	HELO mail1.inlanefreight.htb

```text
250 mail1.inlanefreight.htb
```

	EHLO mail1

```text
250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING
```


### Telnet - Enumerate Users

>The command `VRFY` can be used to enumerate existing users on the system. However, this does not always work. Depending on how the SMTP server is configured, the SMTP server may issue `code 252` and confirm the existence of a user that does not exist on the system. A list of all SMTP response codes can be found [here](https://serversmtp.com/smtp-error/).

	telnet 10.129.14.128 25

```text
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server 
```

	VRFY root

```text
252 2.0.0 root
```

	VRFY cry0l1t3

```text
252 2.0.0 cry0l1t3
```

	VRFY testuser

```text
252 2.0.0 testuser
```

	VRFY aaaaaaaaaaaaaaaaaaaaaaaaaaaa

```text
252 2.0.0 aaaaaaaaaaaaaaaaaaaaaaaaaaaa
```

	smtp-user-enum -M VRFY -U footprinting-wordlist.txt -t 10.129.178.49 -m101 -w25

```text
 ----------------------------------------------------------
|                   Scan Information                       |
 ----------------------------------------------------------

Mode ..................... VRFY
Worker Processes ......... 101
Usernames file ........... Documents/Wordlists/footprinting-wordlist.txt
Target count ............. 1
Username count ........... 101
Target TCP port .......... 25
Query timeout ............ 25 secs
Target domain ............ 

######## Scan started at Mon Jan  2 13:38:05 2023 #########
10.129.178.49: robin exists
######## Scan completed at Mon Jan  2 13:38:22 2023 #########
1 results.

101 queries in 17 seconds (5.9 queries / sec)
```

### Telnet - Send an Email

	telnet 10.129.14.128 25

```text
Trying 10.129.14.128...
Connected to 10.129.14.128.
Escape character is '^]'.
220 ESMTP Server
```

	EHLO inlanefreight.htb

```text
250-mail1.inlanefreight.htb
250-PIPELINING
250-SIZE 10240000
250-ETRN
250-ENHANCEDSTATUSCODES
250-8BITMIME
250-DSN
250-SMTPUTF8
250 CHUNKING
```

	MAIL FROM: <cry0l1t3@inlanefreight.htb>

```text
250 2.1.0 Ok
```

	RCPT TO: <mrb3n@inlanefreight.htb> NOTIFY=success,failure

```text
250 2.1.5 Ok
```

	DATA

```text
354 End data with <CR><LF>.<CR><LF>
```

```text
From: <cry0l1t3@inlanefreight.htb>
To: <mrb3n@inlanefreight.htb>
Subject: DB
Date: Tue, 28 Sept 2021 16:32:51 +0200
Hey man, I am trying to access our XY-DB but the creds don't work. 
Did you make any changes there?
.
```

```text
250 2.0.0 Ok: queued as 6E1CF1681AB
```

	QUIT

```text
221 2.0.0 Bye
Connection closed by foreign host.
```

### Open Relay Configuration

>Note: With this setting, this SMTP server can send fake emails and thus initialize communication between multiple parties. Another attack possibility would be to spoof the email and read it.

	cat /etc/postfix/main.cf

```text
mynetworks = 0.0.0.0/0
```

### Nmap - Open Relay

	sudo nmap 10.129.14.128 -p25 --script smtp-open-relay -v

```text
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-30 02:29 CEST
NSE: Loaded 1 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 02:29
Completed NSE at 02:29, 0.00s elapsed
Initiating ARP Ping Scan at 02:29
Scanning 10.129.14.128 [1 port]
Completed ARP Ping Scan at 02:29, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 02:29
Completed Parallel DNS resolution of 1 host. at 02:29, 0.03s elapsed
Initiating SYN Stealth Scan at 02:29
Scanning 10.129.14.128 [1 port]
Discovered open port 25/tcp on 10.129.14.128
Completed SYN Stealth Scan at 02:29, 0.06s elapsed (1 total ports)
NSE: Script scanning 10.129.14.128.
Initiating NSE at 02:29
Completed NSE at 02:29, 0.07s elapsed
Nmap scan report for 10.129.14.128
Host is up (0.00020s latency).

PORT   STATE SERVICE
25/tcp open  smtp
| smtp-open-relay: Server is an open relay (16/16 tests)
|  MAIL FROM:<> -> RCPT TO:<relaytest@nmap.scanme.org>
|  MAIL FROM:<antispam@nmap.scanme.org> -> RCPT TO:<relaytest@nmap.scanme.org>
|  MAIL FROM:<antispam@ESMTP> -> RCPT TO:<relaytest@nmap.scanme.org>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<relaytest@nmap.scanme.org>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<relaytest%nmap.scanme.org@[10.129.14.128]>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<relaytest%nmap.scanme.org@ESMTP>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<"relaytest@nmap.scanme.org">
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<"relaytest%nmap.scanme.org">
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<relaytest@nmap.scanme.org@[10.129.14.128]>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<"relaytest@nmap.scanme.org"@[10.129.14.128]>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<relaytest@nmap.scanme.org@ESMTP>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<@[10.129.14.128]:relaytest@nmap.scanme.org>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<@ESMTP:relaytest@nmap.scanme.org>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<nmap.scanme.org!relaytest>
|  MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<nmap.scanme.org!relaytest@[10.129.14.128]>
|_ MAIL FROM:<antispam@[10.129.14.128]> -> RCPT TO:<nmap.scanme.org!relaytest@ESMTP>
MAC Address: 00:00:00:00:00:00 (VMware)

NSE: Script Post-scanning.
Initiating NSE at 02:29
Completed NSE at 02:29, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.48 seconds
           Raw packets sent: 2 (72B) | Rcvd: 2 (72B)
```

# Resources

https://serversmtp.com/smtp-error/