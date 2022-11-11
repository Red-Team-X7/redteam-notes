# ⚙️ httrack
Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

---
## Description

HTTrack is a free and open-source Web crawler and offline browser

## Usage Examples

### Clone website

I have an very old Fedora server that stopped active running almost 10 years ago. I need to backup its data for archive and physically dispose it.

It used to run wiki site based on [moinmoin](http://moinmo.in/). If I just back its static files plus database files, chances are I will never be able to re-active those wiki pages and see them again. So I thought a better idea is to clone the web pages and turn them into static local web site, which I can still access easily.

It turns the journey is more complicated than expected. It took me more than a couple of hours to finally nail it down. So I figure it is worth a post here.

### The Software

A quick search shows HTTrack seems to be best software for this job. It has a GUI version for Linux, called WebHTTrack. It also has a windows version called WinHTTrack. During my fiddling around, I ended up using WinHTTrack. In retrospect, the method used here should also work for WebHTTrack.

### The Challenge

WinHTTrack is generally user friendly. The biggest problem is moin wiki requires a user login to view the content.

[The cookie capture method](https://askubuntu.com/questions/409736/httrack-how-to-copy-a-website-with-email-based-username-login) (“Add URL” followed with “Capture URL”) does not work for moin wiki. Only first page works. Later pages still returns “You are not allowed to view this page”

### The Solution

#### Step 1 – prepare cookies.txt file

-   Install and launch firefox browser
-   Install cookies.txt extension
-   Log into the web site and start browsing
-   Click on “cookies.txt” extension and export cookies.txt for the current site.
-   Also note the firefox user agend
    -   Clock on top-right “settings” icon
    -   Then click on “Help”/”Troubleshooting Information”
    -   Note the “User Agent” string. We will use it later.

#### Step 2 – run WinHTTrack once

-   Start WinHTTrack and set up the project normally without worrying about login
    -   Specifically, you don’t need to use “Add URL” button to do anything special. Just type in the URL in the text input area.
-   Click on “Finish” to start downloading
    -   It will warn the site seems empty. That is expected.

#### Step 3 – copy over the cookies.txt

-   Copy the exported cookies.txt file to the top level directory of the local clone.
    -   For example, if HTTrack working directory is “%USER%\Documents\httrack-websites” and your project name is “erick-wiki”, then the destination directory is “%USER%\Documents\httrack-websites\erick-wiki”

#### Step 4 – run it again with proper options

A few options had to be set properly

-   Click on “Set options …” and a new pop-up window shows up
-   On “Spider” tab, set “Spider” to “no robots.txt rules”
-   On “Browser ID” tab, set “Browser Identity” to the “User Agent” of Firefox browser noted in step 1
-   On “Scan Rules” tab, click on “Exclude links”, another pop-up windows shows up
    -   Here you can exclude the files you like to clone
    -   Most importantly, you need to exclude the “logout” URL. Otherwise cookies.txt will be updated/deleted and you will note be able to continue cloning
        -   In my case, the URL will end with “?action=logout”. So I set “criterion” to “Links containing:”, and set “String” to “action=logout”
-   (Optional) On “Experts Only” tab, change “Travel mode” to “can go both up and down”
-   (Optional) On “Flow control”, set “number of connections” to higher number for faster cloning. _Note: your website may have surge limit as Moinmoin does, in which case you will need to turn off this feature on the web server in order to increase bandwidth._
-   Once all set, click on “Next” and “Finish” to start cloning.
	
---
## References
- https://junsun.net/wordpress/2021/02/clone-a-website-behind-login-with-winhttrack/