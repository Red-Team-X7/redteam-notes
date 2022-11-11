# 💢 wpscan
Tags: #💢
Related to: 
See also: 
Previous: [[Web Application Analysis]], [[Web Vulnerability Scanners]], [[Hacking Wordpress]]

---
## Description

WordPress Security Scanner.

## Usage Examples

### Enumerate plugins

	wpscan --url <url> -e ap

### Enumerate users

	wpscan --url <url> -e u

### Enumerate vulnerable plugins

	wpscan --url http://10.10.110.100:65000/wordpress --enumerate vp -o wpscan.txt

### Check WordPress Vulnerability Database

### Enumerate users

	wpscan --url http://10.10.110.100:65000/wordpress --enumerate u

### Bruteforce WordPress login

	wpscan --url http://10.10.110.100:65000/wordpress --usernames names.txt --passwords cewl.out
 
# References

https://wpvulndb.com/ // wordpress vulnerability database