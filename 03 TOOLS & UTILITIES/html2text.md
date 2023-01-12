# ⚙️ html2text

Tags: #⚙️
Related to: [[singlefile]], [[onehistory]]  ,[[html2text]]
See also:
Previous: [[Hacking Wordpress]], [[OSINT - Corporate Recon]], [[OSINT]]

## Description

An advanced HTML-to-text converter.

## Usage Examples

### Convert the HTML output to a nice readable format

	curl -s -X GET http://blog.inlanefreight.com/wp-content/plugins/mail-masta/ | html2text

```text
****** Index of /wp-content/plugins/mail-masta ******
[[ICO]]       Name                 Last_modified    Size Description
===========================================================================
[[PARENTDIR]] Parent_Directory                         -  
[[DIR]]       amazon_api/          2020-05-13 18:01    -  
[[DIR]]       inc/                 2020-05-13 18:01    -  
[[DIR]]       lib/                 2020-05-13 18:01    -  
[[   ]]       plugin-interface.php 2020-05-13 18:01  88K  
[[TXT]]       readme.txt           2020-05-13 18:01 2.2K  
===========================================================================
     Apache/2.4.29 (Ubuntu) Server at blog.inlanefreight.com Port 80
```

### Download Website and Extract Information

	cat *.html | html2text | grep "Emma Williams"

```text
Emma Williams  emma.williams@inlanefreight.com
```

# References