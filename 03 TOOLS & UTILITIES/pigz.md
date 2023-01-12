# ⚙️||💢 pigz

Tags: #⚙️
Related to: [[gzip]]
See also: 
Previous: [[OSINT - Corporate Recon]]

## Description

Parallel Implementation of GZipCompress is a fully functional replacement for gzip that exploits multiple processors and multiple cores to the hilt when compressing data.

## Usage Examples

### Decompress to stdout

	pigz -dc rapid7-fdns-db.json.gz | grep "target-company"

```text
{"timestamp":"...","name":"autodiscover.swp-target-company.de","type":"a","value":"10.125.65.10"}
{"timestamp":"...","name":"booking.target-company-reisebuero.de","type":"a","value":"10.64.96.118"}
{"timestamp":"...","name":"campaigns.target-company.com","type":"cname","value":"mnto-lon0000000.com"}
{"timestamp":"...","name":"danzas-mig.target-company.com","type":"a","value":"10.9.149.36"}
{"timestamp":"...","name":"danzas-rel.target-company.com","type":"a","value":"10.9.149.73"}
{"timestamp":"...","name":"dev.target-company.foreverdigital.org","type":"a","value":"10.10.202.10"}
{"timestamp":"...","name":"ecard.target-company.com","type":"a","value":"10.26.61.134"}
{"timestamp":"...","name":"target-company-llc.at","type":"a","value":"10.9.149.49"}
{"timestamp":"...","name":"target-company-llc.biz","type":"a","value":"10.9.149.53"}
{"timestamp":"...","name":"target-company-buchen.de","type":"a","value":"10.237.138.44"}
{"timestamp":"...","name":"target-company-christmas.de","type":"a","value":"10.160.13.20"}
{"timestamp":"...","name":"target-company-christmas.de","type":"a","value":"10.160.15.20"}
{"timestamp":"...","name":"target-company-container.com","type":"a","value":"10.9.149.53"}
{"timestamp":"...","name":"target-company-cruises.com","type":"a","value":"10.10.64.166"}
<SNIP>
```

# References