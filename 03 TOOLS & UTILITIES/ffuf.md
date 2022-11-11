# 💢 ffuf 

Tags: #💢 
Related to: 
See also: 
Previous: [[Web Application Analysis]]

## Description

Fuzz Faster U Fool.

## Usage Examples

### Enumerate files and folders

	ffuf -u http://10.129.1.145/FUZZ -w /usr/share/wordlists/dirb/common.txt -mc 200,204,301,302,307,401 -o ffuf.txt
	
	-u	// target url
	-w	// wordlist
	-mc	// match HTTP status codes, or "all" for everything. (default: 200,204,301,302,307,401,403)
	-o	// write output to file


# References
https://github.com/ffuf/ffuf
https://codingo.io/tools/ffuf/bounty/2020/09/17/everything-you-need-to-know-about-ffuf.html

