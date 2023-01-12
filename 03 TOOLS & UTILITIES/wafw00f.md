# 💢 wafw00f

Tags: #💢
Related to: 
See also: 
Previous: [[IDS & IPS Identification]], [[Information Gathering - Web Edition]]

## Description

Identify and fingerprint Web Application Firewall products.

## Usage Examples

| **Command** | **Description** |
|-|-|
| `-a`, `--findall` | Find all WAFs, do not stop testing on the first one |
| `-i`, `--input` | Read targets from a file. Input format can be csv, json or text |
| `-p`, `--proxy` | Use an HTTP proxy to perform requests |

	wafw00f -v https://www.tesla.com

```text
                   ______
                  /      \
                 (  Woof! )
                  \  ____/                      )
                  ,,                           ) (_
             .-. -    _______                 ( |__|
            ()``; |==|_______)                .)|__|
            / ('        /|\                  (  |__|
        (  /  )        / | \                  . |__|
         \(_)_))      /  |  \                   |__|

                    ~ WAFW00F : v2.2.0 ~
    The Web Application Firewall Fingerprinting Toolkit
    
[*] Checking https://www.tesla.com
[+] The site https://www.tesla.com is behind CacheWall (Varnish) WAF.
[~] Number of requests: 2
```

# References