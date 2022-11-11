# ⚙️ stty

Tags: #⚙️
Related to:
See also:
Previous:

## Description

Change and print terminal line settings.

## Usage Examples

### Upgrade terminal for improved functionality (arrow keys, etc.)

	www-data@curling:/var/www/html/templates/protostar$ ^[[D^[[A^[[C^[[D^[[A^[[C

	which python
	which python3
	
#### Spawn a bash terminal

	python3 -c 'import pty;pty.spawn("/bin/bash")'

#### Background it
	<Ctrl+Z>

#### Change terminal line settings
	stty raw -echo;fg
	
	raw		// same as -ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr -icrnl -ixon -ixoff -icanon -opost -isig -iuclc -ixany -imaxbel -xcase min 1 time 0
	-echo	// echo input characters
	;fg		// plays nice with zsh

#### Enable clear screen functionality

	export TERM=xterm

### Reset terminal line settings

	reset

### Set TTY row and column count

Get TTY row and column count:

	stty size	// rows 64; columns 117;	// from working terminal

Set row and column count:

	stty rows 65 cols 117				// to target terminal

# References