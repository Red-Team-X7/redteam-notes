# ⚙️ lsof
Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

---
## Description

List open files.

## Usage Examples

### Show listening ports

	sudo lsof -Pni
	sudo lsof -Pni | grep 23

### List which process has a file open

	sudo lsof /var/log/clamav/freshclam.log

---
## References
- [[]]