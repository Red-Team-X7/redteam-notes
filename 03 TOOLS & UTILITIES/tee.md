# ⚙️ tee
Tags: #⚙️ 
Related to: 
See also: 
Previous: 

## Description

Read from standard input and write to standard output and files.

## Usage Examples

### Save output to a file for programs lacking the functionality to do so

	joomscan -ec --url http://10.129.161.239  | tee joomscan.out

### Append to log

	./custom-tool.py 10.129.28.119 | tee -a logs.custom-tool

# References