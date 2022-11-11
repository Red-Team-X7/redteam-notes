# ⚙️ braa

Tags: #⚙️
Related to:
See also:
Previous: [[Footprinting]]

## Description

Braa is a mass snmp scanner. The intended usage of such a tool is of course making SNMP queries - but unlike snmpget or snmpwalk from net-snmp, it is able to query dozens or hundreds of hosts simultaneously, and in a single process. Thus, it consumes very few system resources and does the scanning VERY fast.

## Usage Examples

### Bruteforce SNMP service OIDs

	braa <community string>@<FQDN/IP>:.1.*

# References