# ⚙️ mount umount

Tags: #⚙️
Related to:
See also: [[findmnt]]
Previous:

## Description

Mount/Unmount a filesystem.

## Usage Examples

### Mount a specific NFS share

	mount -t nfs <FQDN/IP>:/<share> ./target-NFS/ -o nolock

### Unmount a specific NFS share

	umount ./target-NFS

### Mount Windows share

	sudo mount -t cifs -o username=htb-student,password=Academy_WinFun! //ipaddoftarget/"Company Data" /home/user/Desktop/

### Unmount Windows share

	sudo umount -a -t cifs -l

# References