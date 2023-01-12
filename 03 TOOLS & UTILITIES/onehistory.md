# ⚙️ onehistory

Tags: #⚙️
Related to: [[singlefile]], [[html2text]], [[npm]], [[jq]], [[csvtojson]]
See also: [[hunchly]]
Previous: [[OSINT - Corporate Recon]], [[OSINT]]

## Description

A command line tool to backup your histories of different browsers into one file. It can do sorting, filtering, searching, displaying, and exporting statistics.

## Usage Examples

### Install

	sudo apt install cargo
	cargo install onehistory
	vi ~/.zshrc

```text
export PATH=$PATH:/home/kali/.cargo/bin
```

### Export Firefox History to CSV

	onehistory export -c history.csv

```text
INFO  onehistory::export] Export 63 histories in /home/kali/history.csv.
```

	head history.csv

```text
visit-time,title,visit-count,typed-count,id,url
1607535086780,Contact – Inlanefreight,1,,tgIKscfGm4PL,https://www.inlanefreight.com/index.php/contact/
1607535085390,News – Inlanefreight,1,,6S_PX7_woFpV,https://www.inlanefreight.com/index.php/news/
1607535084030,Offices – Inlanefreight,1,,UNWCj5EDwP2e,https://www.inlanefreight.com/index.php/offices/
1607535081962,Career – Inlanefreight,1,,6r25bcvsVT21,https://www.inlanefreight.com/index.php/career/
1607535044507,Inlanefreight,2,,6bhPbKqKh9He,https://www.inlanefreight.com/
1607535044304,https://inlanefreight.com/,2,,Od54NGgg3cyS,https://inlanefreight.com/
1607535043995,http://inlanefreight.com/,2,,sfBT401xyE7c,http://inlanefreight.com/
```

### Sorted History View

	sudo apt install npm jq -y && sudo npm install -g csvtojson
	csvtojson < history.csv | jq . 

```text
[                                                       
  { 
    "visit-time": "1607535086780",
    "title": "Contact – Inlanefreight",
    "visit-count": "1",                                 
    "typed-count": "", 
    "id": "tgIKscfGm4PL",
    "url": "https://www.inlanefreight.com/index.php/contact/"
  },                                                    
  { 
    "visit-time": "1607535085390",
    "title": "News – Inlanefreight",
    "visit-count": "1",                                 
    "typed-count": "", 
    "id": "6S_PX7_woFpV",
    "url": "https://www.inlanefreight.com/index.php/news/"
  },                                                    
  {
    "visit-time": "1607535084030",
    "title": "Offices – Inlanefreight",
    "visit-count": "1",
    "typed-count": "",
    "id": "UNWCj5EDwP2e",
    "url": "https://www.inlanefreight.com/index.php/offices/"
  }, 
  <...SNIP...>
]
```


# References

https://github.com/1History/1History