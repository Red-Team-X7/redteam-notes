# ⚙️ rsync

Tags: #⚙️
Related to: 
See also: 
Previous: [[Footprinting]], [[REMOTE MANAGEMENT]]

## Description

## Usage Examples

### Enumerating an Open Share

	rsync -av --list-only rsync://127.0.0.1/dev

```text
receiving incremental file list
drwxr-xr-x             48 2022/09/19 09:43:10 .
-rw-r--r--              0 2022/09/19 09:34:50 build.sh
-rw-r--r--              0 2022/09/19 09:36:02 secrets.yaml
drwx------             54 2022/09/19 09:43:10 .ssh

sent 25 bytes  received 221 bytes  492.00 bytes/sec
total size is 0  speedup is 0.00
```

### Sync Files to Attacker Machine

	rsync -av rsync://127.0.0.1/dev
	`sync -av rsync://127.0.0.1/dev -e ssh
	rsync -av rsync://127.0.0.1/dev -e ssh -p2222

# References