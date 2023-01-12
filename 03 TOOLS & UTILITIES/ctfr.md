# 💢 ctfr

Tags: #💢
Related to: 
See also: 
Previous: [[DNS Analysis]]

## Description

Do you miss AXFR technique? This tool allows to get the subdomains from a HTTPS website in a few seconds. How does it work? CTFR does not use neither dictionary attack nor brute-force, it just abuses of Certificate Transparency logs.

## Usage Examples

### Install

	git clone https://github.com/UnaPibaGeek/ctfr.git

### Get subdomains

	python3 ctfr.py -d starbucks.com

```text
          ____ _____ _____ ____  
         / ___|_   _|  ___|  _ \ 
        | |     | | | |_  | |_) |
        | |___  | | |  _| |  _ < 
         \____| |_| |_|   |_| \_\

     Version 1.2 - Hey don't miss AXFR!
    Made by Sheila A. Berta (UnaPibaGeek)


[!] ---- TARGET: starbucks.com ---- [!]
<...snip...>
scm.starbucks.com
[-]  *.scmdev.starbucks.com
[-]  *.scmdev.starbucks.com
scmdev.starbucks.com
[-]  *.scmtest.starbucks.com
scmtest.starbucks.com
[-]  *.starbucks.com
[-]  *.starbucks.com
starbucks.com
[-]  *.stories.starbucks.com
stories.starbucks.com
[-]  *.storiesadmin.starbucks.com
storiesadmin.starbucks.com
[-]  *.storiesapi.starbucks.com
storiesapi.starbucks.com
[-]  *.test.starbucks.com
[-]  *.test.starbucks.com
*.test.starbucks.com.br
[-]  ArcherGRC.starbucks.com
[-]  ChdLyncConf01.Starbucks.com
ChdLyncEdge01.Starbucks.com
[-]  ChdLyncConf01.Starbucks.com
ChdLyncEdge01.Starbucks.com
sip.starbucks.com
starbucks.com
[-]  ChdLyncWeb01.Starbucks.com
dialin.starbucks.com
Lyncdiscover.starbucks.com
meet.starbucks.com
[-]  ChdLyncWebApp01.Starbucks.com
[-]  ChdLyncWebApp01.starbucks.com
[-]  CiscoSpark.starbucks.com
[-]  Enterprise.Loyalty.API.starbucks.com
[-]  Ext.starbucks.com
Ldap-ext.ext.starbucks.com
ldap-ext-prod-chd.ext.starbucks.com
ldap-ext-prod-iad.ext.starbucks.com
Ldap.starbucks.com
MS04157.ext.starbucks.com
[-]  Ext.starbucks.com
Ldap-ext.ext.starbucks.com
ldap-ext-prod-chd.ext.starbucks.com
ldap-ext-prod-iad.ext.starbucks.com
Ldap.starbucks.com
MS04158.ext.starbucks.com
[-]  Globalloadsecureui.starbucks.com
loadsecureui.starbucks.com.br
[-]  Globalsecureui.starbucks.com
secureui.starbucks.com.br
[-]  Globalstagesecureui.starbucks.com
stagesecureui.starbucks.com.br
<...snip...>
```

# References

http://www.certificate-transparency.org/
https://crt.sh/