# ⚙️ jq

Tags: #⚙️
Related to:
See also:
Previous: [[Hacking Wordpress]], [[Information Gathering - Web Edition]], [[OSINT - Corporate Recon]], [[OSINT]]

## Description

Command-line JSON processor.

## Usage Examples

### Certificate transparency

	curl -s https://crt.sh/\?q\=<target-domain>\&output\=json | jq .

```text
[
  {
    "issuer_ca_id": 183267,
    "issuer_name": "C=US, O=Let's Encrypt, CN=R3",
    "common_name": "inlanefreight.com",
    "name_value": "inlanefreight.com\nwww.inlanefreight.com",
    "id": 8022808792,
    "entry_timestamp": "2022-11-20T17:21:52.454",
    "not_before": "2022-11-20T16:21:51",
    "not_after": "2023-02-18T16:21:50",
    "serial_number": "0429e004d5023c66007d661e3755cd36a640"
  },
  {
    "issuer_ca_id": 183267,
    "issuer_name": "C=US, O=Let's Encrypt, CN=R3",
    "common_name": "inlanefreight.com",
    "name_value": "inlanefreight.com\nwww.inlanefreight.com",
    "id": 8020606706,
    "entry_timestamp": "2022-11-20T17:21:51.62",
    "not_before": "2022-11-20T16:21:51",
    "not_after": "2023-02-18T16:21:50",
    "serial_number": "0429e004d5023c66007d661e3755cd36a640"
  },
<...snip...>
```

	curl -s "https://crt.sh/?q=${TARGET}&output=json" | jq -r '.[] | "\(.name_value)\n\(.common_name)"' | sort -u > "${TARGET}_crt.sh.txt"

```text
account-control.facebook.com----retrieve-info.albayrakyangin.com
*.adtools.facebook.com
adtools.facebook.com
*.ak.facebook.com
ak.facebook.com
<...snip...>
```

### Format json responses

	curl http://<SERVER_IP>:<PORT>/api.php/city/london

```text
[{"city_name":"London","country_name":"(UK)"}]
```

	curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq

```text
[
  {
    "city_name": "London",
    "country_name": "(UK)"
  }
]
```


# References