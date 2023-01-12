# 🔥 DNS

Tags: #🔥
Related to: [[dig]], [[dnsenum]], [[ctfr]], [[nmap]], [[nslookup]], [[gobuster]], [[ffuf cewl]]
See also:
Previous: [[TACTICS]], [[Footprinting]], [[Information Gathering - Web Edition]], [[OSINT - Corporate Recon]]

## Description

## Cheatsheet

| **Command** | **Description** |
| --- | --- |
| `dig ns <domain.tld> @<nameserver>` | NS request to the specific nameserver. |
| `dig any <domain.tld> @<nameserver>` | ANY request to the specific nameserver. |
| `dig axfr <domain.tld> @<nameserver>` | AXFR request to the specific nameserver. |
| `dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>` | Subdomain brute forcing. |

| **Command** | **Description** |
|-|-|
| `nslookup $TARGET` | Identify the `A` record for the target domain. |
| `nslookup -query=A $TARGET` | Identify the `A` record for the target domain. |
| `dig $TARGET @<nameserver/IP>` | Identify the `A` record for the target domain.  |
| `dig a $TARGET @<nameserver/IP>` | Identify the `A` record for the target domain.  |
| `nslookup -query=PTR <IP>` | Identify the `PTR` record for the target IP address. |
| `dig -x <IP> @<nameserver/IP>` | Identify the `PTR` record for the target IP address.  |
| `nslookup -query=ANY $TARGET` | Identify `ANY` records for the target domain. |
| `dig any $TARGET @<nameserver/IP>` | Identify `ANY` records for the target domain. |
| `nslookup -query=TXT $TARGET` | Identify the `TXT` records for the target domain. |
| `dig txt $TARGET @<nameserver/IP>` | Identify the `TXT` records for the target domain. |
| `nslookup -query=MX $TARGET` | Identify the `MX` records for the target domain. |
| `dig mx $TARGET @<nameserver/IP>` | Identify the `MX` records for the target domain. |

#### Passive Subdomain Enumeration

| **Resource/Command** | **Description** |
|-|-|
| `VirusTotal` | [https://www.virustotal.com/gui/home/url](https://www.virustotal.com/gui/home/url) |
| `Censys` | [https://censys.io/](https://censys.io/) |
| `Crt.sh` | [https://crt.sh/](https://crt.sh/) |
| `curl -s https://sonar.omnisint.io/subdomains/{domain} \| jq -r '.[]' \| sort -u` | All subdomains for a given domain. |
| `curl -s https://sonar.omnisint.io/tlds/{domain} \| jq -r '.[]' \| sort -u` | All TLDs found for a given domain. |
| `curl -s https://sonar.omnisint.io/all/{domain} \| jq -r '.[]' \| sort -u` | All results across all TLDs for a given domain. |
| `curl -s https://sonar.omnisint.io/reverse/{ip} \| jq -r '.[]' \| sort -u` | Reverse DNS lookup on IP address. |
| `curl -s https://sonar.omnisint.io/reverse/{ip}/{mask} \| jq -r '.[]' \| sort -u` | Reverse DNS lookup of a CIDR range. |
| `curl -s "https://crt.sh/?q=${TARGET}&output=json" \| jq -r '.[] \| "\(.name_value)\n\(.common_name)"' \| sort -u` | Certificate Transparency. |
| `cat sources.txt \| while read source; do theHarvester -d "${TARGET}" -b $source -f "${source}-${TARGET}";done` | Searching for subdomains and other information on the sources provided in the source.txt list. |

#### Sources.txt

```txt
baidu
bufferoverun
crtsh
hackertarget
otx
projecdiscovery
rapiddns
sublist3r
threatcrowd
trello
urlscan
vhost
virustotal
zoomeye
```

#### Active Subdomain Enumeration

| **Resource/Command** | **Description** |
|-|-|
| `HackerTarget` | [https://hackertarget.com/zone-transfer/](https://hackertarget.com/zone-transfer/) |
| `SecLists` | [https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists) |
| `nslookup -type=any -query=AXFR $TARGET nameserver.target.domain` | Zone Transfer using Nslookup against the target domain and its nameserver. |
| `gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"` | Bruteforcing subdomains. |

#### Virtual Hosts

| **Resource/Command** | **Description** |
|-|-|
| `curl -s http://192.168.10.10 -H "Host: randomtarget.com"` | Changing the HOST HTTP header to request a specific domain. |
| `cat ./vhosts.list \| while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://<IP address> -H "HOST: ${vhost}.target.domain" \| grep "Content-Length: ";done` | Bruteforcing for possible virtual hosts on the target domain. |
| `ffuf -w ./vhosts -u http://<IP address> -H "HOST: FUZZ.target.domain" -fs 612` | Bruteforcing for possible virtual hosts on the target domain using `ffuf`. |

#### Crawling

| **Resource/Command** | **Description** |
|-|-|
| `ZAP` | [https://www.zaproxy.org/](https://www.zaproxy.org/) |
| `ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt` | Discovering files and folders that cannot be spotted by browsing the website.
| `ffuf -w ./folders.txt:FOLDERS,./wordlist.txt:WORDLIST,./extensions.txt:EXTENSIONS -u http://www.target.domain/FOLDERS/WORDLISTEXTENSIONS` | Mutated bruteforcing against the target web server. |

#### Dangerous Settings

| **Option** | **Description** |
| --- | --- |
| `allow-query` | Defines which hosts are allowed to send requests to the DNS server. |
| `allow-recursion` | Defines which hosts are allowed to send recursive requests to the DNS server. |
| `allow-transfer` | Defines which hosts are allowed to receive zone transfers from the DNS server. |
| `zone-statistics` | Collects statistical data of zones. |

## Usage Examples

### Local DNS Configuration

	cat /etc/bind/named.conf.local

```text
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";
zone "domain.com" {
    type master;
    file "/etc/bind/db.domain.com";
    allow-update { key rndc-key; };
};
```

### NS Query

	dig ns inlanefreight.htb @10.129.14.128

```text
; <<>> DiG 9.16.1-Ubuntu <<>> ns inlanefreight.htb @10.129.14.128
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45010
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: ce4d8681b32abaea0100000061475f73842c401c391690c7 (good)
;; QUESTION SECTION:
;inlanefreight.htb.             IN      NS

;; ANSWER SECTION:
inlanefreight.htb.      604800  IN      NS      ns.inlanefreight.htb.

;; ADDITIONAL SECTION:
ns.inlanefreight.htb.   604800  IN      A       10.129.34.136

;; Query time: 0 msec
;; SERVER: 10.129.14.128#53(10.129.14.128)
;; WHEN: So Sep 19 18:04:03 CEST 2021
;; MSG SIZE  rcvd: 107
```

### ANY Query

	dig any inlanefreight.htb @10.129.14.128

```text
; <<>> DiG 9.16.1-Ubuntu <<>> any inlanefreight.htb @10.129.14.128
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7649
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 5, AUTHORITY: 0, ADDITIONAL: 2

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4096
; COOKIE: 064b7e1f091b95120100000061476865a6026d01f87d10ca (good)
;; QUESTION SECTION:
;inlanefreight.htb.             IN      ANY

;; ANSWER SECTION:
inlanefreight.htb.      604800  IN      TXT     "v=spf1 include:mailgun.org include:_spf.google.com include:spf.protection.outlook.com include:_spf.atlassian.net ip4:10.129.124.8 ip4:10.129.127.2 ip4:10.129.42.106 ~all"
inlanefreight.htb.      604800  IN      TXT     "atlassian-domain-verification=t1rKCy68JFszSdCKVpw64A1QksWdXuYFUeSXKU"
inlanefreight.htb.      604800  IN      TXT     "MS=ms97310371"
inlanefreight.htb.      604800  IN      SOA     inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
inlanefreight.htb.      604800  IN      NS      ns.inlanefreight.htb.

;; ADDITIONAL SECTION:
ns.inlanefreight.htb.   604800  IN      A       10.129.34.136

;; Query time: 0 msec
;; SERVER: 10.129.14.128#53(10.129.14.128)
;; WHEN: So Sep 19 18:42:13 CEST 2021
;; MSG SIZE  rcvd: 437
```

### AXFR Zone Transfer

#### dig

	dig axfr inlanefreight.htb @10.129.14.128

```text
; <<>> DiG 9.16.1-Ubuntu <<>> axfr inlanefreight.htb @10.129.14.128
;; global options: +cmd
inlanefreight.htb.      604800  IN      SOA     inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
inlanefreight.htb.      604800  IN      TXT     "MS=ms97310371"
inlanefreight.htb.      604800  IN      TXT     "atlassian-domain-verification=t1rKCy68JFszSdCKVpw64A1QksWdXuYFUeSXKU"
inlanefreight.htb.      604800  IN      TXT     "v=spf1 include:mailgun.org include:_spf.google.com include:spf.protection.outlook.com include:_spf.atlassian.net ip4:10.129.124.8 ip4:10.129.127.2 ip4:10.129.42.106 ~all"
inlanefreight.htb.      604800  IN      NS      ns.inlanefreight.htb.
app.inlanefreight.htb.  604800  IN      A       10.129.18.15
internal.inlanefreight.htb. 604800 IN   A       10.129.1.6
mail1.inlanefreight.htb. 604800 IN      A       10.129.18.201
ns.inlanefreight.htb.   604800  IN      A       10.129.34.136
inlanefreight.htb.      604800  IN      SOA     inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
;; Query time: 4 msec
;; SERVER: 10.129.14.128#53(10.129.14.128)
;; WHEN: So Sep 19 18:51:19 CEST 2021
;; XFR size: 9 records (messages 1, bytes 520)
```

#### nmap

	sudo nmap -sN -n --script /usr/share/nmap/scripts/dns-zone-transfer.nse --script-args domain=<domain.tld>,server=<nameserver>

#### hackertarget

>Attacker: https://hackertarget.com/zone-transfer/
>Target: zonetransfer.me

```text
; <<>> DiG 9.10.3-P4-Debian <<>> axfr @nsztm1.digi.ninja zonetransfer.me
; (1 server found)
;; global options: +cmd
zonetransfer.me.	7200	IN	SOA	nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
zonetransfer.me.	300	IN	HINFO	"Casio fx-700G" "Windows XP"
zonetransfer.me.	301	IN	TXT	"google-site-verification=tyP28J7JAUHA9fw2sHXMgcCC0I6XBmmoVi04VlMewxA"
zonetransfer.me.	7200	IN	MX	0 ASPMX.L.GOOGLE.COM.
zonetransfer.me.	7200	IN	MX	10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me.	7200	IN	MX	10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX5.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	A	5.196.105.14
zonetransfer.me.	7200	IN	NS	nsztm1.digi.ninja.
zonetransfer.me.	7200	IN	NS	nsztm2.digi.ninja.
_acme-challenge.zonetransfer.me. 301 IN	TXT	"6Oa05hbUJ9xSsvYy7pApQvwCUSSGgxvrbdizjePEsZI"
_sip._tcp.zonetransfer.me. 14000 IN	SRV	0 0 5060 www.zonetransfer.me.
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me. 7200	IN PTR www.zonetransfer.me.
asfdbauthdns.zonetransfer.me. 7900 IN	AFSDB	1 asfdbbox.zonetransfer.me.
asfdbbox.zonetransfer.me. 7200	IN	A	127.0.0.1
asfdbvolume.zonetransfer.me. 7800 IN	AFSDB	1 asfdbbox.zonetransfer.me.
canberra-office.zonetransfer.me. 7200 IN A	202.14.81.230
cmdexec.zonetransfer.me. 300	IN	TXT	"; ls"
contact.zonetransfer.me. 2592000 IN	TXT	"Remember to call or email Pippa on +44 123 4567890 or pippa@zonetransfer.me when making DNS changes"
dc-office.zonetransfer.me. 7200	IN	A	143.228.181.132
deadbeef.zonetransfer.me. 7201	IN	AAAA	dead:beaf::
dr.zonetransfer.me.	300	IN	LOC	53 20 56.558 N 1 38 33.526 W 0.00m 1m 10000m 10m
DZC.zonetransfer.me.	7200	IN	TXT	"AbCdEfG"
email.zonetransfer.me.	2222	IN	NAPTR	1 1 "P" "E2U+email" "" email.zonetransfer.me.zonetransfer.me.
email.zonetransfer.me.	7200	IN	A	74.125.206.26
Hello.zonetransfer.me.	7200	IN	TXT	"Hi to Josh and all his class"
home.zonetransfer.me.	7200	IN	A	127.0.0.1
Info.zonetransfer.me.	7200	IN	TXT	"ZoneTransfer.me service provided by Robin Wood - robin@digi.ninja. See http://digi.ninja/projects/zonetransferme.php for more information."
internal.zonetransfer.me. 300	IN	NS	intns1.zonetransfer.me.
internal.zonetransfer.me. 300	IN	NS	intns2.zonetransfer.me.
intns1.zonetransfer.me.	300	IN	A	81.4.108.41
intns2.zonetransfer.me.	300	IN	A	167.88.42.94
office.zonetransfer.me.	7200	IN	A	4.23.39.254
ipv6actnow.org.zonetransfer.me.	7200 IN	AAAA	2001:67c:2e8:11::c100:1332
owa.zonetransfer.me.	7200	IN	A	207.46.197.32
robinwood.zonetransfer.me. 302	IN	TXT	"Robin Wood"
rp.zonetransfer.me.	321	IN	RP	robin.zonetransfer.me. robinwood.zonetransfer.me.
sip.zonetransfer.me.	3333	IN	NAPTR	2 3 "P" "E2U+sip" "!^.*$!sip:customer-service@zonetransfer.me!" .
sqli.zonetransfer.me.	300	IN	TXT	"' or 1=1 --"
sshock.zonetransfer.me.	7200	IN	TXT	"() { :]}; echo ShellShocked"
staging.zonetransfer.me. 7200	IN	CNAME	www.sydneyoperahouse.com.
alltcpportsopen.firewall.test.zonetransfer.me. 301 IN A	127.0.0.1
testing.zonetransfer.me. 301	IN	CNAME	www.zonetransfer.me.
vpn.zonetransfer.me.	4000	IN	A	174.36.59.154
www.zonetransfer.me.	7200	IN	A	5.196.105.14
xss.zonetransfer.me.	300	IN	TXT	"'>alert('Boo')"
zonetransfer.me.	7200	IN	SOA	nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
;; Query time: 77 msec
;; SERVER: 81.4.108.41#53(81.4.108.41)
;; WHEN: Fri Jan 06 10:27:32 UTC 2023
;; XFR size: 50 records (messages 1, bytes 1994)



; <<>> DiG 9.10.3-P4-Debian <<>> axfr @nsztm2.digi.ninja zonetransfer.me
; (1 server found)
;; global options: +cmd
zonetransfer.me.	7200	IN	SOA	nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
zonetransfer.me.	300	IN	HINFO	"Casio fx-700G" "Windows XP"
zonetransfer.me.	301	IN	TXT	"google-site-verification=tyP28J7JAUHA9fw2sHXMgcCC0I6XBmmoVi04VlMewxA"
zonetransfer.me.	7200	IN	MX	0 ASPMX.L.GOOGLE.COM.
zonetransfer.me.	7200	IN	MX	10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me.	7200	IN	MX	10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	MX	20 ASPMX5.GOOGLEMAIL.COM.
zonetransfer.me.	7200	IN	A	5.196.105.14
zonetransfer.me.	7200	IN	NS	nsztm1.digi.ninja.
zonetransfer.me.	7200	IN	NS	nsztm2.digi.ninja.
_acme-challenge.zonetransfer.me. 301 IN	TXT	"2acOp15rSxBpyF6L7TqnAoW8aI0vqMU5kpXQW7q4egc"
_acme-challenge.zonetransfer.me. 301 IN	TXT	"6Oa05hbUJ9xSsvYy7pApQvwCUSSGgxvrbdizjePEsZI"
_sip._tcp.zonetransfer.me. 14000 IN	SRV	0 0 5060 www.zonetransfer.me.
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me. 7200	IN PTR www.zonetransfer.me.
asfdbauthdns.zonetransfer.me. 7900 IN	AFSDB	1 asfdbbox.zonetransfer.me.
asfdbbox.zonetransfer.me. 7200	IN	A	127.0.0.1
asfdbvolume.zonetransfer.me. 7800 IN	AFSDB	1 asfdbbox.zonetransfer.me.
canberra-office.zonetransfer.me. 7200 IN A	202.14.81.230
cmdexec.zonetransfer.me. 300	IN	TXT	"; ls"
contact.zonetransfer.me. 2592000 IN	TXT	"Remember to call or email Pippa on +44 123 4567890 or pippa@zonetransfer.me when making DNS changes"
dc-office.zonetransfer.me. 7200	IN	A	143.228.181.132
deadbeef.zonetransfer.me. 7201	IN	AAAA	dead:beaf::
dr.zonetransfer.me.	300	IN	LOC	53 20 56.558 N 1 38 33.526 W 0.00m 1m 10000m 10m
DZC.zonetransfer.me.	7200	IN	TXT	"AbCdEfG"
email.zonetransfer.me.	2222	IN	NAPTR	1 1 "P" "E2U+email" "" email.zonetransfer.me.zonetransfer.me.
email.zonetransfer.me.	7200	IN	A	74.125.206.26
Hello.zonetransfer.me.	7200	IN	TXT	"Hi to Josh and all his class"
home.zonetransfer.me.	7200	IN	A	127.0.0.1
Info.zonetransfer.me.	7200	IN	TXT	"ZoneTransfer.me service provided by Robin Wood - robin@digi.ninja. See http://digi.ninja/projects/zonetransferme.php for more information."
internal.zonetransfer.me. 300	IN	NS	intns1.zonetransfer.me.
internal.zonetransfer.me. 300	IN	NS	intns2.zonetransfer.me.
intns1.zonetransfer.me.	300	IN	A	81.4.108.41
intns2.zonetransfer.me.	300	IN	A	52.91.28.78
office.zonetransfer.me.	7200	IN	A	4.23.39.254
ipv6actnow.org.zonetransfer.me.	7200 IN	AAAA	2001:67c:2e8:11::c100:1332
owa.zonetransfer.me.	7200	IN	A	207.46.197.32
robinwood.zonetransfer.me. 302	IN	TXT	"Robin Wood"
rp.zonetransfer.me.	321	IN	RP	robin.zonetransfer.me. robinwood.zonetransfer.me.
sip.zonetransfer.me.	3333	IN	NAPTR	2 3 "P" "E2U+sip" "!^.*$!sip:customer-service@zonetransfer.me!" .
sqli.zonetransfer.me.	300	IN	TXT	"' or 1=1 --"
sshock.zonetransfer.me.	7200	IN	TXT	"() { :]}; echo ShellShocked"
staging.zonetransfer.me. 7200	IN	CNAME	www.sydneyoperahouse.com.
alltcpportsopen.firewall.test.zonetransfer.me. 301 IN A	127.0.0.1
testing.zonetransfer.me. 301	IN	CNAME	www.zonetransfer.me.
vpn.zonetransfer.me.	4000	IN	A	174.36.59.154
www.zonetransfer.me.	7200	IN	A	5.196.105.14
xss.zonetransfer.me.	300	IN	TXT	"'>alert('Boo')"
zonetransfer.me.	7200	IN	SOA	nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
;; Query time: 7 msec
;; SERVER: 34.225.33.2#53(34.225.33.2)
;; WHEN: Fri Jan 06 10:27:32 UTC 2023
;; XFR size: 51 records (messages 1, bytes 2113)
```

### ANY and AXFR Zone Transfer

	nslookup -type=NS zonetransfer.me

```text
Server:		10.100.0.1
Address:	10.100.0.1#53

Non-authoritative answer:
zonetransfer.me	nameserver = nsztm2.digi.ninja.
zonetransfer.me	nameserver = nsztm1.digi.ninja.
```

	nslookup -type=any -query=AXFR zonetransfer.me nsztm1.digi.ninja

```text
Server:		nsztm1.digi.ninja
Address:	81.4.108.41#53

zonetransfer.me
	origin = nsztm1.digi.ninja
	mail addr = robin.digi.ninja
	serial = 2019100801
	refresh = 172800
	retry = 900
	expire = 1209600
	minimum = 3600
zonetransfer.me	hinfo = "Casio fx-700G" "Windows XP"
zonetransfer.me	text = "google-site-verification=tyP28J7JAUHA9fw2sHXMgcCC0I6XBmmoVi04VlMewxA"
zonetransfer.me	mail exchanger = 0 ASPMX.L.GOOGLE.COM.
zonetransfer.me	mail exchanger = 10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me	mail exchanger = 10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me	mail exchanger = 20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me	mail exchanger = 20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me	mail exchanger = 20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me	mail exchanger = 20 ASPMX5.GOOGLEMAIL.COM.
Name:	zonetransfer.me
Address: 5.196.105.14
zonetransfer.me	nameserver = nsztm1.digi.ninja.
zonetransfer.me	nameserver = nsztm2.digi.ninja.
_acme-challenge.zonetransfer.me	text = "6Oa05hbUJ9xSsvYy7pApQvwCUSSGgxvrbdizjePEsZI"
_sip._tcp.zonetransfer.me	service = 0 0 5060 www.zonetransfer.me.
14.105.196.5.IN-ADDR.ARPA.zonetransfer.me	name = www.zonetransfer.me.
asfdbauthdns.zonetransfer.me	afsdb = 1 asfdbbox.zonetransfer.me.
Name:	asfdbbox.zonetransfer.me
Address: 127.0.0.1
asfdbvolume.zonetransfer.me	afsdb = 1 asfdbbox.zonetransfer.me.
Name:	canberra-office.zonetransfer.me
Address: 202.14.81.230
cmdexec.zonetransfer.me	text = "; ls"
contact.zonetransfer.me	text = "Remember to call or email Pippa on +44 123 4567890 or pippa@zonetransfer.me when making DNS changes"
Name:	dc-office.zonetransfer.me
Address: 143.228.181.132
Name:	deadbeef.zonetransfer.me
Address: dead:beaf::
dr.zonetransfer.me	loc = 53 20 56.558 N 1 38 33.526 W 0.00m 1m 10000m 10m
DZC.zonetransfer.me	text = "AbCdEfG"
email.zonetransfer.me	naptr = 1 1 "P" "E2U+email" "" email.zonetransfer.me.zonetransfer.me.
Name:	email.zonetransfer.me
Address: 74.125.206.26
Hello.zonetransfer.me	text = "Hi to Josh and all his class"
Name:	home.zonetransfer.me
Address: 127.0.0.1
Info.zonetransfer.me	text = "ZoneTransfer.me service provided by Robin Wood - robin@digi.ninja. See http://digi.ninja/projects/zonetransferme.php for more information."
internal.zonetransfer.me	nameserver = intns1.zonetransfer.me.
internal.zonetransfer.me	nameserver = intns2.zonetransfer.me.
Name:	intns1.zonetransfer.me
Address: 81.4.108.41
Name:	intns2.zonetransfer.me
Address: 167.88.42.94
Name:	office.zonetransfer.me
Address: 4.23.39.254
Name:	ipv6actnow.org.zonetransfer.me
Address: 2001:67c:2e8:11::c100:1332
Name:	owa.zonetransfer.me
Address: 207.46.197.32
robinwood.zonetransfer.me	text = "Robin Wood"
rp.zonetransfer.me	rp = robin.zonetransfer.me. robinwood.zonetransfer.me.
sip.zonetransfer.me	naptr = 2 3 "P" "E2U+sip" "!^.*$!sip:customer-service@zonetransfer.me!" .
sqli.zonetransfer.me	text = "' or 1=1 --"
sshock.zonetransfer.me	text = "() { :]}; echo ShellShocked"
staging.zonetransfer.me	canonical name = www.sydneyoperahouse.com.
Name:	alltcpportsopen.firewall.test.zonetransfer.me
Address: 127.0.0.1
testing.zonetransfer.me	canonical name = www.zonetransfer.me.
Name:	vpn.zonetransfer.me
Address: 174.36.59.154
Name:	www.zonetransfer.me
Address: 5.196.105.14
xss.zonetransfer.me	text = "'><script>alert('Boo')</script>"
zonetransfer.me
	origin = nsztm1.digi.ninja
	mail addr = robin.digi.ninja
	serial = 2019100801
	refresh = 172800
	retry = 900
	expire = 1209600
	minimum = 3600
```

### AXFR Zone Transfer - Internal

	dig axfr internal.inlanefreight.htb @10.129.14.128

```text
; <<>> DiG 9.16.1-Ubuntu <<>> axfr internal.inlanefreight.htb @10.129.14.128
;; global options: +cmd
internal.inlanefreight.htb. 604800 IN   SOA     inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
internal.inlanefreight.htb. 604800 IN   TXT     "MS=ms97310371"
internal.inlanefreight.htb. 604800 IN   TXT     "atlassian-domain-verification=t1rKCy68JFszSdCKVpw64A1QksWdXuYFUeSXKU"
internal.inlanefreight.htb. 604800 IN   TXT     "v=spf1 include:mailgun.org include:_spf.google.com include:spf.protection.outlook.com include:_spf.atlassian.net ip4:10.129.124.8 ip4:10.129.127.2 ip4:10.129.42.106 ~all"
internal.inlanefreight.htb. 604800 IN   NS      ns.inlanefreight.htb.
dc1.internal.inlanefreight.htb. 604800 IN A     10.129.34.16
dc2.internal.inlanefreight.htb. 604800 IN A     10.129.34.11
mail1.internal.inlanefreight.htb. 604800 IN A   10.129.18.200
ns.internal.inlanefreight.htb. 604800 IN A      10.129.34.136
vpn.internal.inlanefreight.htb. 604800 IN A     10.129.1.6
ws1.internal.inlanefreight.htb. 604800 IN A     10.129.1.34
ws2.internal.inlanefreight.htb. 604800 IN A     10.129.1.35
wsus.internal.inlanefreight.htb. 604800 IN A    10.129.18.2
internal.inlanefreight.htb. 604800 IN   SOA     inlanefreight.htb. root.inlanefreight.htb. 2 604800 86400 2419200 604800
;; Query time: 0 msec
;; SERVER: 10.129.14.128#53(10.129.14.128)
;; WHEN: So Sep 19 18:53:11 CEST 2021
;; XFR size: 15 records (messages 1, bytes 664)
```

### IXFR Zone Transfer

	dig ixfr <domain.tld> @<nameserver>

### Subdomain Brute Forcing

#### dig

	for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.inlanefreight.htb @10.129.14.128 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done

```text
ns.inlanefreight.htb.   604800  IN      A       10.129.34.136
mail1.inlanefreight.htb. 604800 IN      A       10.129.18.201
app.inlanefreight.htb.  604800  IN      A       10.129.18.15
```

#### dnsenum

	dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb

```text
dnsenum VERSION:1.2.6

-----   inlanefreight.htb   -----

Host's addresses:
__________________

Name Servers:
______________

ns.inlanefreight.htb.                    604800   IN    A        10.129.34.136

Mail (MX) Servers:
___________________

Trying Zone Transfers and getting Bind Versions:
_________________________________________________

unresolvable name: ns.inlanefreight.htb at /usr/bin/dnsenum line 900 thread 1.

Trying Zone Transfer for inlanefreight.htb on ns.inlanefreight.htb ...
AXFR record query failed: no nameservers

Brute forcing with /home/cry0l1t3/Pentesting/SecLists/Discovery/DNS/subdomains-top1million-110000.txt:
_______________________________________________________________________________________________________

ns.inlanefreight.htb.                    604800   IN    A        10.129.34.136
mail1.inlanefreight.htb.                 604800   IN    A        10.129.18.201
app.inlanefreight.htb.                   604800   IN    A        10.129.18.15
ns.inlanefreight.htb.                    604800   IN    A        10.129.34.136

...SNIP...
done.

```

### Subdomain Bruteforcing Using Patterns

	lert-api-shv-{GOBUSTER}-sin6
	atlas-pp-shv-{GOBUSTER}-sin6

| **Command** | **Description** |
|--|-- |
|`dns` | Launch the DNS module |
|`-q` | Don't print the banner and other noise |
|`-r` | Use custom DNS server |
|`-d` | A target domain name |
|`-p` | Path to the patterns file |
|`-w` | Path to the wordlist |
|`-o` | Output file |

	export TARGET="facebook.com"
	export NS="d.ns.facebook.com"
	export WORDLIST="numbers.txt"
	gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"

```text
Found: lert-api-shv-01-sin6.facebook.com
Found: atlas-pp-shv-01-sin6.facebook.com
Found: atlas-pp-shv-02-sin6.facebook.com
Found: atlas-pp-shv-03-sin6.facebook.com
Found: lert-api-shv-03-sin6.facebook.com
Found: lert-api-shv-02-sin6.facebook.com
Found: lert-api-shv-04-sin6.facebook.com
Found: atlas-pp-shv-04-sin6.facebook.com
```

### Certificate Transparency

>See Also: https://search.censys.io/certificates

	python3 ctfr.py -d inlanefreight.com

```text
          ____ _____ _____ ____  
         / ___|_   _|  ___|  _ \ 
        | |     | | | |_  | |_) |
        | |___  | | |  _| |  _ < 
         \____| |_| |_|   |_| \_\
	
    Made by Sheila A. Berta (UnaPibaGeek)
	
inlanefreight.com
vc.inlanefreight.com
wlan.inlanefreight.com
afdc0102.inlanefreight.com
autodiscover.inlanefreight.com
kfdcex07.inlanefreight.com
kfdcex08.inlanefreight.com
videoconf.inlanefreight.com
<SNIP>
```

	curl -s "https://crt.sh/?q=${TARGET}&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "${TARGET}_crt.sh.txt"

| **Command** | **Description** |
| --- | --- |
| `curl -s` | Issue the request with minimal output. |
| `https://crt.sh/?q=<DOMAIN>&output=json` | Ask for the json output. |
| `jq -r '.[]' "\(.name_value)\n\(.common_name)"'` | Process the json output and print certificate's name vale and common name one per line. |
| `sort -u` | Sort alphabetically the output provided and removes duplicates. |

```text
account-control.facebook.com----retrieve-info.albayrakyangin.com
*.adtools.facebook.com
adtools.facebook.com
*.ak.facebook.com
ak.facebook.com
<...snip...>
```

### vHost Fuzzing

| **Flag** | **Description** |
|-|-|
| `-w` | Path to our wordlist
| `-u` | URL we want to fuzz
| `-H "HOST: FUZZ.randomtarget.com"` | This is the `HOST` Header, and the word `FUZZ` will be used as the fuzzing point.
| `-fs 612` | Filter responses with a size of 612, default response size in this case.

	ffuf -w ./vhosts -u http://192.168.10.10 -H "HOST: FUZZ.randomtarget.com" -fs 612

```text
        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://192.168.10.10
 :: Wordlist         : FUZZ: ./vhosts
 :: Header           : Host: FUZZ.randomtarget.com
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405
 :: Filter           : Response size: 612
________________________________________________

dev-admin               [Status: 200, Size: 120, Words: 7, Lines: 12]
www                     [Status: 200, Size: 185, Words: 41, Lines: 9]
some                    [Status: 200, Size: 195, Words: 41, Lines: 9]
:: Progress: [12/12] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::
```

	ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-big.txt -u http://10.129.156.165  -H "HOST: FUZZ.inlanefreight.htb"

```text
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.156.165
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-big.txt
 :: Header           : Host: FUZZ.inlanefreight.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
________________________________________________

full                    [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 93ms]
10                      [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 94ms]
news                    [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 94ms]
12                      [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 94ms]
home                    [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 95ms]
serial                  [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 97ms]
2006                    [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 96ms]
img                     [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 97ms]
index                   [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 97ms]
spacer                  [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 97ms]
contact                 [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 98ms]
new                     [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 99ms]
images                  [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 100ms]
about                   [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 101ms]
warez                   [Status: 200, Size: 10918, Words: 3499, Lines: 376, Duration: 101ms]
<...snip...>
```

	ffuf -w /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-big.txt -u http://10.129.156.165  -H "HOST: FUZZ.inlanefreight.htb" -fs 10918

```text
        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.5.0 Kali Exclusive <3
________________________________________________

 :: Method           : GET
 :: URL              : http://10.129.156.165
 :: Wordlist         : FUZZ: /usr/share/seclists/Discovery/Web-Content/directory-list-lowercase-2.3-big.txt
 :: Header           : Host: FUZZ.inlanefreight.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403,405,500
 :: Filter           : Response size: 10918
________________________________________________

customers               [Status: 200, Size: 94, Words: 3, Lines: 6, Duration: 42ms]
app                     [Status: 200, Size: 103, Words: 3, Lines: 6, Duration: 46ms]
ap                      [Status: 200, Size: 102, Words: 3, Lines: 6, Duration: 45ms]
citrix                  [Status: 200, Size: 100, Words: 3, Lines: 6, Duration: 144ms]
www2                    [Status: 200, Size: 96, Words: 2, Lines: 6, Duration: 49ms]
dmz                     [Status: 200, Size: 95, Words: 2, Lines: 6, Duration: 40ms]
```

	curl -s 10.129.156.165 -H "Host: customers.inlanefreight.htb"

```text
<!doctype html>
<head>FLAG No.4:</head>
<body>
        HTB{...}
</body>
```

	curl -s 10.129.156.165 -H "Host: app.inlanefreight.htb"

```text
<!doctype html>
<head>FLAG No.2:</head>
<body>
        HTB{...}
</body>
```

	curl -s 10.129.156.165 -H "Host: ap.inlanefreight.htb" 

```
<!doctype html>
<head>FLAG No.1:</head>
<body>
        HTB{...}
</body>
```

	curl -s 10.129.156.165 -H "Host: citrix.inlanefreight.htb"

```
<!doctype html>
<head>FLAG No.3:</head>
<body>
        HTB{...}
</body>
```

	curl -s 10.129.156.165 -H "Host: dmz.inlanefreight.htb"

```text
<!doctype html>
<head>FLAG</head>
<body>
        HTB{...}
</body>
```

### WHOIS - MNT-REF

	whois -B --sources RIPE,ARIN target-company

```text
% Information related to 'ORG-ZZ000-RIPE'

organisation:   ORG-ZZ000-RIPE
org-name:       Target-Company LLC
country:        CO
org-type:       XXX
address:        Street 00
address:        00000
address:        City
address:        COUNTRY
phone:          +00000000000
fax-no:         +00000000000
mnt-ref:        EU-IBM-XXX-0000
mnt-ref:        HN0000-MNT
mnt-ref:        AS0000-MNT
mnt-ref:        RIPE-XXX-ZZ-MNT
mnt-by:         RIPE-XXX-ZZ-MNT
mnt-by:         HL0000-MNT
abuse-c:        AHA000-RIPE
created:        2010-01-12T13:57:44Z
last-modified:  2021-10-14T12:14:22Z
source:         RIPE
e-mail:         full.name@target-company.com

% Information related to 'AHA000-RIPE'

role:           ABUSE Target-Company LLC
address:        Street 00, 00000 City, Country
e-mail:         dns.admin@target-company.com
abuse-mailbox:  dns.admin@target-company.com
nic-hdl:        AHA000-RIPE
mnt-by:         RK00000-MNT
created:        2014-11-15T11:54:10Z
last-modified:  2014-11-15T11:54:10Z
source:         RIPE

% Information related to 'HN0000-RIPE'

role:           Target-Company NOC
address:        Street 00, 00000 City, Country
e-mail:         dns.admin@target-company.com
nic-hdl:        HN0000-RIPE
mnt-by:         AA00000-MNT
created:        2019-04-07T06:44:22Z
last-modified:  2019-04-07T06:44:22Z
source:         RIPE
```

### WHOIS - Netblocks

	whois -h whois.arin.net target-company | grep -v "#" | sed -r '/^\s*$/d'

```text
Target-Company (C00000) 10-10-60-68 (NET-10-10-60-68-1) 10.10.60.68 - 10.10.60.69
Target-Company (C00000) 10-10-60-70 (NET-10-10-60-70-1) 10.10.60.70 - 10.10.60.71
```

### Shodan

#### Get IP Addresses

	shodan domain <TARGET-DOMAIN> | grep -w "A" | cut -d"A" -f2 | cut -d" " -f7 | sort -u > IPv4s.txt
	cat IPv4s.txt | wc -l

```text
36
```

#### Passive Port Scan

	for ip in $(cat IPv4s.txt);do shodan host $ip;done

```text
X.X.164.24
Hostnames:               vc.inlanefreight.com
Country:                 United Kingdom
Organization:            Inlanefreight
Updated:                 2020-07-23T15:26:40.055514
Number of open ports:    7

Ports:
    443/tcp  
   2222/tcp  
   5060/udp TANDBERG/4137 (X12.5.1) 
   5222/tcp  
   7001/tcp  
   7443/tcp  
   8443/tcp  

X.X.48.186
Hostnames:               mail.inlanefreight.com
Country:                 United Kingdom
Organization:            Inlanefreight
Updated:                 2020-07-08T08:36:17.845819
Number of open ports:    2

Ports:
    443/tcp  
   8888/tcp  

<SNIP>
```

#### Domain Information

	shodan domain target-company.com

```text
TARGET-COMPANY.COM

                         A      10.19.14.43
campaigns                CNAME  isp-id077411.com
ecard                    A      10.19.14.134
pages                    CNAME  target-company.isp.com
solutions                CNAME  unbouncepages.com
staging                  A      10.19.14.217
www                      CNAME  www-en.tar-comp.com
www-mig                  A      10.19.14.45
www-rel                  A      10.19.14.68
www2                     CNAME  www2.tar-comp.com
```

#### Additional Domain Information

	shodan domain tar-comp.com

```text
TAR-COMP.COM

                         A      10.19.14.53
                         MX     mx3.mailprovider.com
                         MX     mx4.mailprovider.com
                         NS     ns1.ns-provider.net
                         NS     ns6.ns-provider.net
                         NS     ns2.ns-provider.net
                         NS     ns5.ns-provider.net
                         SOA    ns1.ns-provider.net
prod                     A      10.19.14.37
prod                     AAAA   d34d:b33f:4:3::37
prod-mig                 A      10.19.14.38
prod-rel                 A      10.19.14.72
prod-rel                 AAAA   2a04:1447:4:3::72
training                 A      10.19.14.50
hip                      A      10.7.148.165
hleforms                 A      10.7.148.167
hod                      A      10.7.148.130
hody81                   CNAME  hody.tar-comp.com
kf123t01-1               A      10.7.148.233
kf123t01-1               A      10.7.148.231
mail-archive             A      10.7.148.134
sap                      A      10.7.148.161
www                      CNAME  www-en.hlcl.com
www-de                   A      10.19.14.49
www-de                   AAAA   d34d:b33f:4:3::49
www-en                   A      10.19.14.43
www-en                   AAAA   d34d:b33f:4:3::43
www2                     A      10.19.14.44
www2                     AAAA   d34d:b33f:4:3::44
```

#### Search the Database

	shodan search target-company | cut -d" " -f1-3

```text
10.29.26.251    8500    ec2-10-29-46-251.us-east-2.compute.amazonaws.com      HTTP/1.1 302 Found\r\nServer:
10.65.126.101   25      target-company.de 220 target-company.de ESMTP
10.62.241.109   8081    3ef15ea9.ip4.static.isp-provider.com    HTTP/1.1 200 OK\r\nCache-Control:
10.120.232.207  80      target-company-test.tracker.com    HTTP/1.1 302 Found\r\nDate:
10.54.2.133     23              C i s c o  S y s t e m s\r\n     ROUTER INTERNET\r\n
10.11.184.41    80              HTTP/1.1 301 Moved
10.11.184.41    443             HTTP/1.1 200 OK\r\nServer:
```

### Get Cloud Provider and Perhaps Service/Region

#### Installation

	git clone https://github.com/oldrho/ip2provider.git
	cd ip2provider
	pip3 install -r requirements.txt

#### Usage

	cat Target_Company.IPv4s | ./ip2provider.py

```text
X.X.X.20 digitalocean unknown unknown
X.X.X.66 aws AMAZON us-east-1
X.X.X.16 aws AMAZON eu-central-1
X.X.X.24 aws AMAZON eu-central-1
X.X.X.27 aws AMAZON eu-west-1
X.X.X.17 aws AMAZON eu-central-1
<SNIP>
```

	pigz -dc rapid7-fdns-db.json.gz | grep "target-company" | grep "core.microsoft.net\|s3.amazonaws.com\|s3-*.amazonaws.com\|googleapis.com/storage/v1/b/"

```text
{"timestamp":"...","name":"target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"cn-api.target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"com-target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"dev.target-company.core.microsoft.net","type":"a","value":"X.X.X.127"}
<SNIP>
```

# Resources

https://github.com/UnaPibaGeek/ctfr
https://whois.domaintools.com/
https://search.censys.io/certificates
https://dnsdumpster.com/