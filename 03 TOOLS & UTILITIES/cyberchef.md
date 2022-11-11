# ⚙️ cyberchef
Tags: #⚙️ 
Related to: 
See also: 
Previous: 

## Description

CyberChef is a simple, intuitive web app for carrying out all manner of "cyber" operations within a web browser.
Carry out different operations on data of different types: Encode/decode, convert, parse, decompress, decrypt, disassemble, extract...

## Usage Examples

### CyberChef

Decode data:

```
00000000: 425a 6839 3141 5926 5359 819b bb48 0000  BZh91AY&SY...H..
00000010: 17ff fffc 41cf 05f9 5029 6176 61cc 3a34  ....A...P)ava.:4
00000020: 4edc cccc 6e11 5400 23ab 4025 f802 1960  N...n.T.#.@%...`
00000030: 2018 0ca0 0092 1c7a 8340 0000 0000 0000   ......z.@......
00000040: 0680 6988 3468 6469 89a6 d439 ea68 c800  ..i.4hdi...9.h..
00000050: 000f 51a0 0064 681a 069e a190 0000 0034  ..Q..dh........4
00000060: 6900 0781 3501 6e18 c2d7 8c98 874a 13a0  i...5.n......J..
00000070: 0868 ae19 c02a b0c1 7d79 2ec2 3c7e 9d78  .h...*..}y..<~.x
00000080: f53e 0809 f073 5654 c27a 4886 dfa2 e931  .>...sVT.zH....1
00000090: c856 921b 1221 3385 6046 a2dd c173 0d22  .V...!3.`F...s."
000000a0: b996 6ed4 0cdb 8737 6a3a 58ea 6411 5290  ..n....7j:X.d.R.
000000b0: ad6b b12f 0813 8120 8205 a5f5 2970 c503  .k./... ....)p..
000000c0: 37db ab3b e000 ef85 f439 a414 8850 1843  7..;.....9...P.C
000000d0: 8259 be50 0986 1e48 42d5 13ea 1c2a 098c  .Y.P...HB....*..
000000e0: 8a47 ab1d 20a7 5540 72ff 1772 4538 5090  .G.. .U@r..rE8P.
000000f0: 819b bb48                                ...H
```
 https://gchq.github.io/CyberChef/#recipe=From_Hexdump()Bzip2_Decompress(false)Gunzip()Bzip2_Decompress(false)Untar()Detect_File_Type(true,true,true,true,true,true,true/disabled)&input=MDAwMDAwMDA6IDQyNWEgNjgzOSAzMTQxIDU5MjYgNTM1OSA4MTliIGJiNDggMDAwMCAgQlpoOTFBWSZTWS4uLkguLgowMDAwMDAxMDogMTdmZiBmZmZjIDQxY2YgMDVmOSA1MDI5IDYxNzYgNjFjYyAzYTM0ICAuLi4uQS4uLlApYXZhLjo0CjAwMDAwMDIwOiA0ZWRjIGNjY2MgNmUxMSA1NDAwIDIzYWIgNDAyNSBmODAyIDE5NjAgIE4uLi5uLlQuIy5AJS4uLmAKMDAwMDAwMzA6IDIwMTggMGNhMCAwMDkyIDFjN2EgODM0MCAwMDAwIDAwMDAgMDAwMCAgIC4uLi4uLnouQC4uLi4uLgowMDAwMDA0MDogMDY4MCA2OTg4IDM0NjggNjQ2OSA4OWE2IGQ0MzkgZWE2OCBjODAwICAuLmkuNGhkaS4uLjkuaC4uCjAwMDAwMDUwOiAwMDBmIDUxYTAgMDA2NCA2ODFhIDA2OWUgYTE5MCAwMDAwIDAwMzQgIC4uUS4uZGguLi4uLi4uLjQKMDAwMDAwNjA6IDY5MDAgMDc4MSAzNTAxIDZlMTggYzJkNyA4Yzk4IDg3NGEgMTNhMCAgaS4uLjUubi4uLi4uLkouLgowMDAwMDA3MDogMDg2OCBhZTE5IGMwMmEgYjBjMSA3ZDc5IDJlYzIgM2M3ZSA5ZDc4ICAuaC4uLiouLn15Li48fi54CjAwMDAwMDgwOiBmNTNlIDA4MDkgZjA3MyA1NjU0IGMyN2EgNDg4NiBkZmEyIGU5MzEgIC4%2BLi4uc1ZULnpILi4uLjEKMDAwMDAwOTA6IGM4NTYgOTIxYiAxMjIxIDMzODUgNjA0NiBhMmRkIGMxNzMgMGQyMiAgLlYuLi4hMy5gRi4uLnMuIgowMDAwMDBhMDogYjk5NiA2ZWQ0IDBjZGIgODczNyA2YTNhIDU4ZWEgNjQxMSA1MjkwICAuLm4uLi4uN2o6WC5kLlIuCjAwMDAwMGIwOiBhZDZiIGIxMmYgMDgxMyA4MTIwIDgyMDUgYTVmNSAyOTcwIGM1MDMgIC5rLi8uLi4gLi4uLilwLi4KMDAwMDAwYzA6IDM3ZGIgYWIzYiBlMDAwIGVmODUgZjQzOSBhNDE0IDg4NTAgMTg0MyAgNy4uOy4uLi4uOS4uLlAuQwowMDAwMDBkMDogODI1OSBiZTUwIDA5ODYgMWU0OCA0MmQ1IDEzZWEgMWMyYSAwOThjICAuWS5QLi4uSEIuLi4uKi4uCjAwMDAwMGUwOiA4YTQ3IGFiMWQgMjBhNyA1NTQwIDcyZmYgMTc3MiA0NTM4IDUwOTAgIC5HLi4gLlVAci4uckU4UC4KMDAwMDAwZjA6IDgxOWIgYmI0OCAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgLi4uSA

## References

https://gchq.github.io/CyberChef