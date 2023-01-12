# 🔥 google dorks

Tags: #🔥 
Related to: 
See also: 
Previous: [[TACTICS]]


## Description

## Cheatsheet

| **Dork** | **Description** |
|-|-|
| `cache:securitytrails.com` | this dork will show you the cached version of any website |
| `allintext:hacking tools` | searches for specific text contained on any web page |
| `allintitle:"Security Companies"` | exactly the same as `allintext`, but will show pages that contain titles with X characters |
| `allinurl:clientarea` | it can be used to fetch results whose URL contains all the specified characters |
| `inurl:admin` | this is exactly the same as `allinurl`, but it is only useful for one single keyword |
| `filetype:email security filetype: pdf` | used to search for any kind of file extensions |
| `intitle:security tools` | used to search for various keywords inside the title, for example, it will search for titles beginning with "security" but "tools" can be somewhere else in the page |
| `inanchor:"cyber security"` | this is useful when you need to search for an exact anchor text used on any links |
| `intext:"safe internet"` | useful to locate pages that contain certain characters or strings inside their text |
| `site:securitytrails.com` | will show you the full list of all indexed URLs for the specified domain and subdomain |
| `how to * a website` | wildcard used to search pages that contain "anything" before your word, e.g. , will return "how to…" design/create/hack, etc… "a website" |
| `"security" "tips"` | this is a logical operator, e.g.  will show all the sites which contain "security" or "tips," or both words |
| `security + trails` | used to concatenate words, useful to detect pages that use more than one specific key |
| `security -trails` | minus operator is used to avoiding showing results that contain certain words |

## Usage Examples


### Log files

	allintext:username filetype:log

### Vulnerable web servers

	inurl:/proc/self/cwd

### Open FTP servers

	intitle:"index of" inurl:ftp

### ENV files

	DB_USERNAME filetype:env

### SSH private keys

	intitle:index.of id_rsa -id_rsa.pub
	filetype:log username putty

### Email lists

	filetype:xls inurl:"email.xls"
	site:.edu filetype:xls inurl:"email.xls"

### Live cameras

	inurl:top.htm inurl:currenttime
	intitle:"webcamXP 5"
	inurl:"lvappl.htm"

### MP3, Movie, and PDF files

	intitle:index of mp3
	intitle:index of pdf intext: .mp4

### Weather

	intitle:"Weather Wing WS-2"

### Zoom videos

	inurl:zoom.us/j and intext:scheduled for

### SQL dumps

	"index of" "database.sql.zip"

### WordPress Admin

	intitle:"Index of" wp-admin

### Apache2

	intitle:"Apache2 Ubuntu Default Page: It works"

### phpMyAdmin

	"Index of" inurl:phpmyadmin

### JIRA/Kibana

	inurl:Dashboard.jspa intext:"Atlassian Jira Project Management Software"
	inurl:app/kibana intext:Loading Kibana

### cPanel password reset

	inurl:_cpanel/forgotpwd

### Government documents

	allintitle: restricted filetype:doc site:gov

# Resource

https://securitytrails.com/blog/google-hacking-techniques