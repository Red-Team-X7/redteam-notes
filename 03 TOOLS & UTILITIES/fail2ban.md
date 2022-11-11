# ⚙️ fail2ban

Tags: #⚙️
Related to: 
See also: 
Previous: [[ ]]

## Description

Fail2Ban scans log files like `/var/log/auth.log` and bans IP addresses conducting too many failed login attempts. It does this by updating system firewall rules to reject new connections from those IP addresses, for a configurable amount of time. Fail2Ban comes out-of-the-box ready to read many standard log files, such as those for sshd and Apache, and is easily configured to read any log file of your choosing, for any error you wish.

## Usage Examples

### Setup

See HTB Academy note.

# References

https://github.com/fail2ban/fail2ban