# ⚙️ wc

Tags: #⚙️
Related to: 
See also: 
Previous:

## Description

Print newline, word, and byte counts for each file.

## Usage Examples

### Print number of lines counted

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

```text
root /bin/bash
sync /bin/sync
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

	cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l

```text
5
```

# References