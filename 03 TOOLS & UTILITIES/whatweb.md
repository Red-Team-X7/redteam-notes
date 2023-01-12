# 💢 whatweb

Tags: #💢
Related to: 
See also: [[wappalyzer]]
Previous: [[Web Vulnerability Scanners]], [[Getting Started]], [[Information Gathering - Web Edition]]

## Description

Next generation Web scanner. Identify technologies used by websites.

## Usage Examples

### Help

	whatweb -h

```text
.$$$     $.                                   .$$$     $.                                                                                                                                                                                   
$$$$     $$. .$$$  $$$ .$$$$$$.  .$$$$$$$$$$. $$$$     $$. .$$$$$$$. .$$$$$$.                                                                                                                                                               
$ $$     $$$ $ $$  $$$ $ $$$$$$. $$$$$ $$$$$$ $ $$     $$$ $ $$   $$ $ $$$$$$.                                                                                                                                                              
$ `$     $$$ $ `$  $$$ $ `$  $$$ $$' $ `$ `$$ $ `$     $$$ $ `$      $ `$  $$$'                                                                                                                                                             
$. $     $$$ $. $$$$$$ $. $$$$$$ `$  $. $  :' $. $     $$$ $. $$$$   $. $$$$$.                                                                                                                                                              
$::$  .  $$$ $::$  $$$ $::$  $$$     $::$     $::$  .  $$$ $::$      $::$  $$$$                                                                                                                                                             
$;;$ $$$ $$$ $;;$  $$$ $;;$  $$$     $;;$     $;;$ $$$ $$$ $;;$      $;;$  $$$$                                                                                                                                                             
$$$$$$ $$$$$ $$$$  $$$ $$$$  $$$     $$$$     $$$$$$ $$$$$ $$$$$$$$$ $$$$$$$$$'                                                                                                                                                             
                                                                                                                                                                                                                                            
                                                                                                                                                                                                                                            
WhatWeb - Next generation web scanner version 0.5.5.
Developed by Andrew Horton (urbanadventurer) and Brendan Coles (bcoles).
Homepage: https://www.morningstarsecurity.com/research/whatweb

Usage: whatweb [options] <URLs>

TARGET SELECTION:
  <TARGETs>                     Enter URLs, hostnames, IP addresses, filenames or
                                IP ranges in CIDR, x.x.x-x, or x.x.x.x-x.x.x.x
                                format.
  --input-file=FILE, -i         Read targets from a file. You can pipe
                                hostnames or URLs directly with -i /dev/stdin.

TARGET MODIFICATION:
  --url-prefix                  Add a prefix to target URLs.
  --url-suffix                  Add a suffix to target URLs.
  --url-pattern                 Insert the targets into a URL.
                                e.g. example.com/%insert%/robots.txt

AGGRESSION:
The aggression level controls the trade-off between speed/stealth and
reliability.
  --aggression, -a=LEVEL        Set the aggression level. Default: 1.
  1. Stealthy                   Makes one HTTP request per target and also
                                follows redirects.
  3. Aggressive                 If a level 1 plugin is matched, additional
                                requests will be made.
  4. Heavy                      Makes a lot of HTTP requests per target. URLs
                                from all plugins are attempted.

HTTP OPTIONS:
  --user-agent, -U=AGENT        Identify as AGENT instead of WhatWeb/0.5.5.
<...snip...>
```

### Aggressive Scan

	whatweb -a3 https://www.facebook.com -v

```text
WhatWeb report for https://www.facebook.com
Status    : 200 OK
Title     : <None>
IP        : 31.13.92.36
Country   : IRELAND, IE

Summary   : Strict-Transport-Security[max-age=15552000; preload], PasswordField[pass], Script[text/javascript], X-XSS-Protection[0], HTML5, X-Frame-Options[DENY], Meta-Refresh-Redirect[/?_fb_noscript=1], UncommonHeaders[x-fb-rlafr,x-content-type-options,x-fb-debug,alt-svc]

Detected Plugins:
[ HTML5 ]
	HTML version 5, detected by the doctype declaration


[ Meta-Refresh-Redirect ]
	Meta refresh tag is a deprecated URL element that can be
	used to optionally wait x seconds before reloading the
	current page or loading a new page. More info:
	https://secure.wikimedia.org/wikipedia/en/wiki/Meta_refresh

	String       : /?_fb_noscript=1

[ PasswordField ]
	find password fields

	String       : pass (from field name)

[ Script ]
	This plugin detects instances of script HTML elements and
	returns the script language/type.

	String       : text/javascript

[ Strict-Transport-Security ]
	Strict-Transport-Security is an HTTP header that restricts
	a web browser from accessing a website without the security
	of the HTTPS protocol.

	String       : max-age=15552000; preload

[ UncommonHeaders ]
	Uncommon HTTP server headers. The blacklist includes all
	the standard headers and many non standard but common ones.
	Interesting but fairly common headers should have their own
	plugins, eg. x-powered-by, server and x-aspnet-version.
	Info about headers can be found at www.http-stats.com

	String       : x-fb-rlafr,x-content-type-options,x-fb-debug,alt-svc (from headers)

[ X-Frame-Options ]
	This plugin retrieves the X-Frame-Options value from the
	HTTP header. - More Info:
	http://msdn.microsoft.com/en-us/library/cc288472%28VS.85%29.
	aspx

	String       : DENY

[ X-XSS-Protection ]
	This plugin retrieves the X-XSS-Protection value from the
	HTTP header. - More Info:
	http://msdn.microsoft.com/en-us/library/cc288472%28VS.85%29.
	aspx

	String       : 0

HTTP Headers:
	HTTP/1.1 200 OK
	Vary: Accept-Encoding
	Content-Encoding: gzip
	x-fb-rlafr: 0
	Pragma: no-cache
	Cache-Control: private, no-cache, no-store, must-revalidate
	Expires: Sat, 01 Jan 2000 00:00:00 GMT
	X-Content-Type-Options: nosniff
	X-XSS-Protection: 0
	X-Frame-Options: DENY
	Strict-Transport-Security: max-age=15552000; preload
	Content-Type: text/html; charset="utf-8"
	X-FB-Debug: r2w+sMJ7lVrMjS/ETitC6cNpJXma0r3fbt0rIlnTPAfQqTc+U4PQopVL7sR/6YA/ZKRkqP1wMPoFdUfMBP1JSA==
	Date: Wed, 06 Oct 2021 09:04:27 GMT
	Alt-Svc: h3=":443"; ma=3600, h3-29=":443"; ma=3600,h3-27=":443"; ma=3600
	Connection: close

WhatWeb report for https://www.facebook.com/?_fb_noscript=1
Status    : 200 OK
Title     : <None>
IP        : 31.13.92.36
Country   : IRELAND, IE

Summary   : Cookies[noscript], Strict-Transport-Security[max-age=15552000; preload], PasswordField[pass], Script[text/javascript], X-XSS-Protection[0], HTML5, X-Frame-Options[DENY], UncommonHeaders[x-fb-rlafr,x-content-type-options,x-fb-debug,alt-svc]

Detected Plugins:
[ Cookies ]
	Display the names of cookies in the HTTP headers. The
	values are not returned to save on space.

	String       : noscript

[ HTML5 ]
	HTML version 5, detected by the doctype declaration


[ PasswordField ]
	find password fields

	String       : pass (from field name)

[ Script ]
	This plugin detects instances of script HTML elements and
	returns the script language/type.

	String       : text/javascript

[ Strict-Transport-Security ]
	Strict-Transport-Security is an HTTP header that restricts
	a web browser from accessing a website without the security
	of the HTTPS protocol.

	String       : max-age=15552000; preload

[ UncommonHeaders ]
	Uncommon HTTP server headers. The blacklist includes all
	the standard headers and many non standard but common ones.
	Interesting but fairly common headers should have their own
	plugins, eg. x-powered-by, server and x-aspnet-version.
	Info about headers can be found at www.http-stats.com

	String       : x-fb-rlafr,x-content-type-options,x-fb-debug,alt-svc (from headers)

[ X-Frame-Options ]
	This plugin retrieves the X-Frame-Options value from the
	HTTP header. - More Info:
	http://msdn.microsoft.com/en-us/library/cc288472%28VS.85%29.
	aspx

	String       : DENY

[ X-XSS-Protection ]
	This plugin retrieves the X-XSS-Protection value from the
	HTTP header. - More Info:
	http://msdn.microsoft.com/en-us/library/cc288472%28VS.85%29.
	aspx

	String       : 0

HTTP Headers:
	HTTP/1.1 200 OK
	Vary: Accept-Encoding
	Content-Encoding: gzip
	Set-Cookie: noscript=1; path=/; domain=.facebook.com; secure
	x-fb-rlafr: 0
	Pragma: no-cache
	Cache-Control: private, no-cache, no-store, must-revalidate
	Expires: Sat, 01 Jan 2000 00:00:00 GMT
	X-Content-Type-Options: nosniff
	X-XSS-Protection: 0
	X-Frame-Options: DENY
	Strict-Transport-Security: max-age=15552000; preload
	Content-Type: text/html; charset="utf-8"
	X-FB-Debug: 7bEryjJ3tsTb/ap562d5L6KUJyJJ3bJh9XoamIo2lCVrX4cK/VAGbLx7muaAwnyobVm9myC3fQ+CXJqkk0eacg==
	Date: Wed, 06 Oct 2021 09:04:31 GMT
	Alt-Svc: h3=":443"; ma=3600, h3-29=":443"; ma=3600,h3-27=":443"; ma=3600
	Connection: close
```

# References