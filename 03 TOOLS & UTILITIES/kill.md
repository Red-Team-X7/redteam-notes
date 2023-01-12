# ⚙️ kill

Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

## Description

Kill processes by name.

## Usage Examples

### List signals

	kill -l

```text
 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX
```

 **The most commonly used are:**

|Signal|Description|
|:----|:----|
|1|SIGHUP - This is sent to a process when the terminal that controls it is closed.|
|2|SIGINT - Sent when a user presses [Ctrl] + C in the controlling terminal to interrupt a process.|
|3|SIGQUIT - Sent when a user presses [Ctrl] + D to quit.|
|9|SIGKILL - Immediately kill a process with no clean-up operations.|
|15|SIGTERM - Program termination.|
|19|SIGSTOP - Stop the program. It cannot be handled anymore.|
|20|SIGTSTP - Sent when a user presses [Ctrl] + Z to request for a service to suspend. The user can handle it afterward.|

### Kill process by PID

	ps aux | grep -i vlc
	sudo kill 9 571877

### Kill suspended job

	jobs -p

```text
[1]  + 87055 suspended
```

	sudo kill -9 87055

# References