# ⚙️ head | tail | sort | grep | cut | tr | column | awk | sed | xargs

Tags: #⚙️ 
Related to: [[awk]], [[sed]], [[tr]], [[head]], [[tail]], [[cut]], [[column]], [[xargs]]
See also: 
Previous:


## Description

Print lines that match patterns.

## Usage Examples

### Cheat Sheet

#### Filtering programs

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

#### Pattern matching

|**Regular Expression**|**Matches**|
|:----|:----|
|**Character classes**| |
|`.`|any character except newline|
|`\w\d\s`|word, digit, whitespace|
|`\W\D\S`|not word, digit, whitespace|
|`[abc]`|any of a, b, or c|
|`[^abc]`|not a, b, or c|
|`[a-g]`|character between a & g|
|**Anchors**| |
|`^abc$`|start / end of the string|
|`\b\B`|word, not-word boundary|
|**Escaped characters**| |
|`\.\*\\`|escaped special characters|
|`\t\n\r`|tab, linefeed, carriage return|
|**Groups & Lookaround**| |
|`(abc)`|capture group|
|`\1`|backreference to group #1|
|`(?:abc)`|non-capturing group|
|`(?=abc)`|positive lookahead|
|`(?!abc)`|negative lookahead|
|**Quantifiers & Alternation**| |
|`a*a+a?`|0 or more, 1 or more, 0 or 1|
|`a{5}a{2,}`|exactly five, two or more|
|`a{1,3}`|between one & three|
|`a+?a{2,}?`|match as few as possible|
|`ab|cd`|match ab or cd|

### Sort UID 0 accounts to “bubble up” to the top

	sort -t: -k3 -n /etc/passwd
	
### Filter unique paths of a domain

	curl https://inlanefreight.com/

```text
<!DOCTYPE html>
<html lang="en-US">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<snip>
<link rel="profile" href="http://gmpg.org/xfn/11">
<snip>
href="https://www.inlanefreight.com/index.php/feed/" />
<snip>
<a href='https://www.inlanefreight.com/index.php/offices/'>Offices</a></li>
<a href="https://www.inlanefreight.com/index.php/news/">News</a></li>
<a href='https://www.inlanefreight.com/index.php/career/'>Career</a></li>
<a href="https://www.inlanefreight.com/index.php/about-us/">About Us</a></li>
<a href='https://www.inlanefreight.com/index.php/contact/'>Contact</a></li>
<snip>
```

	curl https://www.inlanefreight.com/ | grep -Eo "https:\/\/.{0,3}\.inlanefreight\.com[^\"\']*" | sort -u

```text
https://www.inlanefreight.com/
https://www.inlanefreight.com/index.php/about-us/
https://www.inlanefreight.com/index.php/career/
https://www.inlanefreight.com/index.php/comments/feed/
https://www.inlanefreight.com/index.php/contact/
https://www.inlanefreight.com/index.php/feed/
https://www.inlanefreight.com/index.php/news/
https://www.inlanefreight.com/index.php/offices/
https://www.inlanefreight.com/index.php/wp-json/
https://www.inlanefreight.com/index.php/wp-json/oembed/1.0/embed?url=https%3A%2F%2Fwww.inlanefreight.com%2F
https://www.inlanefreight.com/index.php/wp-json/oembed/1.0/embed?url=https%3A%2F%2Fwww.inlanefreight.com%2F&#038;format=xml
https://www.inlanefreight.com/index.php/wp-json/wp/v2/pages/7
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/animate.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/bootstrap.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/bootstrap-progressbar.min.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/colors/default.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/font-awesome.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/jquery.smartmenus.bootstrap.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/magnific-popup.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/owl.carousel.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/owl.transitions.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/images/breadcrumb-back.jpg
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/bootstrap.min.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/jquery.smartmenus.bootstrap.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/jquery.smartmenus.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/navigation.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/owl.carousel.min.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/style.css?ver=5.6.8
https://www.inlanefreight.com/wp-includes/css/dist/block-library/style.min.css?ver=5.6.8
https://www.inlanefreight.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=3.3.2
https://www.inlanefreight.com/wp-includes/js/jquery/jquery.min.js?ver=3.5.1
https://www.inlanefreight.com/wp-includes/js/wp-embed.min.js?ver=5.6.8
https://www.inlanefreight.com/wp-includes/wlwmanifest.xml
https://www.inlanefreight.com/xmlrpc.php?rsd
```

### Include path/filename in result

	grep -ri zap cheatsheet/*

```text
cheatsheet/cheatsheet-110.md:# ZAP Shortcuts
cheatsheet/cheatsheet-144.md:| `ZAP` | [https://www.zaproxy.org/](https://www.zaproxy.org/) |
```

### Filter everyone with a bash shell

	cat /etc/passwd | grep bash | awk  -F: '{print $1}'

```text
root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
htb-student:x:1002:1002::/home/htb-student:/bin/bash
```

### Exclude results

	cat /etc/passwd | grep -v "false\|nologin"

```text
root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
postgres:x:111:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

### Remove delimiters and show words in a specific position

	cat /etc/passwd

```text
root:x:0:0:root:/root:/usr/bin/zsh
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
<snip>
```

	cat /etc/passwd | grep -v "false\|nologin"

```text
root:x:0:0:root:/root:/usr/bin/zsh
sync:x:4:65534:sync:/bin:/bin/sync
cntlm:x:104:65534::/var/run/cntlm:/bin/sh
arpwatch:x:119:124:ARP Watcher,,,:/var/lib/arpwatch:/bin/sh
postgres:x:132:138:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
kali:x:1000:1000:,,,:/home/kali:/usr/bin/zsh
```

	cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1

```text
root
sync
mrb3n
cry0l1t3
htb-student
```

### Filter through directories recursively

	grep -r categories /usr/share/nmap/scripts/*.nse

```text
/usr/share/nmap/scripts/acarsd-info.nse:categories = {"safe","discovery"}
/usr/share/nmap/scripts/address-info.nse:categories = {"default", "safe"}
/usr/share/nmap/scripts/afp-brute.nse:categories = {"intrusive", "brute"}
/usr/share/nmap/scripts/afp-ls.nse:categories = {"discovery", "safe"}
/usr/share/nmap/scripts/afp-path-vuln.nse:categories = {"exploit", "intrusive", "vuln"}
/usr/share/nmap/scripts/afp-serverinfo.nse:categories = {"default", "discovery", "safe"}
/usr/share/nmap/scripts/afp-showmount.nse:categories = {"discovery", "safe"}
/usr/share/nmap/scripts/ajp-auth.nse:categories = {"default", "auth", "safe"}
/usr/share/nmap/scripts/ajp-brute.nse:categories = {"intrusive", "brute"}
/usr/share/nmap/scripts/ajp-headers.nse:categories = {"discovery", "safe"}
/usr/share/nmap/scripts/ajp-methods.nse:categories = {"default", "safe"}
/usr/share/nmap/scripts/ajp-request.nse:categories = {"discovery", "safe"}
/usr/share/nmap/scripts/allseeingeye-info.nse:categories = { "discovery", "safe", "version" }
/usr/share/nmap/scripts/amqp-info.nse:categories = {"default", "discovery", "safe", "version"}
/usr/share/nmap/scripts/asn-query.nse:categories = {"discovery", "external", "safe"}
/usr/share/nmap/scripts/auth-owners.nse:categories = {"default", "safe"}
/usr/share/nmap/scripts/auth-spoof.nse:categories = {"malware", "safe"}
```

### Filter through directories recursively, following symbolic links

	grep -R -i password . 2>/dev/null | cut -d ":" -f1 | uniq | sort | grep conf

```text
./apache2/sites-available/default-ssl.conf
./debconf.conf
./dovecot/conf.d/10-auth.conf
./dovecot/conf.d/10-logging.conf
./dovecot/conf.d/10-ssl.conf
./dovecot/conf.d/auth-checkpassword.conf.ext
./dovecot/conf.d/auth-static.conf.ext
./dovecot/conf.d/auth-system.conf.ext
./hdparm.conf
./mysql/mysql.conf.d/mysqld.cnf
./overlayroot.conf
./proftpd/proftpd.conf
./samba/smb.conf
./ssh/ssh_config
./ssh/sshd_config
```

### Filter recursively using perl regexp

	grep -r categories /usr/share/nmap/scripts/*.nse | grep -oP \".*?\" | sort -u	

```text
"auth"
"broadcast"
"brute"
"default"
"discovery"
"dos"
"exploit"
"external"
"fuzzer"
"intrusive"
"malware"
"safe"
"version"
"vuln"
```

### Filter mutiple strings

	whois 134.209.24.248 | grep "StateProv\|CIDR"

```text
CIDR:           134.209.0.0/16
StateProv:      NY
```

### Filter into program which doesn't accept pipe

Standard Behavior:

	prips 134.209.0.0/16

```text
134.209.0.0
134.209.0.1
134.209.0.2
134.209.0.3
134.209.0.4
134.209.0.5
134.209.0.6
134.209.0.7
134.209.0.8
134.209.0.9
134.209.0.10
```

Piped behavior:

	whois 134.209.24.248 | grep "CIDR" | awk '{print $2}' | prips tmp

```text
usage: prips [options] <start end | CIDR block>
```

Corrected `xargs` behavior:

	whois 134.209.24.248 | grep "CIDR" | awk '{print $2}' | xargs prips

```text
134.209.0.0
134.209.0.1
134.209.0.2
134.209.0.3
134.209.0.4
134.209.0.5
134.209.0.6
134.209.0.7
134.209.0.8
134.209.0.9
```

### Filter the first 10 lines of a file

	head /etc/passwd

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
```

### Filter the last 10 lines of a file

	tail /etc/passwd

```text
miredo:x:115:65534::/var/run/miredo:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:117:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
nm-openvpn:x:118:120:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
nm-openconnect:x:119:121:NetworkManager OpenConnect plugin,,,:/var/lib/NetworkManager:/usr/sbin/nologin
pulse:x:120:122:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
beef-xss:x:121:124::/var/lib/beef-xss:/usr/sbin/nologin
lightdm:x:122:125:Light Display Manager:/var/lib/lightdm:/bin/false
do-agent:x:998:998::/home/do-agent:/bin/false
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

### Filter for unique lines
	cat file | sort -u

### Sort numerically

	unzip -l Python\ 3\ Deep\ Dive\ \(Part\ 2\).zip | cut -d \/ -f2,3 | sort -g

### Sort ports by order of use frequency

	sort -r -k3 /usr/share/nmap/nmap-services

### Rot13 encode

	echo https://www.hackthebox.eu/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'

```text
uggcf://jjj.unpxgurobk.rh/
```

### Rot13 decode

	echo uggcf://jjj.unpxgurobk.rh/ | tr 'A-Za-z' 'N-ZA-Mn-za-m'

```text
https://www.hackthebox.eu/
```

### Filter results in column form

```text
root x 0 0 root /root /bin/bash
sync x 4 65534 sync /bin /bin/sync
mrb3n x 1000 1000 mrb3n /home/mrb3n /bin/bash
cry0l1t3 x 1001 1001  /home/cry0l1t3 /bin/bash
htb-student x 1002 1002  /home/htb-student /bin/bash
```

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

```text
root         x  0     0      root               /root        /bin/bash
sync         x  4     65534  sync               /bin         /bin/sync
mrb3n        x  1000  1000   mrb3n              /home/mrb3n  /bin/bash
cry0l1t3     x  1001  1001   /home/cry0l1t3     /bin/bash
htb-student  x  1002  1002   /home/htb-student  /bin/bash
```

### Filter second word in string

```text
CIDR:           134.209.0.0/16
```


	whois 134.209.24.248 | grep "CIDR" | awk '{print $2}'

```text
134.209.0.0/16
```

### Print the first and last field of the line

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

```text
root         x  0     0      root               /root        /bin/bash
sync         x  4     65534  sync               /bin         /bin/sync
mrb3n        x  1000  1000   mrb3n              /home/mrb3n  /bin/bash
cry0l1t3     x  1001  1001   /home/cry0l1t3     /bin/bash
htb-student  x  1002  1002   /home/htb-student  /bin/bash
```

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

```text
root /bin/bash
sync /bin/sync
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

### Print nse categories, outputting only lines between “” using perl regexp

	grep -r categories /usr/share/nmap/scripts/*.nse | grep default | awk -F: {print $1} print	// omit last "print" on zsh

```
/usr/share/nmap/scripts/address-info.nse:categories = 		{"default", "safe"}
/usr/share/nmap/scripts/afp-serverinfo.nse:categories =		{"default", "discovery", "safe"}
/usr/share/nmap/scripts/ajp-auth.nse:categories = 			{"default", "auth", "safe"}
/usr/share/nmap/scripts/ajp-methods.nse:categories = 		{"default", "safe"}
/usr/share/nmap/scripts/amqp-info.nse:categories = 			{"default", "discovery", "safe", "version"}
/usr/share/nmap/scripts/auth-owners.nse:categories = 		{"default", "safe"}
/usr/share/nmap/scripts/backorifice-info.nse:categories = 	{"default", "discovery", "safe"}
```

### Substitute text

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

```text
root /bin/bash
sync /bin/sync
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'

```text
root /HTB/bash
sync /HTB/sync
mrb3n /HTB/bash
cry0l1t3 /HTB/bash
htb-student /HTB/bash
```

The "`s`" flag at the beginning stands for the substitute command. Then we specify the pattern we want to replace. After the slash (`/`), we enter the pattern we want to use as a replacement in the third position. Finally, we use the "`g`" flag, which stands for replacing all matches.

### Replace sequence of repeating character with a single occurence

	whois 134.209.24.248 | grep "Netrange\|CIDR"

```text
CIDR:           134.209.0.0/16
```

	whois 134.209.24.248 | grep "Netrange\|CIDR" | tr -s [:space:]

```text
CIDR: 134.209.0.0/16
```

# References

[How to replace a string with sed in current and recursive subdirectories](https://victoria.dev/blog/how-to-replace-a-string-with-sed-in-current-and-recursive-subdirectories/)