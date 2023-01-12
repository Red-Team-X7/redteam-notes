# 💢 ffuf cewl

Tags: #💢 
Related to:
See also: 
Previous: [[Attacking Web Applications with Ffuf]], [[Information Gathering - Web Edition]],[[PasswdAttacks]], [[Web Application Analysis]]

## Description

```text
ffuf - Fast web fuzzer written in Go.
cewl - Custom word list generator.
```

## Usage Examples

```text
MATCHER OPTIONS:
  -mc                 Match HTTP status codes, or "all" for everything. (default: 200,204,301,302,307,401,403,405)
  -ml                 Match amount of lines in response
  -mr                 Match regexp
  -ms                 Match HTTP response size
  -mw                 Match amount of words in response

FILTER OPTIONS:
  -fc                 Filter HTTP status codes from response. Comma separated list of codes and ranges
  -fl                 Filter by amount of lines in response. Comma separated list of line counts and ranges
  -fr                 Filter regexp
  -fs                 Filter HTTP response size. Comma separated list of sizes and ranges
  -fw                 Filter by amount of words in response. Comma separated list of word counts and ranges
```

### vHost Fuzzing

| **Flag** | **Description** |
|-|-|
| `-w` | Path to our wordlist
| `-u` | URL we want to fuzz
| `-H "HOST: FUZZ.randomtarget.com"` | This is the `HOST` Header, and the word `FUZZ` will be used as the fuzzing point.
| `-fs 612` | Filter responses with a size of 612, default response size in this case.

	ffuf -w ./vhosts -u http://192.168.10.10 -H "HOST: FUZZ.randomtarget.com" -fs 612

```text
        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://192.168.10.10
 :: Wordlist         : FUZZ: ./vhosts
 :: Header           : Host: FUZZ.randomtarget.com
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response size: 612
________________________________________________

dev-admin               [Status: 200, Size: 120, Words: 7, Lines: 12]
www                     [Status: 200, Size: 185, Words: 41, Lines: 9]
some                    [Status: 200, Size: 195, Words: 41, Lines: 9]
:: Progress: [12/12] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
```

### Enumerate Files and Folders

| **Flag** | **Description** |
|-|-|
| `-recursion` | Activates the recursive scan |
| `-recursion-depth` | Specifies the maximum depth to scan |
| `-u` | Our target URL, and `FUZZ` will be the injection point |
| `-w` | Path to our wordlist |
| `-mc` | match HTTP status codes, or "all" for everything. (default: 200,204,301,302,307,401,403) |
| `-o` | write output to file |

	ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt

```text
        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://192.168.10.10/FUZZ
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

wp-admin                [Status: 301, Size: 317, Words: 20, Lines: 10]
[INFO] Adding a new job to the queue: http://192.168.10.10/wp-admin/FUZZ

wp-includes             [Status: 301, Size: 320, Words: 20, Lines: 10]
[INFO] Adding a new job to the queue: http://192.168.10.10/wp-includes/FUZZ

wp-content              [Status: 301, Size: 319, Words: 20, Lines: 10]
[INFO] Adding a new job to the queue: http://192.168.10.10/wp-content/FUZZ

admin                   [Status: 302, Size: 0, Words: 1, Lines: 1]
login                   [Status: 302, Size: 0, Words: 1, Lines: 1]
feed                    [Status: 301, Size: 0, Words: 1, Lines: 1]
[INFO] Adding a new job to the queue: http://192.168.10.10/feed/FUZZ
```

### Sensitive Information Disclosure

#### Select Target Extension List

	ls -1 /usr/share/seclists/Discovery/Web-Content/raft-*extensions*

```text
/usr/share/seclists/Discovery/Web-Content/raft-large-extensions-lowercase.txt
/usr/share/seclists/Discovery/Web-Content/raft-large-extensions.txt
/usr/share/seclists/Discovery/Web-Content/raft-medium-extensions-lowercase.txt
/usr/share/seclists/Discovery/Web-Content/raft-medium-extensions.txt
/usr/share/seclists/Discovery/Web-Content/raft-small-extensions-lowercase.txt
/usr/share/seclists/Discovery/Web-Content/raft-small-extensions.txt
```

#### Create Target Folders List

	cat folders.txt

```text
wp-admin
wp-content
wp-includes
```

#### Create Target Words List

	cewl -m5 --lowercase -w wordlist.txt http://192.168.10.10

#### Combine Folder/Word/Extention Lists and Fuzz

| **Flags** | **Description** |
|-|-|
| `-w` | We separate the wordlists by coma and add an alias to them to inject them as fuzzing points later |
| `-u` | Our target URL with the fuzzing points |

	ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://192.168.10.10/FOLDERS/WORDLISTEXTENSIONS

```text
        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://192.168.10.10/FOLDERS/WORDLISTEXTENSIONS
 :: Wordlist         : FOLDERS: ./folders.txt
 :: Wordlist         : WORDLIST: ./wordlist.txt
 :: Wordlist         : EXTENSIONS: ./extensions.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
________________________________________________

[Status: 200, Size: 8, Words: 1, Lines: 2]
    * EXTENSIONS: ~
    * FOLDERS: wp-content
    * WORDLIST: secret

[Status: 200, Size: 0, Words: 1, Lines: 1]
    * FOLDERS: wp-includes
    * WORDLIST: comment
    * EXTENSIONS: .php

[Status: 302, Size: 0, Words: 1, Lines: 1]
    * FOLDERS: wp-admin
    * WORDLIST: comment
    * EXTENSIONS: .php
...
```

	curl http://192.168.10.10/wp-content/secret~

```text
Oooops!
```

# References
https://github.com/ffuf/ffuf
https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html

