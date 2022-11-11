# 💢 snmpwalk

Tags:
Related to:
See also:
Previous: [[SNMP Analysis]], [[Getting Started]], [[Footprinting]]

## Description

snmpwalk is an SNMP application that uses SNMP GETNEXT requests to query a network entity for a tree of information.

## Usage Examples

### Scan SNMP on an IP

	snmpwalk -v 2c -c public 10.129.42.253 1.3.6.1.2.1.1.5.0	

```shell-session
iso.3.6.1.2.1.1.5.0 = STRING: "gs-svcscan"
```

	snmpwalk -v 2c -c private  10.129.42.253 

```shell-session
Timeout: No Response from 10.129.42.253
```

### Query OIDs

	snmpwalk -v2c -c <community string> <FQDN/IP>

# References