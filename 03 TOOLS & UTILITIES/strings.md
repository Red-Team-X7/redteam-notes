# ⚙️ strings
Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

---
## Description

Print the sequences of printable characters in files.

## Usage Examples

### Search binary for strings

	strings server.exe | grep -A3 Access	// "Access" would have been shown from the nc connection

```
-A NUM, --after-context=NUM
              Print NUM lines of trailing context  after  matching  lines.   Places  a  line  containing  a  group
              separator  (--)  between  contiguous groups of matches.  With the -o or --only-matching option, this
              has no effect and a warning is given.
```

```
Enter Access Name: 
Admin
Access Password: 
Wrong username!
P@$$worD
Correct Password!
```
	
---
## References
- [[]]