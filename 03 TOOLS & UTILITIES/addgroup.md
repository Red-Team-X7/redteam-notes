# ⚙️ addgroup, adduser

Tags: #⚙️

## Description

**adduser** and **addgroup** add users and groups to the system according to command line options and configuration information in _/etc/adduser.conf_. They are friendlier front ends to the low level tools like **useradd,** **groupadd** and **usermod** programs, by default choosing Debian policy conformant UID and GID values, creating a home directory with skeletal configuration, running a custom script, and other features.  

----
### Synopsis
**adduser** [options] [--home DIR] [--shell SHELL] [--no-create-home] [--uid ID] [--firstuid ID] [--lastuid ID] [--ingroup GROUP | --gid ID] [--disabled-password] [--disabled-login] [--gecos GECOS] [--add_extra_groups] user

**adduser** --system [options] [--home DIR] [--shell SHELL] [--no-create-home] [--uid ID] [--group | --ingroup GROUP | --gid ID] [--disabled-password] [--disabled-login] [--gecos GECOS] user

**addgroup** [options] [--gid ID] group

**addgroup** --system [options] [--gid ID] group

**adduser** [options] user group

-----

## Usage Examples
1. To add a new group- `sudo addgroup groupname`
2. To add a new group with specified group id- `sudo addgroup groupname --gid 12345`
3. To create a group with specific shell-`sudo addgroup groupname --shell /bin/sh`
4. To enter verbose mode-`sudo addgroup groupname --debug`
5. To display help realted to addgroup command-`addgroup --help`
6. To display version-`addgroup --version`

-----

# Options
**--conf FILE**

Use FILE instead of _/etc/adduser.conf_.

**--disabled-login**

Do not run passwd to set the password. The user won't be able to use her account until the password is set.

**--disabled-password**

Like --disabled-login, but logins are still possible (for example using SSH RSA keys) but not using password authentication.

**--force-badname**

By default, user and group names are checked against the configurable regular expression **NAME_REGEX** specified in the configuration file. This option forces **adduser** and **addgroup** to apply only a weak check for validity of the name.

**--gecos GECOS**

Set the gecos field for the new entry generated. **adduser** will not ask for finger information if this option is given.

**--gid ID**

When creating a group, this option forces the new groupid to be the given number. When creating a user, this option will put the user in that group.

**--group**

When combined with **--system**, a group with the same name and ID as the system user is created. If not combined with **--system**, a group with the given name is created. This is the default action if the program is invoked as **addgroup**.

**--help**

Display brief instructions.

**--home DIR**

Use DIR as the user's home directory, rather than the default specified by the configuration file. If the directory does not exist, it is created and skeleton files are copied.

**--shell SHELL**

Use SHELL as the user's login shell, rather than the default specified by the configuration file.

**--ingroup GROUP**

Add the new user to GROUP instead of a usergroup or the default group defined by **USERS_GID** in the configuration file. This affects the users primary group. To add additional groups, see the **add_extra_groups** option

**--no-create-home**

Do not create the home directory, even if it doesn't exist.

**--quiet**

Suppress informational messages, only show warnings and errors.

**--debug**

Be verbose, most useful if you want to nail down a problem with adduser.

**--system**

Create a system user or group.

**--uid ID**

Force the new userid to be the given number. **adduser** will fail if the userid is already taken.

**--firstuid ID**

Override the first uid in the range that the uid is chosen from (overrides **FIRST_UID** specified in the configuration file).

**--lastuid ID**

Override the last uid in the range that the uid is chosen from ( **LAST_UID** )

**--add_extra_groups**

Add new user to extra groups defined in the configuration file.

**--version**

Display version and copyright information.

-----

## Files
**/etc/adduser.conf**
								Default Configuration file for another adduser and addgroup.
