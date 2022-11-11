# ⚙️ taskkill
Tags: #⚙️
Related to:
See also:
Previous:

## Description

This tool is used to terminate tasks by process id (PID) or image name.

## Usage Examples

### kill task by PID

	netstat -o

```
-o	// Displays the owning process ID associated with each connection.
```

```
Active Connections

  Proto  Local Address          Foreign Address        State           PID
  TCP    127.0.0.1:4444         DANTE-WS03:49825       CLOSE_WAIT      2264
  TCP    127.0.0.1:49825        DANTE-WS03:4444        FIN_WAIT_2      2844
  TCP    172.16.1.102:80        172.16.1.100:36654     ESTABLISHED     3016
  TCP    172.16.1.102:80        172.16.1.100:36666     CLOSE_WAIT      3016
  TCP    172.16.1.102:80        172.16.1.100:36668     ESTABLISHED     3016
  TCP    172.16.1.102:49780     10.10.16.52:9001       CLOSE_WAIT      4956
  TCP    172.16.1.102:49784     10.10.14.96:5555       CLOSE_WAIT      7980
  TCP    172.16.1.102:49790     10.10.14.96:5555       CLOSE_WAIT      5272
  TCP    172.16.1.102:49805     10.10.14.96:5555       ESTABLISHED     7148
  TCP    172.16.1.102:49808     10.10.14.96:4004       ESTABLISHED     2844
  TCP    172.16.1.102:49823     10.10.16.52:9001       ESTABLISHED     4824
  TCP    172.16.1.102:49826     10.10.14.96:6666       ESTABLISHED     2264
 ```

	taskkill /F /PID pid_number

# References