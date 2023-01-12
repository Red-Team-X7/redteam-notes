# ⚙️ ssh

Tags: #⚙️
Related to:
See also: [[ssh-audit]]
Previous: [[Getting Started]]


## Description

OpenSSH remote login client

## Usage Examples

### SSH Using Password

	ssh root@<vps-ip-address>

```text
root@<vps-ip-address>'s password: 

[root@VPS ~]# 
```

### Use a specified private key

	ssh -i ssh.key joanna@10.129.183.214

### Enforce password-based authentication

	ssh <user>@<FQDN/IP> -o PreferredAuthentications=password

### Escape characters

The supported escapes (assuming the default ‘~’) are:

```
~.      Disconnect.

~^Z     Background ssh.

~#      List forwarded connections.

~&      Background ssh at logout when waiting for forwarded connection / X11 sessions to terminate.

~?      Display a list of escape characters.

~B      Send a BREAK to the remote system (only useful if the peer supports it).

~C      Open command line.

~R      Request rekeying of the connection (only useful if the peer supports it).

~V      Decrease the verbosity (LogLevel) when errors are being written to stderr.

~v      Increase the verbosity (LogLevel) when errors are being written to stderr.
```

### Drop into SSH command mode and local port forward

Drop into ssh command mode and port forward our 9002 to the /var/www/internal web server port 52846:

	~C
	-L 9002:127.0.0.1:52846	// local port forward

Firefox:

	http://localhost:9002/

### Upgrade to SSH shell and tunnel

Edit /etc/proxychains4.conf file to proxy requests through SOCKS port 1080:

	socks5 127.0.0.1 1080

Add your public key to the target and upgrade to SSH shell:

	ssh-keygen -b 4096								// create key in ~/.ssh/
	cat ~/.ssh/id_rsa.pub							// add this to target /root/.ssh/authorized_keys
																								// and if you created authorized_keys, ensure that the
																								// permissions are root:root and chmod 700.
	ssh -i ~/.ssh/id_rsa -D 1080 root@10.10.110.100	// root@DANTE-WEB-NIX01

nmap through proxychains:

```
Note: nmap SYN scan is not proxy aware and there is limited support for the Nmap --proxies option. Instead, we can use a TCP Connect Scan (-sT), which uses the OS to issue a higher-level connect system call that routes the traffic through the proxy.
```

	proxychains nmap 172.16.1.10 -sT -sV -Pn -T5

```
Nmap scan report for 172.16.1.10
Host is up, received user-set (0.11s latency).
Scanned at 2021-12-25 16:43:34 EST for 115s
Not shown: 996 closed tcp ports (conn-refused)
PORT    STATE SERVICE     REASON  VERSION
22/tcp  open  ssh         syn-ack OpenSSH 8.2p1 Ubuntu 4 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http        syn-ack Apache httpd 2.4.41 ((Ubuntu))
139/tcp open  netbios-ssn syn-ack Samba smbd 4.6.2
445/tcp open  netbios-ssn syn-ack Samba smbd 4.6.2
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

	proxychains firefox http://172.16.1.10

	proxychains ssh margaret@172.16.1.10
	

### Generate SSH keys

	ssh-keygen -t rsa -b 4096 -f vps-ssh

```text
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): ******************
Enter same passphrase again: ******************
Your identification has been saved in vps-ssh
Your public key has been saved in vps-ssh.pub
The key fingerprint is:
SHA256:zXyVAWK00000000000000000000VS4a/f0000+ag cry0l1t3@parrot
The key's randomart image is:
...SNIP...
```

With the command shown above, we generate two different keys. The `vps-ssh` is the `private key` and must not be shared anywhere or with anyone. The second `vps-ssh.pub` is the `public key` which we can now insert in the Vultr control panel.

### Add public SSH key to VPS

	mkdir ~/.ssh
	echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
	chmod 600 ~/.ssh/authorized_keys

Once we have added this to the `authorized_keys` file, we can use the `private key` to log in to the system via SSH.

### Use SSH Keys

	ssh cry0l1t3@<vps-ip-address> -i vps-ssh-cry0l1t3

```text
[cry0l1t3@VPS ~]$
```

# References