# 🤖 ai programs
Tags: #🤖
Related to: 
See also: 
Previous: [[bash]], [[python]]

## Description

A collection of programs made using GPT-3.

## Usage Examples

### Python

#### Sort Obsidian Tags

```python
import warnings
warnings.simplefilter(action='ignore', category=FutureWarning)  # removes FutureWarning: "Possible nested set at position 1"

while True:
    data = input("Enter data to be alphabetized or quit() to exit: ")
    if data == 'quit()':
        break  

    data = data.split(', ') # split data into a list
    data.sort()             # sort the list alphabetically

    print('\n' + ', '.join(data) + '\n')  # print each element separated by a comma
```

```text
Enter data to be alphabetized or quit() to exit: <unsorted data>
```

```text
[[awk]], [[braa]], [[crackmapexec]], [[curl]], [[cut]], [[dig]], [[dnsenum]], [[enum4linux]], [[evil-winrm]]. [[w_wmiexec]], [[grep]], [[jq]], [[mount umount]], [[msfconsole]], [[mssqlclient]], [[mysql]], [[netcat ncat nc]], [[nmap]], [[onesixtyone]], [[openssl]], [[openssl]], [[rdp-sec-check]], [[rpcclient]], [[samrdump]], [[showmount]], [[smbclient]], [[smbmap]], [[snmpwalk]], [[sort]], [[ssh-audit]], [[ssh]], [[telnet]], [[wget]], [[xfreerdp]]
```

#### Get Subdomains From SSL Certificates

```python
import requests

# Certificate Search Website
url = "https://crt.sh/?q=hackthebox.eu&output=json"

# Get json data
response = requests.get(url)
data = response.json()

# Avoid duplicate subdomains
subdomains = set()

# Get subdomains
for item in data:
    subdomains.add(item['common_name'])

# Print them
for subdomain in sorted(subdomains):
    print(subdomain)
```

```text
*.enterprise-dev.hackthebox.eu
*.hackthebox.eu
aaamidatlantic-status.polaris.synopsys.com
analytics.hackthebox.eu
api.ctf.hackthebox.eu
api.hackthebox.eu
beta-status.astronomer.io
certificates-dev.hackthebox.eu
<...snip...>
```

### Bash

#### Play Penalty Sound for Running Applications

```bash
#!/bin/bash

# List of programs to check for
programs=( "Telegram" "Firefox" "Chrome" )

# Path to the flac file to play
flac_file="/path/to/your/file.flac"

while true; do
    # Check if any of the programs are running
    for program in "${programs[@]}"; do
        if pgrep "$program" > /dev/null; then
            # If a program is running, play the flac file
            cvlc "$flac_file" --play-and-exit
        fi
    done
    # Sleep for 1 second before checking again
    sleep 1
done

```

# References

https://chat.openai.com/chat/