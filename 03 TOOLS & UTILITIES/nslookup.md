# ⚙️ nslookup
Tags: #⚙️ 
Related to: 
See also: [[dns zone transfer]] [[dns cache snooping]], [[whois]]
Previous: [[ ]]

---
## Description
Query Internet name servers interactively.

## Usage Examples

### DNS Zone Transfer
	nslookup
	
#### Resolve a name or IP
	[name or IP addr]  
    
#### Use a different DNS server
	server [serverIPaddr or name]  
    
#### Say we're interested in all types of records
	set type=any  
    
#### Perform a zone transfer of all records for a given domain and store output
	ls -d [target_domain] [> filename]  
    
#### View file
	view [filename]

### DNS Cache Snooping
	nslookup  
  	set norecurse  
	www.counterhack.com http://www.counterhack.com
	set recurse  
	www.counterhacker.com http://www.counterhacker.com 
	set norecurse  
  
  	C:\> for /F %i in (names.txt) do @echo %i & nslookup -norecurse %i [DNSserver] | find "answer" & echo.

	for i in `cat names.txt`; do host -r $i [nameserver]; done  
	rndc dumpdb -cache  
	lsof -a -c named -d cwd

---
## References
- http://blog.commandlinekungfu.com/2009/03/episode-17-dns-cache-snooping-in-single.html