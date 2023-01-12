# 💢 ip2provider

Tags: #💢
Related to: 
See also: 
Previous: [[OSINT - Corporate Recon]]

## Description

Check which cloud provider is hosting a particular IP address. Some providers will also have service and region listed.

## Usage Examples

### Installation

	git clone https://github.com/oldrho/ip2provider.git
	cd ip2provider
	pip3 install -r requirements.txt

### Usage

	cat Target_Company.IPv4s | ./ip2provider.py

```text
X.X.X.20 digitalocean unknown unknown
X.X.X.66 aws AMAZON us-east-1
X.X.X.16 aws AMAZON eu-central-1
X.X.X.24 aws AMAZON eu-central-1
X.X.X.27 aws AMAZON eu-west-1
X.X.X.17 aws AMAZON eu-central-1
<SNIP>
```

	pigz -dc rapid7-fdns-db.json.gz | grep "target-company" | grep "core.microsoft.net\|s3.amazonaws.com\|s3-*.amazonaws.com\|googleapis.com/storage/v1/b/"

```text
{"timestamp":"...","name":"target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"cn-api.target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"com-target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"dev.target-company.core.microsoft.net","type":"a","value":"X.X.X.127"}
<SNIP>
```

# References