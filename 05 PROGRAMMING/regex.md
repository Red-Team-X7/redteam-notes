# 🤖 regex

Tags: #🤖
Related to:
See also:
Previous: [[PROGRAMMING]]

## Description

Interpret patterns.

## Usage Examples

|Regular Expression|Match|
|:----|:----|
|**Character classes**| |
|`.`|any character except newline|
|`\w\d\s`|word, digit, whitespace|
|`\W\D\S`|not word, digit, whitespace|
|`[abc]`|any of a, b, or c|
|`[^abc]`|not a, b, or c|
|`[a-g]`|character between a & g|
|**Anchors**| |
|`^abc$`|start / end of the string|
|`\b\B`|word, not-word boundary|
|**Escaped characters**| |
|`\.\*\\`|escaped special characters|
|`\t\n\r`|tab, linefeed, carriage return|
|**Groups & Lookaround**| |
|`(abc)`|capture group|
|`\1`|backreference to group #1|
|`(?:abc)`|non-capturing group|
|`(?=abc)`|positive lookahead|
|`(?!abc)`|negative lookahead|
|**Quantifiers & Alternation**| |
|`a*a+a?`|0 or more, 1 or more, 0 or 1|
|`a{5}a{2,}`|exactly five, two or more|
|`a{1,3}`|between one & three|
|`a+?a{2,}?`|match as few as possible|
|`ab|cd`|match ab or cd|

### Filter all unique paths of a domain

	curl https://inlanefreight.com/

```shell-session
<snip>
<a href='https://www.inlanefreight.com/index.php/offices/'>Offices</a></li>
<a href="https://www.inlanefreight.com/index.php/news/">News</a></li>
<a href='https://www.inlanefreight.com/index.php/career/'>Career</a></li>
<a href="https://www.inlanefreight.com/index.php/about-us/">About Us</a></li>
<a href='https://www.inlanefreight.com/index.php/contact/'>Contact</a></li>
<snip>
```

	curl https://www.inlanefreight.com/ | grep -Eo "https:\/\/.{0,3}\.inlanefreight\.com[^\"\']*" | sort -u

```shell-session
https://www.inlanefreight.com/
https://www.inlanefreight.com/index.php/about-us/
https://www.inlanefreight.com/index.php/career/
https://www.inlanefreight.com/index.php/comments/feed/
https://www.inlanefreight.com/index.php/contact/
https://www.inlanefreight.com/index.php/feed/
https://www.inlanefreight.com/index.php/news/
https://www.inlanefreight.com/index.php/offices/
https://www.inlanefreight.com/index.php/wp-json/
https://www.inlanefreight.com/index.php/wp-json/oembed/1.0/embed?url=https%3A%2F%2Fwww.inlanefreight.com%2F
https://www.inlanefreight.com/index.php/wp-json/oembed/1.0/embed?url=https%3A%2F%2Fwww.inlanefreight.com%2F&#038;format=xml
https://www.inlanefreight.com/index.php/wp-json/wp/v2/pages/7
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/animate.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/bootstrap.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/bootstrap-progressbar.min.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/colors/default.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/font-awesome.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/jquery.smartmenus.bootstrap.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/magnific-popup.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/owl.carousel.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/css/owl.transitions.css?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/images/breadcrumb-back.jpg
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/bootstrap.min.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/jquery.smartmenus.bootstrap.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/jquery.smartmenus.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/navigation.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/js/owl.carousel.min.js?ver=5.6.8
https://www.inlanefreight.com/wp-content/themes/ben_theme/style.css?ver=5.6.8
https://www.inlanefreight.com/wp-includes/css/dist/block-library/style.min.css?ver=5.6.8
https://www.inlanefreight.com/wp-includes/js/jquery/jquery-migrate.min.js?ver=3.3.2
https://www.inlanefreight.com/wp-includes/js/jquery/jquery.min.js?ver=3.5.1
https://www.inlanefreight.com/wp-includes/js/wp-embed.min.js?ver=5.6.8
https://www.inlanefreight.com/wp-includes/wlwmanifest.xml
https://www.inlanefreight.com/xmlrpc.php?rsd
```

# References

https://regexr.com/ // learn, build, and test regex