# ⚙️ less / more

Tags: #⚙️ 
Related to: 
See also: 
Previous: [[ ]]

## Description

```text
more:  more is a filter for paging through text one screenful at a time.

less:  opposite of more

       Less is a program similar to more, but it has many more features. Less does not have to read the
       entire input file before starting, so with large input files it starts up faster than text editors like vi.
```

To read files, we do not necessarily have to use an editor for that. There are two tools called `more` and `less`, which are very identical. These are fundamental `pagers` that allow us to scroll through the file in an interactive view.

## Usage Examples

### Output does not remain in the terminal when quit.
	less /etc/password

### Output does remain in the terminal when quit.
	more /etc/password

# References