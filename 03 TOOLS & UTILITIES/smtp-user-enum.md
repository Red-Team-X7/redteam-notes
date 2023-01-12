# 💢 smtp-user-enum

Tags: #💢
Related to: 
See also: 
Previous: [[SMTP Analysis]], [[SMTP]]

## Description

Brute Force Usernames via EXPN/VRFY/RCPT TO.

## Usage Examples

### Bruteforce Usernames

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

# References

https://www.kali.org/tools/smtp-user-enum/