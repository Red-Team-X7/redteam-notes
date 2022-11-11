# ⚙️ xxd

Tags: #⚙️
Related to:
See also:
Previous:

---
## Description

Make a hexdump or do the reverse.

## Usage Examples

### Reverse hex dump
	cat 1.txt | xxd -r > 2.txt


### Remove bad UNICODE character from the beginning of a script

Script: Sherlock.ps1

==<U+FFFF>==
```
	<#

		File: Sherlock.ps1
		Author: @_RastaMouse
		License: GNU General Public License v3.0

	#>

	$Global:ExploitTable = $null

	function Get-FileVersionInfo ($FilePath) {

		$VersionInfo = (Get-Item $FilePath).VersionInfo
		$FileVersion = ( "{0}.{1}.{2}.{3}" -f $VersionInfo.FileMajorPart, $VersionInfo.FileMinorPart, $VersionInfo.FileBuildPart, $VersionInfo.FilePrivatePart )

		return $FileVersion

	}
```

#### Output in postscript plain hexdump style

	xxd -ps Sherlock.ps1 > Sherlock.ps1.hex

	efbbb3c230a0a2020202046696c653a20536865726c6f636b2e7073310a2
	20417574686f723a20405f52617374614d6f7573650a202020204c696365
	6e73653a20474e552047656e6572616c205075626c6963204c6963656e73
	652076332e300a0a233e0a0a24476c6f62616c3a4578706c6f6974546162
	6c65203d20246e756c6c0a0a66756e6374696f6e204765742d46696c6556
	657273696f6e496e666f20282446696c655061746829207b0a0a20202020
	2456657273696f6e496e666f203d20284765742d4974656d202446696c65
	50617468292e56657273696f6e496e666f0a202020202446696c65566572
	73696f6e203d202820227b307d2e7b317d2e7b327d2e7b337d22202d6620
	2456657273696f6e496e666f2e46696c654d616a6f72506172742c202456
	657273696f6e496e666f2e46696c654d696e6f72506172742c2024566572
	73696f6e496e666f2e46696c654275696c64506172742c20245665727369
	6f6e496e666f2e46696c65507269766174655061727420290a0a20202020
	72657475726e202446696c6556657273696f6e0a0a7d0a...

#### Delete the beginning 6 characters (in vi for example), and reverse the operation.

	xxd -r -ps Sherlock.ps1.hex > Sherlock.ps1

---
### Hex encode

	echo https://www.hackthebox.eu/ | xxd -p

```shell-session
68747470733a2f2f7777772e6861636b746865626f782e65752f0a
```

### Hex decode

	echo 68747470733a2f2f7777772e6861636b746865626f782e65752f0a | xxd -p -r

```shell-session
https://www.hackthebox.eu/
```

# References