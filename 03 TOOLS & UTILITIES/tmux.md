# ⚙️ tmux

Tags: #⚙️
Related to:
See also:
Previous: [[Getting Started]]

## Description

Terminal multiplexer.

## Cheatsheet

| Command | Description |
|-|-|
| `tmux` | Start tmux |
| `ctrl+b` | tmux: default prefix |
| `prefix c` | tmux: new window |
| `prefix 1` | tmux: switch to window (`1`) |
| `prefix shift+%` | tmux: split pane vertically |
| `prefix shift+"` | tmux: split pane horizontally |
| `prefix ->` | tmux: switch to the right pane |

## Cheatsheet

| Shell command | Description |
| --- | ---- |
| `tmux new-session -s sessionname`<br>`tmux new -s sessionname` | Create a named session called *sessionname* |
| `tmux new -s sessionname -d top` | Create detached session and run *top* inside |
| `tmux new -s sessionname -n win` | Create session *sessionname* with window *win* |
| `tmux list-sessions` <br> `tmux ls` | |
| `tmux attach` | |
| `tmux attach -t sessionname` | Attach to session with name *sessionname* |
| `tmux kill-session -t sessionname` | |
| `tmux has-session -t sessionname`| Returns 0 if session exists |

PREFIX (`CTRL-b`) + ... | Description | Custom mapping
--------------------- | ----------- | --------------
`d`|Detach |
`:`|Enter command mode |
`?`|See all keybindings |
`r`| Reload config file (`.tmux.conf`)| yes
`(`| Switch to next session |
`)`| Switch to previous session |
`s`| Show session menu |
`$`| Rename session |
`P`| Toggle logging output to ~/*window_name*.log|yes
`ESCAPE`|Enter copy mode |
`p`|Paste from buffer|
`CTRL-c`|Copy buffer to MAC clipboard |

## Windows

PREFIX (`CTRL-b`) + ... | Description | Custom mapping
--------------------- | ----------- | --------------
`c`| Create window |
`,`| Rename window |
`n`|Go to next window |
`CTRL-h`, `CTRL-l`|Select next/previous window|yes
`0`|Go to window no `0` |
`1`|Go to window no `1` |
`f`|Find window by name |
`w`|Select window by menu |
`&`|Kill window (after confirmation) |
`.`| Move window to another session |

## Panes

PREFIX (`CTRL-b`) + ... | Description | Custom mapping
--------------------- | ----------- | --------------
`%`|Split horizontally |
`PIPE`|Split horizontally | yes
`"`|Split vertically |
`-` | Split vertically|yes
`o`|Cycle through panes |
`h`, `j`, `k`, `l`|Select next pane in vim-direction|yes
 `SPACE`|Cycle pane layout (`even-horizontal`, `even-vertical`, `main-horizontal`, `main-vertical`, `tiled`) |
`H`, `J`, `K`, `L`|Resize pane in vim-direction (5 column-wise)|yes
`!`| Move active pane to a new window |
`z`| Zoom pane | tmux 1.8
`UP`| Maximize pane | yes
`DOWN` | Redo maximize pane | yes
`x`|Kill pane (after confirmation) |

## Command mode

Command|Description
-------|-----------
`new-window -n redis "redis-server"`|Open new window, name it *windowname* and run *redis-server* in it.
`capture-pane`|Copy entire visible contents of pane into the paste buffer
`show-buffer`|Show contents of actual buffer
`save-buffer file.txt`|Save buffer to `file.txt`
`list-buffers`|Show all buffers
`choose-buffer`|Choose a buffer and paste
`join-pane -s source_session_name:1.1`|Move pane 1 in window 1 of session source_session_name to the actual window`
`join-pane -s src_sess:2.1 -t dst_sess:1.1`|Move pane 1 in window 2 of session src_sess to session dst_session in window 1 near pane 1`

## Copy mode
PREFIX (`CTRL-b`) + ... |Description
---|-----------
`[`|Use navigation keys (PageUp/PageDown)
`h`, `j`, `k`, `l`|Move around
`ENTER`|Leave copy mode
`w`|Jump to next word
`b`|Jump to previous word
`fA`|Jump to next `A` in the actual line
`FA`|Jump to previous `A` in the actual line
`CTRL-b`|Down one page
`CTRL-f`|Up one page
`g`|Jump to top of buffer
`G`|Jump to bottom of buffer
`?`|Backward search
`/`|Foreward search
`n`|Go to next occurence
`N`|Go to previous occurence
`SPACE`|Begin selecting text
`v`|Begin selecting text
`y`|Copy selection to buffer

### Module Summary

This module introduces the fundamentals of file inclusion vulnerabilities. Web applications often present a large attack surface, and as information security professionals, it is important to understand common attacks against a variety of frameworks and server-side languages. A successful file inclusion attack may result in sensitive data exposure (such as configuration files containing credentials) or even remote code execution.

In this module, we will cover:

-   An intro to file inclusion vulnerabilities
-   Local File Inclusion (LFI)
-   Path Traversal
-   Bypassing basic LFI restrictions
-   LFI to remote code execution (RCE)
    -   RCE through PHP wrappers
    -   RCE through Remote File Inclusion (RFI)
    -   RCE through malicious file uploads
    -   RCE through log poisoning
-   Automating LFI exploitation
-   Preventing LFI exploitation

* * * * *

This module is broken down into sections with accompanying hands-on exercises to practice each of the tactics and techniques we cover. The module ends with a practical hands-on skills assessment to gauge your understanding of the various topic areas.

You can start and stop the module at any time and pick up where you left off. There is no time limit or "grading", but you must complete all of the exercises and the skills assessment to receive the maximum number of cubes and have this module marked as complete in any paths you have chosen.

As you work through the module, you will see example commands and command output for the various topics introduced. It is worth reproducing as many of these examples as possible to further reinforce the concepts introduced in each section. You can do this in the `PwnBox` provided in the interactive sections or in your own virtual machine.

* * * * *

The module is classified as "`Medium`" and assumes a working knowledge of the Linux command line and an understanding of information security fundamentals. The module also assumes a basic understanding of web applications and web requests, and will build on this understanding to teach how Arbitrary File Upload vulnerabilities work and how to exploit them.

In addition to the above, a firm grasp of the following modules can be considered as prerequisites for the successful completion of this module:

-   Introduction to Networking
-   Linux Fundamentals
-   Web Requests# tmux cheatsheet

## Usage Examples

### 

# References