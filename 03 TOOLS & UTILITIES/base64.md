# ⚙️ base64

Tags: #⚙️
Related to:
See also:
Previous:

## Description

base64 encode/decode data and print to standard output.

## Usage Examples

### Encode a binary shell to transfer it to another system

	base64 shell -w 0

```text
f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU
```

Now, we can copy this `base64` string, go to the remote host, and use `base64 -d` to decode it, and pipe the output into a file:

```text
echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > shell
```

# References