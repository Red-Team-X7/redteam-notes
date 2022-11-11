# ⚙️ chmod chown

Tags: #⚙️
Related to:
See also:
Previous:

## Description

```shell-session
chmod: Change file mode bits.
chown: Change file owner and group.
```

Under Linux, permissions are assigned to users and groups. Each user can be a member of different groups, and membership in these groups gives the user specific, additional permissions. Each file and directory belongs to a specific user and a specific group. So the permissions for users and groups that defined a file are also defined for the respective owners. When we create new files or directories, they belong to the group we belong to and us. The whole permission system on Linux systems is based on the octal number system, and basically, there are three different types of permissions a file or directory can be assigned:

-   (`r`) - Read
-   (`w`) - Write
-   (`x`) - Execute

The permissions can be set for the `owner`, `group`, and `others` like presented in the next example with their corresponding permissions.

	ls -l /etc/passwd

```shell-session
- rwx rw- r--   1 root root 1641 May  4 23:42 /etc/passwd
- --- --- ---   |  |    |    |   |__________|
|  |   |   |    |  |    |    |        |_ Date
|  |   |   |    |  |    |    |__________ File Size
|  |   |   |    |  |    |_______________ Group
|  |   |   |    |  |____________________ User
|  |   |   |    |_______________________ Number of hard links
|  |   |   |_ Permission of others (read)
|  |   |_____ Permissions of the group (read, write)
|  |_________ Permissions of the owner (read, write, execute)
|____________ File type (- = File, d = Directory, l = Link, ... )
```

## Usage Examples

### Change Permissions

We can modify permissions using the `chmod` command, permission group references (`u` - owner, `g` - Group, `o` - others, `a` - All users), and either a [`+`] or a [`-`] to add remove the designated permissions. In the following example, a user creates a new shell script owned by that user, not executable, and set with read/write permissions for all users.

	ls -l shell

```shell-session
-rwxr-x--x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can then apply `read` permissions for all users and see the result.

	chmod a+r shell && ls -l shell

```shell-session
-rwxr-xr-x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

We can also set the permissions for all other users to `read` only using the octal value assignment.

	chmod 754 shell && ls -l shell

```shell-session
-rwxr-xr--   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Let us look at all the representations associated with it to understand better how the permission assignment is calculated.

```shell-session
Binary Notation:                4 2 1  |  4 2 1  |  4 2 1
----------------------------------------------------------
Binary Representation:          1 1 1  |  1 0 1  |  1 0 0
----------------------------------------------------------
Octal Value:                      7    |    5    |    4
----------------------------------------------------------
Permission Representation:      r w x  |  r - x  |  r - -
```

If we sum the set bits from the `Binary Representation` assigned to the values from `Binary Notation` together, we get the `Octal Value`. The `Permission Representation` represents the bits set in the `Binary Representation` by using the three characters, which only recognizes the set permissions easier.

### Change Owner

To change the owner and/or the group assignments of a file or directory, we can use the `chown` command. The syntax is like following:

#### Syntax - chown

	chown <user>:<group> <file/directory>

In this example, "shell" can be replaced with any arbitrary file or folder.

	chown root:root shell && ls -l shell

```shell-session
-rwxr-xr--   1 root root 0 May  4 22:12 shell
```

#### SUID & GUID

Besides assigning direct user and group permissions, we can also configure special permissions for files by setting the `Set User ID` (`SUID`) and `Set Group ID` (`GUID`) bits. These `SUID`/`GUID` bits allow, for example, users to run programs with the rights of another user. Administrators often use this to give their users special rights for certain applications or files. The letter "`s`" is used instead of an "`x`". When executing such a program, the SUID/GUID of the file owner is used.

It is often the case that administrators are not familiar with the applications but still assign the SUID/GUID bits, which leads to a high-security risk. Such programs may contain functions that allow the execution of a shell from the pager, such as the application "`journalctl`."

If the administrator sets the SUID bit to "`journalctl`," any user with access to this application could execute a shell as `root`. More information about this and other such applications can be found at [GTFObins](https://gtfobins.github.io/gtfobins/journalctl/).

# References