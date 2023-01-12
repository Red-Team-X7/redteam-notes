# 💢 shodan

Tags: #⚙️
Related to: 
See also: 
Previous: [[OSINT - Corporate Recon]]

## Description

Search engine for internet connected devices.

## Usage Examples

### Get IP Addresses

	shodan domain <TARGET-DOMAIN> | grep -w "A" | cut -d"A" -f2 | cut -d" " -f7 | sort -u > IPv4s.txt
	cat IPv4s.txt | wc -l

```text
36
```

### Passive Port Scan

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

### Domain Information

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

### Additional Domain Information

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

### Search the Database

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

# References