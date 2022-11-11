# ⚙️ sum
Tags: #⚙️
Related to:
See also:
Previous:

## Description

Compute and check message digests.

## Usage Examples

### Validate file format and integrity 

	file shell

```shell-session
shell: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, no section header
```

	md5sum shell

```shell-session
321de1d7e7c3735838890a72c9ae7d1d shell
```

### Verify SHA-256 sum

	echo "4246a77b6ca2a2844749437d1a441fc759c6b8ec316187647cd9b1019da6f6fc Eternal Loop.zip" | sha256sum -c -

```shell-session
Eternal Loop.zip: OK
```

# References