# ⚙️ whois
Tags: #⚙️ 
Related to:
See also:
Previous: [[Information Gathering - Web Edition]]

## Description

Cient for the whois directory service.

## Usage Examples

### Lookup IP Address Range(s)  / CIDR

	whois facebook.com

```text
Domain Name: FACEBOOK.COM
Registry Domain ID: 2320948_DOMAIN_COM-VRSN
Registrar WHOIS Server: whois.registrarsafe.com
Registrar URL: https://www.registrarsafe.com
Updated Date: 2021-09-22T19:33:41Z
Creation Date: 1997-03-29T05:00:00Z
Registrar Registration Expiration Date: 2030-03-30T04:00:00Z
Registrar: RegistrarSafe, LLC
Registrar IANA ID: 3237
Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
Registrar Abuse Contact Phone: +1.6503087004
Domain Status: clientDeleteProhibited https://www.icann.org/epp#clientDeleteProhibited
Domain Status: clientTransferProhibited https://www.icann.org/epp#clientTransferProhibited
Domain Status: clientUpdateProhibited https://www.icann.org/epp#clientUpdateProhibited
Domain Status: serverDeleteProhibited https://www.icann.org/epp#serverDeleteProhibited
Domain Status: serverTransferProhibited https://www.icann.org/epp#serverTransferProhibited
Domain Status: serverUpdateProhibited https://www.icann.org/epp#serverUpdateProhibited
Registry Registrant ID:
Registrant Name: Domain Admin
Registrant Organization: Facebook, Inc.
Registrant Street: 1601 Willow Rd
Registrant City: Menlo Park
Registrant State/Province: CA
Registrant Postal Code: 94025
Registrant Country: US
Registrant Phone: +1.6505434800
Registrant Phone Ext:
Registrant Fax: +1.6505434800
Registrant Fax Ext:
Registrant Email: domain@fb.com
Registry Admin ID:
Admin Name: Domain Admin
Admin Organization: Facebook, Inc.
Admin Street: 1601 Willow Rd
Admin City: Menlo Park
Admin State/Province: CA
Admin Postal Code: 94025
Admin Country: US
Admin Phone: +1.6505434800
Admin Phone Ext:
Admin Fax: +1.6505434800
Admin Fax Ext:
Admin Email: domain@fb.com
Registry Tech ID:
Tech Name: Domain Admin
Tech Organization: Facebook, Inc.
Tech Street: 1601 Willow Rd
Tech City: Menlo Park
Tech State/Province: CA
Tech Postal Code: 94025
Tech Country: US
Tech Phone: +1.6505434800
Tech Phone Ext:
Tech Fax: +1.6505434800
Tech Fax Ext:
Tech Email: domain@fb.com
Name Server: C.NS.FACEBOOK.COM
Name Server: B.NS.FACEBOOK.COM
Name Server: A.NS.FACEBOOK.COM
Name Server: D.NS.FACEBOOK.COM
DNSSEC: unsigned
<SNIP>
```

	C:\htb> whois.exe facebook.com

```text
Whois v1.21 - Domain information lookup
Copyright (C) 2005-2019 Mark Russinovich
Sysinternals - www.sysinternals.com

Connecting to COM.whois-servers.net...

WHOIS Server: whois.registrarsafe.com
   Registrar URL: http://www.registrarsafe.com
   Updated Date: 2021-09-22T19:33:41Z
   Creation Date: 1997-03-29T05:00:00Z
   Registry Expiry Date: 2030-03-30T04:00:00Z
   Registrar: RegistrarSafe, LLC
   Registrar IANA ID: 3237
   Registrar Abuse Contact Email: abusecomplaints@registrarsafe.com
   Registrar Abuse Contact Phone: +1-650-308-7004
   Domain Status: clientDeleteProhibited https://icann.org/epp#clientDeleteProhibited
   Domain Status: clientTransferProhibited https://icann.org/epp#clientTransferProhibited
   Domain Status: clientUpdateProhibited https://icann.org/epp#clientUpdateProhibited
   Domain Status: serverDeleteProhibited https://icann.org/epp#serverDeleteProhibited
   Domain Status: serverTransferProhibited https://icann.org/epp#serverTransferProhibited
   Domain Status: serverUpdateProhibited https://icann.org/epp#serverUpdateProhibited
   Name Server: A.NS.FACEBOOK.COM
   Name Server: B.NS.FACEBOOK.COM
   Name Server: C.NS.FACEBOOK.COM
   Name Server: D.NS.FACEBOOK.COM
   DNSSEC: unsigned
   URL of the ICANN Whois Inaccuracy Complaint Form: https://www.icann.org/wicf/
>>> Last update of whois database: 2021-10-11T06:03:10Z <<<
<SNIP>
```

### Lookup MNT-REF

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

## References

https://www.internic.net/whois.html
https://domain.glass/