# ⚙️ ps

Tags: #⚙️ 
Related to: 
See also: 
Previous: 

## Description

Report a snapshot of the current processes.

## Usage Examples

### See every process on the system using standard syntax

	ps -ef | grep joanna

### Check to see if a service is running

	ps -aux | grep ssh

### Determine what user the ProFTPd service is running under

	ps aux | grep proftpd

```text
proftpd   1587  0.0  0.1 126440  3576 ?        Ss   10:02   0:00 proftpd: (accepting connections)
htb-stu+  6816  0.0  0.0  13144  1040 pts/0    S+   10:57   0:00 grep --color=auto proftpd
```

	htb-student@nixfund:~$ ps aux | grep proftpd | grep -v grep

```text
proftpd   1587  0.0  0.1 126440  3576 ?        Ss   10:02   0:00 proftpd: (accepting connections)
```

	htb-student@nixfund:~$ ps aux | grep proftpd | grep -v grep | cut -d " " -f1

```text
proftpd
```



# References