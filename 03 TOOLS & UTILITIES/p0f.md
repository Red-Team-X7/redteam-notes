# 💢 p0f 

Tags: 
Related to: 
See also: 
Previous: [[ ]]

## Description
Passive OS fingerprinting tool.

P0f is a tool that utilizes an array of sophisticated, purely passive traffic fingerprinting mechanisms to identify the players behind any incidental TCP/IP communications (often as little as a single normal SYN) without interfering in any way. Version 3 is a complete rewrite of the original codebase, incorporating a significant number of improvements to network-level fingerprinting, and introducing the ability to reason about application-level payloads (e.g., HTTP).

## Usage Examples

### Promiscuous mode
	p0f -i eth0 -p -o /tmp/p0f.log

# References