# ⚙️ redis-cli

Tags: #⚙️
Related to:
See also:
Previous:

## Description

Command-line client to redis-server.

## Usage Examples

### Connect to host

	redis-cli -h {target_IP}

### Get information and statistics about the server

	info

```shell-session
redis_version:5.0.7
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:66bd629f924ac924
```

```shell-session
# Keyspace
db0:keys=4,expires=0,avg_ttl=0
```

	select 0

```shell-session
OK
```

	KEYS *

```shell-session
1) "flag"
2) "numb"
3) "temp"
4) "stor"
```

	GET flag

```shell-session
<...FLAG...>
```

# References