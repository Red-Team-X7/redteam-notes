# 💢 theharvester
Tags: #💢
Related to: 
See also: 
Previous: [[OSINT Analysis]], [[Information Gathering - Web Edition]], [[OSINT - Corporate Recon]]

# Description

theHarvester is used to gather open source intelligence (OSINT) on a company or domain.

## Usage Examples

### Gather Information from Sources

	cat sources.txt

```text
anubis
bevigil
baidu
binaryedge
bing
bingapi
bufferoverun
censys
certspotter
crtsh
dnsdumpster
duckduckgo
fullhunt
github-code
hackertarget
hunter
intelx
omnisint
otx
pentesttools
projecdiscovery
qwant
rapiddns
rocketreach
securityTrails
shodan
sublist3r
threatcrowd
threatminer
urlscan
vhost
virustotal
yahoo
zoomeye
```

	export TARGET="facebook.com"
	cat sources.txt | while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}_${TARGET}";done

```text
<SNIP>
*******************************************************************
*  _   _                                            _             *
* | |_| |__   ___    /\  /\__ _ _ ____   _____  ___| |_ ___ _ __  *
* | __|  _ \ / _ \  / /_/ / _` | '__\ \ / / _ \/ __| __/ _ \ '__| *
* | |_| | | |  __/ / __  / (_| | |   \ V /  __/\__ \ ||  __/ |    *
*  \__|_| |_|\___| \/ /_/ \__,_|_|    \_/ \___||___/\__\___|_|    *
*                                                                 *
* theHarvester 4.0.0                                              *
* Coded by Christian Martorella                                   *
* Edge-Security Research                                          *
* cmartorella@edge-security.com                                   *
*                                                                 *
*******************************************************************


[*] Target: facebook.com

[*] Searching Urlscan.

[*] ASNS found: 29
--------------------
AS12578
AS13335
AS13535
AS136023
AS14061
AS14618
AS15169
AS15817

<SNIP>
```

	ll -1

```text
baidu_facebook.json
baidu_facebook.xml
bufferoverun_facebook.json
bufferoverun_facebook.xml
crtsh_facebook.json
crtsh_facebook.xml
hackertarget_facebook.json
hackertarget_facebook.xml
otx_facebook.json
otx_facebook.xml
rapiddns_facebook.json
rapiddns_facebook.xml
sources.txt
sublist3r_facebook.json
sublist3r_facebook.xml
threatcrowd_facebook.json
threatcrowd_facebook.xml
urlscan_facebook.json
urlscan_facebook.xml
virustotal_facebook.json
virustotal_facebook.xml
zoomeye_facebook.json
zoomeye_facebook.xml
```

	cat facebook.com_*.txt | sort -u > facebook.com_subdomains_passive.txt
	cat facebook.com_subdomains_passive.txt | wc -l

```text
11947
```


# References