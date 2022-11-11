# ⚙️ du
Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

---
## Description

Estimate file space usage.

## Usage Examples

### Build chisel

	git clone https://github.com/jpillora/chisel.git
	cd chisel
	go build		// from within git cloned directory
	du -hs chisel	// 11M

Build smaller:

	go build -ldflags="-s -w"
	du -hs chisel	// 7.8M chisel

```
-s	// disable symbol table
-w	// disable DWARF generation
```

Pack it smaller:

	upx brute chisel
	du -hs chisel	// 3.0M chisel

```
brute	// Quickly get the best compression ratio
```


### Get human readable summary of file size

	du -hs chisel	// 11M chisel

```
-h	// print sizes in human readable format (e.g., 1K 234M 2G)
-s	// display only a total for each argument
```
	
---
## References
- [[]]