# 🤖 semgrep
Tags: #🤖
Related to: 
See also: 
Previous: [[PROGRAMMING]]

## Description

Static source code analyzer which works on 20+ languages.

## Usage Examples

### Install

	python3 -m pip install semgrep

#### Add to path in zsh

	path+=('/home/kali/.local/bin')
	export PATH

### Analyze code

	semgrep --config auto badcode.php

```text
etching rules from https://semgrep.dev/registry.

Scanning across multiple languages:
    <multilang> | 52 rules × 2 files
            php | 29 rules × 1 file 

  100%|█████|3/3 tasks

Findings:

  badcode.php 
     php.lang.security.exec-use.exec-use
        Executing non-constant commands. This can lead to command injection.
        Details: https://sg.run/5Q1j

         13┆ exec("cat /var/log/apache2/access.log | grep " . $cmd);
          ⋮┆----------------------------------------
     php.lang.security.injection.tainted-sql-string.tainted-sql-string
        User data flows into this manually-constructed SQL string. User data can be safely inserted
        into SQL strings using prepared statements or an object-relational mapper (ORM). Manually-
        constructed SQL strings is a possible indicator of SQL injection, which could let an
        attacker steal or manipulate data from the database. Instead, use prepared statements
        (`$mysqli->prepare("INSERT INTO test(id, label) VALUES (?, ?)");`) or a safe library.
        Details: https://sg.run/lZYG

          9┆ mysql_query("SELECT user FROM users WHERE id = " . $id);


Ran 1197 rules on 1 file: 2 findings.
```

# References
https://semgrep.dev/docs/getting-started/