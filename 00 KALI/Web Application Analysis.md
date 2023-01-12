# 😈 Web Application Analysis

Tags: #😈
Related to: 
See also: 
Previous: [[KALI]]

[[CMS & Framework Identification]]
[[Web Application Proxies]]
[[Web Crawlers & Directory Bruteforce]]
[[Web Vulnerability Scanners]]

[[burpsuite]]
[[commix]]
[[skipfish]]
[[sqlmap]]
[[wpscan]]
[[zap]]

[[ffuf cewl]]
[[payloadallthethings]]
[[aquatone]]
[[wappalyzer]]

## OWASP Top 10

|Number|Category|Description|
|:----|:----|:----|
|1|Broken Access Control|Restrictions are not appropriately implemented to prevent users from accessing other users accounts, viewing sensitive data, accessing unauthorized functionality, modifying data, etc.|
|2|Cryptographic Failures|Failures related to cryptography which often leads to sensitive data exposure or system compromise.|
|3|Injection|User-supplied data is not validated, filtered, or sanitized by the application. Some examples of injections are SQL injection, command injection, LDAP injection, etc.|
|4|Insecure Design|These issues happen when the application is not designed with security in mind.|
|5|Security Misconfiguration|Missing appropriate security hardening across any part of the application stack, insecure default configurations, open cloud storage, verbose error messages which disclose too much information.|
|6|Vulnerable and Outdated Components|Using components (both client-side and server-side) that are vulnerable, unsupported, or out of date.|
|7|Identification and Authentication Failures|Authentication-related attacks that target user's identity, authentication, and session management.|
|8|Software and Data Integrity Failures|Software and data integrity failures relate to code and infrastructure that does not protect against integrity violations. An example of this is where an application relies upon plugins, libraries, or modules from untrusted sources, repositories, and content delivery networks (CDNs).|
|9|Security Logging and Monitoring Failures|This category is to help detect, escalate, and respond to active breaches. Without logging and monitoring, breaches cannot be detected..|
|10|Server-Side Request Forgery|SSRF flaws occur whenever a web application is fetching a remote resource without validating the user-supplied URL. It allows an attacker to coerce the application to send a crafted request to an unexpected destination, even when protected by a firewall, VPN, or another type of network access control list (ACL).|


# References

https://wpvulndb.com/wordpresses/541 
https://owasp.org/www-project-top-ten/