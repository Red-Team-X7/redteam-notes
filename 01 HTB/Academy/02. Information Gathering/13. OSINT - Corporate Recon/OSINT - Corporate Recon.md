# OSINT: Corporate Recon

Tags: #🧑
Related to: [[csvtojson]], [[ctfr]], [[curl]], [[dig]], [[exiftool]], [[h8mail]],[[head]], [[host]], [[html2text]], [[IP2Provider]],  [[ipcalc]], [[jq]], [[npm]], [[pigz]], [[shodan]], [[singlefile]], [[theharvester]], [[whois]]
See also:
Previous: [[HTB Academy]]

![[logo_osint_corporate_recon.png]]

OSINT (Open-source Intelligence) is a crucial stage of the penetration testing process. A thorough examination of publicly available information can increase the chances of finding a vulnerable system, gaining valid credentials through password spraying, or gaining a foothold via social engineering. There is a vast amount of publicly available information from which relevant information needs to be selected.

### Module Summary

This Module covers the OSINT phase of a security assessment. Strong OSINT skills are essential for penetration testers and red teamers. They can often lead to information crucial to the success of the engagement, such as a foothold into the target network.

In this Module, we will cover:

-   An overview of Open Source Intelligence Gathering
-   Gathering information about a target company
-   Gathering information about target personnel
-   Leveraging business and social networks
-   Using leak/breach data effectively

This Module is broken down into sections with accompanying hands-on exercises to practice each of the tactics and techniques we cover.

As you work through the Module, you will see example commands and command output for the various topics introduced. It is worth reproducing as many of these examples as possible to reinforce further the concepts presented in each section. You can do this in the Pwnbox provided in the interactive sections or your virtual machine.

You can start and stop the Module at any time and pick up where you left off. There is no time limit or "grading," but you must complete all of the exercises and the skills assessment to receive the maximum number of cubes and have this Module marked as complete in any paths you have chosen.

The Module is classified as "Hard" but assumes a working knowledge of the Linux command line and an understanding of information security fundamentals.

A firm grasp of the following modules can be considered prerequisites for successful completion of this Module:

-   Introduction to Networking
-   Linux Fundamentals

### Cheatsheet

|**Documentation**|
|-|
| [History Master](https://addons.mozilla.org/en-US/firefox/addon/history-master/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search) |
| [SingleFile](https://addons.mozilla.org/en-US/firefox/addon/single-file/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search) |

|**Company Information**|
|-|
| [https://www.google.com/maps/](https://www.google.com/maps/) |
| [https://earth.google.com](https://earth.google.com) |
| [https://showmystreet.com/](https://showmystreet.com/) |
| [https://www.xing.com](https://www.xing.com) |
| [https://www.monster.com/](https://www.monster.com/) |
| [https://indeed.com](https://indeed.com) |
| [https://www.glassdoor.de](https://www.glassdoor.de) |
| [https://www.trustpilot.com/](https://www.trustpilot.com/) |

|**Domain Information**|
|-|
| [https://crt.sh/](https://crt.sh/) |
| [CTFR.py](https://github.com/UnaPibaGeek/ctfr) |
| [https://certificate.transparency.dev/](https://certificate.transparency.dev/) |
| [ARIN Search](https://www.arin.net/resources/registry/whois/rws/cli/) |
| [https://mxtoolbox.com/](https://mxtoolbox.com/SuperTool.aspx) |
| [ICANN Lookup](https://lookup.icann.org/) |
| [https://dnsdumpster.com/](https://dnsdumpster.com/) |
| [GCP IP ranges](https://www.gstatic.com/ipranges/cloud.json) |
| [Azure IP ranges](https://www.microsoft.com/en-us/download/details.aspx?id=56519) |
| [DigitalOcean IP Ranges](https://www.digitalocean.com/docs/spaces/) |
| [AWS IP Ranges](https://ip-ranges.amazonaws.com/ip-ranges.json) |
| [IP2Provider.py](https://github.com/oldrho/ip2provider) |
| [https://buckets.grayhatwarfare.com/](https://buckets.grayhatwarfare.com/) |
| [https://builtwith.com/](https://builtwith.com/) |
| [https://www.shodan.io/](https://www.shodan.io/) |
| [https://archive.org/](https://archive.org/) |
| [https://archive.fo/](https://archive.fo/) |
| [Subdomain Finder](https://subdomainfinder.c99.nl/)  |

|**Files**|
|-|
| [https://www.virustotal.com/gui/](https://www.virustotal.com/gui/) |
| [http://archive.fo/](http://archive.fo/) |
| [https://pastebin.com/](https://pastebin.com/) |
| [Exiftool](https://github.com/exiftool/exiftool) |

|**Social Networks**|
|-|
| [https://twitter.com/](https://twitter.com) |
| [https://www.linkedin.com/](https://www.linkedin.com) |
| [https://www.instagram.com/](https://www.instagram.com/) |
| [https://www.snapchat.com/](https://www.snapchat.com/) |
| [https://www.youtube.com/](https://www.youtube.com/) |
| [https://www.wechat.com/](https://www.wechat.com) |
| [https://www.facebook.com/](https://www.facebook.com/) |

|**Search Engines**|
|-|
| [https://www.google.com/](https://www.google.com/) |
| [https://www.bing.com/](https://www.bing.com/) |
| [https://yahoo.com](https://yahoo.com) |
| [https://www.baidu.com/](https://www.baidu.com/) |
| [https://yandex.ru/](https://yandex.ru/) |
| [https://duckduckgo.com/](https://duckduckgo.com/) |
| [https://ask.com](https://ask.com) |
| [https://www.ecosia.org/](https://www.ecosia.org/) |
| [https://www.aol.de](https://www.aol.de) |
| [https://archive.org/](https://archive.org/) |
| [https://allpeople.com/](https://allpeople.com/) |
| [https://hunter.io/](https://hunter.io/) |
| [https://emailrep.io/](https://emailrep.io/) |
| [https://rocketreach.co/](https://rocketreach.co/) |
| [https://www.crunchbase.com/](https://www.crunchbase.com/) |
| [https://finance.yahoo.com/](https://finance.yahoo.com/) |
| [https://tineye.com/](https://tineye.com/) |
| [https://images.google.com/](https://images.google.com/) |
| [https://app.neilpatel.com/en/seo_analyzer/backlinks](https://app.neilpatel.com/en/seo_analyzer/backlinks) |
| [https://www.virustotal.com/gui/](https://www.virustotal.com/gui/) |
| [theHarvester.py](https://github.com/laramies/theHarvester) |
| [h8mail.py](https://github.com/khast3x/h8mail) |
| [https://securitytrails.com/](https://securitytrails.com/) |

|**Development Platforms**|
|-|
| [https://github.com/](https://github.com/) |
| [https://about.gitlab.com/](https://about.gitlab.com/) |
| [https://code.google.com/](https://code.google.com/) |
| [https://bitbucket.org/](https://bitbucket.org/) |
| [https://searchcode.com/](https://searchcode.com/) |
| [https://pastebin.com/](https://pastebin.com/) |

|**Forums**|
|-|
| [https://www.reddit.com/](https://www.reddit.com/) |
| [https://stackoverflow.com/](https://stackoverflow.com/) |
| [https://quora.com/](https://quora.com/) |
| [https://www.sitepoint.com/](https://www.sitepoint.com/community/) |
| [https://www.codeproject.com/](https://www.codeproject.com/) |
| [https://teamtreehouse.com/](https://teamtreehouse.com) |
| [https://stackexchange.com/](https://stackexchange.com/) |

|**Leak Resources**|
|-|
| [Rapid7 FDNS Databases](https://opendata.rapid7.com/sonar.fdns_v2/) |
| [https://haveibeenpwned.com/](https://haveibeenpwned.com/) |
| [http://archive.fo/](http://archive.fo/) |
| [https://archive.org/](https://archive.org/) |
| [https://www.cvedetails.com/](https://www.cvedetails.com/) |
| [https://www.exploit-db.com/](https://www.exploit-db.com/) |
| [https://vuldb.com/](https://vuldb.com/) |
| [https://cve.mitre.org/](https://cve.mitre.org/) |
| [https://www.securityfocus.com/](https://www.securityfocus.com/) |

# Introduction

## Open-Source Intelligence

| `curl -s` | Issue the request with minimal output. |
| `https://crt.sh/?q=<DOMAIN>&output=json` | Ask for the json output. |
| `jq -r '.[]' "\(.name_value)\n\(.common_name)"'` | Process the json output and print certificate's name vale and common name one per line. |
| `sort -u` | Sort alphabetically the output provided and removes duplicates. |* * * * *

`Open-Source Intelligence` (`OSINT`) is a process for finding publicly available information on a target company and/or individuals that allows identification of events (i.e., public and private meetings), external and internal dependencies, and connections. OSINT uses public (`Open-Source`) information from freely available sources to obtain the desired results. Some sources for collecting data are, for example, mass media such as television, radio, print media, or the Internet. The information collected from these sources will be analyzed, evaluated, and linked to each other to gain the necessary insights about our target.

The focus of OSINT lies in the word "`Intelligence`," which means constructing relationships between individual pieces of information from which we can create specific patterns and profiles about the target. The art here is to look `behind the scenes` and `think outside the box`.

It is essential to understand that the individuality and design of each company are usually entirely different. Therefore the focus of this Module is to understand and internalize the OSINT process's principles in the best possible way. We do not have to pay attention to the resources or tools we use since those can differ significantly, but rather on `the way` we find the information and use it during our assessments and how we present it to our clients to provide them the most value.

* * * * *

### Definition of OSINT
-------------------

There are many ways of describing OSINT. Many definitions of it are unfortunately wrong and could lead to `illegal` activities in most countries. In most guides and resources, we only find introductions of individual resources and tools aimed at providing us with all the most necessary information. With this, only the "`Open-Source`" part of `OSINT` is covered, and the "`Intelligence`" behind it is completely ignored or skipped. Knowing which tools are available and which ones we choose that best fit our own approach, with a bit of luck, only covers `10%` of what is needed for `OSINT`. We will see and use some resources and tools throughout this Module, but no tool can replace the core elements. All `OSINT` tools are based on specific information resources and are therefore limited to those. Those tools may help us to find some information quickly, but, as mentioned before, this is only a tiny fraction of the whole picture.

`Open-source information or open sources, is any data that can be obtained from public sources by anyone without any restrictions, whether for free or commercially, in a legal and ethically acceptable way.`

In `OSINT`, information is categorized and linked together to form a logical connection. For example, it could be an employee of a company with a developer role who uses specific source code components from their private Github repository for the company infrastructure. Whether any particular tool will even show us this source is questionable. However, the intelligence we apply manually allows us to logically relate such details to our target company.

It is `essential` to understand `precisely` what `OSINT` is and what it is `not`. OSINT is based `only` on the passive gathering of information about the target company from publicly available and (without registration or authentication required) accessible sources. To make it clear, this is mainly about interaction with the target and not about third parties. Information that is disclosed on different platforms by our target company (for example, on LinkedIn) can be used with a registered account, of course. If, for example, we are dealing with internal forums, for which we need to register to access internal information (confidential & non-public), we are actively interacting with our target, which is no longer part of OSINT. There must be no active enumeration or interaction with the target, such as brute-forcing subdomains or similar, during the OSINT phase. This type of interaction with the target is part of the active enumeration phase. The `OSINT` process should consist of only using publicly available information.

>Note: In this Module, we will see some examples of how this information can be used in later phases of our penetration test. Examples that will have to do with phone calls or physical access are, therefore, not part of the OSINT process.

`It cannot be stressed strongly enough how important it is to differentiate between these categories.`

Even if the customer has an open S3 bucket running on AWS as an example, which was not contractually defined in the scope of work and we identify it by brute-forcing the names, we are already a violation of the contract. This type of activity could lead to a problematic situation with significant consequences.

A distinction `must` be made between tools that `actively interact` with the available resources of the target company and use different methods to retrieve information or use the `disclosed information` to connect it to other parts of the databases. For example, when a tool tries to find vhosts or subdomains by brute-forcing, it is an active scanning method that sends requests to the DNS servers to confirm the existence of one of these vhosts or subdomains and is, therefore `no longer part` of OSINT.

However, when a tool extracts the SSL certificate from a web server and compares the data in databases such as [crt.sh](https://crt.sh/), also known as `Certificate Transparency`, we are not performing an active scan against the target company. In this case, we are merely using the viewable information to obtain additional information from third parties.

Below is a table that shows a few examples of when it is `OSINT` and its legality.

| **Activity** | **OSINT?** | **Legality** |
| --- | --- | --- |
| Looking for employees on Social Networks | `Yes` | Legal. Open-Source information. |
| Viewing company's website | `Yes` | Legal. Open-Source information. |
| Directory brute-forcing company's website | `No` | Illegal without permission since it is an active enumeration/scanning process. |
| Brute-forcing company's subdomains | `No` | Illegal without permissions since it is an active enumeration/scanning process. |
| Looking at certificate transparency logs to identify subdomains | `Yes` | Legal. No direct interaction with the target company. |
| Using third-party services that have collected information about the target company | `Yes` | No direct interaction with the target company. |
| Using third-party services that scan the target company | `No` | Illegal without permissions since it is an active enumeration/scanning process requested by us. |

## OSINT Methodology

* * * * *

During our penetration tests, we use OSINT to understand our target company better. The better we understand our target, the easier it will be to adapt our attacks to it, especially when it comes to `Social Engineering`. Suppose we were to go ahead and scan our customer's network. It is common for well-secured networks to have integrated IDS/IPS that would immediately ban us for several hours, if not days, based on our scan. Triggering this type of alarm right at the beginning does not show the professionalism of our activities and even contradicts it.

To perform OSINT efficiently, we need a structure that shows us the essential aspects and dependencies of the information resources and core information. The following diagram shows the critical core elements required and can, of course, contain additional components.

![[osint-structure4.png]]

Here we distinguish between the `Core Elements` we need and the `Information Resources` from which we can extract the corresponding core information.

`Core Elements` are pieces of information that give us a better picture of the company and its infrastructure. These can be names and versions of software applications, servers, names, user names, hashes, URLs, passwords, and much more.

`Information Resources` are resources from which we obtain these Core Elements. These information resources can be websites, social networks, documents, scripts, and many others.

| `Core Elements` | `Information Resources` |
| --- | --- |
| Company Information | Home Page |
| Infrastructure | Files |
| Leaks | Social Networks |
| | Search Engines |
| | Development Platforms |
| | Leak Resources |

This helps us to keep an eye on which resources we can use most of the time and tick them off one by one. However, we have to keep in mind that any information we find will lead to repeated searches and new resources for more detailed information. We can think of it as a growing tree where the core elements represent the branches, and as we add branches, we will have more nodes to connect to perform much more thorough and detailed research.

Therefore, it is highly recommended to organize the whole process in `cycles` and repeat the search with the new information for each new cycle. This systematic approach allows us to have a structured workflow and clean documentation that will enable the client and us to understand precisely how the data and information have been obtained.

For example, we can take the company name from its `website` and then search on `social networks` or use `search engines`. We can also search for it on different `development platforms` or different `forums`. Once we have gathered the core information about it, we start the `cycle` again, this time using the newly gathered information during the search for related information for the corresponding category. We try to get from the `rough to the detailed` to get a general overview of the company and only then go into detail. This makes it easier for us to research, obtain structured information, and create clear documentation.

![[osint-cycle.png]]

An important point to mention here, which may not be so apparent at first sight, is that there is no order for the information resources we need or must follow. This means that we have a great deal of flexibility to search through the different information resources and to adapt the information we find to our approach.

`Finally, a methodology is not a step-by-step guide but a structured workflow independent of the individual test cases.`

When we use OSINT, we can divide our core information results into three categories:

| **`Company Information`** | **`Infrastructure`** | **`Leaks`** |
| --- | --- | --- |
| Organization | Domain Information | Archives |
| Locations | Public Domain Records | Internal Leaks |
| Staff | Domain Structure | Breaches |
| Contact Information | Cloud Storage |\
 |
| Business Records | Email Addresses |\
 |
| Services | Third-Parties |\
 |
| Social Networks | Compounded Social Networks |\
 |
|\
 | Technologies in Use |\
 |

In this methodology, we take a point from the information categories (`Core Elements`) and search for the relevant information for it through the different `information resources`.

Theoretically, the reverse procedure can be used too. We could filter out the different information resources and enter the corresponding information results into our documentation information areas. This is the most common method used by most people for OSINT. However, it has a significant disadvantage because we have many `information resources` to adapt our methodology to, rather than our information resources to our methodology. The result is that we are left with an unstructured approach and are guided by the information resources but not by the information results. We will explain this in more detail in a moment.

During OSINT, we will come across many different resources, which contain information not only for one category but also for others. Therefore we should have at least `two separate browsers` open.

* * * * *

### Workflow
--------

`It is essential to understand that, using this methodology, we adapt our information resources to the methodology, not the methodology to our information resources.`

As a simple example, we can imagine that we want to search for all employees of a target company. Most people would start looking for the company on social networks like LinkedIn, Xing, and others, look at the company's homepage, and maybe even start a Google search. As mentioned before, this is the method that most people use, and therefore we base our methodology on the information resources.

However, if we follow our methodology, we will work step by step through the information resources shown above in cycles, starting, for example, with the home page, moving on to the social networks, using various search engines and development platforms and forums. In this way, we work according to an organized structure and get far more results.

It requires a little more effort to go through the same page several times to cover different information areas and categories (`Core Elements`). However, we maintain a structured and transparent methodology without overlooking specific details relevant to a particular information area and category. This also allows us to create clear and detailed documentation and work in cycles independent of the cases.

To make this structured methodology efficient, we need to work with two browser windows.

#### `1. Research Browser`

We use this one only for our research. Here we send all search requests and log the entire OSINT process. The research browser's history must be cleaned before use to prevent us from logging results from other companies. We can use the add-on called [History Master](https://github.com/jiacai2050/history-master) to log our searches and finally export them as documentation.

#### `2. Resource Browser`

The resource browser serves as a summary of the information resources we find during the investigation. In this one, we move all the information resources to which we can return to search for information for other categories. For example, we will get to know development platforms containing leaks and names of employees or developers, email addresses, and usernames.

In this part, we can also use the add-on called [SingleFile](https://addons.mozilla.org/en-US/firefox/addon/single-file/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search). This allows us to copy the web pages with the information and save them locally as proof.

The actual process is quite simple, as we now split our results between `two` browsers. So as soon as we have found a new information resource and examined it in the `Research Browser` and discover that there is more useful information there, we drag the newly opened tab to the `Resource Browser`, which we will turn to later.

Next, let us assume we are working on the section/phase to look for email addresses. It looks like this, but it can also expand to other information resources.

![[infra-emails.png]]

We study the `home page`, `social networks`, use the `search engines`, `developer platforms`, and the `leak resources` if we are going to follow this structure. Once we have gathered the relevant information, the `cycle` starts again in this phase, and we begin again with the home page, social networks, etc., but this time with the new information we have found from the `first cycle`.

`We document all our discoveries and structure them accordingly to each phase and our cycle.`

If we find valuable information on an information resource that we want to document, we should download this web page accordingly with `SingleFile` and save it. We will find in the beginning that our documentation (if done correctly) will be far more than 50 pages longer than most OSINT reports that are usually delivered to the client.

We also know that the employer is mainly interested in the results. However, this is not a reason not to make our documentation as detailed as it is. For the employer, the short documentation at the beginning will be sufficient. However, if the employer then wants to remove the found/leaked information, the concise documentation will not be adequate by far. Here, the information resource and the procedure for how this information resource was found are of great importance.

* * * * *

### Logging
-------

To work efficiently and in a structured way, we must also document the results and information we find clearly. However, we also need to log our steps and prove how we found the information. With the two different browsers, we have found a way to separate our search from the resources. To create clear documentation, we need three components:

1.  Visited websites
2.  Timestamp
3.  Queries

All of this information is stored in our browser history, and we can use it quite efficiently for our purposes. A handy add-on for this is [History Master](https://github.com/jiacai2050/history-master). This add-on gives us many different options, like sorting, filtering, searching, displaying, and exporting statistics.

![[history-master1.png]]

To work with history efficiently, we need a few more packages that will allow us to display the results better and make them easier to filter. If we have exported our history from `History Master` and look at it, it will look something like this:

### History CSV

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

We can install the appropriate packages as follows:

### Install NPM, JQ, and Csvtojson

	sudo apt install npm jq -y && sudo npm install -g csvtojson

This would help us sort our output much better, allowing it to be filtered with `jq`, an incredibly powerful JSON processing command-line tool. We will pipe that gathered data into `jq` to print the JSON appealingly for now.

### Sorted History View

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

### SingleFile

We can store all the websites locally using the [SingleFile](https://addons.mozilla.org/en-US/firefox/addon/single-file/?utm_source=addons.mozilla.org&utm_medium=referral&utm_content=search) add-on from which we have found the relevant information for each category. This gives us the possibility to search web page contents locally as well as proof for our documentation. This add-on offers an excellent way to download all open tabs with one click. This means that we no longer have to worry about individual screenshots of the pages and do not have to do it manually for each page.

![[singlefile.png]]

Another great advantage of this is that these stored pages can also be searched locally by our customers with simple terminal commands to see which web page the corresponding information is located on.

	cat *.html | html2text | grep "Emma Williams"

```text
Emma Williams  emma.williams@inlanefreight.com
```

This add-on also offers the possibility to save visited websites automatically. However, as we do not know what information the websites we visit will contain, this is not recommended. Of course, this can also be used for the log if necessary.

>Important Note: In this module, a real company is used to illustrate efficiency based on real situations. Therefore, many graphics in the next sections are mostly censored in order not to put this company in focus. It is also strictly forbidden for students to use this module's content to trace the selected company and do further research against it or its personnel.

## Business Investigation

* * * * *

During the investigation of a company, we collect all possible data about it. In the process, we work our way from the rough to the detailed. Business Investigation is divided into three categories of information that we can obtain:

| `Company Information` | `Infrastructure` | `Leaks` |
| --- | --- | --- |

We should note down or at least keep in mind some questions that will help us get a clear and efficient overview during our research. These questions will also help us establish links between the individual pieces of information that the actual `intelligence` piece of the phrase `OSINT` stands for.

* * * * *

### Company Information
-------------------

Company information includes the company's general overview. This means we will try to understand the company's structure:

-   How many employees does the company have?
-   What is its objective?
-   How is the company positioned in society and the market?
-   How profitable is the company?
-   How does the company function?
-   How do they manage their tasks?
-   What services does the company provide?
-   How is the company positioned financially?
-   Which target group does the company pursue?
-   Where is the company located?
-   What are the physical security measures?
-   How do interaction and advertising with (potential) customers take place?
-   How strong is the company's reputation?

This information provides us with an excellent overview of the company, enabling us to identify different companies' interests. We can then assess very precisely the level of damage a breach of the company's infrastructure would cause.

The process of staff investigation, such as employees, supervisors, and team leaders, can provide us with valuable information that allows us to assess their knowledge and experience. It is a very time-consuming stage to search for these people, as we first have to find all the people employed by the target company and then try to find everything relevant about them if the signed contract allows it.

In this search, we try to determine:

-   What position do the employees hold?
-   Which departments exist within the company?
-   Their day-to-day tasks.
-   What are they responsible for?
-   What dependencies do the employee have?

Here we will only deal roughly with the individual employees. We will deal with them more directly in another Module called `OSINT: Staff Investigation`. It requires a slightly different approach to work with the information in an efficient and structured way. Once we have gathered this information, we will move on to profiling, which we will deal with more extensively in the `OSINT: Staff Profiling` Module.

Social networks are used for personal profiles and the sharing of information from one's own private life. They are also used to publish products and news that provide new information about the company and its technologies. Therefore, in this phase, we try to determine:

-   Which products are being developed?
-   Which technologies are utilized?
-   Who are the developers?
-   Which conferences do the employees attend?
-   Where are these products used?
-   Who uses these products and services?

For example, when new software is released and sold to thousands of companies, it is interesting to get a demo of that software and analyze it for vulnerabilities. If we can identify a vulnerability, all companies that use this specific software version will also be affected by the vulnerability.

* * * * *

### Infrastructure
--------------

For the infrastructure domain, we move into more technical details. Here we try to find out:

-   How is the company set up in terms of information technology?
-   Who are the administrators?
-   Does it meet the best possible security standards?
-   Which technologies are used?
-   What entries are there about the domain?
-   Which certificates can be obtained?
-   How many domains are registered to the company?
-   What is the ASN?
-   Which netblocks has the company reserved?
-   Which third-party providers are used, and for what?
-   How many and which servers are publicly accessible?
-   How many and which email addresses are available?

This gives us a much better understanding of the technologies and the technical environment we have to deal with. Understanding how the entire company is positioned from an infrastructure standpoint is essential for identifying potential attack vectors. For example, specific configurations in the DNS servers can give us a rough idea of how experienced our target company's respective administrator is.

* * * * *

### Leaks
-----

Most of the data put on the internet is stored there for decades and can be found easily. We can find different versions of the web servers and the website's design, for example, or documents removed years ago that contained up-to-date information about employees, technologies, or processes.

Internal leaks can be found on various forums. When a developer on StackOverflow asks a question to solve a problem in their code, the code is often shared with the others to give better insight into their issue. If the developer is under a lot of pressure or distracted, they may accidentally post code containing passwords or other sensitive data. The functions that the developers are working on can be much more interesting. These may contain vulnerabilities if inexperienced developers are employed to write specific sections of code.

# Company Information

## Organization

* * * * *

When we talk about company information, we focus our interest on the points that can give us a detailed view of the entire business and its processes. This type of essential information is usually found on the target company's websites. We will not necessarily find all the necessary information to give us an `insight` into the company and its `processes`. This could tell us which companies will be most interested in working with our target company and which requirements must be met. Understanding our target company's business processes can give us an idea of how to structure our attacks. Therefore we can design our attacks to be executed during a specific step in the process.

We can also get an insight into the company's dependencies. From this, we will be able to conclude which technologies are needed to manage the company, which will indicate how the company may be structured from an infrastructure perspective.

![[osint-org.png]]

Generally, the company's home page, social networks, and search engines can be used to map out the company's organizational structure. There are no useful tools that can be used to map out the company's organizational structure efficiently. Instead, we must rely on the logical association between the information we will find during OSINT and the actual intelligence.

Furthermore, it is challenging to keep it dynamic because every company has unique staffing needs and employees, all of whom bring different strengths, weaknesses, and abilities. Therefore this field of OSINT is more a repeatable process than a static method.

---

### Locations

If our engagement is a red team assessment, then such information is much more relevant than a regular penetration test procedure. Red-teaming can also include, among other things, the physical security of the company and is used to determine which methods and techniques can be used to obtain highly sensitive information that may not be accessible from the internet. The company's locations are of great importance for this. However, the scope and rules for which procedures may and may not be used must be strictly observed.

Companies already pay a lot of money to attract potential customers by presenting themselves to their customers in the best possible way and sell themselves better from a marketing point of view. Here we can always ask ourselves when the company would arouse our `interest`.

![[osint-locations.png]]

### Staff

Every company's marketing department attaches great importance to the best possible representation of its `staff` so that potential customers can be sure they will be taken care of in a professional manner. The company's employees handle all the processes. We are interested in the information they use to interact with the company and its infrastructure. This may include but is not limited to email addresses, phone numbers, usernames, passwords, and the social networks on which they operate.

The employee's role in the company can also be used to assess their privileges in specific areas. Thus, a manager would likely have higher rights than customer support. However, even if a secretary does not have direct access to the systems, the individuals in these roles can be an attractive attack vector for us since they most likely have full access to calendars, plans, contact data, email addresses, and more.

![[osint-staff.png]]

* * * * *

### Contact Information
-------------------

Another critical point for all potential customers is the company's accessibility. For this reason, `contact details` are always disclosed. After all, customers may want to find out more about the company or even arrange a meeting. Contact information includes phone numbers and email addresses, and usernames from various communication portals such as Skype, Microsoft Teams, Slack, Discord, etc. These usernames can also be associated with the employees. This part of OSINT will be discussed in more detail at `OSINT: Staff Investigation`.

![[osint-contact.png]]

* * * * *

### Business Records
----------------

Significant customers look at the company's website and the `business records`, to learn more about it. From an OSINT perspective, they can also tell us a lot about its progress. These include the company's `locations`, `financial` situation, `references`, and `reputation`. We are particularly interested in poor feedback about the company.

Poor feedback requires poor communication and the resulting `failures` in the `business processes`. If a customer's inquiry or request is not fulfilled, it may not always be a human mistake on the part of the employee but may indicate `technical issues`. Companies often try to "hide" this feedback not to create a wrong impression for potential customers.

Business records also include the degree of recognition in the market. For example, we can get this through reviews by (former) employees or on social networks. Customer satisfaction also plays a role. We can conclude how structured and coordinated the company works internally to complete its services and overcome customer problems for the services provided.

The company's financial situation tells us a lot about its commitment and productivity. If a company continually offers new products and services, it can positively affect its financial situation. Depending on the company's size, the downside of this is that it can lead to chaotic processes. This can mean a great deal of organizational effort and communication. Therefore, it leads to a higher risk of phishing attacks because the content of a detailed, customized phishing email is rarely actually checked.

![[osint-business-records.png]]

* * * * *

### Services
--------

`Services` are also explained in great detail on the website so that the number of external inquiries is kept to a minimum. For this reason, how each service is carried out is usually discussed in detail. All other questions that arise are generally specific.

![[osint-services.png]]

* * * * *

### Social Networks
---------------

We can also ask where to find more information about the company during a phone call. We are usually directed to `blog posts`, `videos`, or `documentation` from a marketing perspective that would give us better insight into the company. We can find a variety of information about the target company through the different social media networks. We usually first direct our focus to the company's linked accounts via its home page. In turn, these may lead us to different sources of information not mentioned on the home page.

We can also search the different platforms themselves to see where the company is represented on social networks. Finally, we can use search engines or forums to find out if the company is mentioned there.

![[osint-social.png]]

## Locations

* * * * *

When we look into a company's locations, we have to identify the most obvious locations in advance. Larger companies that are active in the field of production sometimes have sites that they do not mention. These can also be identified in the OSINT process. The most prominent locations are usually listed on the company's home page. After all, the company wants to attract potential customers with the number of locations it has. It is an overall strategy for companies to present themselves as the best all over the world. This contributes significantly to marketing and increases the number of customers and thus the turnover.

In general, we can find basic information about a company's locations in advance using the following resources:

![[osint-locations.png]]

* * * * *

### Home Page
---------

If we start with the home page and browse through the site a little, we will find `countries`, `cities`, `addresses`, and possibly even `maps` that show the company's locations.

![[locations.png]]

Most of the time, we will also find lists that include the countries and/or cities where the company has its offices. These locations are usually managed locally by administrators but also may be managed centrally. If the company is centrally managed, these locations (either the entire company or specific locations) within the scope can also provide us with attack vectors that we can use to get into the systems' central administration infrastructure.

![[locations-hp.png]]

* * * * *

### Social Networks
---------------

Social networks are used to share much information, especially information that potential customers can use to learn more about the company. This includes the publication of locations of offices or production facilities. This type of information can be found on many social networks such as [Twitter](https://twitter.com), [LinkedIn](https://www.linkedin.com), [Instagram](https://www.instagram.com), [Snapchat](https://www.snapchat.com), [YouTube](https://www.youtube.com), [WeChat](https://www.wechat.com/en/), [Facebook](https://www.facebook.com), and others. Most links to a company's social networks can be found on their home page.

![[locations-sm.png]]

If we look through the posts on Twitter, we can find the company's locations and even potential routes that they use. By looking at the routes, we can determine how long specific people will be on the road, which may help us calculate the time it takes to become active as penetration testers.

![[locations-sm-twitter.png]]

Regarding the countries that the company transits, we know that it is international cooperation, which suggests that most business is conducted in English. Therefore employees may be using American or UK English keyboards and not a Chinese keyboard layout. This is valuable information to generate possible passwords when targeting employees in an attempt to gain access to externally exposed services such as email or VPN.

* * * * *

### Search Engines
--------------

Every company `location` can provide us with another potential attack vector, whether physical or technical. Each site has different employees and managers who have their way of working and can open up different attack paths for us than other locations. As soon as we have detailed information about the locations, we should document them and, in the best case, add a graphical representation as evidence in our documentation. For example, we can use [Google Maps](https://maps.google.com/), [Google Earth](https://earth.google.com/web/), [ShowMyStreet](https://showmystreet.com/), and many others to obtain these types of views.

![[location.png]]

In this case, we could pretend to be a significant client for potential collaboration and organize a meeting to be let into the building and get a much better insight into the company's processes. If the contract requires a physical test, we can also get an inside view of the building's physical security, such as door locks, windows, security, cameras, rooms, departments, and more.

Information about locations is mainly interesting for `physical Red Team` operations. This is because it distinguishes between the times at which a "break-in" can be most efficient. If a physical assessment is conducted during working hours, we must be granted appropriate access to restricted areas upfront. If possible, it is better to find a way to enter the building at night if the alarm systems and their vulnerabilities allow it. The locations themselves are the company's buildings and the location of the `offices`. Sometimes there are also badge readers that we can see and use to identify how to set up our cloner to hijack access cards wirelessly.

Suppose a manager or even higher employee feels safe in their office, which has only access to a minimal number of employees and suddenly finds a USB stick on their desk. In that case, they may wonder where it came from. The feeling of being safe increases the likelihood that the USB stick we leave behind will be plugged into their computer.

In larger companies, we will find some of these locations, which at first glance already indicate some potential weaknesses in the field of physical security. Suppose we have such an assignment where we also have to test the organization's physical security. In that case, we can use the same resources to get a picture of the terrain or even physically walk through the location as a "passerby" and record a video of the terrain with a simulated phone call. Depending on whether the location and the terrain allow it, we can also take photos from a distance. By using the online resources, we will also be able to gain some information, as shown below:

![[locations-se1.png]]

However, we have to keep in mind that these photos have not been made today and may not be up to date. Nevertheless, if we take a closer look at them, we can already see some interesting characteristics of the building, which could be helpful for us.

![[locations-se-close.png]]

We see on the second floor that there are windows that can be opened from the outside. The black pipes on the roof are metal air ducts. Theoretically, these can be used as a clamping aid for climbing up with the help of a grappling hook if a simple ladder is not available. The insight into the building itself also shows the door mechanisms that were installed. This plays a role when we want to access restricted areas when entering the building, like the manager's office, as we have previously assumed as an example.

If we take a closer look at the building from the left side, we will discover some more important information.

![[locations-se-close-left.png]]

Here we recognize three other vital parts of the building. First, we see an elevator that may be useful to us. This type of place is an excellent spot to "drop" a USB stick that we have configured, which others can then pick up. We should never underestimate a person's curiosity. If we label the USB stick with "Confidential," it will increase the interest of the people who find it. Confidential material is only ever intended for certain groups of people, and the desire to know something "secret" is far stronger than just an openly presented object. Furthermore, we see the same door mechanism to the right of the staircase. This confirms that the second floor is not a closed area but that this mechanism was most likely installed on all doors in the building.

The tilting window has blinds, which on higher floors are generally used to protect against the sun. These rooms can be valuable and may be computer rooms or server rooms which are of great interest to us. Another interesting aspect is that we can determine the width and height of the building. Building regulations dictate how specific parts of a building can be designed and must be built in most countries. Also, the bricks have standard dimensions, which we can use to determine the dimensions. Now let us look at the building from the back.

![[locations-se-close-back.png]]

We can see an antenna, another entrance into the building, and an installed camera at the back of the building. The second entrance is also attractive for us because it offers another possibility to enter the building. The antenna could become interesting for us if no camera is installed on the side of the building. A lot of information can be gained from these types of photos. Finally, we use these photos as the basis for scenarios that could lead to someone entering the building. If we are required to test physical security, we will make recommendations to close such potential gaps, which could lead to an intrusion.

#### Questions

>What are the city's coordinates where one of the company's offices, "inlanefreight.com" has its headquarters in Germany? (format: 00.0000 N, 0.0000 E)

>What are the city's coordinates where one of the company's offices, "inlanefreight.com" has its headquarters in United Kingdom? (format: 00.0000 N, 0.0000 W)

>What are the city's coordinates where one of the company's offices, "inlanefreight.com" has its headquarters in USA? (format: 00.0000 N, 000.0000 W)

>In which country is the chief financial officer located?

>How many locations does the company have in total? (format: \<num>)

## Staff

* * * * *

Information about the company's employees and managers is essential for us, enabling us to reconstruct the internal corporate structure. With this information, we will be able to identify the different departments' managers and design our social engineering attacks better and more efficiently. We are not yet looking at individual employees, but rather looking at who is employed, who is in charge of what, who is responsible for what, and try to get a picture of the internal communication flow.

The methodology we have used so far can also be applied to staff. However, this field covers many potential attack vectors for `phishing campaigns` and `social engineering` attacks, which we need to filter out. We will get many valuable results, but this does not cover everything applied to the staff. This field will be discussed in more detail in the Module `OSINT: Staff Investigation`.

In this step, we should continue to focus on getting an overview of the company's employees to gain insight into its internal structure and hierarchy and to be able to reconstruct it if necessary.

There are many sources we can use to obtain this information. Among them are the following:

![[osint-staff.png]]

* * * * *

### Home Page
---------

Most of the time, we can find the company's essential contact persons on the "`About Us`" page. These staff members are usually trained to present themselves professionally to customers and have the necessary answers to the most critical questions.

#### About Us

![[staff2.png]]

It is interesting to note that we can read a biography for the C-level staff here. This can serve us very well later in social engineering to find common topics we can discuss and gain a certain amount of trust and sympathy from the relevant persons. An important thing to note here is that these people would only deal with large customers who promise a significant profit. Otherwise, it can be hard to get directly to them.

We are interested in the employees who are already employed and want to know what types of employees the company is actively recruiting. IT offers many different specializations, enabling us to identify which technologies the company works with or plans to work with by reading through open job requisitions. Therefore we can continue to search for job offers on the homepage that are still open or on the company's [LinkedIn](https://www.linkedin.com) profile.

#### Job Offers - HomePage

![[jobs3.png]]

* * * * *

### Files
-----

Often companies offer different flyers, reports, and news in the form of `files`. The software used to create these files is usually registered and only available to authorized employees registered in the system. This data also includes the software that labels the created files with metadata. These can then be extracted and read out with the help of `exiftool`. This information can include usernames, dates, software and version numbers, geographical coordinates, and much more. We should download as many accessible files as possible and extract the metadata accordingly.

#### Report.pdf

	exiftool Report.pdf

```text
ExifTool Version Number         : 11.88
File Name                       : Report.pdf
Directory                       : .
File Size                       : 226 kB
File Modification Date/Time     : 2020:12:07 16:33:00+01:00
File Access Date/Time           : 2020:12:07 16:32:59+01:00
File Inode Change Date/Time     : 2020:12:07 16:34:16+01:00
File Permissions                : rw-rw-r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.5
Linearized                      : No
Page Count                      : 2
Language                        : en-US
Tagged PDF                      : Yes
Title                           : Lorem ipsum dolor
Author                          : John Doe
Creator                         : Microsoft® Word 2016
Create Date                     : 2020:12:03 13:42:50+01:00
Modify Date                     : 2020:12:03 13:42:50+01:00
Producer                        : Microsoft® Word 2016
```

* * * * *

### Social Networks
---------------

Finally, most employees do not want to miss the opportunity to get better job offers from other companies and keep their profiles updated on `business networks`. Maybe even with the latest projects they had to deal with to show off their skills. Every company wants to have the best possible presence on social media and, therefore, publishes links to their `company profiles`. These are often also linked to the profiles of all their `employees`. One such source could be [LinkedIn](https://www.linkedin.com), for example.

#### Employees - LinkedIn

![[linkedin1.png]]

Apart from the individual employees and their profiles, LinkedIn can also give us a better overview of our target company. For example, we can find out an estimated number of employees for our target company.

#### Employees - Number

![[employees2.png]]

This means that we have just over 8,000 employees officially linked to the company. If our scope allows it, we would have over 8,000 potential attack vectors that we could use to attack the company network via a phishing attack.

#### Job Offers - LinkedIn

![[jobs.png]]

On [LinkedIn](https://www.linkedin.com), we can also enter specific keywords in the search field, which will filter the target company employees to make our search more specific. We need people who work on computers and typically are not interested in those that do not use a computer at all in their day-to-day jobs.

#### Employees - IT Department

![[employees3.png]]

Finally, we have filtered out our potential targets very well and have specific ones to focus our attention. All business and social networks will be covered in a later section. Other valuable sources for employees and job positions are:

| | | | | |
| --- | --- | --- | --- | --- |
| [Xing](https://www.xing.com) | [Monster](https://www.monster.com) | [Indeed](https://www.indeed.com) | [Glassdoor](https://www.glassdoor.com) | [TrustPilot](https://www.trustpilot.com) |

However, to make it a little bit clearer how effective OSINT can be and how much data people disclose, check out the following video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/yrjT8m0hcKU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Furthermore, we can use `search engines` we know from which we will discover other employees, the social networks on which they appear, the `development platforms` used by developers, and other files from which we can extract metadata. We can obtain further information through these `internal leaks`. The search for employees requires an adapted approach and represents an additional larger field of information sources. It is crucial to examine them separately. Otherwise, we might get stuck in this phase. This will become much clearer in the `OSINT: Staff Investigation` Module.

#### Questions

>Check the website www.inlanefreight.com and find out the name of the chief operating officer and submit his full name as the answer.

>How many positions does the company Inlanefreight want to have filled in the future?

>How many logistics and software specialists does the Inlanefreight company employ at least?

## Contact Information

* * * * *

Contact details may be relevant to contact the appropriate person and send inquiries to find out more about the company's processes. These may include technical issues where we want to ensure that the products we offer will work with our working environment.

![[osint-contact.png]]

* * * * *

### Home Page
---------

If the company wants to present itself and clarify individual needs in the best possible way, the `contact details` page on their website will list people from different departments.

#### Contact - Website

![[contact.png]]

For example, in the next Penetration Testing phase, we could call the `phone numbers` to pretend to be customers of the company, ask short technical questions, and ask them to help us with our issues. It is also interesting to note that larger companies often have more than one domain. Therefore, the contact persons' `email addresses` may be on a different domain than the one on which the main website is located. We could, for example, use these to prepare our phishing campaigns and use these email addresses as targets. Phishing attacks can provide us with sensitive information, such as passwords or usernames, which can be very helpful, if not essential, in our penetration testing process.

This information is crucial for us, especially for phishing, vishing, and social engineering attacks in the `Exploitation phase`. Employees from the customer service and sales teams communicate a lot with (potential) customers and therefore easily fall into a routine requiring repetitive processes. By human nature, routine operations reduce the attention span, leading to the inattentive and careless performance of their tasks. This is one of the weaknesses that we can use for our purposes when we talk to an employee and influence them to click on a link we send him.

* * * * *

### Social Networks
---------------

Social networks provide us with a platform for interacting with the company's employees and offer a wide variety of information about them. It is irrelevant whether these are private social networks or business networks. What is important is that we can obtain additional information through each of these networks, including `contacts`, `partners`, `co-developers`, their `phone numbers`, and `email addresses`.

![[contact-info-social.png]]

This information is rarely made available to the public. However, with an accepted connection request, we can obtain valuable information and talk directly with the person to find more details.

* * * * *

### Search Engines
--------------

It is also beneficial to note down all the persons' `names` because they have to log in to their domain with the respective identifiers or unique name format. IT people are especially interesting because most companies allow IT people to do their work from home. This indicates that there must be a specific type of remote access mechanism for connecting to the internal network remotely.

Another excellent source to find out the email addresses of the target domain is [Hunter.io](https://www.hunter.io).

#### Email Addresses - Hunter.io

![[hunter.png]]

We can verify each email address via [Emailrep.io](https://emailrep.io) and check how the mail servers handle it.

	curl emailrep.io/<firstname>.<lastname>@<domain>.<tld>

```text
{
  "email": "<firstname>.<lastname>@<domain>.<tld>",
  "reputation": "high",
  "suspicious": false,
  "references": 7,
  "details": {
    "blacklisted": false,
    "malicious_activity": false,
    "malicious_activity_recent": false,
    "credentials_leaked": false,
    "credentials_leaked_recent": false,
    "data_breach": false,
    "first_seen": "never",
    "last_seen": "never",
    "domain_exists": true,
    "domain_reputation": "high",
    "new_domain": false,
    "days_since_domain_creation": 5130,
    "suspicious_tld": false,
    "spam": false,
    "free_provider": false,
    "disposable": false,
    "deliverable": true,
    "accept_all": true,
    "valid_mx": true,
    "primary_mx": "mx1.mailcontrol.com",
    "spoofable": true,
    "spf_strict": true,
    "dmarc_enforced": false,
    "profiles": []
  }
}
```

[RocketReach](https://rocketreach.co) allows us to identify email address formats by domain and the other email addresses linked to the corresponding managers. It is a paid service provider, but the results we get from it are very accurate, and it is an excellent way to find out links to the company's employees and the platforms they use.

#### Email Format

![[email-format2.png]]

#### Linked Email Addresses

![[emails.png]]

#### Google Search

We can also use simple Google search queries to make further connections to employees from other platforms. We must keep in mind that some social media networks are not known worldwide and are only used in specific countries for local purposes. In the process, we will repeatedly come across these platforms, which may contain helpful information. An example of one such platform is [AllPeople](https://allpeople.com).

![[contact-info-social2.png]]

However, we must not forget to use other search engines such as [Bing](https://www.bing.com/), [Yahoo](https://yahoo.com), [DuckDuckGo](https://duckduckgo.com/), and others. Each search engine works differently, and accordingly, we get different results, links, and orders for our queries. Here is a list of the most used search engines:

| | | | | |
| --- | --- | --- | --- | --- |
| [Google](https://www.google.com/) | [Microsoft Bing](https://www.bing.com/) | [Yahoo](https://yahoo.com) | [Baidu](https://www.baidu.com/) | [Yandex](https://yandex.ru/) |
| [DuckDuckGo](https://duckduckgo.com) | [Ask.com](https://ask.com) | [Ecosia](https://www.ecosia.org/) | [Aol.com](https://www.aol.com) | [Internet Archive](https://archive.org/) |

* * * * *

### Leak Resources
--------------

When we talk about leaks, we are not just talking about published databases that contain users' passwords and email addresses. Apart from the fact that these databases offer an excellent research opportunity, if we know the domain to which the email addresses are registered, we can also find new and unknown email addresses.

Apart from that, `WayBackMachine` from [Archive.org](https://web.archive.org) offers us a very effective way to search for contact information. It shows us older versions of the company website when IT security was less in focus than today. Before a company becomes large, the bosses establish themselves much more in all the necessary processes to efficiently control them. Therefore, email addresses were often published on the websites at that time to establish contact with the managers and customers better. However, in most cases, these email addresses are rarely changed by bosses and highly-positioned members. Therefore, we need to review snapshots of the target company website on WayBackMachine as part of the OSINT process. Below is an example of the various snapshots taken for a sample target company. Browsing to one of these would show us the state of the company website on the given date, which may differ significantly from the current website version and provide us with useful information or even expose hidden functionality.

#### WayBackMachine - Snapshots

![[contact-info-social3.png]]

#### Questions

>Check the website www.inlanefreight.com and find out the email address of John Smith and submit it as the answer.

>What is the email address for enterprise customer support?

## Business Records

* * * * *

Business records are also of great importance to us, as they show us how the company is doing in the market and how successful it has been to date. If there are significant fluctuations, we can then focus on the individual events and determine which factors brought about the change. In this way, we can understand in retrospect what impact specific actions related to these factors may have had on the company. Finally, our clients want to know how it can financially harm their company. A detailed overview that identifies these factors can represent an accurate prognosis of the financial damage resulting from a potential intrusion.

![[osint-business-records.png]]

* * * * *

### Home Page
---------

`Financial records` can give us a good overview of how the company is doing and how it is currently growing. It also gives us information about what the company depends on and whether it is presently healthy from a financial standpoint. As soon as a company is under high pressure, it naturally tries to save as much money as possible. These types of financial constraints often force companies to seek out lower-quality services from third parties. It does not matter whether these services are technical or not. With lower quality services, it is more likely that they do not meet the highest security standards and that we will be able to find some information about our target company.

![[finance2.png]]

* * * * *

### Files
-----

Files that we can find on the internet contain not only potentially important metadata but also general information. Every company must present itself efficiently and profitably. After all, they want to attract new customers and show their success to convince them to give them their business. Many companies demonstrate their success through financial reports. These can be found on the company's website or are sent to subscribers via newsletters.

![[business-records-finance2.png]]

Using Google search, we can find and filter out files like .docx, PDFs, and others. We can use `Google Dorks` for these purposes. A small list of the most important "dorks" can be found [here](https://securitytrails.com/blog/google-hacking-techniques).

![[business-records-finance3.png]]

* * * * *

### Social Networks
---------------

In addition to finances, the company's culture also plays an essential role. This enables us to determine how certain situations are handled and how reliably the processes function. Suppose a 3rd-level support staff member is neglected and frustrated with their company's management concerning their position. In that case, it is a very strong demotivator that consequently reflects on their performance, attention, and attentiveness. This employee will most likely put in far less effort and even less thought into the company's future.

With the help of [Google](https://www.google.com), we can find more reviews and reports about the company. This will help us identify where the most difficulties and problems occur in their processes that we can focus on later. It is essential to note the perspective from which the `reviews` have been written. They can be written either by `customer` or an `employee`. When we Google the reviews, we will find sources such as [Indeed.com](https://www.indeed.com), which gives us an excellent opportunity to look at the reviews to get a better idea of the atmosphere and process.

![[reviews2.png]]

* * * * *

### Search Engines
--------------

On [Crunchbase.com](https://www.crunchbase.com), we can find some of the `published records` concerning our target company. Often we can find financial reports from which we can find more helpful information. These reports also list some information about employees.

![[crunchbase.png]]

If our customer is a publicly-traded corporation, it is even easier for us to track its financial status. This is because we can view detailed information on them on [Yahoo! Finance](https://finance.yahoo.com).

![[business-records-finance.png]]

For us as penetration testers, it is enormously important to look behind the scenes and `think outside the box`. We need to understand how the company's financial situation has developed and which `data` and `factors` have contributed to this. If we know these, we can start to trace their `management processes` and go into more detail to understand what steps were necessary and how we as "attackers" could influence them by penetrating the corporate network.

#### Questions

>Investigate the website www.inlanefreight.com and find out how much EBIT they recorded for the third quarter of 2020 and submit it as the answer. (Format example: GBP 000,000)

## Services

* * * * *

We must `think outside the box` regarding a company's services and understand how the background processes are set up. To get a better overview, we should understand the company's goals surrounding its services for its customers and itself.

![[osint-services.png]]

Another valuable indirect source that can give us information about the technical equipment of the target company is its partners, when little information is available about these services, as shown in the following example.

* * * * *

### Home Page
---------

On the product and service descriptions page, we will often find step-by-step instructions that describe the entire process between the customer and the completion of the service or the receipt of the product. Utilizing options that are sometimes provided, such as the localization of the representative offices and contact persons, we can also find, among other things, tools that the website visitor can use. In the following example, we can see where the company's stops are on its shipping routes.

#### Service Finder

![[services.png]]

* * * * *

In this case, we can see that we can find out the specific shipping routes and that they form a network. These services may include information about the `technologies`, their `workflow`, `employees` who take care of these services, and `resources` that may contain potentially security-sensitive information.

#### Service Options

![[services_map.png]]

* * * * *

Suppose we are not familiar with the industry but want to find out how these processes and orders are set up and managed. In that case, we should search through the internet to find out what options are available and look at `similar providers` who may provide additional information. We must remember that all companies in the same industry are usually competitors. At the same time, the desire to be the #1 in the marketplace brings the same desire to provide the `best possible services` to customers, which are often `very similar`. In many cases, the company also takes advantage of `service gaps` that the competitors do not or only poorly fulfill.

These are then often prioritized. This service is presented with much more information to show that this company is significantly better than the competition.

#### Competitors Service Descriptions

![[services_similar2.png]]

* * * * *

Nowadays, the management of services is done almost exclusively through a form of software application. A high focus is placed on `web applications` and `mobile applications`, making operation and control as easy as possible for customers.

#### Service Applications

![[services_apps.png]]

* * * * *

Here we can find information about the software not only from the descriptions but also from videos. They can give us an impression of the features in advance for operating elements that require user input.

#### Service Applications - Resource

![[services_apps_vid2.png]]

* * * * *

We can also find out about different functions of these applications that our target company may not have mentioned by analyzing the company's competitors.

#### Service Applications - Competitors App Features

![[services_similar.png]]

* * * * *

### Files
-----

Information about the target company's `partners` can also be found `in files`. This is because not all partners and technologies are presented and disclosed directly. However, these companies may be marked as "`Powered by`" in these files.

#### Technologies

![[partners_tech.png]]

As mentioned earlier, we can already see that our target company uses `cloud solutions` offered by the provider. This is also very valuable to us, as we now know that we should be on the lookout for potential cloud-based storage locations that may be publicly accessible.

#### Technologies - Powered by

![[tech_poweredby.png]]

In addition to these files, information about services is often stored in detail in documents such as PDF files. This is often done because of the possibility to design these documents to be very visually appealing while communicating a lot of detailed information about the service. Here, too, appearance plays a significant role for the companies. After all, they always want to show that they are up to date and offer unique solutions for their customers' needs. It is precisely these self-developed solutions that provide us a potential attack vector that we could exploit.

#### Electronic Communication

![[services-pdf.png]]

* * * * *

### Social Networks
---------------

In principle, social networks are used by companies for marketing purposes to bring their products and services to the people and to draw attention to themselves. Here, too, information about their services and solutions is presented and published. In most cases, this is also linked so that these solutions can be viewed directly and the company's website is visited. This can play an essential role, especially with new releases of service solutions and applications. If this has been tested poorly (or even not at all) for security and vulnerabilities, then this application/solution represents a potential attack vector.

![[services-twitter.png]]

* * * * *

### Forums
------

A wide variety of technical discussions and news are discussed in forums. These are very useful for us when we want to find out something about a company's performance and services. Every post in the forum usually has a `date` when we find out when an enhancement or application, or service was released. Based on this time-lapse, we can roughly estimate how up-to-date specific `software` may be. For example, if we find an application that uses a `library` containing a vulnerability, we will be able to exploit it with the appropriate preparations and measures. More information about vulnerable libraries and how many applications are affected by those can be found in this [Veracode report](https://www.veracode.com/blog/research/announcing-our-state-software-security-open-source-edition-report).

Larger companies that have a large number of customers sometimes even provide forums for customers. We can often register and peruse these forums. `Technical problems` are usually discussed there, and we can also ask questions to find out more information. We can sometimes even see how the developers or administrators solve specific problems. With a little bit of advanced programming knowledge, we could even understand how a specific software-related problem could be solved.

#### Questions

>Investigate the website www.inlanefreight.com and find out the name of the API application the company uses and submit it as the answer.

>How many liners does the company own in total?

## Social Networks

* * * * *

With social networks, things can now get a bit more complicated and confusing, as they serve as both information elements and sources of information. If we look at social networks as sources of information, we enter what is known as `Social Media Intelligence` (`SOCMINT`). To not lose the orientation and overview of this, during the `OSINT` phase, we focus on the "movement" and presence of the company's social networks. Therefore, in this case, we will deal with the social networks and information elements. Once we get an overview of the company's presence on the social networks, we can move into `SOCMINT` and examine and analyze each platform in more detail.

![[osint-social.png]]

To make the distinction clearer, we use social networks as `Information Elements` (marked green) rather than `Information Sources` (marked red) in this phase. This means that we are collecting the company's connections to social networks.

However, this does not mean that we have to limit ourselves here. We can combine both, but we have to keep in mind that we consider social networks as information elements (i.e., pure information for the company's value). We can find a lot of information about the company itself and its technologies. These include public and internal information but is not limited to:

| `Blogs/News` | `Images & Videos` | `Wikis` | `Documents & Files` | `Social Media` |
| --- | --- | --- | --- | --- |

* * * * *

### Home Page
---------

Almost every medium-sized company strives to keep current and potential customers up to date. In most cases, these sources are also straightforward to find. After all, this `news`, which is also often published on `blogs` and `social media` platforms, provides information about our target companies' progress and success. This information is often provided to convince potential customers that the company is always the best choice.

#### Blogs and News

![[news3.png]]

This news often includes new cooperations with partners and successes achieved by the company. Additionally, new technologies and solutions for customers are presented here that we should also consider. Soon we will look at a document that may contain this type of information.

* * * * *

### Social Networks as Information Component
----------------------------------------

Most companies see social media platforms as essential and indispensable from a marketing point of view. In most cases, we find the links to the various platforms directly on the website itself. On these social media platforms, such as [Twitter](https://twitter.com), [LinkedIn](https://www.linkedin.com), [Xing](https://www.xing.com), [Facebook](https://www.facebook.com), [Instagram](https://www.instagram.com/), [YouTube](https://www.youtube.com), and others, we find not only the `latest news` and `developments` of the company but also older posts that can give us information about the `structure and technologies`.

Another often overlooked component, which does not directly belong to the social media category but fulfills the same purpose, is `newsletters`.

![[socmed2.png]]

* * * * *

### Search Engines
--------------

All search engines also allow us to search for images and videos of the company, which can also provide us with links to social networks and information sources.

#### Images & Videos

Companies often use `images` and `videos` to increase the attractiveness of blog posts and news articles. In the last section, we have already seen that we could identify a mobile application from a video and get a short impression of how it looks. Now let's look at a picture of our target company that provides us with some information.

#### Office

![[sm_image.png]]

Depending on the age of the image, certain information about the target company's technologies may vary.

| **Marked Red** |
| --- |
| However, we can see in this picture in the `marked red` area that the operating system `Windows` is used. If we take a closer look at it, we see some kind of `messenger` in the lower right corner and many small `icons` that indicate the applications used. If the image's resolution was even better, we could also read the `application name`, which we can use to search for known vulnerabilities. We could also get either the `real name` or the sender's `username` from the messenger. |

| **Marked Green** |
| --- |
| In the `marked green` area, we can see that this is a `ThinkPad`. We can see that by the `two red markings` on the mousepad. If we compare the screens' picture, we can see that `Windows` is installed on the `ThinkPad` too. |

| **Marked Blue** |
| --- |
| The `marked blue` area contains a `wireless mouse`. Since we know that these devices can also be exploited from over 100 meters away, we should also note this valuable piece of information. |

| **Marked Yellow** |
| --- |
| In the `marked yellow` area, we can see that our target company uses `Excel`. We do not get more detailed information about the Excel version, but we know it is used with Excel's corresponding `file extensions`. |

`Photos` offer a far more significant security risk than most people realize. Let us say we find a high-resolution photo of a company meeting where the work `IDs` are visible. Especially for `red-team operations`, this is incredibly beneficial because we can use the photo to recreate and prepare a badge to get past the building's security personnel and get inside the company's building.

#### Documents

The search for documents in this section is based on the fact that it allows us, among other things, to refer to sources on which social media platforms these files are stored.

A good start for finding documents and connections is Google. Using `Google Dorks`, we can define parameters that should be displayed. For this part, it is enough to know that we can use the Google Dork "`filetype:`" to define the filetype that we are seeking. This results in output to links that explicitly point to the specified file type of our target. Accordingly, we can download and view them.

Do not forget that we must document `each step` and the corresponding `source` we use to find the information. Otherwise, we will have difficulty describing how and where we got this information from in the report.

![[doc_search2.png]]

Of course, we can and must also use other file types here. We will see later in the section `Internal Leaks` the valuable information these files can give us, which can play a crucial role in the success of our engagement.

* * * * *

### Forums
------

As mentioned earlier, forums serve as a good source of information for technical difficulties and problems. Problems are also discussed and dealt with on social networks. There are countless public forums such as [Reddit](https://www.reddit.com/), [StackOverflow](https://stackoverflow.com/), and others that the company can use for this purpose. Here, too, we focus mainly on the presence of forums where people discuss our target company.

Internal forums that we may stumble upon are very interesting to us. In these, technical questions are answered in far greater detail than in public forums. Therefore, we should keep an eye out if we can perhaps register on an internal forum to search for information.

![[social-networks-stackoverflow.png]]

#### Wikis

The exciting thing about wikis is the information that is published and the `references` and `external links`, which in turn point us to other sources that can provide us with even more information. Some references and resources can be [Wikipedia](https://en.wikipedia.org), [Github](https://github.com), or even `internal/provided wikis` to which it can be linked.

We can find a lot of helpful information from the wikis that describes the company itself or its services. Wikis are created to provide detailed information about specific topics and make them accessible to others. In other words, they often serve `as documentation` that can provide valuable information for us.

For example, we may find a post describing a specific application in detail (i.e., how to install it, how to work with it, and more. We can determine which dependencies these applications have and can later use this information for `Reverse Engineering` to understand the developer better and uncover potential weaknesses.

#### Questions

>How many social networks are shown on the website of the company Inlanefreight?

# Infrastructure

## Domain Information

* * * * *

We use domain information to get a general idea of how the company is structured from a technical standpoint. It is essential to understand the basics of network technology, which we have discussed in Module [Introduction to Networking](https://academy.hackthebox.com/course/preview/introduction-to-networking) to be able to dig into how a company is structured on a technical level.

Here we work our way piece by piece from `rough to detailed` information. Therefore we first have to get a `technical overview` of the company. Since we usually already know the name of the company or even the domain name, this information is generally sufficient to determine how the company is structured.

![[infra-domain-info.png]]

It is important to note that the illustration above is only the generalized illustration that applies to most companies and scenarios and should not limit us. Each company is `individually` set up and structured, which can lead to the fact that we can get the required information via the other information resources to which the arrows in this illustration do not point.

We can classify the rough structure into three categories:

| `Public Records` | `Third Parties` | `Domains` |
| --- | --- | --- |

We need to keep this phase's goal in mind since we will be coming across many different sources and resources. After all, we are only now beginning to get an overview of the company's infrastructure. We have to be careful not to go into detail for now while we work through the following three categories, but to get an overview of how the company is positioned on the Internet.

The element we focus on in the first phase of the company's infrastructure investigation is the domain names we can find ([SLD](https://en.wikipedia.org/wiki/Second-level_domain) and [TLD](https://en.wikipedia.org/wiki/Top-level_domain), i.e., "target-company.com"). After all, these are the primary nodes on which the company's presence on the Internet is based. We then go into each domain and get an overview of the subordinate structure that contains `Netblocks`, `Name Servers`, `Mail Servers`, `subdomains`, and `hosts/IP addresses` for each domain.

![[infra-domains.png]]

#### Public Records

Public Records are the registrars with which the company has registered the corresponding domain. Since we work from rough information to detailed information, we can use the domain name to determine which `IP ranges` the domain is located in. Based on this, we can determine which `IP addresses` may belong to the company. This includes the corresponding `DNS servers` and `Mail servers`, which can later be used for attacks.

Other (`sub`)`domains` are also included. Different administration and marketing areas are shared to manage the corresponding customer groups more efficiently in most cases.

#### Third Parties

Another critical point is `third parties`. Here we have to pay close attention to what assets belong to these third parties because, during our penetration tests, we will need permission from the third party to test their systems or services if they provide services for our client. Here we have to clarify `precisely` which assets belong to these third parties to not accidentally attack them.

This includes `hosting providers` but also the `cloud` and others. If the target company has cloud assets or the website runs via a hosting provider, we `must` request the corresponding permission from the third-party provider from our client. The client must inquire with the third-party provider, inform them, and obtain the appropriate consent for us to test their systems soon.

Otherwise, this could have `serious legal consequences` for us as well as for the client.

#### Domains

Information about a domain can give us many attack vectors. Mainly because a company rarely registers just a single domain. Administrators often become complacent and pay less and less attention to details which makes our work easier.

However, it is essential to pay attention to what was defined by the client in `the scope`. Since we are `always in contact` with the client and contact them directly in case of critical discoveries, we can also suggest extending the scope accordingly if we suspect particular vulnerabilities in another domain. How this is handled, however, depends entirely on the client.

Nevertheless, as good penetration testers, we should always act in the client's best interest and provide the best possible service.

* * * * *

### Social Networks
---------------

We often find references to `domains` or `subdomains` on social media platforms. As we already know, the companies' latest technologies are presented there, and other news is shared. Social media platforms are all aimed at different target groups. Some are more for the general public, and others are for business purposes. Nevertheless, some platforms cover both groups. The dissemination of information is also very much geared to the goal that the company is pursuing. This affects how and where information is shared.

After all, a product or service that is intended for large companies does not necessarily make sense. This is not necessarily true, but this example should only serve as an illustration of the differences. After all, this depends on many factors, such as target group, marketing strategy, product orientation, financial possibilities, and much more. Furthermore, `hashtags` are often a beneficial information element that allows us to narrow down relevant information about our target company on the entire platform (or even across social media platforms).

![[infra-domain-info-fb.png]]

The images we find on these platforms are usually not intended for only one of them. They are often uploaded to other platforms as well. We can find them with a `reverse image search` like [TinEye](https://tineye.com/) or [Google Images](https://images.google.com/) and get additional sources of information that we can use.

* * * * *

### Search Engines
--------------

One of the most efficient methods of searching for `domains` is offered by various `search engines`. In this case, we cannot focus on a domain name, but we have to work with general company terms, such as the company name, the name of the application or service, and others. We must try to narrow down the search results to our target company to avoid misinformation that costs us valuable time. Finally, we need to pay attention to how these (at best unique) terms and labels we use are scattered on the Internet and how they connect us to our target company.

When Googling these terms, we can stumble across a wide variety of information resources. Each of the discovered and visited information resources should be saved in our research browser for later examination.

Another excellent way to find out information about our target domain is to use a particular `Search Engine Optimization` (`SEO`) field called `backlinks`. A backlink is a link from an external page to another website. Search engines like Google use the backlink profile as an indicator to rank the website. The more high-quality backlinks, the more popular a page appears to be on the Internet. The advantage of backlinks analyzers is that they aggregate all backlinks, identifying the sources that discuss and mention our target company. One of such backlinks analyzers is [Ubersuggest](https://app.neilpatel.com/en/seo_analyzer/backlinks).

![[domain-info-ubersuggest.png]]

The interesting thing here is that we can see all the sources and identify the webserver structure and its contents (paths, files, subfolders) without performing any active enumeration.

From the beginning, Google has focused on the evaluation of backlinks as a signal of trust between domains. This orientation has made Google the most powerful and relevant search engine. The famous PageRank calculation, which formed the basis of Google's search algorithm, analyzes links between different pages on the Internet and deduces how trustworthy a particular website is.

* * * * *

### Development Platforms
---------------------

Development platforms also offer excellent information resources for us here, as we will often find code that sometimes even provide information that is dangerous for the company. This information can range from `IP addresses` and `hostnames`, configuration files to `credentials`. These platforms include, but are not limited to:

| [Github](https://github.com/) | [GitLab](https://gitlab.com) | [Google Code](https://code.google.com/) | [Bitbucket](https://bitbucket.org) |
| --- | --- | --- | --- |

Again, we can search for the terms like the company name or the application name they offer. Although the developers know what data might be stored there, this is often considered low-risk. Besides, `configuration files` or even `backups` can also be found. This type of data is not infrequently encrypted, but even if it is, it does not prevent us from downloading them and trying to decrypt them.

>Author's note:
>
>During every investigation of a company where I found sensitive information this way, the most common excuse given by the responsible employees was that no one cared. Nevertheless, I was obligated to immediately contact the customer if I found information such as credentials and recommended that they remove them as quickly as possible. There is no justification from the administrator's or developer's point of view to keep this information unrestricted. The only thing to do is change the leaked credentials immediately and set the resource with this information to "private" if it can not be taken down. In the end, the developers and the administrators could see that this small piece of information allowed me to compromise the company's servers and would have caused massive financial damage.

* * * * *

### Leak Resources
--------------

Once we have a list of the company's `domains`, we can use it to look for known anomalies that affect the company and the corresponding domain. One of the best sources of information for this is [VirusTotal](https://www.virustotal.com), where we can scan each domain for suspicious activity.

![[infra-domain-info-leaks3.png]]

These entries can point to `files`, `email addresses`, `domains`, and other links. Searching on the developer platforms goes hand-in-hand with the leak resources, and it will help us a lot to keep track of things by looking for the related `domains` first and looking at the other information later.

Another source that searches against many different developer platforms is [Searchcode](https://searchcode.com). It searches all possible codes for terms that we specify in the search and shows us the sources accordingly. It is not uncommon for us to come across information that may look something like this:

#### Sourcecode

![[infra-domain-info-leaks.png]]

#### Github

![[infra-domain-info-leaks2.png]]

## Public Domain Records

* * * * *

As we know, we need a rough overview of the technical structure of the company. After we have identified and filtered out all the domains that belong to them, we can focus on their structure and composition.

![[infra-pub-records.png]]

Public domain records also offer us excellent opportunities to trace the company's information technology infrastructure structure. With the right arrangement and knowledge of what the records are for and what information they contain, they can provide us with information about the company's Internet presence. To get this, we need to find out at least four components:

| `1. Netblocks / CIDR` | `2. ASN` | `3. DNS Servers` | `4. Mail Servers` |
| --- | --- | --- | --- |

This gives us an overview of which systems are `accessible` from the internet, in which `address range` they are located, which `IP neighbors` they have, and how the interaction between them takes place.

* * * * *

### Search Engines
--------------

When going through different search engines, we are talking about the search engines that can be used for this purpose and databases containing relevant information for us. The minimum information we need to get from our client, apart from the company's name, is a domain or at least an IP address to start with. The scope of this can vary greatly.

#### 1. Netblocks / CIDR

During a black-box penetration test, our client will often only provide the domain name. We can use this to find out a lot of helpful information. First of all, we should find the `IP address` of the main webserver(s) and the `IP address range(s)` / `CIDR`. For this, we can use the following command.

#### Host

	host www.inlanefreight.com

Now that we have the IP address of the web server, we can find out which `IP address range` it is located in. By default, we can work with the `Whois` protocol used by a distributed database system to retrieve information about internet domains and IP addresses and their owners.

#### Whois

	whois 134.209.24.248

```text
% IANA WHOIS server
% for more information on IANA, visit http://www.iana.org
% This query returned 1 object

refer:        whois.arin.net

inetnum:      134.0.0.0 - 134.255.255.255
organisation: Administered by ARIN
status:       LEGACY

whois:        whois.arin.net

changed:      1993-05
source:       IANA

# whois.arin.net

NetRange:       134.209.0.0 - 134.209.255.255
CIDR:           134.209.0.0/16
NetName:        DIGITALOCEAN-134-209-0-0
NetHandle:      NET-134-209-0-0-1
Parent:         NET134 (NET-134-0-0-0-0)
NetType:        Direct Allocation                                               
OriginAS:       AS14061 
```

We can also search the `WHOIS` databases for the company name. We are often given different identification numbers (`mnt-ref`), which we can use for further searches. These stand for the maintainer objects, which are used as a reference for the organization objects.

#### WHOIS - MNT-REF

	whois -B --sources RIPE,ARIN target-company

```text
% Information related to 'ORG-ZZ000-RIPE'

organisation:   ORG-ZZ000-RIPE
org-name:       Target-Company LLC
country:        CO
org-type:       XXX
address:        Street 00
address:        00000
address:        City
address:        COUNTRY
phone:          +00000000000
fax-no:         +00000000000
mnt-ref:        EU-IBM-XXX-0000
mnt-ref:        HN0000-MNT
mnt-ref:        AS0000-MNT
mnt-ref:        RIPE-XXX-ZZ-MNT
mnt-by:         RIPE-XXX-ZZ-MNT
mnt-by:         HL0000-MNT
abuse-c:        AHA000-RIPE
created:        2010-01-12T13:57:44Z
last-modified:  2021-10-14T12:14:22Z
source:         RIPE
e-mail:         full.name@target-company.com

% Information related to 'AHA000-RIPE'

role:           ABUSE Target-Company LLC
address:        Street 00, 00000 City, Country
e-mail:         dns.admin@target-company.com
abuse-mailbox:  dns.admin@target-company.com
nic-hdl:        AHA000-RIPE
mnt-by:         RK00000-MNT
created:        2014-11-15T11:54:10Z
last-modified:  2014-11-15T11:54:10Z
source:         RIPE

% Information related to 'HN0000-RIPE'

role:           Target-Company NOC
address:        Street 00, 00000 City, Country
e-mail:         dns.admin@target-company.com
nic-hdl:        HN0000-RIPE
mnt-by:         AA00000-MNT
created:        2019-04-07T06:44:22Z
last-modified:  2019-04-07T06:44:22Z
source:         RIPE
```

We can also query the individual databases and identify the associated netblocks.

#### WHOIS - Netblocks

	whois -h whois.arin.net target-company | grep -v "#" | sed -r '/^\s*$/d'

```text
Target-Company (C00000) 10-10-60-68 (NET-10-10-60-68-1) 10.10.60.68 - 10.10.60.69
Target-Company (C00000) 10-10-60-70 (NET-10-10-60-70-1) 10.10.60.70 - 10.10.60.71
```

Here is the [ARIN list](https://www.arin.net/resources/registry/whois/rws/cli/) of other flags we can use to get more information from the maintainer objects.

#### 2. ASN

We can also see another crucial piece of information here, the `OrigisAS`. This is the `Autonomous System Number` (`ASN`). This number is unique and is made publicly available so routing information can be exchanged with other systems. This is done with specific IP prefixes, which we can use to find out the netblocks (`public ASNs`). There are also `private ASNs` intended for systems that only communicate via a provider. Other protocols such as the `Border Gateway Protocol` (`BGP`) are used if this is the case. We can use [MXToolbox](https://mxtoolbox.com/SuperTool.aspx) and its `ASN Lookup` option with the ASN to find out how many subnets the owner has.

![[infra-domain-structure-asn.png]]

Another way to get more information about the domain is to use the [ICANN lookup](https://lookup.icann.org/lookup). Each domain is registered to an organization or person with a unique ID, which provides information about when the domain was created and expires.

![[infra-domain-structure-icann.png]]

#### 3. DNS Servers

DNS servers are essential services today because they help the regular user reach the web services they want. We are now familiar with how DNS works after we have worked through `DNS Enumeration using Python` Module and know what information we can get from it. It is often the case that companies own several domains, and accordingly, these domains can offer different attack vectors that can affect each other. The next step is to look at the DNS records of our target domain using `dig`. `Dig` is a DNS lookup utility that can be used to obtain publicly available information from DNS.

#### DNS Records - Inlanefreight.com

	dig any inlanefreight.com

```shell-session
<SNIP>
;; ANSWER SECTION:
inlanefreight.com.	7191	IN	A	X.X.149.43
inlanefreight.com.	7191	IN	MX	10 cluster-j.inlanefreight.com.
inlanefreight.com.	7191	IN	MX	10 cluster-e.inlanefreight.com.
inlanefreight.com.	7191	IN	TXT	"v=spf1 include:inlanefreight.com ?all"
inlanefreight.com.	7191	IN	TXT	"nFM+YEvc/npla0It+GWBy9tZgud2Z3Q2i/bFxrHRfbzv1G09Mx7pB9=="
inlanefreight.com.	7191	IN	TXT	"MS=ms80134"
inlanefreight.com.	7191	IN	SOA	ns1.inlanefreight.com. abuse.infreight.com. 2012110855 21600 3600 604800 600
inlanefreight.com.	7190	IN	NS	ns1.inlanefreight.com.
inlanefreight.com.	7190	IN	NS	ns2.inlanefreight.com.
<SNIP>
```

If we now take a closer look at the records, we see that the SOA record shows another domain, `infreight.com`. Therefore we will also look at these if the scope allows us to do so. In this case, we assume that we have permission to test this domain as well.

#### DNS Records - Infreight.com

	dig any infreight.com

```text
<SNIP>
;; ANSWER SECTION:
inlanefreight.com.		7200	IN	A	134.209.24.248
inlanefreight.com.		7200	IN	SOA	ns1.infreight.com. adm.infreight.com. 2012111147 21600 3600 604800 600
inlanefreight.com.		7200	IN	MX	10 cluster-e.inlanefreight.com.
inlanefreight.com.		7200	IN	MX	10 cluster-j.inlanefreight.com.
inlanefreight.com.		7200	IN	TXT	"MS=ms90101"
inlanefreight.com.		7200	IN	TXT	"v=spf1 include:mailcontrol.inlanefreight.com include:mailing.inlanefreight.com ?all"
inlanefreight.com.		7200	IN	TXT	Here is the [ARIN list](https://www.arin.net/resources/registry/whois/rws/cli/) of other flags we can use to get more information from the maintainer objects:"8MdY05nra9NlO2voN5icWjuhq0za+5JvpM3xAgt/gg=="
inlanefreight.com.		7200	IN	NS	ns3.inlanefreight.com.
inlanefreight.com.		7200	IN	NS	ns1.inlanefreight.com.
inlanefreight.com.		7200	IN	NS	ns2.inlanefreight.com.
<SNIP>
```

Again, we have discovered new potential targets based on the DNS records only, which we have to document in our list to take a closer look at them later.

Another source we can use, which gives us a much better representation of the DNS servers' records, is [DNSdumpster](https://dnsdumpster.com/).

#### DNSdumpster - Records

![[dnsdumpster_records.png]]

Here we can see the entries for the respective DNS servers and the `locations` of the corresponding hosts and servers.

#### DNSdumpster - Locations

![[dnsdumpster2.png]]

Then we see the respective IP addresses and corresponding subdomains that could be obtained from the entries. Additionally, [DNSdumpster](https://dnsdumpster.com/) can sometimes show us the services running on the server if it can passively identify them.

#### DNSdumpster - Hosts

![[dnsdumpster_hosts.png]]

Finally, at the bottom of the page, we can see a domain map that shows the relationships between the servers connected with the records.

#### DNSdumpster - Domain Map

![[dnsdumpster.png]]

#### 4. Mail Servers

Mail Server / Exchange server (`MX`) is one of the most critical services today, as it ensures that our emails reach the desired communication partners. Other servers use it as an interstation (relay) for sending spam or viruses. It often happens that `MX` servers do not only use specially registered servers as relays. This gives us the possibility to perform an `Open Relay Attack`.

`MX` servers represent a massive attack vector. There is nothing worse for a company apart from a complete compromise than the fact that all unencrypted emails can be intercepted and read. This means that not only GDPR guidelines have been violated by requiring the company to ensure that customer data is kept confidential, but it also significantly impacts customer satisfaction and customer trust, which will be significantly damaged.

[MXtoolbox](https://mxtoolbox.com) offers an excellent service to test the `MX` servers for Open Relay.

#### MXtoolbox - Open Relay Check

![[mxtools.png]]

* * * * *

### Development Platforms
---------------------

Searching for code on developer platforms can bring surprising results. Apart from already highly sensitive data such as user names and passwords, we can also find `configuration files` containing the latest administration settings. We can use [Searchcode](https://searchcode.com) again with specific strings and known `IP addresses` or `domain names` to get such results. However, in this case, we need a basic understanding of the configuration files, how they can look, and which variables can be used for DNS configuration.

![[infra-domain-structure-devplat.png]]

#### Questions

>Find out how many nameservers are responsible for the inlanefreight.com domain and submit the number as the answer.

>Find out the FQDN of the mail server of the inlanefreight.com domain and submit it as the answer.

>What is the registry domain ID of inlanefreight.com?

>What is the name of the registrar of this domain?

>Examine the DNS records and submit the TXT record as the answer.

## Domain Structure

* * * * *

Now that we have gathered a lot of information, we need to focus on the `intelligence` of this process and create an `overview of the domain`, and `analyze` our results. We should take our time because the better we understand the structure of the domain, the easier it will be to take the appropriate steps later. Furthermore, we narrow down the goals and seek out the `low hanging fruit` of all the systems that promise the best possible results for us.

![[infra-domain-structure.png]]

This preparation can take several hours of study but save us time in the following steps because we will not test each system blindly, but `proceed methodically`, `organized` and `structured`. This represents the professionalism of our work and gives a much better impression in the reports for our customers.

* * * * *

### Home Page
---------

Countless websites link to other subdomains. This may be marketing or may have been preconfigured for analysis reasons. Therefore, we should always pay attention to each clickable area on every web page owned by the company.

![[infra-domain-structure-homepage.png]]

#### Subdomains

The search for subdomains is multifaceted, and many methods can be used for this purpose. These methods are widely discussed, and many of these techniques are presented as legal. Here we have to be very careful because only the `first four` techniques are legal and do not directly interact with the target's infrastructure (provided we have permission).

1.  `Certificate Transparency`
2.  `Forward DNS Datasets`
3.  `Web Search`
4.  `Disclosure / Leak`
5.  Subdomain Brute-Forcing
6.  AXFR

`Subdomain brute-forcing` is an active testing method where a domain query is sent to the DNS servers. Any dynamic interaction and investigation of the domain without written permission is `illegal` and may result in criminal charges. If any damage is done in the inquiry, these queries can be tracked very easily.

`AXFR` also belongs to an active method that refers to the misconfiguration of a DNS server. This method can have even `more severe consequences`, as a targeted attempt is already being made to exploit a potential vulnerability.

Therefore, we should `always pay attention` and always check what we do next, and whether it is in line with the contract signed with our client.

* * * * *

### Search Engines
--------------

Since we are still in the passive information gathering phase, we should use passive techniques to find out more subdomains. For this, we can use a tool called [CTFR](https://github.com/UnaPibaGeek/ctfr). It uses `Certificate Transparency` logs from [Certificate Transparency](https://www.certificate-transparency.org) and [crt.sh](https://crt.sh/).

	./ctfr.py -d inlanefreight.com | grep -v "[-]"

```text
          ____ _____ _____ ____  
         / ___|_   _|  ___|  _ \ 
        | |     | | | |_  | |_) |
        | |___  | | |  _| |  _ < 
         \____| |_| |_|   |_| \_\
    Made by Sheila A. Berta (UnaPibaGeek)

inlanefreight.com
vc.inlanefreight.com
afdc0002.inlanefreight.com
afdc0101.inlanefreight.com
afdc0102.inlanefreight.com
wlan.inlanefreight.com
afdc0102.inlanefreight.com
wlan.inlanefreight.com
autodiscover.inlanefreight.com
kfdcex07.inlanefreight.com
kfdcex08.inlanefreight.com
videoconf.inlanefreight.com

[!]  Done. Have a nice day! ;).
```

We can now use [CTFR](https://github.com/UnaPibaGeek/ctfr) for each subdomain in a `For-Loop` because there may be other subdomains in the respective subdomains. After we have collected and documented all passive results, we can use a simple `For-Loop` in Bash to determine the corresponding IP address for each subdomain.

	for sub in $(cat subdomains);do host $sub | grep "has" | cut -d" " -f1,4;done

```text
inlanefreight.com X.X.149.43
vc.inlanefreight.com X.X.164.24
autodiscover.inlanefreight.com X.X.145.34
kfdccv04.inlanefreight.com X.X.48.249
ftp.inlanefreight.com X.X.48.249
rbpoint.inlanefreight.com X.X.48.249
<SNIP>
```

Then we can use `whois` and `ipcalc` to find out the IP ranges for the respective IPv4 addresses.

#### 2. IP Addresses

There are many different resources we can use to find out the IP addresses of our target company. One of the best and most used resources is [Shodan](https://www.shodan.io/). `Shodan` also offers a [CLI](https://cli.shodan.io/) version that we can install. This allows us to query, filter, and save the results directly from the command line, making documentation much more manageable.

#### Shodan

	shodan domain <TARGET-DOMAIN> | grep -w "A" | cut -d"A" -f2 | cut -d" " -f7 | sort -u > IPv4s.txt
	cat IPv4s.txt | wc -l

```text
36
```

Now we can see that we were able to find `36` unique IPv4 addresses that we can later analyze and check for vulnerabilities. Of course, only if they are within the scope and not otherwise specified in the contract. If we run all found IPv4 addresses through `Shodan`, we will determine which ports the hosts have open in a passive way without having to interact with them directly.

	for ip in $(cat IPv4s.txt);do shodan host $ip;done

```text
X.X.164.24
Hostnames:               vc.inlanefreight.com
Country:                 United Kingdom
Organization:            Inlanefreight
Updated:                 2020-07-23T15:26:40.055514
Number of open ports:    7

Ports:
    443/tcp  
   2222/tcp  
   5060/udp TANDBERG/4137 (X12.5.1) 
   5222/tcp  
   7001/tcp  
   7443/tcp  
   8443/tcp  

X.X.48.186
Hostnames:               mail.inlanefreight.com
Country:                 United Kingdom
Organization:            Inlanefreight
Updated:                 2020-07-08T08:36:17.845819
Number of open ports:    2

Ports:
    443/tcp  
   8888/tcp  

<SNIP>
```

[Spyse](https://spyse.com) offers excellent results in an excellent presentation. Apart from the different search options this platform provides, the results are quite accurate and informative. For example, we can search for more IPv4 addresses, and we will find that `Spyse` results in IPv4 addresses that we have not found before.

#### Spyse

![[spyse.png]]

#### Found IPv4 Addresses

	cat IPv4s.txt | grep "48.46\|48.216\|48.218\|48.162"

```text
5
```

After this, we can use [IPinfo.io](https://ipinfo.io). This resource provides an excellent way to identify the subnets and hosting providers. Furthermore, we can use Spyse to search for additional subdomains by entering the top and second-level domains (e.g., target-company.htb).

#### Spyse - Additional IPv4 Addresses

![[spyse_ips.png]]

Good results are also offered by the previously discussed platform [VirusTotal](https://www.virustotal.com). It is important to note that the datasets are collected from different sources by these platforms. Therefore, it is necessary to check both of them and complete the missing entries with each other.

#### VirusTotal

![[infra-domain-info-virustotal.png]]

Another great way to quickly search for subdomains is [C99.nl](https://subdomainfinder.c99.nl/index.php). We should remember that we should always use multiple sources to find all subdomains if possible. This is because we will rarely have situations where a single source provides us with all available subdomains. Additionally, we can see here if the hosts are behind `Cloudflare` and are protected or not.

![[infra-domain-c99nl.png]]

Then we can use `whois` and `ipcalc` to find out the IP ranges for the respective IPv4 addresses.

#### 2. IP Addresses

There are many different resources we can use to find out the IP addresses of our target company. One of the best and most used resources is [Shodan](https://www.shodan.io/). `Shodan` also offers a [CLI](https://cli.shodan.io/) version that we can install. This allows us to query, filter, and save the results directly from the command line, making documentation much more manageable.

#### Shodan* * * * *

### Virtual Hosts
-------------

With the IP addresses and subdomains, we can determine how many and which subdomains are `virtual hosts` (`vHosts`). Some good sources that we can use are [Pentester-Tools](https://pentest-tools.com/information-gathering/find-virtual-hosts) and [Hacker-Target](https://hackertarget.com).

#### Hacker-Target - vHosts

![[hacker-target.png]]

* * * * *

We can easily recognize `vHosts`, because they share the same IP address for at least two subdomains. As we can see from the previous example, we have three `vHosts` sharing the same server.

#### Manual vHosts Discovery

```text
kfdccv04.inlanefreight.com X.X.48.249
ftp.inlanefreight.com X.X.48.249
rbpoint.inlanefreight.com X.X.48.249
```

Another possibility is to enter the IP addresses in a search engine. Most of the time, these are connected to different subdomains or even to other service providers that also run on the same server.

* * * * *

### Development Platforms
---------------------

For the developer platforms, we should be on the lookout for all possible files, as eventually, any of them may contain hints about `domain names` or `IP addresses`. Configuration files are of particular interest, as they may contain access data and have fixed IP addresses and (sub)domains. For this, we can again use [Searchcode](https://searchcode.com) to find files of this kind quickly.

![[infra-domain-structure-devplat.png]]

Another very interesting source of information is the [SEOptimer](https://www.seoptimer.com). This is an SEO analysis tool that examines and evaluates the entire website for individual components. The results include fields like:

-   Sub-Pages
-   SEO
-   Rankings
-   Usability
-   Performance
-   Social
-   Security
-   Technology Rankings
-   Recommendations

In general, marketing tools are designed to evaluate visitors' interactions on the website and allow SEO specialists and web designers to make the appropriate adjustments to improve the rating or create a better UX. Since they work a lot with links, we will likely find out a lot of helpful information.

![[infra-domain-seo.png]]

* * * * *

### Leak Resources
--------------

Leak resources are unauthorized publications of information. This term is broad and can therefore include many different information components. These resources also include databases with datasets containing information about our target company. At the end of 2017, Rapid7 started [Project Sonar](https://opendata.rapid7.com/sonar.fdns_v2/), which collects and stores responses forwarding DNS requests. DNS records such as `A`, `AAAA`, `CNAME`, and `TXT` lookups are stored at certain intervals in individual `GZIP` files in the form of `JSON`. These databases are extensive and can exceed 30GB in compressed format. They contain (sub)domains, record types, and the corresponding IP addresses. This information resource serves as an updated and valuable resource for us to understand our target company's domain better.

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

The advantage here is that we can discover internal IP addresses and new `TLD`s. This gives us a much larger attack surface if the scope in the contract with our customer allows this. Some domains are added for specific fields, which we can use as further information resources.

#### Questions

>Investigate the website www.inlanefreight.com and find out the Apache version of the webserver and submit it as the answer. (Format: 0.0.00)

>What is the hosting provider for the inlanefreight.com domain?

>What is the ASN for the inlanefreight.com domain?

>On which operating system is the webserver www.inlanefreight.com running?

>How many JS resources are there on the Inlanefreight website?

## Cloud Storage

* * * * *

Working with various cloud providers such as `Google Cloud Platform (GCP)`, `Microsoft Azure`, or `Amazon Web Services (AWS)` can be complex. Primarily because, from a legal point of view, it is dealt with on a cross-border basis. If personal data is collected, processed, or used in the cloud, personal data protection must be guaranteed by data protection regulations. The characteristic of the cloud is the transfer of data from the user to the cloud provider. When data is transferred from the user to the cloud provider, the user relinquishes responsibility under data protection law and transfers it entirely to the cloud provider. The user thus also fundamentally loses the possibility of influencing the handling of the data transmitted by them. However, at the civil law level in Europe, a different distribution of liability is also possible with appropriate contract design, namely a (partial) retention of liability by the user.

![[infra-cloud.png]]

After all, the cloud servers are not always located in the same country as we are. Therefore, other regulations and laws applicable in the respective country, which may collide with ours. This is important to understand as we are still in the `passive` information gathering process and therefore may not actively interact with and scan the target company.

We can now resolve the domains found into IP addresses and compare them to the netblocks for these three cloud providers. If we find any IP addresses within these IP ranges, we can assume that it is a cloud provider. For us, the most critical component in the corporate use of a cloud provider is open cloud storage because if they have been misconfigured, they are publicly `accessible` and `viewable`. Some of those cloud providers are, but not limited to:

| | | | | |
| --- | --- | --- | --- | --- |
| Cloud Provider | [GCP](https://www.gstatic.com/ipranges/cloud.json) | [Azure](https://www.microsoft.com/en-us/download/details.aspx?id=56519) | [AWS](https://ip-ranges.amazonaws.com/ip-ranges.json) | [DigitalOcean](https://www.digitalocean.com/docs/spaces/) |
| Open Cloud Storage | `Google Storage Bucket` | `Block Blob` | `S3 Buckets` | `Spaces` |

We can also automate this process with the tool [ip2provider.py](https://github.com/oldrho/ip2provider). This will automatically compare the IP addresses with the netblocks and show if they are successful matches.

#### IP2Provider.py - Installation

	git clone https://github.com/oldrho/ip2provider.git
	cd ip2provider
	pip3 install -r requirements.txt

#### IP2Provider.py - Usage

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

* * * * *

### Home Page
---------

When searching for cloud buckets, one factor makes it difficult for us to identify the bucket belonging to the company. This is that everyone can create their own name for the desired bucket. This means that anyone can create a bucket with the target company's name without it belonging to the company.

Here we can also find a list of URLs from which we can see which cloud provider the storage belongs to and where we could find it.

| `Cloud Provider` | `URL` |
| --- | --- |
| [GCP](https://www.gstatic.com/ipranges/cloud.json) | https://www.googleapis.com/storage/v1/b/ \<bucket-name>/iam |
| [Azure](https://www.microsoft.com/en-us/download/details.aspx?id=56519) | https:// \<bucket-name>.core.windows.net/ \<container>/ |
| | https:// \<bucket-name>.blob.core.windows.net/ \<container>/ |
| [AWS](https://ip-ranges.amazonaws.com/ip-ranges.json) | https:// \<bucket-name>.s3.amazonaws.com |
| | https://s3- \<region>.amazonaws.com/ \<company-name> |

Almost all (`~95%`) vulnerabilities in the cloud happen due to `misconfigurations`. These misconfigurations include, but are not limited to:

-   ACLs
-   Bucket Policies
-   Service Control Policies
-   Public Access Blocks
-   IAM Policies

Cloud environments extend the penetration testing process enormously. However, this does not affect the OSINT process since we ultimately use public resources to not interact with our target company. Further investigation of cloud buckets will be covered in another Module, as we need to investigate and understand the setup and the individual configuration options to work with them effectively. However, we already know enough to find open cloud buckets. Whether they are open and whether we can see the content on them requires interaction. Therefore, we will stop after finding them, and in the next stage, we will deal with them and enumerate them.

The first information resource often used for this purpose is the company's website. Buckets are often used as a source for the web servers and their contents are linked accordingly. An example may look something like this:

![[infra-cloud-homepage-link.png]]

We can also use this content and the names of the files or the company's full domain name (i.e., www-target-company-com) for [Searchcode](https://searchcode.com) to see if they are publicly retrievable and if there might even be more information resources for them. To do this, we take the name of the file and can, for example, look for other cloud providers to see if they are available there. The more unique the name of the file is, the more accurate the results will be. These are then easier to identify and connect to the target company.

![[infra-cloud-searchcode-homepage.png]]

* * * * *

### Search Engines
--------------

If files have been tagged or named in conjunction with the company name, we can use the search engines we know and filter the results based on the cloud providers. Aside from file names and company names, we may also use employee names or application names if they appear unique. For this, we can set the known domains from the cloud providers as the assumed content (with the `inurl:` tag) for our results. This will reduce the results only to those that contain this domain. Finally, we know that the buckets' label will not necessarily have the name or label we have already seen. For this, search engines help us to expand our search scope but also to reduce it.

![[infra-cloud-google.png]]

Another information resource that serves very well for finding such buckets is the [GrayHatWarfare](https://buckets.grayhatwarfare.com/) Project. This project is an online tool that searches for open cloud buckets and archives them. This is one of the most widely used tools currently, and it also gives excellent results since it contains an enormous amount of records.

The `GrayHatWarfare Project` offers us many different options, such as filtering by buckets, files, file types, keywords, and even an API interface. We can search these buckets for files and see which of them might be relevant for us. The advantage is that we do not have any interaction with buckets owned by the target company as long as we do not explicitly call the files or list them via the CLI.

![[infra-cloud-greyhatwarfare.png]]

* * * * *

### Development Platforms
---------------------

Again, developer platforms are of great use to us, as we can search code to find out if specific files exist in connection with the cloud buckets. As we know, `Searchcode` also redirects us to the resource that points to the corresponding file. Often used strings in these files are `AccountName` and `AccountKey`, used for authorization (like username and password).

![[infra-cloud-devplat.png]]

These files usually contain the `IP addresses` or the `bucket names` for the corresponding cloud storage. We can use these to search again on `GrayHatWarfare` and filter out the results. Therefore, if we follow these files and examine them more closely, we will most likely find a lot more helpful information that we will need for our documentation and further research.

![[infra-cloud-github.png]]

* * * * *

### Leak Resources
--------------

Another source that can point us to the buckets and forward them is the aforementioned [Rapid7 database](https://opendata.rapid7.com/sonar.fdns_v2/). Since this works with the forward DNS requests and responses and documents those, it is even very likely that we will find entries that will show us the corresponding buckets.

#### IP2Provider.py - Usage

	pigz -dc rapid7-fdns-db.json.gz | grep "target-company" | grep "core.microsoft.net\|s3.amazonaws.com\|s3-*.amazonaws.com\|googleapis.com/storage/v1/b/"

```text
{"timestamp":"...","name":"target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"cn-api.target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"com-target-company.s3.amazonaws.com","type":"cname","value":"s3-1-w.amazonaws.com"}
{"timestamp":"...","name":"dev.target-company.core.microsoft.net","type":"a","value":"X.X.X.127"}
<SNIP>
```

* * * * *

### Possible Protections
--------------------

Since we have already seen that our target company uses hosting providers such as `AWS` and `Azure`, we can strongly assume that they are also behind the security mechanisms of these providers. These can be individual `Web Application Firewalls` (`WAF`) and other security measures like `Intrusion Detection/Prevention Systems` (`IDS/IPS`) that can detect our attempts to access or exploit the corresponding server.

Even if we look for our target company's partners, we can assume which security services they offer and use. By looking at their services, we can also guess what security measures may be present in our target company's networks.

#### Questions

>10 Investigate the website and find the bucket name of AWS that the company used and submit it as the answer. (Format: sub.domain.tld)

## Email Addresses

* * * * *

Identifying existing email addresses can also provide us with a massive attack vector that we can use to our advantage. We can use emails in many ways. Among other things, email can be used not only for phishing attacks, but we can also analyze the traffic of these to identify which is the "central" point for the processing of emails. After all, this will have by far the most sent emails. We can also subscribe to newsletters and analyze their headers with [MXTools](https://mxtoolbox.com/EmailHeaders.aspx), which will also show us the route of the email and its security settings.

![[infra-emails.png]]

Email addresses may have different structures even within the same company. One of the most common examples is when the `first` and `last name` (`first.lastname@domain.tld`) is used in the email address. However, the email addresses can be created with `usernames` (`username@domain.tld`) not to show the user's full name.

* * * * *

### Home Page
---------

The company's website is often the stop for us to find out interesting information. In most cases, we find the first points of contact through email addresses on the `contact` or `about page`. We may find email addresses for personal contact with the `individual`, for `business` and informational purposes, as well as for `job applications` or even `department heads`. This also helps us to understand very well how the internal infrastructure may be set up. In larger companies with multiple locations, the individual departments are managed with the country codes available in the email addresses. Therefore, we can often find information on the offices or local information pages. It is helpful if the individual departments and their functions are described on this page, which can help us to understand the internal infrastructure better.

![[infra-domain-emails-contact.png]]

Finally, companies often try to use as short terms as possible, as these are easier to remember and require less effort to type. Therefore, the domains for the email addresses can be different but still belong to the same domain. For example, if we find a company with the name `Target-Company.com`, the abbreviated variant could be `TarCom.com` or `TC.com`, if they are still available.

* * * * *

### Social Networks
---------------

As we already know, many conversations occur on social networks, and therefore a lot of information is shared. We can also find email addresses there that point to particular addresses for exceptional cases. Here we can use the combination of social networks and search engines to find them. In the search engines, such as Google, we then use the corresponding Google dorks (`inurl:` & `intext:`) to optimize social networks' results.

![[infra-emails-social.png]]

For the dork `inurl:` we set the domain of the corresponding social network we are looking for. Next, we use the dork `intext:` with the extension for an email address (`@domain.tld`) that belongs to our target company. This then gives us some results that we can further investigate to establish further links.

Another critical role for email addresses is their `reputation`. This could tell us whether the corresponding email address has already been used for spam activities, has been blacklisted, whether `SPF` or `DMARC` is used, and much more. To get this information, we can use the information resource called [Emailrep](https://emailrep.io/). Apart from the information we get from it, using the API is very useful for us as we can easily use it with `cURL`.

#### Email Reputation - Emailrep.io

	curl -s emailrep.io/info@target-company.com

```text
{
  "email": "info@target-company.com",
  "reputation": "low",
  "suspicious": false,
  "references": 1,
  "details": {
    "blacklisted": false,
    "malicious_activity": false,
    "malicious_activity_recent": false,
    "credentials_leaked": false,
    "credentials_leaked_recent": false,
    "data_breach": false,
    "first_seen": "never",
    "last_seen": "never",
    "domain_exists": true,
    "domain_reputation": "low",
    "new_domain": false,
    "days_since_domain_creation": null,
    "suspicious_tld": false,
    "spam": false,
    "free_provider": false,
    "disposable": false,
    "deliverable": true,
    "accept_all": true,
    "valid_mx": true,
    "primary_mx": "mx-4.mailprovider.com",
    "spoofable": true,
    "spf_strict": true,
    "dmarc_enforced": false,
    "profiles": [
      "twitter"
    ]
  }
}
```

If we take a closer look at the results, we will see that this email address is `spoofable`. This could be of great importance for later phases of a pentest, as it represents a weak point that we could exploit. More importantly, it indicates that other email addresses may also be affected and that the entire mail server may be misconfigured.

* * * * *

### Search Engines
--------------

Once we have worked through the most used social networks, we can use the search engines to look for other information resources, including company email addresses. We can use the same Google Dork (`intext:`) to filter the results and match them with the existing list.

![[infra-emails-google.png]]

On the first page of the 18,000 results, we can already find an email interface of the company based on this simple usage, which can and should also be investigated in more detail later (if the scope allows this). Suppose we encounter a case where a large number of results appear that belong to a single domain. In that case, we can also use the dorks to exclude specific information resources by placing a minus in front of the dork (`-inurl:`).

A very efficient tool for this is called [theHarvester](https://github.com/laramies/theHarvester). This tool searches the information resources we provide, such as Google, Netcraft, Spyse, Twitter, and others for entries. Some of these services offer API keys that are bound to the corresponding account to execute the requests. Often there are limits on the number of requests we can send.

#### TheHarvester

	python3 theHarvester.py -d inlanefreight.com -b google,hunter,netcraft,spyse,twitter,dnsdumpster

```text
*******************************************************************
*  _   _                                            _             *
* | |_| |__   ___    /\  /\__ _ _ ____   _____  ___| |_ ___ _ __  *
* | __|  _ \ / _ \  / /_/ / _` | '__\ \ / / _ \/ __| __/ _ \ '__| *
* | |_| | | |  __/ / __  / (_| | |   \ V /  __/\__ \ ||  __/ |    *
*  \__|_| |_|\___| \/ /_/ \__,_|_|    \_/ \___||___/\__\___|_|    *
*                                                                 *
* theHarvester 3.2.0dev3                                          *
* Coded by Christian Martorella                                   *
* Edge-Security Research                                          *
* cmartorella@edge-security.com                                   *
*                                                                 *
******************************************************************* 

[*] Target: inlanefreight.com 

[*] Searching Dnsdumpster. 
[*] Searching Netcraft. 
Google is blocking your ip and the workaround, returning
	Searching 0 results.
	Searching 100 results.
	Searching 200 results.
[*] Searching Google. 
	Searching 0 results.
	Searching 100 results.
	Searching 200 results.
	
[*] No IPs found.

[*] Emails found: 9
---------------------
hlwire@inlanefreight.com
hru@inlanefreight.com
info@inlanefreight.com
ir@inlanefreight.com
joe.spring@inlanefreight.com
johan.troe@inlanefreight.com
john.mcleen@inlanefreight.com
last@inlanefreight.com
jack.daniels@inlanefreight.com

[*] Hosts found: 78
---------------------
autodiscover-add.inlanefreight.com:X.X.145.35
autodiscover.ext.inlanefreight.com:X.X.145.35
autodiscover.inlanefreight.com:X.X.145.34
certupd.inlanefreight.com:X.X.48.117
citrix-dev.inlanefreight.com:X.X.48.160
citrix.inlanefreight.com:X.X.48.207
crmtest.inlanefreight.com:X.X.48.128
customs.inlanefreight.com:X.X.141.19
dme.inlanefreight.com:X.X.48.148
<SNIP>
```

* * * * *

### Development Platforms
---------------------

Apart from insight into the company's technologies and source code, development platforms also serve very well to find out email addresses. Developers' email addresses are interesting, as they are often linked on different platforms, which we can then investigate and analyze later in the staff investigation phase. We will go into this in another Module called `OSINT: Staff Investigation`.

Here we can also use the combination of the developer platforms and the search engines to find out the developers' email addresses. Just as we used the Google Dorks for social networks, we use them again, only this time for the developer platforms.

![[infra-emails-google-dev.png]]

Another useful combination is searching for images in connection with the email addresses. This search option is usually overlooked, as most people do not see any relationship between email addresses and images. However, users often upload images linked to such an email address in the text or in some other way.

A small difference is that we no longer use the `inurl:` dork for the information resource but `intext:` to extend the linking to the individual information resources.

![[infra-emails-google-graphics.png]]

* * * * *

### Leak Resources
--------------

In principle, leaks can be displayed in any form. What counts is `how`, `where`, and `what` exactly was found. It becomes much more relevant when this information is used to complete and adapt an attack against the company. Here, the `attitude` of the developers to the information they discuss in public plays a significant role. Moreover, some are unaware that the information they share can be viewed publicly, assuming no one is looking for it. Furthermore, it is precisely this kind of attitude that often puts companies at risk of being attacked.

![[infra-emails-gitlab.png]]

Moreover, several factors come together because even if the developers are aware of it, misconfigurations are another factor that makes even their settings seem ineffective. Misconfigurations can even lead to calendars with appointments being publicly visible.

Email addresses often play a significant role in this field, as they are linked via a wide variety of platforms. Let us consider that passwords are often used repeatedly across multiple platforms. The risk is relatively high that if we can find a password for an email address and log it into a company's email interface, this will lead to significant information leakage that may even result in full compromise. One of the most effective tools that can be used to support linking is [h8mail](https://github.com/khast3x/h8mail).

#### H8mail - Usage

	h8mail -c h8mail_config.ini -t first.lastname@target-company.com

```text
                  Official h8mail posts:
                  https://khast3x.club/tags/h8mail/

          Version 2.5.5 - "ROCKSMASSON.5"

        ._____. ._____.     ;____________;
        | ._. | | ._. |     ;   h8mail   ;
        | !_| |_|_|_! |     ;------------;
        !___| |_______!  Heartfelt Email OSINT
        .___|_|_| |___.    Use responsibly
        | ._____| |_. | ;____________________;
        | !_! | | !_! | ; github.com/khast3x ;
        !_____! !_____! ;--------------------;

[>] h8mail is up to date
[~] Removing duplicates
[>] Targets:
[>] first.lastname@target-company.com
[~] scylla.so is down, skipping
[~] Target factory started for first.lastname@target-company.com
[~] [first.lastname@target-company.com]>[hunter.io public]
[>] Found 0 related emails for first.lastname@target-company.com using hunter.io (public)
[~] [first.lastname@target-company.com]>[hunter.io private]
[>] Found 0 related emails for first.lastname@target-company.com using hunter.io (private)
[~] [first.lastname@target-company.com]>[leaklookup public]
[>] Found 7 entries for first.lastname@target-company.com using LeakLookup (public)

 __________________________________________________________________________________________

[>] Showing results for first.lastname@target-company.com
LEAKLOOKUP_PUB |     first.lastname@target-company.com > antipublic-combo
LEAKLOOKUP_PUB |     first.lastname@target-company.com > collection-4-eu
LEAKLOOKUP_PUB |     first.lastname@target-company.com > collection-4-u
LEAKLOOKUP_PUB |     first.lastname@target-company.com > exploit.in
LEAKLOOKUP_PUB |     first.lastname@target-company.com > imesh.com
LEAKLOOKUP_PUB |     first.lastname@target-company.com > myspace.com
LEAKLOOKUP_PUB |     first.lastname@target-company.com > onlinerspambot
__________________________________________________________________________________________


                                   Session Recap:
                 Target                  |                   Status
__________________________________________________________________________________________

   first.lastname@target-company.com     |          Breach Found (7 elements)
__________________________________________________________________________________________

Execution time (seconds):   17.408742904663086
```

From the results, we can see that the email address we analyzed is contained in seven different databases whose passwords can be viewed. Another option is to use the service of [HaveIBeenPwned](https://haveibeenpwned.com/) to determine if any of the email addresses we found are already in databases that contain passwords for them and have been compromised.

![[haveibeenpwned.png]]

HaveIBeenPwned also goes through all available databases and checks the entries for the existence of the email address we entered. It will show us which platforms have been affected by this data's loss if it is there.

#### Questions

>What is the email address of the CEO?

## Third Parties

* * * * *

Identifying `third-party` providers requires a little more `manual` work and research. Since we know that there may be severe legal consequences for us, including a criminal charge, we should look at this issue here. In the case of a black-box penetration test, we must `pay close attention` to which `third-party` providers offer services to our target company.

However, this does not mean that we are not allowed to test systems from third-party suppliers. For this purpose, "`Penetration Testing Authorisation Forms`" exist, which must be filled in and submitted. This is to inform the third-party vendors that they will most likely receive alerts for the specific systems and should be aware that this is done with our intent. This will also prevent our Internet Service Provider (ISP) from being contacted and blocking our access to the internet. It will also stop us from being charged for attacking the hosts.

We should not use attacks such as DDOS unless all parties have agreed to do so not to restrict the services we provide to other users. But here, too, there are always precise specifications (`Penetration Testing Rules of Engagement`) from third-party suppliers that we have to follow.

If no forms are available from the third-party provider, our customer must contact the third-party provider and obtain permission. Otherwise, our customer must fill out and submit the documents and provide us with confirmation of permission to test the systems.

#### Penetration Testing Authorisation Forms

| Provider | Penetration Testing Authorisation Forms |
| --- | --- |
| `Amazon Web Services` | <https://aws.amazon.com/forms/penetration-testing-request> |
| `Digital Ocean` | <https://cloud.digitalocean.com/support/tickets/new> |
| `Google Cloud` | <https://support.google.com/cloud/answer/6262505?hl=en> |
| `Microsoft Azure` | <https://security-forms.azure.com/penetration-testing> |

By now, we should have gathered enough information to keep an eye out for the third parties. When looking for them, we must assemble an extensive collection of information resources.

![[infra-3rd-parties.png]]

We can see from the graph that we can get this information about third-party vendors from pretty much any information resource. We will go through the information resources that we have transferred to our `Resource Browser` in this step. If we have followed the methodology, we already have many information resources such as different websites, providers, files, and images that we can use for this. Here we need to summarize them and get an overview of how the company is positioned and which providers are used.

Apart from the different software the company uses, the hosting providers play an essential role. Based on this, we will assess how extensive the inventory is in the cloud, if at all, and what these `hosting providers` offer for security measures.

* * * * *

### Hosting Provider
----------------

It is always necessary to establish who the `third-party` providers are and what services they provide to the company. This should always be discussed in the meetings before the penetration test.

[SecurityTrails](https://securitytrails.com) does an excellent job in this research, which we should take advantage of.

![[securitytrails.png]]

Based on these results, we determined the four different hosting providers that our target company uses. We can search for the names of the hosting providers on Google, for example, and see their `penetration test policies` and `rules of engagement` and how best to get permissions for them.

If we do not find a hosting provider in the list, it is most likely a `self-hosted system`.

* * * * *

### Documents
---------

Here we should take a closer look at the providers who could make files available to us. These files can contain valuable information about the company itself and its processes and show us whom they work with to manage the infrastructure. For this search, we use the search engines like Google with the dork `site:` which will limit our searches to the pages we need. The most used providers for documents include, but are not limited to:

| **Provider** | **Dork** |
| --- | --- |
| Google Docs | `site:docs.google.com` |
| Google Cloud | `site:cloud.google.com` |
| Google Storage | `site:storage.googleapis.com` |
| Microsoft | `site:docs.microsoft.com` |
| Amazon Web Services | `site:amazonaws.com` |

![[infra-3rd-parties-google.png]]

#### Questions

>Investigate the website www.inlanefreight.com and find out which cloud provider the company most likely focuses on and submit it as the answer.

## Compounded Networks

* * * * *

Compounded networks use platforms that are suitable for both `personal` and `business` purposes. The difference between information sharing and information dissemination is that people on these platforms disclose less information about themselves. They want to make sure that potential employers or their current employers do not get the wrong impression. Confrontation is an essential aspect of professional life that every employee wants to avoid.

![[infra-networks.png]]

In most cases, we can already find all the links to the social networks on which the company is linked on the company's home page. The best known compounded social media platforms are, but not limited to:

| [Facebook](https://www.facebook.com) | [Instagram](https://www.instagram.com) | [Twitter](https://twitter.com) |
| --- | --- | --- |

Another essential difference between real conversations and opinions on social media platforms is that people often express views on a topic that they would not usually have the courage to communicate in a face-to-face conversation. This is because people `feel safe` to express their opinions at a distance `without the risk` of provoking direct conflict, and above all, they have much more `time` to respond than in a face-to-face conversation.

By reading through such `comments` and `posts`, we can create a pattern of how our target employee thinks about a specific topic. Above all, security-relevant information may be published when one is actually looking for help. However, the `stress` and `worry` that we get careless and unfocused can lead to such publications of `security-related information`.

#### Twitter - Security-Related Information

![[cn_twitter.png]]

Furthermore, posts on these platforms can also draw attention to illegal activities by the employee. Suppose our employee, as an example, has taken specific courses and training paid for by our client, and the employee shares this publicly with all others. In that case, it is a violation of the general terms and conditions for which our client is liable and accordingly also `security-relevant`. We cannot say whether `company-specific` information has been shared, but we should investigate the employee more in detail to prove or disprove this fact.

#### Facebook - Sharing Paid Trainings

![[cn_fb.png]]

* * * * *

### Social Networks
---------------

Here we focus not on the search for compounded social networks but the content within them. For this purpose, the corresponding `hashtags` are suitable, which primarily connect users with the company. In addition to the individual persons, partners can also be recognized, since they often thank them for a friendly comment or can also make themselves known through some other activity.

Besides that, pictures are often shared and published to leave a specific impression, which should impress in one way or another.

![[workspace.png]]

The focus here is on finding social groups created either by the company itself, its employees, or third parties in which specific topics are discussed. In doing so, we should narrow down the search for these groups as best we can with the information we have already obtained. After all, if we search only for Java, we will get quite a few results that will make our work more difficult. However, if we use several terms, such as `Java` + `target-company` + `web interface`, we will reduce our search results many times and become much more precise.

Basically, in compounded social networks, we can obtain internal information that is not directly visible. To do this, we should examine fields such as `groups`, `comments`, `images`, and the like. It is crucial to trace the entire conversation as best as possible and try to find out the background and why and how it came about that this conversation is taking place. Complaints that reflect employees' internal impressions of the company are excellent indicators of this.

## Technologies in Use

* * * * *

One of the most valuable pieces of information about the infrastructure is the technologies the company uses. Often it is not always easy to get much of this information passively. However, we do have some tools at our disposal to help us extract this information. Here, too, any information resource can be of great importance. The focus here is on identifying technologies that we can later use to adapt our attacks against the company. Especially for social engineering attacks, this plays an important role later on. We can interact with the employees and communicate and build trust with customized information (which only trusted people know).

![[infra-techs.png]]

Such information includes any software or provider that makes such an application available. Once we understand what the company is using technologies, this will give us a reasonably accurate picture of the aspects that will be most relevant to us as we prepare our attack on the company.

* * * * *

### Home Page
---------

We can already learn a lot of information from a company's home page. This can be, for example, different `forms` or content from the `source code` of the page. Especially with CMS, like WordPress applications, it is quite helpful because they are individually combined with different plugins. Often, weak points are found in the individual plugins, which can then be exploited to penetrate the company's network.

Another beneficial source that can tell us a lot about the target company's website alone is [BuiltWith](https://builtwith.com/). It lists all the technologies that are used by the web server and are deployed on it.

#### BuiltWith

![[builtwith.png]]

BuiltWith analyzes the content of the website and identifies the technologies used for it. This gives us an even better overview of how the web developers work and their knowledge, which we can use to assess how experienced they are. This is because we can use our assessments to identify or rule out certain security-related aspects, making our attack vector much more straightforward.

* * * * *

### Search Engines
--------------

In the section `Public Domain Records`, we already used the `Shodan CLI` to find information about the respective IP addresses. Shodan showed us which services it recognized and the technologies behind them. We can get the necessary information about the domain from Shodan using the "domain" parameter and see what details we will find about it. Most of the time, we get a good insight into the systems related to the domain, and sometimes we can even identify the vhosts directly, apart from the subdomains. Sometimes we can even find other domains with different TLDs that extend our attack vector if the scope in the contract allows it.

#### Shodan - Domain Information

	shodan domain target-company.com

```text
TARGET-COMPANY.COM

                         A      10.19.14.43
campaigns                CNAME  isp-id077411.com
ecard                    A      10.19.14.134
pages                    CNAME  target-company.isp.com
solutions                CNAME  unbouncepages.com
staging                  A      10.19.14.217
www                      CNAME  www-en.tar-comp.com
www-mig                  A      10.19.14.45
www-rel                  A      10.19.14.68
www2                     CNAME  www2.tar-comp.com
```

We can then also use this to get an even better overview of the infrastructure since, in this example, we know that the domains are interrelated and bound to a single company.

#### Shodan - Additional Domain Information

	shodan domain tar-comp.com

```text
TAR-COMP.COM

                         A      10.19.14.53
                         MX     mx3.mailprovider.com
                         MX     mx4.mailprovider.com
                         NS     ns1.ns-provider.net
                         NS     ns6.ns-provider.net
                         NS     ns2.ns-provider.net
                         NS     ns5.ns-provider.net
                         SOA    ns1.ns-provider.net
prod                     A      10.19.14.37
prod                     AAAA   d34d:b33f:4:3::37
prod-mig                 A      10.19.14.38
prod-rel                 A      10.19.14.72
prod-rel                 AAAA   2a04:1447:4:3::72
training                 A      10.19.14.50
hip                      A      10.7.148.165
hleforms                 A      10.7.148.167
hod                      A      10.7.148.130
hody81                   CNAME  hody.tar-comp.com
kf123t01-1               A      10.7.148.233
kf123t01-1               A      10.7.148.231
mail-archive             A      10.7.148.134
sap                      A      10.7.148.161
www                      CNAME  www-en.hlcl.com
www-de                   A      10.19.14.49
www-de                   AAAA   d34d:b33f:4:3::49
www-en                   A      10.19.14.43
www-en                   AAAA   d34d:b33f:4:3::43
www2                     A      10.19.14.44
www2                     AAAA   d34d:b33f:4:3::44
```

Shodan also has databases in which information is stored over a specific and relatively long period. We can use the Shodan CLI to search this database for entries related to our target company.

#### Shodan - Search the Database

	shodan search target-company | cut -d" " -f1-3

```text
10.29.26.251    8500    ec2-10-29-46-251.us-east-2.compute.amazonaws.com      HTTP/1.1 302 Found\r\nServer:
10.65.126.101   25      target-company.de 220 target-company.de ESMTP
10.62.241.109   8081    3ef15ea9.ip4.static.isp-provider.com    HTTP/1.1 200 OK\r\nCache-Control:
10.120.232.207  80      target-company-test.tracker.com    HTTP/1.1 302 Found\r\nDate:
10.54.2.133     23              C i s c o  S y s t e m s\r\n     ROUTER INTERNET\r\n
10.11.184.41    80              HTTP/1.1 301 Moved
10.11.184.41    443             HTTP/1.1 200 OK\r\nServer:
```

If we discover something interesting that has a name, we will see that we can find new attack vectors that we could not have found without this search. In this case, we found out that a `CISCO router` with a specific IPv4 address was being used in addition to AWS for cloud services.

#### Additional Attack Vector - Login

![[tech_login.png]]

#### Questions

>Which version of WordPress is used on the Inlanefreight domain page?

>What is the name of the theme that is used on the WordPress site?

>Which WAF is being used? (Format: \<name>)

# Leaks

## Leaked Information

* * * * *

We can use the same techniques we have learned so far for leaked information. However, the focus here is on information that only employees are likely to have. The word "leak" refers to a source of leakage in companies, organizations, and governments. In this case, information is disclosed that is not intended for public consumption. This information can still be damaging, regardless of the company's infrastructure.

![[leaks.png]]

Leaks are not only made by attackers but also by the company's own employees. If it is an employee, the cause of such information disclosure can be either `accidental` (through carelessness), `intentional`, or `forced`. In the third case, it is a lose-lose situation into which one has been forced and in which there is usually time pressure.

* * * * *

### Accidental Leak
---------------

Accidental leaks represent a disclosure of information and data that, in most cases, is intended for internal purposes only. This is done only by the employees of the company for many reasons. Generally, accidental leaks are referred to as `information disclosure`.

To illustrate this as thoroughly as possible, we can imagine source code that contains commented-out credentials that the developers have inserted for convenience. Suppose, however, and we find these credentials in the source code, which is an essential part of its function. In that case, it is information disclosure and no longer refers to the contents of the code but access rights (and thus to the administration and configuration of the system).

* * * * *

### Intentional Leak
----------------

Intentional leak takes place purposefully and always has the goal of making secret, confidential or private data public. With a leak, an insider wants to expose dishonorable, immoral, unethical behavior and make it accessible to the public. In some cases, attackers want to cause damage with a leak.

If we go back to our previous example and assume the developer added those credentials there on purpose and the intent for harm, then this is a leak.

In a leak, rules and laws are deliberately broken. Because at its core, a leak is data theft and violates confidentiality agreements. A leak becomes possible when an internal employee violates the trust and security rules given to them. For attackers, a leak requires them to find software vulnerabilities to steal data. A leak can occur by an insider who had legitimate access to the data, but it does not have to. Websites or social media profiles can also be hacked by outsiders, allowing data to be stolen. The insider, also known as a whistleblower, remains anonymous to avoid prosecution.

* * * * *

### Forced Leak
-----------

A forced leak means that the person or organization concerned often has no way to avoid the prospective personal or cooperative damage. This type of disclosure usually involves blackmailing the person or organization concerned. This is often the modus operandi of various malware activities that force the person or organization to pay with money or specific activities, or the encrypted/stolen data is kept and published. These are cases where `Digital Forensics & Incident Response` (`DFIR`) is used to identify the attackers and undo the damage caused by the malware.

* * * * *

### Leak Resources
--------------

The source of a leak can be any conceivable information resource. We can see how efficient our methodology is since we no longer base our information gathering approach on information resources but on the categories of information we want. Here we examine the information resources already found for the data for each category. There are information resources designed to find this type of content, and these are divided into three fields, `archives`, `internal leaks`, and `breaches`.

## Archives

* * * * *

An archive represents anything that contains an enormous amount of written information in some structured form and is not a library. It is therefore used to store information that can be accessed (un)restricted. An archive, therefore, stores information about the required information resource at specific intervals with special conditions. From 1999, it has been extended by other archives, so it is now a digital library that includes significant collections of texts and books, audio files, videos, images, and software. The Internet Archive is dedicated to the long-term archiving of digital data in a freely accessible form.

Besides the already mentioned forums and social media platforms, archives should not be left out. These archives, such as [WayBack Machine](https://archive.org/) or [Archive.fo](http://archive.fo), create so-called `snapshots` or `captures` of websites and store `images`, `videos`, `audio` recordings, `software`, and `files` that have been published on the websites.

#### WayBack Machine

![[wayback.png]]

#### Archive.fo

![[archive.png]]

These captures of web pages are taken by a `crawler`. In 2018 the WayBack Machine archived over `380 billions` of web pages. Viewing older versions of these sites also allows us to see and analyze the `source code`. This can include, for example, the `robots.txt` of a web server, which may indicate `hidden folders` on the webserver that still exist.

#### WayBack Machine - Robots.txt

![[wayback_robots.png]]

We can also display URLs that the WayBack Machine has crawled. Here it is often shocking how many `URLs` are publicly accessible even if we think that the published information from the past no longer exists. We may also find content that has been removed by our target company for security reasons, for example, that describes their technology in too much detail or even reveals other information such as their internal processes.

#### WayBack Machine - URLs

![[wayback_urls.png]]

Another interesting feature of WayBack Machine is that it also shows us in the `Summary` how many new links it has captured compared to the previous year. Here we get an overview of potentially existing folders and files that are now hidden from the public but still exist for further development or as a backup on the system. These can be detected using the filter located at the top right above the table. There we can enter the file extensions that are being searched for. Applications and administrators use many different file extensions. A list of them can be found at [FileInfo.com](https://fileinfo.com/filetypes/backup).

#### WayBack Machine - New Captures

![[wayback_news.png]]

* * * * *

### Pastebin
--------

Another critical information resource is [Pastebin.com](https://pastebin.com). There, different people share information in text form with each other. Pastebin is a web application that acts as a kind of online clipboard and can store any text, even large text blocks, on the web and make it accessible to third parties via a link. The interesting feature of the tool is that it supports syntax highlighting for many programming languages. This makes the code much more convenient to read and easier to understand. Since this feature, which is crucial for programmers, is missing from most blogs, social networks, forums, or chat programs, it has been reported that there are now over 15 million "pastes" on the website. Pastebin now offers some options not to save the shared information permanently. These include setting a `password`, which in most cases are relatively weak, and the `Burn after reading` function, which deletes the content after viewing. As we have done in previous search engine searches, we can also narrow down the results using the `site:` dork to the Pastebin page, giving us some impressive results.

![[leaks-pastebin.png]]

As we can see, there are 380 different results in this example that we can either filter out further or look through. We can also use this technique to find email addresses or use the unique information we already know to find more leaks. The art of finding this type of information is to combine the different information that we already know. To efficiently discover these leaks, the research we have done in the previous sections is necessary. Otherwise, we would be blindly searching for leaks on the off chance that our search might take an incalculably long time and even yield no results.

![[leaks-pastebin2.png]]

## Internal Leaks

* * * * *

Most employees who create and edit documents and are not familiar with IT security may not know which data will be published even under certain conditions. They are cautious about what they write in the `document`. Still, they don't know that it is not always necessary to write `sensitive data` in the documents, whether it contains information about the company's `working environment`.

Almost all websites have their own `images`, `files`, `documents`, and `notes` which they make available to the visitors. In most cases, these were created or at least edited on computers. Whenever files are modified, so-called `metadata` is written to the resulting files. These often contain the name of the `application` that was used for it and sometimes its `version`. Even some `operating systems` write their own metadata into these files.

For a regular user, this data is irrelevant. Still, it gives us an excellent insight into the employees' working environment and the software they are using along with the versions.

One of the most effective and most comfortable to use tools is `Exiftool`. On the website of our target company, we could find some reports which are available for download. We can take advantage of them, download them, and examine these reports to determine if specific metadata has been added to the files.

#### Exiftool - Metadata

	exiftool Document.pdf

```text
ExifTool Version Number         : 12.00
File Name                       : Document.pdf
Directory                       : .
File Size                       : 4.0 MB
File Modification Date/Time     : 2020:04:24 16:23:19+02:00
File Access Date/Time           : 2020:07:30 00:30:51+02:00
File Inode Change Date/Time     : 2020:07:30 00:30:51+02:00
File Permissions                : rw-r--r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.7
Linearized                      : No
Encryption                      : Standard V4.4 (128-bit)
User Access                     : Print, Extract, Print high-res
Create Date                     : 2020:04:08 10:53:37+02:00
Creator                         : Adobe InDesign CC 13.1 (Macintosh)
Modify Date                     : 2020:04:24 16:15:30+02:00
Has XFA                         : No
Language                        : EN-US
XMP Toolkit                     : Adobe XMP Core 5.4-c006 80.159825, 2016/09/16-03:31:08
Metadata Date                   : 2020:04:24 16:15:30+02:00
Creator Tool                    : Adobe InDesign CC 13.1 (Macintosh)
Instance ID                     : uuid:da179e62-c27b-48f1-8518-538ba698b1e7
Original Document ID            : xmp.did:f625069d-c7b1-4b2c-8945-87eaed62b00c
Document ID                     : xmp.id:46618852-5c98-4e71-85a5-c3c9125f857d
Rendition Class                 : proof:pdf
Derived From Instance ID        : xmp.iid:0849cef1-c44c-4813-9603-2cdaa291c2dd
Derived From Document ID        : xmp.did:7cd2e215-5e40-4c22-8fbe-235713816a03
Derived From Original Document ID: xmp.did:f649061d-c7b1-4b2c-8945-87eadb62a02c
Derived From Rendition Class    : default
History Action                  : converted
History Parameters              : from application/x-indesign to application/pdf
History Software Agent          : Adobe InDesign CC 13.1 (Macintosh)
History Changed                 : /
History When                    : 2020:04:08 10:53:38+02:00
Format                          : application/pdf
Producer                        : Adobe PDF Library 15.0
Trapped                         : False
Page Layout                     : TwoPageRight
Page Count                      : 120
```

We already know which `software` and `version` were used to create this document from the downloaded document without looking at its contents. We also see precisely `when` this document was created and `last edited`. We can also see the `PDF version`, `encryption` type, `language`, `operating system` used to create this document, and other valuable information.

Since we know that specific software tends to insert its metadata into files, we must be careful how we download the files from our target company. Often, when we download images using `Firefox`, we can see that the metadata, such as the `date` and `time` of creation, may differ from actual values. It is therefore recommended to download these files via `wget` to avoid accidentally manipulating the metadata.

#### Download Report

	wget https://TARGET_COMPANY.azureedge.net/<SNIP>.pdf -O Report.pdf

#### Exiftool - Metadata of Generated Report

	exiftool Report.pdf

```text
ExifTool Version Number         : 12.00
File Name                       : Report.pdf
Directory                       : .
File Size                       : 12 kB
File Modification Date/Time     : 2020:07:30 00:52:08+02:00
File Access Date/Time           : 2020:07:30 00:52:08+02:00
File Inode Change Date/Time     : 2020:07:30 00:52:08+02:00
File Permissions                : rw-r--r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.5
Linearized                      : Yes
Author                          : Lars Doe
Company                         : Microsoft
Create Date                     : 2020:07:20 09:10:18-05:00
Modify Date                     : 2020:07:28 14:10:29-05:00
Language                        : EN-US
Tagged PDF                      : Yes
XMP Toolkit                     : Adobe XMP Core 5.2-c001 63.139439, 2010/09/27-13:37:26
Metadata Date                   : 2020:07:28 14:10:29-05:00
Creator Tool                    : Acrobat PDFMaker 10.1 for Word
Document ID                     : uuid:70f23a54-45a3-40de-8dc6-1d5b7b07a362
Instance ID                     : uuid:31e1b9ba-210c-4cbe-b912-6b546ed49061
Subject                         : 2
Format                          : application/pdf
Creator                         : Lars Doe
Producer                        : Adobe PDF Library 10.0
Page Layout                     : OneColumn
Page Count                      : 1
```

From this generated report, we can draw a lot of useful information because we learn that the `software versions` differ as well as the `full name` of the creator. If we look at the `company` that is entered in the metadata and connect this to the `link` we used to download the report, we will be able to determine which `platform` the company uses.

Internal leaks include almost `any file` from which we can extract metadata. However, other sources may reveal internal information. The more we analyze the company, the better we learn to understand its structure. This gives us a variety of results, which can lead to `internal calendars`.

Calendars contain not only the `date` and `time` of certain `events`, but also `names`, `email addresses`, `locations`, `topic` content, `links`, and other information. This makes them very valuable, as it is assumed that no third party can access this information.

#### Internal Calendar

![[leaks_calendar.png]]

Not only metadata and poorly hidden internal applications can provide us with valuable information but also whole software or code published on [Github](https://github.com/) or [Gitlab](https://gitlab.com). This content can also contain `security-related` information that developers have forgotten to remove.

#### Gitlab - Versions

![[sm_gitlab.png]]

#### Github - Passwords

![[sm_company_repo2.png]]

#### Questions

>Investigate the website www.inlanefreight.com and try to find any additional information that a file might contain and submit the found flag as the answer.

## Breaches

* * * * *

When we talk about breaches, we mean any documentation of existing losses of information. Apart from various news like the attack on [SolarWinds](https://www.cnet.com/news/solarwinds-hack-officially-blamed-on-russia-what-you-need-to-know/), many databases contain more detailed information about it. These include descriptions of vulnerabilities and even `Proofs-of-Concept` (`POCS`). One of the largest databases for stolen passwords with the respective email addresses is "`Collection #1-5`". Here are some facts about this database:

| **`Collection #1-5`** | |
| --- | --- |
| Total size | `1 TB` |
| Unique emails | `772,904,991` |
| Unique passwords | `21,222,975` |
| Unique combinations of passwords and email addresses | `1,160,253,228` |

* * * * *

We have already seen the resource, [Have I Been Pwned?](https://haveibeenpwned.com/) (`HIBP`). This resource works exactly with this database to determine if the given email address is stored there. If we work with offline cracking, `HIBP` offers us the possibility to download huge password lists since these lists are excellent for cracking password-protected `files` or `hashes` that we find during our penetration test. The probability of current passwords being used repeatedly is very high. Of course, we should try smaller lists and self-generated lists before using ~11 GB lists.

From the previous `metadata`, we could determiethe version of `Acrobat`. There exist also databases where already known vulnerabilities are published. Such databases are, but not limited to:

| [CVEdetails](https://www.cvedetails.com/) | [Exploit-DB](https://www.exploit-db.com/) | [VulDB](https://vuldb.com) | [CVE.MITRE](https://cve.mitre.org/) | [SecurityFocus](https://www.securityfocus.com/) |
| --- | --- | --- | --- | --- |

#### CVEdetails - Acrobat 10.1

![[breaches_cve.png]]

![image](https://academy.hackthebox.com/storage/modules/28/breaches_cve.png)

* * * * *

Breaches also include the so-called `0-days` and `N-days` exploits. `0-day` exploits are publicly published vulnerabilities that the software providers have not yet fixed. `N-day` exploits represent ways to exploit the targets that have not yet patched the publicly known vulnerabilities. This means that although a patch or update for the specific vulnerability exists, it has not yet been applied. When we talk about breaches, we mean any documentation of existing losses of information. Apart from various news like the attack on [SolarWinds](https://www.cnet.com/news/solarwinds-hack-officially-blamed-on-russia-what-you-need-to-know/), there are also many databases that contain more detailed information about it. These include descriptions of vulnerabilities and even Proofs-of-Concept (POCs)., the company has not yet updated the software.

`0-days` and `N-days` exploits can often be found on `IT security forums` as well as on the `deep-web` or `dark-web`. These are often auctioned off, and the companies themselves are also willing to pay a lot of money to find out what the vulnerability looks like. This gives them a direct insight into the vulnerability and an idea of how to patch it.

Many applications and operating systems are often `not updated`, as this could harm the functionality of the `business workflow`. As a result, many administrators `risk` leaving outdated software and potential vulnerabilities in place rather than dealing with updates and patches that could shut down the entire business workflow.

After all, we don't think about how vulnerable an application, which is less than one year old, can be. In other Modules we will learn how quickly vulnerabilities can be found in new applications.

#### Exploit-DB - Latest Buffer Overflows

![[breaches_exploitdb.png]]

# Next Steps

## Intelligence

* * * * *

Finally, when we have collected all the information, we can start to connect the pieces more precisely. This is the main component of OSINT and brings out the actual value. In OSINT, the term "`intelligence`" has a different definition than the basic definition used by psychologists in the scientific world. Since there are many disagreements in the definition of "intelligence," scientists try to follow a more modern approach, which is described as follows:

Modern research focuses on information processing. How well, how fast, how long does someone need to process information, impressions, and stimuli. How quickly can they retrieve this information? In this context, intelligence is not seen as a fixed entity but as a variable and, consequently, as a process. How does the brain process all the information that comes at us? How well do the cognitive abilities function?

Here, an essential role is played by three different elements:

| `Origin` | ➔ | `Impact` | ➔ | `State` |
| --- | --- | --- | --- | --- |

Since there is neither a fixed definition for "intelligence" nor a precise definition explicitly for OSINT, we define it as follows:

`Based on the fact that every state has an origin and an impact, the term "intelligence" in OSINT consists of the ability to find out and link the connections between these elements with the information found.`

In this way, we process information from the past and present to assess the effects in the future. By analyzing the `present information` and the `changed conditions` with the `past`, the main focus is on the significant factors for the present condition. If a company was hacked (`origin`) in the past and there is no detected intrusion at the moment, it can be determined that the `impact` has brought about a change in the `state`. The `connections` between these elements represent a step-by-step process that shows the way in which the past state has been changed.

![[intelligence1.png]]

* * * * *

### Origin
------

`Each origin refers to an activity carried out in the past with the aim of changing the future state through some particular impact.`

This means that each activity has a purpose and goal to be achieved. For us, the necessary steps for this are essential. Therefore, we try to determine which actions had to be taken to cause the desired impact to reach the current state. Even if we do not know the state, we can use the steps to calculate its impact and required actions to achieve the desired state.

* * * * *

### Impact
------

To cause or provoke an impact, we need the combination of purpose or goal with the corresponding action. The goal alone has no direct effect on the desired state, just as little as an arbitrary action without a goal. Because with the second, the result would lead to a random state. The steps that need to be taken depend on the `environment` and `information`. Therefore, to calculate the impact, we need information about the current state and the environment in which our target is located. Accordingly, we gain insight into the dependent factors by which we can calculate step-by-step which actions have to be executed to achieve the desired state's corresponding impact.

* * * * *

### State
-----

A state is the result and functioning of different goals and the actions that have been taken to achieve them. The achievement of a particular state always automatically leads to `side-effects`. These side-effects are unintended impacts on the object and/or its environment.

Especially in information security, `side-effects` define exactly the component/vulnerability we try to detect during our penetration tests. We can say that no security-conscious administrator wants to make their company's network vulnerable or put it at risk. The misconfigurations caused by those `side-effects` of the actions to achieve the desired `state` and functionality are, in most cases, unintentional. These are precisely the flaws that we as penetration testers use to uncover these vulnerabilities in combination with our `objectives` (simulation of an attacker) and the `actions` based on an example (in a penetration test), which `impact` these can have on the company.

* * * * *

### Next Steps
----------

During our OSINT investigation, we only have information on the different conditions for different periods. To understand the `impact` between two different `states` and thus discover the potential `side-effects`, we need to recreate the individual steps between impact and state as best as possible by linking the information gathered.

As an example, we can take a simple software update. In simple terms, an update is an improvement of the existing software and its version. Thus, the old version would be the `origin`, and the new one would be the current `state`. The developers had set themselves individual goals before developing a new version, improving the service, or closing specific security vulnerabilities or bugs. The individual `steps` represent the development process in which the code is renewed, expanded, and improved. Each change (`action`) to the code has an `impact` on the entire software. This can be new functions or improved performance. However, this can lead to new errors and bugs, representing the `side-effects` we want to discover.

Therefore, the art is to track these single steps and, in the best case, as many as possible. To do this, we need to put ourselves in the administrator's shoes as best we can. This is also the role of the feedback left by employees, discovered during our investigation. This feedback gives us an impression of the working atmosphere and its conditions. A lousy atmosphere leads to dissatisfaction, demotivation, carelessness, and finally to mistakes that we try to discover. Once we have found which side-effects have arisen or could have arisen, we gain an accurate picture of how the software works and thus an understanding of what actions we need to take to achieve our desired state of the software.

>Author's Note: We are aware that the current tasks are limited to only a few sources. This is because we do not want to violate any third party's terms and conditions. We are currently working on a massive OSINT Lab where you can perfect your skills to the smallest detail. However, the planning and development of this require some time, and therefore we ask for your patience.










































