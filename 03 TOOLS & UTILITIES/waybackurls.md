# 💢 waybackurls

Tags: #💢
Related to: 
See also: 
Previous: [[00 KALI/Information Gathering]], [[Information Gathering - Web Edition]]

## Description

## Usage Examples

### Install

	go install github.com/tomnomnom/waybackurls@latest

### Get List of Crawled URLs With Date Obtained

	waybackurls -dates https://facebook.com > waybackurls.txt
	cat waybackurls.txt

```text
2018-05-20T09:46:07Z http://www.facebook.com./
2018-05-20T10:07:12Z https://www.facebook.com/
2018-05-20T10:18:51Z http://www.facebook.com/#!/pages/Welcome-Baby/143392015698061?ref=tsrobots.txt
2018-05-20T10:19:19Z http://www.facebook.com/
2018-05-20T16:00:13Z http://facebook.com
2018-05-21T22:12:55Z https://www.facebook.com
2018-05-22T15:14:09Z http://www.facebook.com
2018-05-22T17:34:48Z http://www.facebook.com/#!/Syerah?v=info&ref=profile/robots.txt
2018-05-23T11:03:47Z http://www.facebook.com/#!/Bin595
<SNIP>
```

# References

https://github.com/tomnomnom/waybackurls