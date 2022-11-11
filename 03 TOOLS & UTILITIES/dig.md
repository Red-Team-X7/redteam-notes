# ⚙️ dig

Tags: #⚙️
Related to:
See also: [[dns zone transfer]], [[dns cache snooping]], [[whois]]
Previous: [[Footprinting]]

## Description

DNS lookup utility.

## Usage Examples

### NS request to the specific nameserver

	dig ns <domain.tld> @<nameserver>

### ANY request to the specific nameserver

	dig any <domain.tld> @<nameserver>

### AXFR request to the specific nameserver

	dig axfr <domain.tld> @<nameserver>

### IXFR request to the specific nameserver

	dig ixfr <domain.tld> @<nameserver>
  
# References