# ⚙️ braa

Tags: #⚙️
Related to:
See also: [[snmpwalk]] , [[onesixtyone]]
Previous: [[Footprinting]]

## Description

Braa is a mass snmp scanner. The intended usage of such a tool is of course making SNMP queries - but unlike snmpget or snmpwalk from net-snmp, it is able to query dozens or hundreds of hosts simultaneously, and in a single process. Thus, it consumes very few system resources and does the scanning VERY fast.

## Usage Examples

### Bruteforce community strings of the SNMP service

	onesixtyone -c community-strings.list <FQDN/IP>
	onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp.txt 10.129.218.7

```text
Scanning 1 hosts, 3220 communities
10.129.218.7 [backup] Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
```

### Bruteforce SNMP service OIDs

	braa <community string>@<FQDN/IP>:.1.*
	braa backup@10.129.218.7:.1.*

```text
10.129.218.7:89ms:.0:Linux NIXHARD 5.4.0-90-generic #101-Ubuntu SMP Fri Oct 15 20:00:55 UTC 2021 x86_64
10.129.218.7:289ms:.0:.10
10.129.218.7:109ms:.0:210419
10.129.218.7:109ms:.0:Admin <tech@inlanefreight.htb>
10.129.218.7:690ms:.0:NIXHARD
10.129.218.7:134ms:.0:Inlanefreight
10.129.218.7:91ms:.0:72
10.129.218.7:125ms:.0:19
10.129.218.7:99ms:.1:.1
10.129.218.7:89ms:.2:.1
<...snip...>
```

# References