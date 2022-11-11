# 💢 dnsenum
Tags: #💢
Related to:
See also:
Previous: [[DNS Analysis]], [[Footprinting]]

## Description

Dnsenum is a multithreaded perl script to enumerate DNS information of a domain and to discover non-contiguous ip blocks. The main purpose of Dnsenum is to gather as much information as possible about a domain. The program currently performs the following operations:

## Usage Examples

###  Bruteforce subdomain

	dnsenum --dnsserver <nameserver> --enum -p 0 -s 0 -o found_subdomains.txt -f ~/subdomains.list <domain.tld>

# References