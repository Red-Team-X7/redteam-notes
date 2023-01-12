# 🔥 MySQL

Tags: #🔥
Related to: [[nmap]]
See also:
Previous: [[TACTICS]], [[Footprinting]]

## Description

## Cheatsheet

| **Command** | **Description** |
| --- | --- |
| `mysql -u <user> -p<password> <IP address>` | Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password. |
| `show databases;` | Show all databases. |
| `use <database>;` | Select one of the existing databases. |
| `show tables;` | Show all available tables in the selected database. |
| `show columns from <table>;` | Show all columns in the selected database. |
| `select * from <table>;` | Show everything in the desired table. |
| `select * from <table> where <column> = "<string>";` | Search for needed `string` in the desired table. |



#### Dangerous Settings

| **Settings** | **Description** |
| --- | --- |
| `user` | Sets which user the MySQL service will run as. |
| `password` | Sets the password for the MySQL user. |
| `admin_address` | The IP address on which to listen for TCP/IP connections on the administrative network interface. |
| `debug` | This variable indicates the current debugging settings |
| `sql_warnings` | This variable controls whether single-row INSERT statements produce an information string if warnings occur. |
| `secure_file_priv` | This variable is used to limit the effect of data import and export operations. |

## Usage Examples

### Default Configuration

	sudo apt install mysql-server -y
	cat /etc/mysql/mysql.conf.d/mysqld.cnf | grep -v "#" | sed -r '/^\s*$/d'

```text
[client]
port		= 3306
socket		= /var/run/mysqld/mysqld.sock

[mysqld_safe]
pid-file	= /var/run/mysqld/mysqld.pid
socket		= /var/run/mysqld/mysqld.sock
nice		= 0

[mysqld]
skip-host-cache
skip-name-resolve
user		= mysql
pid-file	= /var/run/mysqld/mysqld.pid
socket		= /var/run/mysqld/mysqld.sock
port		= 3306
basedir		= /usr
datadir		= /var/lib/mysql
tmpdir		= /tmp
lc-messages-dir	= /usr/share/mysql
explicit_defaults_for_timestamp

symbolic-links=0

!includedir /etc/mysql/conf.d/
```

### Scanning MySQL Server

	sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*

```text
Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-21 00:53 CEST
Nmap scan report for 10.129.14.128
Host is up (0.00021s latency).

PORT     STATE SERVICE     VERSION
3306/tcp open  nagios-nsca Nagios NSCA
| mysql-brute: 
|   Accounts: 
|     root:<empty> - Valid credentials
|_  Statistics: Performed 45010 guesses in 5 seconds, average tps: 9002.0
|_mysql-databases: ERROR: Script execution failed (use -d to debug)
|_mysql-dump-hashes: ERROR: Script execution failed (use -d to debug)
| mysql-empty-password: 
|_  root account has empty password
| mysql-enum: 
|   Valid usernames: 
|     root:<empty> - Valid credentials
|     netadmin:<empty> - Valid credentials
|     guest:<empty> - Valid credentials
|     user:<empty> - Valid credentials
|     web:<empty> - Valid credentials
|     sysadmin:<empty> - Valid credentials
|     administrator:<empty> - Valid credentials
|     webadmin:<empty> - Valid credentials
|     admin:<empty> - Valid credentials
|     test:<empty> - Valid credentials
|_  Statistics: Performed 10 guesses in 1 seconds, average tps: 10.0
| mysql-info: 
|   Protocol: 10
|   Version: 8.0.26-0ubuntu0.20.04.1
|   Thread ID: 13
|   Capabilities flags: 65535
|   Some Capabilities: SupportsLoadDataLocal, SupportsTransactions, Speaks41ProtocolOld, LongPassword, DontAllowDatabaseTableColumn, Support41Auth, IgnoreSigpipes, SwitchToSSLAfterHandshake, FoundRows, InteractiveClient, Speaks41ProtocolNew, ConnectWithDatabase, IgnoreSpaceBeforeParenthesis, LongColumnFlag, SupportsCompression, ODBCClient, SupportsMultipleStatments, SupportsAuthPlugins, SupportsMultipleResults
|   Status: Autocommit
|   Salt: YTSgMfqvx\x0F\x7F\x16\&\x1EAeK>0
|_  Auth Plugin Name: caching_sha2_password
|_mysql-users: ERROR: Script execution failed (use -d to debug)
|_mysql-variables: ERROR: Script execution failed (use -d to debug)
|_mysql-vuln-cve2012-2122: ERROR: Script execution failed (use -d to debug)
MAC Address: 00:00:00:00:00:00 (VMware)

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.21 seconds
```

### Interaction with the MySQL Server

	mysql -u root -h 10.129.14.132

```text
ERROR 1045 (28000): Access denied for user 'root'@'10.129.14.1' (using password: NO)
```

	mysql -u root -pP4SSw0rd -h 10.129.14.128

```text
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 150165
Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)                                                         
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.                                     
Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

	show databases;

```text
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.006 sec)
```

	select version();

```text
+-------------------------+
| version()               |
+-------------------------+
| 8.0.27-0ubuntu0.20.04.1 |
+-------------------------+
1 row in set (0.001 sec)
```

	use mysql;
	show tables;

```text
+------------------------------------------------------+
| Tables_in_mysql                                      |
+------------------------------------------------------+
| columns_priv                                         |
| component                                            |
| db                                                   |
| default_roles                                        |
| engine_cost                                          |
| func                                                 |
| general_log                                          |
| global_grants                                        |
| gtid_executed                                        |
| help_category                                        |
| help_keyword                                         |
| help_relation                                        |
| help_topic                                           |
| innodb_index_stats                                   |
| innodb_table_stats                                   |
| password_history                                     |
...SNIP...
| user                                                 |
+------------------------------------------------------+
37 rows in set (0.002 sec)
```

	use sys;
	show tables;

```text
+-----------------------------------------------+
| Tables_in_sys                                 |
+-----------------------------------------------+
| host_summary                                  |
| host_summary_by_file_io                       |
| host_summary_by_file_io_type                  |
| host_summary_by_stages                        |
| host_summary_by_statement_latency             |
| host_summary_by_statement_type                |
| innodb_buffer_stats_by_schema                 |
| innodb_buffer_stats_by_table                  |
| innodb_lock_waits                             |
| io_by_thread_by_latency                       |
...SNIP...
| x$waits_global_by_latency                     |
+-----------------------------------------------+
```

	select host, unique_users from host_summary;

```text
+-------------+--------------+                   
| host        | unique_users |                   
+-------------+--------------+                   
| 10.129.14.1 |            1 |                   
| localhost   |            2 |                   
+-------------+--------------+                   
2 rows in set (0,01 sec)
```

### Example - Get User Email Address

	mysql -u robin -probin -h 10.129.249.57

```text
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MySQL connection id is 308
Server version: 8.0.27-0ubuntu0.20.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

	show databases;

```text
+--------------------+
| Database           |
+--------------------+
| customers          |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.144 sec)
```

	use customers;

```text
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```

	show tables;

```text
+---------------------+
| Tables_in_customers |
+---------------------+
| myTable             |
+---------------------+
1 row in set (0.107 sec)
```

	show columns from myTable;

```text
+-----------+--------------------+------+-----+---------+----------------+
| Field     | Type               | Null | Key | Default | Extra          |
+-----------+--------------------+------+-----+---------+----------------+
| id        | mediumint unsigned | NO   | PRI | NULL    | auto_increment |
| name      | varchar(255)       | YES  |     | NULL    |                |
| email     | varchar(255)       | YES  |     | NULL    |                |
| country   | varchar(100)       | YES  |     | NULL    |                |
| postalZip | varchar(20)        | YES  |     | NULL    |                |
| city      | varchar(255)       | YES  |     | NULL    |                |
| address   | varchar(255)       | YES  |     | NULL    |                |
| pan       | varchar(255)       | YES  |     | NULL    |                |
| cvv       | varchar(255)       | YES  |     | NULL    |                |
+-----------+--------------------+------+-----+---------+----------------+
9 rows in set (0.036 sec)

```

	select * from myTable;

```text
+----+---------------------+------------------------------------------+--------------------+-------------+-------------------------------+-----------------------------------+---------------------+------+
| id | name                | email                                    | country            | postalZip   | city                          | address                           | pan                 | cvv  |
+----+---------------------+------------------------------------------+--------------------+-------------+-------------------------------+-----------------------------------+---------------------+------+
|  1 | Emery Reyes         | diam.eu@icloud.htb                       | Spain              | 26-579      | Quảng Ngãi                    | 675-4432 Nunc Av.                 | 519358 9482346334   | 144  |
|  2 | Kristen Trujillo    | tellus.id@google.htb                     | Costa R.htb        | 376420      | Chiclayo                      | 101-8154 Ac Rd.                   | 546871 777532 7590  | 125  |
|  3 | Fletcher Jimenez    | lobortis@outlook.htb                     | Germany            | 3515        | Timaru                        | 9562 Dui, St.                     | 559 47883 93145 224 | 550  |
|  4 | Boris Sharp         | donec@protonmail.htb                     | Pakistan           | 1317        | Jönköping                     | 728-7809 Cras Road                | 4716447833847468    | 536  |
|  5 | Ruth Carson         | suspendisse.aliquet@yahoo.htb            | Pakistan           | 14945       | Oviedo                        | 324-8221 Ut Road                  | 5164782453566544    | 449  |
|  6 | Caryn Porter        | neque@aol.htb                            | New Zealand        | 3798        | Vichy                         | Ap #770-5801 Donec Rd.            | 4916 475 64 6748    | 590  |
|  7 | G.htbe Stein        | eget@google.htb                          | Spain              | 80125       | Jeonju                        | 305-2770 Lectus. Rd.              | 485 51263 38542 847 | 402  |
|  8 | Emery Watson        | non@icloud.htb                           | Austria            | 23940       | Secunderabad                  | Ap #542-2284 Mauris, Street       | 4716 5544 1838 4955 | 411  |
|  9 | Silas Holder        | metus@hotmail.htb                        | Netherlands        | 63-851      | San Cristóbal de la Laguna    | Ap #604-7295 Duis St.             | 5186 1252 1481 7760 | 863  |
| 10 | Patrick Walls       | aliquet@yahoo.htb                        | Indonesia          | 776718      | Weelde                        | 118-5893 Rhoncus. Ave             | 513 51634 82351 610 | 430  |
| 11 | Barclay Knight      | ut.nec@yahoo.htb                         | Poland             | FX6 7KT     | Sankt Wendel                  | 977-1992 Lacus. Avenue            | 4532532734638447    | 592  |
<...snip...>
```

	select * from myTable where name ="Otto Lang";

```text
+----+-----------+---------------------+---------+-----------+---------+-----------------+------------------+------+
| id | name      | email               | country | postalZip | city    | address         | pan              | cvv  |
+----+-----------+---------------------+---------+-----------+---------+-----------------+------------------+------+
| 88 | Otto Lang | ultrices@google.htb | France  | 76733-267 | Belfast | 4708 Auctor Rd. | 5322224628183391 | 595  |
+----+-----------+---------------------+---------+-----------+---------+-----------------+------------------+------+
1 row in set (0.074 sec)
```

# Resources