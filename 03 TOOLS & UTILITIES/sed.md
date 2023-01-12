# ⚙️ sed

Tags: #⚙️
Related to: [[grep]], [[awk]], [[tr]], [[head]], [[tail]], [[cut]], [[column]], [[xargs]]
See also:
Previous:

## Description

Stream editor for filtering and transforming text.

## Usage Examples

### Remove Blank Lines

>Note: The `-r` option enables extended regular expressions, which can make the regular expression pattern more concise. The `/^\s*$/d` pattern matches any line that consists only of zero or more whitespace characters (`\s*`) at the beginning of the line (`^`) and end of the line (`$`). The `d` command tells sed to delete any lines that match this pattern.

	cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'

```text
sysLocation    Sitting on the Dock of the Bay
sysContact     Me <me@example.org>
sysServices    72
master  agentx
agentaddress  127.0.0.1,[::1]
view   systemonly  included   .1.3.6.1.2.1.1
view   systemonly  included   .1.3.6.1.2.1.25.1
rocommunity  public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly
```

# References