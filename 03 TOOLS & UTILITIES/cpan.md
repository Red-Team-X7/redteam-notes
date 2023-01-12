# 💢 cpan

Tags: #💢
Related to: 
See also: 
Previous: [[Footprinting]], [[REMOTE MANAGEMENT]]

## Description

Easily interact with CPAN from the command line.

## Usage Examples

### RDP Security Check - Installation

	sudo cpan

```text
Loading internal logger. Log::Log4perl recommended for better logging

CPAN.pm requires configuration, but most of it can be done automatically.
If you answer 'no' below, you will enter an interactive dialog for each
configuration option instead.

Would you like to configure as much as possible automatically? [yes] yes


Autoconfiguration complete.

commit: wrote '/root/.cpan/CPAN/MyConfig.pm'

You can re-run configuration any time with 'o conf init' in the CPAN shell

cpan shell -- CPAN exploration and modules installation (v2.27)
Enter 'h' for help.


cpan[1]> install Encoding::BER

Fetching with LWP:
http://www.cpan.org/authors/01mailrc.txt.gz
Reading '/root/.cpan/sources/authors/01mailrc.txt.gz'
............................................................................DONE
...SNIP...
```

# References