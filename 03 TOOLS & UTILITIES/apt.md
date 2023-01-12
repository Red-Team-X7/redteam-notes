# ⚙️ apt

Tags: #⚙️
Related to: [[dpkg]], [[aptitude]]
See also:
Previous:

## Description

Provides a high-level commandline interface for the package management system.

## Usage Examples

### Install an application with automatic yes to prompts

	sudo apt install tmux -y

### List installed packages

	apt list --installed

### List package reverse dependencies

	apt-cache rdepends lintian

### Show additional package info

```
apt-cache show impacket-scripts
```

```text
Package: impacket-scripts
Version: 1.4
Architecture: all
Maintainer: Kali Developers <devel@kali.org>
Installed-Size: 13
Depends: python3-impacket (>= 0.9.20), python3-ldap3 (>= 2.5.0), python3-ldapdomaindump
Breaks: python-impacket (<< 0.9.18)
Replaces: python-impacket (<< 0.9.18)
Priority: optional
Section: misc
Filename: pool/main/i/impacket-scripts/impacket-scripts_1.4_all.deb
Size: 2080
<SNIP>
```

### Update a system

	sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y

### Install tools from a list

	sudo apt install $(cat tools.list | tr "\n" " ") -y

### Prevent a package from being upgraded

	sudo apt-mark hold code-oss
	sudo rm /usr/bin/code
	sudo rm /usr/bin/code-oss

```text
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and are no longer required: 
  libarmadillo9 libboost-locale1.71.0 libcfitsio8 libdap25 libgdal27 libgfapi0
  ...SNIP...
```

# References