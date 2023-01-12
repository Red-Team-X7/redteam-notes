# 🔥 MSSQL

Tags: #🔥
Related to: [[impacket-mssqlclient]], [[metasploit framework]]
See also:
Previous: [[TACTICS]], [[Footprinting]]

## Description

## Cheatsheet

| **Command** | **Description** |
| --- | --- |
| `mssqlclient.py <user>@<FQDN/IP> -windows-auth` | Log in to the MSSQL server using Windows authentication. |

#### MSSQL Databases

| Default System Database | Description |
| --- | --- |
| `master` | Tracks all system information for an SQL server instance |
| `model` | Template database that acts as a structure for every new database created. Any setting changed in the model database will be reflected in any new database created after changes to the model database |
| `msdb` | The SQL Server Agent uses this database to schedule jobs & alerts |
| `tempdb` | Stores temporary objects |
| `resource` | Read-only database containing system objects included with SQL server |

#### Dangerous Settings

This is not an extensive list because there are countless ways MSSQL databases can be configured by admins based on the needs of their respective organizations. We may benefit from looking into the following:

-   MSSQL clients not using encryption to connect to the MSSQL server
-   The use of self-signed certificates when encryption is being used. It is possible to spoof self-signed certificates
-   The use of [named pipes](https://docs.microsoft.com/en-us/sql/tools/configuration-manager/named-pipes-properties?view=sql-server-ver15)
-   Weak & default `sa` credentials. Admins may forget to disable this account

## Usage Examples

### nmap MSSQL Script Scan

	sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248

```text
Starting Nmap 7.91 ( https://nmap.org ) at 2021-11-08 09:40 EST
Nmap scan report for 10.129.201.248
Host is up (0.15s latency).

PORT     STATE SERVICE  VERSION
1433/tcp open  ms-sql-s Microsoft SQL Server 2019 15.00.2000.00; RTM
| ms-sql-ntlm-info: 
|   Target_Name: SQL-01
|   NetBIOS_Domain_Name: SQL-01
|   NetBIOS_Computer_Name: SQL-01
|   DNS_Domain_Name: SQL-01
|   DNS_Computer_Name: SQL-01
|_  Product_Version: 10.0.17763

Host script results:
| ms-sql-dac: 
|_  Instance: MSSQLSERVER; DAC port: 1434 (connection failed)
| ms-sql-info: 
|   Windows server name: SQL-01
|   10.129.201.248\MSSQLSERVER: 
|     Instance name: MSSQLSERVER
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|     TCP port: 1433
|     Named pipe: \\10.129.201.248\pipe\sql\query
|_    Clustered: false

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 8.52 seconds
```

### MSSQL Ping in Metasploit

	msf6 auxiliary(scanner/mssql/mssql_ping) > set rhosts 10.129.201.248

```text
rhosts => 10.129.201.248
```

	msf6 auxiliary(scanner/mssql/mssql_ping) > run

```text
[*] 10.129.201.248:       - SQL Server information for 10.129.201.248:
[+] 10.129.201.248:       -    ServerName      = SQL-01
[+] 10.129.201.248:       -    InstanceName    = MSSQLSERVER
[+] 10.129.201.248:       -    IsClustered     = No
[+] 10.129.201.248:       -    Version         = 15.0.2000.5
[+] 10.129.201.248:       -    tcp             = 1433
[+] 10.129.201.248:       -    np              = \\SQL-01\pipe\sql\query
[*] 10.129.201.248:       - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
```

### Connecting with Mssqlclient.py

	impacket-mssqlclient backdoor:Password1@10.129.47.27 -windows-auth
	python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth

```text
Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

Password:
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(SQL-01): Line 1: Changed database context to 'master'.
[*] INFO(SQL-01): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server (150 7208) 
[!] Press help for extra shell commands
```

	select name from sys.databases
	sp_databases

```text
DATABASE_NAME DATABASE_SIZE REMARKS                                                                                                                                                                                                                                             
------------- ------------- -------
Employees     16384         NULL                                                                                                                                                                                                                                                             
master         6592         NULL                                                                                                                                                                                                                                                             
model         16384         NULL                                                                                                                                                                                                                                                             
msdb          15872         NULL                                                                                                                                                                                                                                                             
tempdb        24576         NULL  
```

# Resources