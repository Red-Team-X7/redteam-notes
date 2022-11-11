# ⚙️ tmux screen

Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]


## Description

Terminal multiplexer

## Usage Examples

### ippSec example session

#### Edit config

	cat .tmux.conf  

```
# Remap prefix to screens
set -g prefix C-a
bind C-a send-prefix
unbind C-b

# Quality of life stuff
set -g history-limit 10000
set -g allow-rename off  // prevent tmux renaming when you've set a static name

# Join windows
bind-key j command-prompt -p "join pane from:" "join pane -s '%%'"
bind-key s command-prompt -p "send pane to:"   "join pane -t '%%'"

# Search Mode VI (default is emacs)
set-window-option -g mode-keys vi

run-shell /opt/tmux-logging/logging.tmux
```

#### Create session

	tmux new -s HTB

#### Connect to openvpn

	sudo openvpn <key>.ovpn

#### Rename current window

	<Ctrl+B>	// prefix key
	,			// rename window

#### Create new window

	<Ctrl+B>	// prefix key
	c			// create new window

#### SSH into mining rig

	ssh kraken

#### List windows in session

	tmux ls

```
MINER: 1 windows (created Mon Nov 27 21:33:24 2018) [186x47]
```

#### Attach additional session in mining rig

	tmux attach -t MINER	// MINER is an SSH session

#### Create new window inside that session

	<Ctrl+B>	// prefix key
	c			// create new window

#### Switch to main terminal

This is the biggest benefit to switching the bind key:

	<Ctrl+A>  // prefix key
	1

#### Detatch from existing session

	<Prefit>
	d

#### Exit out of miner

	exit

#### Reattach to existing session

	tmux attach

#### Kill session

	tmux kill-session

#### Switch window

	<Ctrl+B>	  // prefix key
	<window #>  // select window

#### Split window vertically

	<Ctrl+B>	 // prefix key
	<Shift+%>  // split window vertically

#### Split window horizontally

	<Ctrl+B>	 // prefix key
	<Shift+">  // split window horizontally

#### Switch between panes

	<Ctrl+B>  // prefix key
	left      // switch to left pane

	<Ctrl+B>	// prefix key
	right     // switch to left pane

# References

<iframe width="560" height="315" src="https://www.youtube.com/embed/Lqehvpe_djs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

```
https://tmuxcheatsheet.com/  // cheatsheet
```