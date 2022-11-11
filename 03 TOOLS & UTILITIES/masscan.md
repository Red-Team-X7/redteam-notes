# 💢 masscan
Tags: #💢
Related to: 
See also: 
Previous: [[Live Host Identification]]

---
## Description
This is the fastest Internet port scanner. It can scan the entire Internet in under 6 minutes, transmitting 10 million packets per second.

It produces results similar to nmap, the most famous port scanner. Internally, it operates more like scanrand, unicornscan, and ZMap, using asynchronous transmission. The major difference is that it’s faster than these other scanners. In addition, it’s more flexible, allowing arbitrary address ranges and port ranges.

NOTE: masscan uses a custom TCP/IP stack. Anything other than simple port scans will cause conflict with the local TCP/IP stack. This means you need to either use the -S option to use a separate IP address, or configure your operating system to firewall the ports that masscan uses.

## Usage Examples
### Scan subnet for specified ports
	masscan -p22,80,445 192.168.1.0/24

### Use binary file format to save space with large scans
	masscan -p0-65535 --rate 15000 --output-format binary --output-filename full.mass 10.0.0.0/8

### Convert binary format to other formats
	masscan --read-scan full.mass --output-format xml --output-filename full.xml

---
## References
- https://github.com/robertdavidgraham/masscan