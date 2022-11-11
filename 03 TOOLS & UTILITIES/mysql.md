# ⚙️ mysql

Tags: #⚙️
Related to:
See also:
Previous: [[Footprinting]]

## Description

the MariaDB command-line tool

## Usage Examples

### Login to the MySQL server

	mysql -u <user> -p<password> <FQDN/IP>

### Change database

	use users;	// ERROR 1044 (42000): Access denied for user 'ona_sys'@'localhost' to database 'users'
	use mysql;	// ERROR 1044 (42000): Access denied for user 'ona_sys'@'localhost' to database 'mysql'
	use ona_default;
	
```
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```

show tables;

```
+------------------------+
| Tables_in_ona_default  |
+------------------------+
| blocks                 |
| configuration_types    |
| configurations         |
| custom_attribute_types |
| custom_attributes      |
| dcm_module_list        |
| device_types           |
| devices                |
| dhcp_failover_groups   |
| dhcp_option_entries    |
| dhcp_options           |
| dhcp_pools             |
| dhcp_server_subnets    |
| dns                    |
| dns_server_domains     |
| dns_views              |
| domains                |
| group_assignments      |
| groups                 |
| host_roles             |
| hosts                  |
| interface_clusters     |
| interfaces             |
| locations              |
| manufacturers          |
| messages               |
| models                 |
| ona_logs               |
| permission_assignments |
| permissions            |
| roles                  |
| sequences              |
| sessions               |
| subnet_types           |
| subnets                |
| sys_config             |
| tags                   |
| users                  |
| vlan_campuses          |
| vlans                  |
+------------------------+
40 rows in set (0.01 sec)
```

	describe users;
	
```
	+----------+------------------+------+-----+-------------------+-----------------------------+
| Field    | Type             | Null | Key | Default           | Extra                       |
+----------+------------------+------+-----+-------------------+-----------------------------+
| id       | int(10) unsigned | NO   | PRI | NULL              | auto_increment              |
| username | varchar(32)      | NO   | UNI | NULL              |                             |
| password | varchar(64)      | NO   |     | NULL              |                             |
| level    | int(4)           | NO   |     | 0                 |                             |
| ctime    | timestamp        | NO   |     | CURRENT_TIMESTAMP | on update CURRENT_TIMESTAMP |
| atime    | datetime         | YES  |     | NULL              |                             |
+----------+------------------+------+-----+-------------------+-----------------------------+
6 rows in set (0.00 sec)
```

	select id, username, password from users;
	
```
+----+----------+----------------------------------+
| id | username | password                         |
+----+----------+----------------------------------+
|  1 | guest    | 098f6bcd4621d373cade4e832627b4f6 |
|  2 | admin    | 21232f297a57a5a743894a0e4a801fc3 |
+----+----------+----------------------------------+
2 rows in set (0.00 sec)
```

Search for cracked hash. [^2]

	098f6bcd4621d373cade4e832627b4f6:test
	21232f297a57a5a743894a0e4a801fc3:admin

Try dumping users:

	SELECT User FROM mysql.user;	// ERROR 1142 (42000): SELECT command denied to user 'ona_sys'@'localhost' for table 'user'
	mysql -u root -p	// try n1nj4W4rri0R!	// ERROR 1698 (28000): Access denied for user 'root'@'localhost'

# References