# ⚙️ sort

Tags: #⚙️ 
Related to: 
See also: 
Previous: 

## Description

Sort lines of text files.

## Usage Examples

### Filtering programs

| **Command** | **Description** |
| --------------|---------------|
| `head` | Prints the first ten lines of STDOUT or a file. |
| `tail` | Prints the last ten lines of STDOUT or a file. |
| `sort` | Sorts the contents of STDOUT or a file. |
| `grep` | Searches for specific results that contain given patterns. |
| `cut` | Removes sections from each line of files. |
| `tr` | Replaces certain characters. |
| `column` | Command-line based utility that formats its input into multiple columns. |
| `awk` | Pattern scanning and processing language. |
| `sed` | A stream editor for filtering and transforming text. |

### Sort Obsidian Module & Tag List

#### Sort Tag List

	echo [[PasswdAttacks]], [[Web Application Analysis]], [[Attacking Web Applications with Ffuf]], [[Information Gathering - Web Edition]] | tr ',' '\n' | sort | tr '\n' ','

```text
[[Attacking Web Applications with Ffuf]],[[Information Gathering - Web Edition]],[[PasswdAttacks]],[[Web Application Analysis]]
```

#### Sort Module List

>`sort << EOF`
>Module List
>`EOF`

```text
[[Active Directory BloodHound]]
[[Active Directory Enumeration & Attacks]]
[[Active Directory LDAP]]
[[Active Directory PowerView]]
[[Attacking Common Applications]]
[[Attacking Common Services]]
[[Attacking Enterprise Networks]]
[[Attacking Web Applications with Ffuf]]
[[Broken Authentication]]
[[Bug Bounty Hunting Process]]
[[Command Injections]]
[[Cracking Passwords with Hashcat]]
[[Cross-Site Scripting (XSS)]]
[[DNS Enumeration Using Python]]
[[Documentation & Reporting]]
[[File Inclusion]]
[[File Transfers]]
[[File Upload Attacks]]
[[Footprinting]]
[[Getting Started]]
[[Hacking Wordpress]]
[[Information Gathering - Web Edition]]
[[Introduction to Active Directory]]
[[Introduction to Bash Scripting]]
[[Introduction to Networking]]
[[Introduction to Python 3]]
[[Introduction to Web Applications]]
[[Intro to Academy]]
[[Intro to Assembly Language]]
[[Intro to Network Traffic Analysis]]
[[JavaScript Deobfuscation]]
[[Learning Process]]
[[Linux Fundamentals]]
[[Linux Privilege Escalation]]
[[Login Brute Forcing]]
[[Network Enumeration with Nmap]]
[[OSINT - Corporate Recon]]
[[Password Attacks]]
[[Penetration Testing Process]]
[[Pivoting, Tunneling & Port Forwarding]]
[[Secure Coding 101 - JavaScript]]
[[Server-side Attacks]]
[[Session Security]]
[[Setting Up]]
[[Shells & Payloads]]
[[SQL Injection Fundamentals]]
[[SQLMap Essentials]]
[[Stack-Based Buffer Overflows on Linux x86]]
[[Stack-Based Buffer Overflows on Windows x86]]
[[Using the Metasploit-Framework]]
[[Using Web Proxies]]
[[01 HTB/Academy/03. Vulnerability Assessment/14. Vulnerability Assessment/Vulnerability Assessment]]
[[Web Attacks]]
[[Web Requests]]
[[Web Service & API Attacks]]
[[Whitebox Pentesting 101]]
[[Windows Fundamentals]]
[[Windows Privilege Escalation]]
```


### Cause UID 0 accounts to “bubble up” to the top

	sort -t: -k3 -n /etc/passwd

### Filter for unique lines

	cat file | sort -u

### Sort numerically

	unzip -l Python\ 3\ Deep\ Dive\ \(Part\ 2\).zip | cut -d \/ -f2,3 | sort -g

### Sort ports by order of use frequency

	sort -r -k3 /usr/share/nmap/nmap-services

# References