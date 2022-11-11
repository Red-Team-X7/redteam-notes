# ⚙️ sort

Tags: #⚙️ 
Related to: 
See also: 
Previous: 

## Description

Sort lines of text files.

## Usage Examples

### Filtering programs

| **Command** | **Description** |
| --------------|---------------|
| `head` | Prints the first ten lines of STDOUT or a file. |
| `tail` | Prints the last ten lines of STDOUT or a file. |
| `sort` | Sorts the contents of STDOUT or a file. |
| `grep` | Searches for specific results that contain given patterns. |
| `cut` | Removes sections from each line of files. |
| `tr` | Replaces certain characters. |
| `column` | Command-line based utility that formats its input into multiple columns. |
| `awk` | Pattern scanning and processing language. |
| `sed` | A stream editor for filtering and transforming text. |

### Cause UID 0 accounts to “bubble up” to the top

	sort -t: -k3 -n /etc/passwd

### Filter for unique lines
	cat file | sort -u

### Sort numerically

	unzip -l Python\ 3\ Deep\ Dive\ \(Part\ 2\).zip | cut -d \/ -f2,3 | sort -g

### Sort ports by order of use frequency

	sort -r -k3 /usr/share/nmap/nmap-services

# References