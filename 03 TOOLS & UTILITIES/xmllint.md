# ⚙️ xmllint

Tags: #⚙️
Related to:
See also:
Previous:

## Description

Command line XML tool.

## Usage Examples

### Request and prettify xml output

	curl -s http://10.129.42.190/nibbleblog/content/private/users.xml | xmllint  --format -

```text
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<users>
  <user username="admin">
    <id type="integer">0</id>
    <session_fail_count type="integer">2</session_fail_count>
    <session_date type="integer">1608182184</session_date>
  </user>
  <blacklist type="string" ip="10.10.10.1">
    <date type="integer">1512964659</date>
    <fail_count type="integer">1</fail_count>
  </blacklist>
  <blacklist type="string" ip="10.10.14.2">
    <date type="integer">1608182171</date>
    <fail_count type="integer">5</fail_count>
  </blacklist>
</users>
```

# References