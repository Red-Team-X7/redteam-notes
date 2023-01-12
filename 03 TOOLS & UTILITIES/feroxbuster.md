# 💢 feroxbuster

Tags: #💢
Related to: 
See also: [[gobuster]]
Previous: [[Web Crawlers & Directory Bruteforce]]

## Description

feroxbuster is a tool designed to perform Forced Browsing. Forced browsing is an attack where the aim is to enumerate and access resources that are not referenced by the web application, but are still accessible by an attacker. feroxbuster uses brute force combined with a wordlist to search for unlinked content in target directories. These resources may store sensitive information about web applications and operational systems, such as source code, credentials, internal network addressing, etc… This attack is also known as Predictable Resource Location, File Enumeration, Directory Enumeration, and Resource Enumeration.

## Usage Examples

### Enumerate files and directories

	feroxbuster -k -u https://streamio.htb -x php -o streamio.htb.feroxbuster -w raft-medium-directories-lowercase.txt 

# References