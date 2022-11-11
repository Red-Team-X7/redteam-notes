# 🔥 upgrade shell

Tags: #🔥 
Related to: 
See also: [[stty]], [[rlwrap]]
Previous: [[TTP]]


## Description

Often during pen tests you may obtain a shell without having tty, yet wish to interact further with the system. Here are some commands which will allow you to spawn a tty shell. Obviously some of this will depend on the system environment and installed packages. 

## Usage Examples

```shell-session
-   python -c 'import pty; pty.spawn("/bin/sh")'
-   echo os.system('/bin/bash')
-   /bin/sh -i
-   perl —e 'exec "/bin/sh";'
-   perl: exec "/bin/sh";
-   ruby: exec "/bin/sh"
-   lua: os.execute('/bin/sh')
-   (From within IRB): exec "/bin/sh"
-   (From within vi) :!bash
-   (From within vi) :set shell=/bin/bash:shell
-   (From within nmap) !sh
```

### Upgrade a terminal for improved functionality (arrow keys, history, etc.)

| **Command**   | **Description**   |
| --------------|-------------------|
| `echo $TERM` and `stty size` | Get local terminal type and size |
| `which python` or `which python3` or `which script` | Locate an interpreter |
| `python -c 'import pty; pty.spawn("/bin/bash")'` or `script -q /dev/null -c bash` | Upgrade shell TTY (1) |
| `ctrl+z` then `stty raw -echo;` then `fg` then `enter` twice | Upgrade shell TTY (2) |
| `export TERM=xterm-256color` then `stty rows 67 columns 318` | Set remote terminal type and size |

# References
https://netsec.ws/?p=337  // "Many of these will also allow you to escape jail shells."
https://blog.ropnop.com/upgrading-simple-shells-to-fully-interactive-ttys/