# ⚙️ jq

Tags: #⚙️
Related to:
See also:
Previous: [[Hacking Wordpress]]

## Description

Command-line JSON processor.

## Usage Examples

### Format json responses

	curl http://<SERVER_IP>:<PORT>/api.php/city/london

```shell-session
[{"city_name":"London","country_name":"(UK)"}]
```

	curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq

```shell-session
[
  {
    "city_name": "London",
    "country_name": "(UK)"
  }
]
```


# References