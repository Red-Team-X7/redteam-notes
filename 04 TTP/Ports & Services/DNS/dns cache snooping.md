# 🔥 dns cache snooping

Tags: #🔥 
Related to: 
See also: [[dns zone transfer]], [[nslookup]]
Previous: [[TTP]]

## Description

## Usage Examples

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


# References

http://blog.commandlinekungfu.com/2009/03/episode-17-dns-cache-snooping-in-single.html