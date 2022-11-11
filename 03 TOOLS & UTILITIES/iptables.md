# ⚙️ iptables
Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

---
## Description


## Usage Examples

### Block inbound access to TCP port 22

sudo iptables -i eth0 -A INPUT -p tcp --dport 22 -j DROP
	
	-i eth0			// Match packets on the eth0 interface.
	-A				// Append rule to INPUT filter.
	-p tcp			// Match TCP packets only.
	--dport 4444	// Match packets destined to port 4444.
	-j ACCEPT		// Accept the packet ("jump" to ACCEPT).

### Allow inbound connections to port 4444

sudo iptables -i eth0 --insert INPUT -p tcp --dport 4444 -j ACCEPT

	-i eth0			// Match packets on the eth0 interface.
	--insert INPUT	// Insert the rule at the top of the INPUT chain.
	-p tcp			// Match TCP packets only.
	--dport 4444	// Match packets destined to port 4444.
	-j ACCEPT		// Accept the packet ("jump" to ACCEPT).

### Flush all rules by restarting iptables
	service iptables restart	// sudo iptables -F

### List rules

	iptables -L		// list all rules in the selected chain. If no chain is selected, all chains are listed.

---
## References
- [[]]