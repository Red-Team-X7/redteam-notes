# 🔥 dns zone transfer
Tags: #🔥
Related to: 
See also: [[dns cache snooping]], [[whois]], [[dig]], [[nmap]]
Previous: [[TTP]]

## Description

## Usage Examples

### Zone Transfer

#### dig method
	
	dig @NS1.LIGHTSPEEDHOSTING.COM lightspeedhosting.com -t AXFR

```
; <<>> DiG 9.16.15-Debian <<>> @NS1.LIGHTSPEEDHOSTING.COM lightspeedhosting.com -t AXFR
; (1 server found)
;; global options: +cmd
lightspeedhosting.com.  86400   IN      SOA     ns1.lightspeedhosting.com. info.lightspeedhosting.com. 2017030215 86400 7200 3600000 86400
lightspeedhosting.com.  14400   IN      MX      1 aspmx.l.google.com.
lightspeedhosting.com.  14400   IN      MX      5 alt1.aspmx.l.google.com.
lightspeedhosting.com.  14400   IN      MX      5 alt2.aspmx.l.google.com.
lightspeedhosting.com.  14400   IN      MX      10 aspmx2.googlemail.com.
lightspeedhosting.com.  14400   IN      MX      10 aspmx3.googlemail.com.
lightspeedhosting.com.  14400   IN      TXT     "MS=DC80ECEDA4A4DC761B61CF31EE8C047CBB26907C"
lightspeedhosting.com.  14400   IN      TXT     "google-site-verification=pqJP8HrTDiyAJgddkQn2dZJRuksXosE9XxsFjeYBpa8"
lightspeedhosting.com.  14400   IN      TXT     "v=spf1 ip4:148.59.137.13 ip4:148.59.137.73 include:_spf.google.com a mx ~all"
lightspeedhosting.com.  86400   IN      NS      ns1.lightspeedhosting.com.
lightspeedhosting.com.  86400   IN      NS      ns2.lightspeedhosting.com.
lightspeedhosting.com.  14400   IN      A       148.59.137.19
7899333.lightspeedhosting.com. 14400 IN CNAME   sendgrid.net.
_amazonses.lightspeedhosting.com. 14400 IN TXT  "JlOaTIDxEqgY9R2/yF70GwV39gpuhLsNSWl/oj0i4sc="
4o4gkifx4camwl6q7lbr4legq7p624kb._domainkey.lightspeedhosting.com. 14400 IN CNAME 4o4gkifx4camwl6q7lbr4legq7p624kb.dkim.amazonses.com.
cm._domainkey.lightspeedhosting.com. 14400 IN TXT "k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC+DsJ8s9oYtSaUGiGHkyFuxLN4NZ+nhf5wS/HwqAB93JZhNApPB0XpGMZZ9TuQDBAj4YE2DAIs3BavT5wI0F1xzzCn59VbWstGqQFRlqWiAQj8RQ3ODudJuubZe/jM1QtsX4MJewR0yqZT89KmpMOa45bmiJakel167CZgA2BuowIDAQAB"
s1._domainkey.lightspeedhosting.com. 14400 IN CNAME s1.domainkey.u7899333.wl084.sendgrid.net.
s2._domainkey.lightspeedhosting.com. 14400 IN CNAME s2.domainkey.u7899333.wl084.sendgrid.net.
yvvj7nkaiwoqijn5tunfi4hklxocmqxy._domainkey.lightspeedhosting.com. 14400 IN CNAME yvvj7nkaiwoqijn5tunfi4hklxocmqxy.dkim.amazonses.com.
zyxb2qmbgwmehwj72qcgwxqsvwwl7wfl._domainkey.lightspeedhosting.com. 14400 IN CNAME zyxb2qmbgwmehwj72qcgwxqsvwwl7wfl.dkim.amazonses.com.
app.lightspeedhosting.com. 14400 IN     A       148.59.137.13
dev.lightspeedhosting.com. 14400 IN     A       148.59.137.58
dns.lightspeedhosting.com. 14400 IN     A       148.59.137.8
dns2.lightspeedhosting.com. 14400 IN    A       148.59.137.9
em2095.lightspeedhosting.com. 14400 IN  CNAME   u7899333.wl084.sendgrid.net.
et1.lightspeedhosting.com. 14400 IN     A       149.28.127.174
fax.lightspeedhosting.com. 14400 IN     A       67.227.209.202
localhost.lightspeedhosting.com. 14400 IN A     127.0.0.1
login.lightspeedhosting.com. 14400 IN   A       148.59.137.13
manage.lightspeedhosting.com. 14400 IN  A       148.59.137.25
monitor.lightspeedhosting.com. 14400 IN A       69.167.134.120
www.monitor.lightspeedhosting.com. 14400 IN A   69.167.134.120
my.lightspeedhosting.com. 14400 IN      A       148.59.137.13
my.lightspeedhosting.com. 14400 IN      MX      1 148.59.137.13.
my.lightspeedhosting.com. 14400 IN      TXT     "v=spf1 ip4:148.59.137.13 a mx ~all"
_amazonses.my.lightspeedhosting.com. 14400 IN TXT "/3M1y0Mvu+6A0oZScaf0lLRL6aYIRJCgUsFRtx1Jd3Q="
6f64cgzcyvwvx4sh6w6t4fbdgkegsegn._domainkey.my.lightspeedhosting.com. 14400 IN CNAME 6f64cgzcyvwvx4sh6w6t4fbdgkegsegn.dkim.amazonses.com.
f5c5fahnozc3eeb3zyqlmoxfic2wf5kq._domainkey.my.lightspeedhosting.com. 14400 IN CNAME f5c5fahnozc3eeb3zyqlmoxfic2wf5kq.dkim.amazonses.com.
qjcinemvscssibu643zbc72jdt64hj64._domainkey.my.lightspeedhosting.com. 14400 IN CNAME qjcinemvscssibu643zbc72jdt64hj64.dkim.amazonses.com.
ns1.lightspeedhosting.com. 14400 IN     A       148.59.137.8
ns2.lightspeedhosting.com. 14400 IN     A       148.59.137.9
pbx.lightspeedhosting.com. 14400 IN     A       148.59.137.6
pbx1.lightspeedhosting.com. 14400 IN    A       148.59.137.6
phone.lightspeedhosting.com. 14400 IN   A       148.59.137.6
portal.lightspeedhosting.com. 14400 IN  A       148.59.137.13
skynet.lightspeedhosting.com. 14400 IN  A       148.59.137.17
stage.lightspeedhosting.com. 14400 IN   A       148.59.137.58
url3275.lightspeedhosting.com. 14400 IN CNAME   sendgrid.net.
vault.lightspeedhosting.com. 14400 IN   A       148.59.137.17
voicemail.lightspeedhosting.com. 14400 IN A     148.59.137.100
www.lightspeedhosting.com. 14400 IN     CNAME   lightspeedhosting.com.
lightspeedhosting.com.  86400   IN      SOA     ns1.lightspeedhosting.com. info.lightspeedhosting.com. 2017030215 86400 7200 3600000 86400
;; Query time: 128 msec
;; SERVER: 148.59.137.8#53(148.59.137.8)
;; WHEN: Tue Jul 13 08:23:28 EDT 2021
;; XFR size: 52 records (messages 1, bytes 2131)
```

### nmap method

	sudo nmap -sN -n --script /usr/share/nmap/scripts/dns-zone-transfer.nse --script-args domain=lightspeedhosting.com,server=NS1.LIGHTSPEEDHOSTING.COM

```
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-13 08:30 EDT
Pre-scan script results:
| dns-zone-transfer: 
| lightspeedhosting.com.                                                 SOA    ns1.lightspeedhosting.com. info.lightspeedhosting.com.
| lightspeedhosting.com.                                                 MX     1 aspmx.l.google.com.
| lightspeedhosting.com.                                                 MX     5 alt1.aspmx.l.google.com.
| lightspeedhosting.com.                                                 MX     5 alt2.aspmx.l.google.com.
| lightspeedhosting.com.                                                 MX     10 aspmx2.googlemail.com.
| lightspeedhosting.com.                                                 MX     10 aspmx3.googlemail.com.
| lightspeedhosting.com.                                                 TXT    "MS=DC80ECEDA4A4DC761B61CF31EE8C047CBB26907C"
| lightspeedhosting.com.                                                 TXT    "google-site-verification=pqJP8HrTDiyAJgddkQn2dZJRuksXosE9XxsFjeYBpa8"
| lightspeedhosting.com.                                                 TXT    "v=spf1 ip4:148.59.137.13 ip4:148.59.137.73 include:_spf.google.com a mx ~all"
| lightspeedhosting.com.                                                 NS     ns1.lightspeedhosting.com.
| lightspeedhosting.com.                                                 NS     ns2.lightspeedhosting.com.
| lightspeedhosting.com.                                                 A      148.59.137.19
| 7899333.lightspeedhosting.com.                                         CNAME  sendgrid.net.
| _amazonses.lightspeedhosting.com.                                      TXT    "JlOaTIDxEqgY9R2/yF70GwV39gpuhLsNSWl/oj0i4sc="
| 4o4gkifx4camwl6q7lbr4legq7p624kb._domainkey.lightspeedhosting.com.     CNAME  4o4gkifx4camwl6q7lbr4legq7p624kb.dkim.amazonses.com.
| cm._domainkey.lightspeedhosting.com.                                   TXT    "k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC+DsJ8s9oYtSaUGiGHkyFuxLN4NZ+nhf5wS/HwqAB93JZhNApPB0XpGMZZ9TuQDBAj4YE2DAIs3BavT5wI0F1xzzCn59VbWstGqQFRlqWiAQj8RQ3ODudJuubZe/jM1QtsX4MJewR0yqZT89KmpMOa45bmiJakel167CZgA2BuowIDAQAB"
| s1._domainkey.lightspeedhosting.com.                                   CNAME  s1.domainkey.u7899333.wl084.sendgrid.net.
| s2._domainkey.lightspeedhosting.com.                                   CNAME  s2.domainkey.u7899333.wl084.sendgrid.net.
| yvvj7nkaiwoqijn5tunfi4hklxocmqxy._domainkey.lightspeedhosting.com.     CNAME  yvvj7nkaiwoqijn5tunfi4hklxocmqxy.dkim.amazonses.com.
| zyxb2qmbgwmehwj72qcgwxqsvwwl7wfl._domainkey.lightspeedhosting.com.     CNAME  zyxb2qmbgwmehwj72qcgwxqsvwwl7wfl.dkim.amazonses.com.
| app.lightspeedhosting.com.                                             A      148.59.137.13
| dev.lightspeedhosting.com.                                             A      148.59.137.58
| dns.lightspeedhosting.com.                                             A      148.59.137.8
| dns2.lightspeedhosting.com.                                            A      148.59.137.9
| em2095.lightspeedhosting.com.                                          CNAME  u7899333.wl084.sendgrid.net.
| et1.lightspeedhosting.com.                                             A      149.28.127.174
| fax.lightspeedhosting.com.                                             A      67.227.209.202
| localhost.lightspeedhosting.com.                                       A      127.0.0.1
| login.lightspeedhosting.com.                                           A      148.59.137.13
| manage.lightspeedhosting.com.                                          A      148.59.137.25
| monitor.lightspeedhosting.com.                                         A      69.167.134.120
| www.monitor.lightspeedhosting.com.                                     A      69.167.134.120
| my.lightspeedhosting.com.                                              A      148.59.137.13
| my.lightspeedhosting.com.                                              MX     1 148.59.137.13.
| my.lightspeedhosting.com.                                              TXT    "v=spf1 ip4:148.59.137.13 a mx ~all"
| _amazonses.my.lightspeedhosting.com.                                   TXT    "/3M1y0Mvu+6A0oZScaf0lLRL6aYIRJCgUsFRtx1Jd3Q="
| 6f64cgzcyvwvx4sh6w6t4fbdgkegsegn._domainkey.my.lightspeedhosting.com.  CNAME  6f64cgzcyvwvx4sh6w6t4fbdgkegsegn.dkim.amazonses.com.
| f5c5fahnozc3eeb3zyqlmoxfic2wf5kq._domainkey.my.lightspeedhosting.com.  CNAME  f5c5fahnozc3eeb3zyqlmoxfic2wf5kq.dkim.amazonses.com.
| qjcinemvscssibu643zbc72jdt64hj64._domainkey.my.lightspeedhosting.com.  CNAME  qjcinemvscssibu643zbc72jdt64hj64.dkim.amazonses.com.
| ns1.lightspeedhosting.com.                                             A      148.59.137.8
| ns2.lightspeedhosting.com.                                             A      148.59.137.9
| pbx.lightspeedhosting.com.                                             A      148.59.137.6
| pbx1.lightspeedhosting.com.                                            A      148.59.137.6
| phone.lightspeedhosting.com.                                           A      148.59.137.6
| portal.lightspeedhosting.com.                                          A      148.59.137.13
| skynet.lightspeedhosting.com.                                          A      148.59.137.17
| stage.lightspeedhosting.com.                                           A      148.59.137.58
| url3275.lightspeedhosting.com.                                         CNAME  sendgrid.net.
| vault.lightspeedhosting.com.                                           A      148.59.137.17
| voicemail.lightspeedhosting.com.                                       A      148.59.137.100
| www.lightspeedhosting.com.                                             CNAME  lightspeedhosting.com.
|_lightspeedhosting.com.                                                 SOA    ns1.lightspeedhosting.com. info.lightspeedhosting.com.
```

### Incremental Zone Transfer
dig can perform an incremental zone transfer, pulling only recently updated records  
(N is an integer that refers to the serial number of a Start of Authority record.  
The incremental zone transfer request will pull all records that have changed since  
the SOA serial number was the N we specified):

	dig @[server] [domain] -t IXFR=[N]
  
## References