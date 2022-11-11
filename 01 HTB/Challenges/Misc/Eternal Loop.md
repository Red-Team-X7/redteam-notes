# 🧩 Eternal Loop

Tags: #🧩
Related to: [[sum]], [[unzip]], [[john]], [[sqlitebrowser]], [[head]]
See also:
Previous: [[HTB]]

# Description

Can you find a way out of this loop?

## Validate checksum

	echo "4246a77b6ca2a2844749437d1a441fc759c6b8ec316187647cd9b1019da6f6fc Eternal Loop.zip" | sha256sum -c -

```shell-session
Eternal Loop.zip: OK
```

## Unzip

	unzip unzip Eternal\ Loop.zip
	tree

```shell-session
.
├── 37366.zip
```

## Explore

### Unzip archive (it's password protected)

	unzip 37366.zip

```shell-session
Archive:  37366.zip
[37366.zip] 5900.zip password:
```

### Create a hashfile and crack with john

	john 37366.zip.hash

```shell-session
5900    (37366.zip/5900.zip)     
```

>Note: The password is the same as the filename of the contained zip (5900).

	unzip 37366.zip

```shell-session
Archive:  37366.zip
[37366.zip] 5900.zip password: 5900
  inflating: 5900.zip
```

### Unzip archive (use contained zip filename as password)

	unzip 5900.zip

```shell-session
Archive:  5900.zip
[5900.zip] 49805.zip password: 49805
  inflating: 49805.zip
```

### Unzip archive using password flag (-P)

Get the contained zip filename:

	unzip -l 49805.zip

```shell-session
13811.zip
```

	unzip -P 13811 49805.zip

```shell-session
Archive:  49805.zip
  inflating: 13811.zip
```

## Automate

### Unzip recursively

	cat unzipr.sh

```bash
#!/bin/bash

ZIPFILE=$1
RESULT=0

while [ $RESULT -eq 0 ]
do
	PASSWORD=$( unzip -l $ZIPFILE | grep -E "^\s+[0-9]+" | grep -Eo "[0-9]+\.zip" | grep -Eo "[0-9]+" )
	unzip -P "$PASSWORD" "$ZIPFILE"
	RESULT=$?
	echo "Unzipped $ZIPFILE using password $PASSWORD ($RESULT)"
	ZIPFILE="$PASSWORD.zip"
done
```

	chmod +x unzipr.sh
	./unzipr.sh 37366.zip

```shell-session
Archive:  37366.zip
	inflating: 5900.zip   

<...SNIP...>

Unzipped 27833.zip using password 6969 (0)
Archive:  6969.zip
	skipping: DoNotTouch    incorrect password
Unzipped 6969.zip using password  (82)
```

>Note: 6969.zip password is not name of contents: `DoNotTouch`

### Create a hashfile and crack with john

	zip2john 6969.zip > 6969.zip.hash

```shell-session
ver 2.0 efh 5455 efh 7875 6969.zip/DoNotTouch PKZIP Encr: TS_chk, cmplen=335181, decmplen=884736, crc=E8183254 ts=5B04 cs=5b04 type=8
```

	john --wordlist=/usr/share/wordlists/rockyou.txt  6969.zip.hash

```shell-session
letmeinplease    (6969.zip/DoNotTouch)
```

	unzip -P letmeinplease 6969.zip

```shell-session
Archive:  6969.zip
  inflating: DoNotTouch
```

### Determine file type

	head DoNotTouch

```shell-session
SQLite format 3@
```

This appears to be an SQLite database.

We could browse the database and look for the flag using:

	sqlitebrowser DoNotTouch

But let's try something easier first:

	strings DoNotTouch | grep HTB

```shell-session
1969-01-01 00:00:002069-01-01 00:00:00Chillin with SatanHellHTB{z1p_and_unz1p_ma_bruddahs}
```

`HTB{z1p_and_unz1p_ma_bruddahs}`

# References

https://www.kali.org/tools/john/