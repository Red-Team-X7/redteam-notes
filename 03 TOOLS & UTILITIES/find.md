# ⚙️ find

Tags: #⚙️ 
Related to: [[which]] [[locate]]
See also: 
Previous: 

## Description

Search for files in a directory hierarchy.

## Usage Examples

### Find Files and Directories

|Option|Description|
|:----|:----|
|`-type f`|Hereby, we define the type of the searched object. In this case, `'f'` stands for `'file'`.|
|`-name *.conf`|With `'-name'`, we indicate the name of the file we are looking for. The asterisk (*) stands for 'all' files with the `'.conf'` extension.|
|`-user root`|This option filters all files whose owner is the root user.|
|`-size +20k`|We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB.|
|`-newermt 2020-03-03`|With this option, we set the date. Only files newer than the specified date will be presented.|
|`-exec ls -al {} \;`|This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection.|
|`2>/dev/null`|This is a `STDERR` redirection to the `'null device'`, which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must `not` be an option of the 'find' command.|

``` shell-session
find <location> <options>
```

### Complex usage example

	find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

```shell-session
-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29  /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33  /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33  /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33  /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33  /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33  /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33  /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59  /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04  /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59  /etc/sqlmap/sqlmap.conf
```

|Option|Description|
|:----|:----|
|`-type f`|Hereby, we define the type of the searched object. In this case, 'f' stands for 'file'.|
|`-name *.conf`|With '-name', we indicate the name of the file we are looking for. The asterisk (*) stands for 'all' files with the '.conf' extension.|
|`-user root`|This option filters all files whose owner is the root user.|
|`-size +20k`|We can then filter all the located files and specify that we only want to see the files that are larger than 20 KiB.|
|`-newermt 2020-03-03`|With this option, we set the date. Only files newer than the specified date will be presented.|
|`-exec ls -al {} \;`|This option executes the specified command, using the curly brackets as placeholders for each result. The backslash escapes the next character from being interpreted by the shell because otherwise, the semicolon would terminate the command and not reach the redirection.|
|`2>/dev/null`|This is a STDERR redirection to the 'null device', which we will come back to in the next section. This redirection ensures that no errors are displayed in the terminal. This redirection must not be an option of the `find` command.|

### Send errors to STDERR

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

### Redirect STDOUT to a file

	find /etc/ -name shadow 2>/dev/null > results.txt

### Redirect STDOUT and STDERR to Separate Files

	find /etc/ -name shadow 2> stderr.txt 1> stdout.txt

### Find hidden files & directories

    sudo find /dev -name .\* -type f -print
	sudo find /dev -name .\* -type d -print

### Find IPtables rules

	cd /etc
	find . | grep iptab
	
### Find config files

	cd /opt/ona
	find . | grep config

### find ls
	find . -type f -ls
	
```
394400      4 -rw-------   1 jimmy    jimmy           7 Nov 22  2019 ./.local/share/nano/search_history
394394      4 -rw-r--r--   1 jimmy    jimmy        3771 Apr  4  2018 ./.bashrc
393946      0 -rw-r--r--   1 jimmy    jimmy           0 Nov 21  2019 ./.cache/motd.legal-displayed
394395      4 -rw-r--r--   1 jimmy    jimmy         807 Apr  4  2018 ./.profile
394396      4 -rw-r--r--   1 jimmy    jimmy         220 Apr  4  2018 ./.bash_logout
```

### Find SUID files

	find / -perm -4000 -ls 2>/dev/null

### find exec

	find . -exec /bin/bash -p \; -quit	// bash-5.0#

### Find user's files

	find / -user jimmy -ls 2>/dev/null

```
   286763      4 drwxrwx---   2 jimmy    internal     4096 Nov 23  2019 /var/www/internal
   282830      4 -rwxrwxr-x   1 jimmy    internal      339 Nov 23  2019 /var/www/internal/main.php
     2644      4 -rwxrwxr-x   1 jimmy    internal      185 Nov 23  2019 /var/www/internal/logout.php
     1387      4 -rwxrwxr-x   1 jimmy    internal     3229 Nov 22  2019 /var/www/internal/index.php
```

### Find files a user owns and invert match to filter out useless output

Look for files joanna owns: [^1]

	find . -type f
	history | grep find
	find / -user joanna -ls 2>/dev/null
	
```
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
	
```
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

### Find files between two times

	find / -newermt "2019-11-25" ! -newermt "2019-12-10" -ls 2>/dev/null

```
   403864      4 drwxr-xr-x   2 root     root         4096 Nov 28  2019 /lib/firmware/amd-ucode
   135657      4 drwxr-xr-x   2 root     root         4096 Nov 28  2019 /usr/share/initramfs-tools/hooks
   143485      4 drwxr-xr-x   2 root     root         4096 Nov 28  2019 /usr/share/doc/amd64-microcode
   393271      4 drwxr-xr-x   2 root     root         4096 Nov 28  2019 /etc/modprobe.d
    12718      4 -rw-r--r--   1 root     root           77 Nov 28  2019 /var/lib/initramfs-tools/4.15.0-70-generic
      797     28 -rw-r--r--   1 root     root        25809 Dec  5  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-updates_multiverse_i18n_Translation-en
     1245     48 -rw-r--r--   1 root     root        46084 Dec  6  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-security_restricted_i18n_Translation-en
     1315     16 -rw-r--r--   1 root     root        15328 Dec  3  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-security_multiverse_i18n_Translation-en
     1157     16 -rw-r--r--   1 root     root        16306 Dec  5  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-backports_universe_binary-amd64_Packages
      687    236 -rw-r--r--   1 root     root       241361 Dec  8  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-updates_restricted_binary-amd64_Packages
      688     68 -rw-r--r--   1 root     root        69039 Dec  5  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-updates_restricted_i18n_Translation-en
     1244    124 -rw-r--r--   1 root     root       123008 Dec  6  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-security_restricted_binary-amd64_Packages
      751   3120 -rw-r--r--   1 root     root      3190998 Dec  9  2019 /var/lib/apt/lists/archive.ubuntu.com_ubuntu_dists_bionic-updates_universe_i18n_Translation-en
    14195      4 -rw-r--r--   1 root     root          855 Nov 28  2019 /var/lib/dpkg/info/amd64-microcode.list
      482      0 -rw-r--r--   1 root     root            0 Nov 28  2019 /var/lib/dpkg/triggers/Unincorp
   393217      4 drwxr-xr-x   3 root     root         4096 Nov 28  2019 /boot
   403865  56520 -rw-r--r--   1 root     root     57873685 Nov 28  2019 /boot/initrd.img-4.15.0-70-generic
```

```
-newerXY reference

	Succeeds if timestamp X of the file being considered is newer than timestamp Y of the file reference.   The letters X and Y can be any of the following letters:

		a   The access time of the file reference
		B   The birth time of the file reference
		c   The inode status change time of reference
		m   The modification time of the file reference
		t   reference is interpreted directly as a time
```

# References
[^1]: https://medium.com/@rahulbagul330/how-to-search-multiple-words-or-string-patterns-using-grep-command-7db910aa91ca