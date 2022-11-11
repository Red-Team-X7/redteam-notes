# 💢 joomscan
Tags: #💢
Related to: [[Web Vulnerability Scanners]]
See also: 
Previous: [[ ]]

---
## Description

OWASP JoomScan is an open source project in the perl programming language to detect Joomla CMS vulnerabilities and analyze them.

## Usage Examples

### No man page; check help

joomscan -h
```
    ____  _____  _____  __  __  ___   ___    __    _  _ 
   (_  _)(  _  )(  _  )(  \/  )/ __) / __)  /__\  ( \( )
  .-_)(   )(_)(  )(_)(  )    ( \__ \( (__  /(__)\  )  ( 
  \____) (_____)(_____)(_/\/\_)(___/ \___)(__)(__)(_)\_)
                        (1337.today)
   
    --=[OWASP JoomScan
    +---++---==[Version : 0.0.7
    +---++---==[Update Date : [2018/09/23]
    +---++---==[Authors : Mohammad Reza Espargham , Ali Razmjoo
    --=[Code name : Self Challenge
    @OWASP_JoomScan , @rezesp , @Ali_Razmjo0 , @OWASP

   

Help :

Usage:  joomscan [options]

--url | -u <URL>                |   The Joomla URL/domain to scan.
--enumerate-components | -ec    |   Try to enumerate components.

--cookie <String>               |   Set cookie.
--user-agent | -a <User-Agent>  |   Use the specified User-Agent.
--random-agent | -r             |   Use a random User-Agent.
--timeout <Time-Out>            |   Set timeout.
--proxy=PROXY                   |   Use a proxy to connect to the target URL
           Proxy example: --proxy http://127.0.0.1:8080
                                  https://127.0.0.1:443
                                  socks://127.0.0.1:414
                                  
--about                         |   About Author
--help | -h                     |   This help screen.
--version                       |   Output the current version and exit.
```

### Run scan, piped to tee because there's no output file option

	joomscan -ec -url 10.129.171.59 | tee joomscan.out

---
## References
- https://tools.kali.org/web-applications/joomscan