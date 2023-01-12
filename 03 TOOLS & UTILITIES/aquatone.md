# 💢 aquatone

Tags: #💢
Related to: 
See also: [[hunchly]]
Previous: [[Web Application Analysis]], [[Information Gathering - Web Edition]]

## Description

Aquatone is a tool for visual inspection of websites across a large amount of hosts and is convenient for quickly gaining an overview of HTTP-based attack surface.

## Usage Examples

### Install

Didn't work for me:

	sudo apt install golang chromium-driver
	go get github.com/michenriksen/aquatone
	export PATH="$PATH":"$HOME/go/bin"

Worked for me:

	sudo apt install chromium-l10n
	wget https://github.com/michenriksen/aquatone/releases/download/v1.7.0/aquatone_linux_amd64_1.7.0.zip
	unzip aquatone_linux_amd64_1.7.0.zip
	mv aquatone ~/go/bin

#### Add to Path

##### Print the current PATH variable

	printenv | grep PATH

```text
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games
```

##### Add temporarily

Add `/home/<user>/.local/bin`

```text
export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games:/home/<user>/.local/bin"
```

##### Add permanently

Append the path to the end of the config file:

	vim ~/.zshrc

```text
export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/games:/usr/games:/home/<user>/.local/bin"
```

### Aquatone Options

	aquatone --help

```text
Usage of aquatone:
  -chrome-path string
    	Full path to the Chrome/Chromium executable to use. By default, aquatone will search for Chrome or Chromium
  -debug
    	Print debugging information
  -http-timeout int
    	Timeout in miliseconds for HTTP requests (default 3000)
  -nmap
    	Parse input as Nmap/Masscan XML
  -out string
    	Directory to write files to (default ".")
  -ports string
    	Ports to scan on hosts. Supported list aliases: small, medium, large, xlarge (default "80,443,8000,8080,8443")
  -proxy string
    	Proxy to use for HTTP requests
  -resolution string
    	screenshot resolution (default "1440,900")
  -save-body
    	Save response bodies to files (default true)
  -scan-timeout int
    	Timeout in miliseconds for port scans (default 100)
  -screenshot-timeout int
    	Timeout in miliseconds for screenshots (default 30000)
  -session string
    	Load Aquatone session file and generate HTML report
  -silent
    	Suppress all output except for errors
  -template-path string
    	Path to HTML template to use for report
  -threads int
    	Number of concurrent threads (default number of logical CPUs)
  -version
    	Print current Aquatone version
```

### Take Screenshots of Domains in List

	cat facebook_aquatone.txt | aquatone -screenshot-timeout 1000

```text
aquatone v1.7.0 started at 2021-10-06T10:14:42+01:00

Targets    : 30
Threads    : 2
Ports      : 80, 443, 8000, 8080, 8443
Output dir : aquatone

edge-star-shv-01-cdg2.facebook.com: port 80 open
edge-extern-shv-01-waw1.facebook.com: port 80 open
whatsapp-chatd-edge-shv-01-ams4.facebook.com: port 80 open
edge-secure-shv-01-ham3.facebook.com: port 80 open
sv-se.facebook.com: port 80 open
ko.facebook.com: port 80 open
whatsapp-chatd-msgr-mini-edge-shv-01-lis1.facebook.com: port 80 open
synthetic-e2e-elbprod-sli-shv-01-otp1.facebook.com: port 80 open
edge-star-shv-01-cdg2.facebook.com: port 443 open
edge-extern-shv-01-waw1.facebook.com: port 443 open
whatsapp-chatd-edge-shv-01-ams4.facebook.com: port 443 open
http://edge-star-shv-01-cdg2.facebook.com/: 200 OK
http://edge-extern-shv-01-waw1.facebook.com/: 200 OK
edge-secure-shv-01-ham3.facebook.com: port 443 open
ondemand-edge-shv-01-cph2.facebook.com: port 443 open
sv-se.facebook.com: port 443 open
http://edge-secure-shv-01-ham3.facebook.com/: 200 OK
ko.facebook.com: port 443 open
whatsapp-chatd-msgr-mini-edge-shv-01-lis1.facebook.com: port 443 open
http://sv-se.facebook.com/: 200 OK
http://ko.facebook.com/: 200 OK
synthetic-e2e-elbprod-sli-shv-01-otp1.facebook.com: port 443 open
http://synthetic-e2e-elbprod-sli-shv-01-otp1.facebook.com/: 400 default_vip_400
https://edge-star-shv-01-cdg2.facebook.com/: 200 OK
https://edge-extern-shv-01-waw1.facebook.com/: 200 OK
http://edge-star-shv-01-cdg2.facebook.com/: screenshot timed out
http://edge-extern-shv-01-waw1.facebook.com/: screenshot timed out
https://edge-secure-shv-01-ham3.facebook.com/: 200 OK
https://sv-se.facebook.com/: 200 OK
https://ko.facebook.com/: 200 OK
http://edge-secure-shv-01-ham3.facebook.com/: screenshot timed out
http://sv-se.facebook.com/: screenshot timed out
http://ko.facebook.com/: screenshot timed out
https://synthetic-e2e-elbprod-sli-shv-01-otp1.facebook.com/: 400 default_vip_400
http://synthetic-e2e-elbprod-sli-shv-01-otp1.facebook.com/: screenshot successful
https://edge-star-shv-01-cdg2.facebook.com/: screenshot timed out
https://edge-extern-shv-01-waw1.facebook.com/: screenshot timed out
https://edge-secure-shv-01-ham3.facebook.com/: screenshot timed out
https://sv-se.facebook.com/: screenshot timed out
https://ko.facebook.com/: screenshot timed out
https://synthetic-e2e-elbprod-sli-shv-01-otp1.facebook.com/: screenshot successful
Calculating page structures... done
Clustering similar pages... done
Generating HTML report... done

Writing session file...Time:
 - Started at  : 2021-10-06T10:14:42+01:00
 - Finished at : 2021-10-06T10:15:01+01:00
 - Duration    : 19s

Requests:
 - Successful : 12
 - Failed     : 5

 - 2xx : 10
 - 3xx : 0
 - 4xx : 2
 - 5xx : 0

Screenshots:
 - Successful : 2
 - Failed     : 10

Wrote HTML report to: aquatone/aquatone_report.html
```

### View Report

	firefox aquatone_report.html

# References

https://github.com/michenriksen/aquatone