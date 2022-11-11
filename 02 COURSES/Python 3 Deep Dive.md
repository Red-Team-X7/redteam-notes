#  🗃 Fred Baptiste | Python 3: Deep Dive

Tags: #🗃
Related to: [[python]]
See also:
Previous:

## Python 3: Deep Dive (Part 1 - Functional)

### 1. Introduction

### 2. A Quick Refresher - Basics Review

#### Naming Conventions
```
_my_var		// this is a convention to indicate "internal use" or "private" objects
			// objects named this way will not get imported by a statement such as:
			// from module import *

__my_var	// used to "mangle" class attributes - useful in inheritance chains

__my_val__	// used for system-defined names that have a special meaning to the interpreter
			// don't invent them, stick to the ones pre-defined by Python!

Packages	// short, all-lowercase names. preferably no underscores	utilities
Modules		// short, all-lowercase names. can have underscores			db_utils, dbutils
Classes		// CapWords (upper camel case) convention					BankAccount
Functions	// lowercase, words separated by underscores (snake_case)	open_account
Variables	// lowercase, words separated by underscores (snake_case)	account_id
Constants	// all-uppercase, words separated by underscores			MIN_APR
```

#### 01 - Multi-Line Statements and Strings

Certain physical newlines are ignored in order to form a complete logical line of code.

##### Implicit Examples

```python
a = [1, 
    2, 
    3]
```

```python
a
```

    [1, 2, 3]

You may also add comments to the end of each physical line:

```python
a = [1, #first element
    2, #second element
    3, #third element
    ]
```

```python
a
```

    [1, 2, 3]

Note if you do use comments, you must close off the collection on a new line.

i.e. the following will not work since the closing ] is actually part of the comment:

```python
a = [1, # first element
    2 #second element]
```

      File "<ipython-input-7-ca1d73612a61>", line 2
        2 #second element]
                          ^
    SyntaxError: unexpected EOF while parsing

This works the same way for tuples, sets, and dictionaries.

```python
a = (1, # first element
    2, #second element
    3, #third element
    )
```

```python
a
```

    (1, 2, 3)

```python
a = {1, # first element
    2, #second element
    }
```

```python
a
```

    {1, 2}

```python
a = {'key1': 'value1', #comment,
    'key2': #comment
    'value2' #comment
    }
```

```python
a
```

    {'key1': 'value1', 'key2': 'value2'}

We can also break up function arguments and parameters:

```python
def my_func(a, #some comment
           b, c):
    print(a, b, c)
```

```python
my_func(10, #comment
       20, #comment
       30)
```

    10 20 30

##### Explicit Examples

You can use the ``\`` character to explicitly create multi-line statements.

```python
a = 10
b = 20
c = 30
if a > 5 \
    and b > 10 \
    and c > 20:
    print('yes!!')
```

    yes!!

The identation in continued-lines does not matter:

```python
a = 10
b = 20
c = 30
if a > 5 \
    and b > 10 \
        and c > 20:
    print('yes!!')
```

    yes!!

##### Multi-Line Strings

You can create multi-line strings by using triple delimiters (single or double quotes)

```python
a = '''this is
a multi-line string'''
```

```python
print(a)
```

    this is
    a multi-line string

Note how the newline character we typed in the multi-line string was preserved. Any character you type is preserved. You can also mix in escaped characters line any normal string.

```python
a = """some items:\n
    1. item 1
    2. item 2"""
```

```python
print(a)
```

    some items:
    
        1. item 1
        2. item 2

Be careful if you indent your multi-line strings - the extra spaces are preserved!

```python
def my_func():
    a = '''a multi-line string
    that is actually indented in the second line'''
    return a
```

```python
print(my_func())
```

    a multi-line string
        that is actually indented in the second line

```python
def my_func():
    a = '''a multi-line string
that is not indented in the second line'''
    return a
```

```python
print(my_func())
```

    a multi-line string
    that is not indented in the second line

Note that these multi-line strings are **not** comments - they are real strings and, unlike comments, are part of your compiled code. They are however sometimes used to create comments, such as ``docstrings``, that we will cover later in this course.

In general, use ``#`` to comment your code, and use multi-line strings only when actually needed (like for docstrings).

Also, there are no multi-line comments in Python. You simply have to use a ``#`` on every line.

```python
# this is
#    a multi-line
#    comment
```

The following works, but the above formatting is preferrable.

```python
# this is
    # a multi-line
    # comment
```

#### 02 - Conditionals

A conditional is a construct that allows you to branch your code based on conditions being met (or not)

This is achieved using **if**, **elif** and **else** or the **ternary operator** (aka conditional expression)

```python
a = 2
if a < 3:
    print('a < 3')
else:
    print('a >= 3')
```

    a < 3

**if** statements can be nested:

```python
a = 15

if a < 5:
    print('a < 5')
else:
    if a < 10:
        print('5 <= a < 10')
    else:
        print('a >= 10')
```

    a >= 10

But the **elif** statement provides far better readability:

```python
a = 15
if a < 5:
    print('a < 5')
elif a < 10:
    print('5 <= a < 10')
else:
    print('a >= 10')
```

    a >= 10

In Python, **elif** is the closest you'll find to the switch/case statement available in some other languages.

Python also provides a conditional expression (ternary operator):

X if (condition) else Y

returns (and evaluates) X if (condition) is True, otherwise returns (and evaluates) Y

```python
a = 5
res = 'a < 10' if a < 10 else 'a >= 10'
print(res)
```

    a < 10

```python
a = 15
res = 'a < 10' if a < 10 else 'a >= 10'
print(res)
```

    a >= 10

Note that **X** and **Y** can be any expression, not just literal values:

```python
def say_hello():
    print('Hello!')
    
def say_goodbye():
    print('Goodbye!')
```

```python
a = 5
say_hello() if a < 10 else say_goodbye()
```

    Hello!

```python
a = 15
say_hello() if a < 10 else say_goodbye()
```

    Goodbye!

#### 03 - Functions

Python has many built-in functions and methods we can use

Some are available by default:

```python
s = [1, 2, 3]
len(s)
```

    3

While some need to be imported:

```python
from math import sqrt
```

```python
sqrt(4)
```

    2.0

Entire modules can be imported:

```python
import math
```

```python
math.exp(1)
```

    2.718281828459045

We can define our own functions:

```python
def func_1():
    print('running func1')
```

```python
func_1()
```

    running func1

Note that to "call" or "invoke" a function we need to use the **()**.

Simply using the function name without the **()** refers to the function, but does not call it:

```python
func_1
```

    <function __main__.func_1>

We can also define functions that take parameters:

```python
def func_2(a, b):
    return a * b
```

Note that **a** and **b** can be any type (this is an example of polymorphism - which we will look into more detail later in this course). 

But the function will fail to run if **a** and **b** are types that are not "compatible" with the ***** operator:

```python
func_2(3, 2)
```

    6

```python
func_2('a', 3)
```

    'aaa'

```python
func_2([1, 2, 3], 2)
```

    [1, 2, 3, 1, 2, 3]

```python
func_2('a', 'b')
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-16-4e1c1906827b> in <module>()
    ----> 1 func_2('a', 'b')
    

    <ipython-input-12-abd6021cc10d> in func_2(a, b)
          1 def func_2(a, b):
    ----> 2     return a * b
    

    TypeError: can't multiply sequence by non-int of type 'str'

It is possible to use **type annotations**:

```python
def func_3(a: int, b:int):
    return a * b
```

```python
func_3(2, 3)
```

    6

```python
func_3('a', 2)
```

    'aa'

But as you can see, these do not enforce a data type! They are simply metadata that can be used by external libraries, and many IDE's.

Functions are objects, just like integers are objects, and they can be assigned to variables just as an integer can:

```python
my_func = func_3
```

```python
my_func('a', 2)
```

    'aa'

Functions **must** always return something. If you do not specify a return value, Python will automatically return the **None** object:

```python
def func_4():
    # does something but does not return a value
    a = 2
```

```python
res = func_4()
```

```python
print(res)
```

    None

The **def** keyword is an executable piece of code that creates the function (an instance of the **function** class) and essentially assigns it to a variable name (the function **name**). 

Note that the function is defined when **def** is reached, but the code inside it is not evaluated until the function is called.

This is why we can define functions that call other functions defined later - as long as we don't call them before all the necessary functions are defined.

For example, the following will work:

```python
def fn_1():
    fn_2()
    
def fn_2():
    print('Hello')
    
fn_1()
```

    Hello

But this will not work:

```python
def fn_3():
    fn_4()

fn_3()

def fn_4():
    print('Hello')
```

    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-32-6d843cb5e628> in <module>()
          2     fn_4()
          3 
    ----> 4 fn_3()
          5 
          6 def fn_4():


    <ipython-input-32-6d843cb5e628> in fn_3()
          1 def fn_3():
    ----> 2     fn_4()
          3 
          4 fn_3()
          5 


    NameError: name 'fn_4' is not defined

We also have the **lambda** keyword, that also creates a new function, but does not assign it to any specific name - instead it just returns the function object - which we can, if we wish, assign to a variable ourselves:

```python
func_5 = lambda x: x**2
```

```python
func_5
```

    <function __main__.<lambda>>

```python
func_5(2)
```

    4

We'll examine lambdas in more detail later in this course.

#### 04 - The While Loop

The **while** loop is a way to repeat a block of code as long as a specified condition is met.

```
while <exp is true>:
    code block
```

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

    0
    1
    2
    3
    4

Note that there is no guarantee that a **while** loop will execute at all, not even once, because the condition is tested **before** the loop runs.

```python
i = 5
while i < 5:
    print(i)
    i += 1
```

Some languages have a concept of a while loop that is guaranteed to execute at least once:

```python
do
    code block
while <exp is true>
```

There is no such thing in Python, but it's easy enough to write code that works that way.

We create an infinite loop and test the condition inside the loop and break out of the loop when the condition becomes false:

```python
 i = 5

while True:
    print(i)
    if i >= 5:
        break
```

    5

As you can see the loop executed once (and will always execute at least once, no matter the starting value of i.)

This is a standard pattern and can be useful in a variety of scenarios.

A simple example might be getting repetitive user input until the user performs and action or provides some specific value.
For example, suppose we want to use the console to let users enter their name. We just want to make sure their name is at least 2 characters long, contains printable characters only, and only contains alphabetic characters:
We might try it this way:

```python
min_length = 2

name = input('Please enter your name:')

while not(len(name) >= min_length  and name.isprintable() and name.isalpha()):
    name = input('Please enter your name:')

print('Hello, {0}'.format(name))
```

    Please enter your name:a123
    Please enter your name:a
    Please enter your name:fred
    Hello, fred

This works just fine, but notice that we had to write the code to elicit user input **twice** in our code. This is not good practice, and we can easily clean this up as follows:

```python
min_length = 2

while True:
    name = input('Please enter your name:')
    if len(name) >= min_length  and name.isprintable() and name.isalpha():
        break

print('Hello, {0}'.format(name))
```

    Please enter your name:a
    Please enter your name:123
    Please enter your name:fred
    Hello, fred

We saw how the **break** statement exits the **while** loop and execution resumes on the line immediately after the while code block.

Sometimes, we just want to cut the current iteration short, but continue looping, without exiting the loop itself.

This is done using the **continue** statement:

```python
a = 0
while a < 10:
    a += 1
    if a % 2:
        continue
    print(a)
```

    2
    4
    6
    8
    10

Note that there are much better ways of doing this! We'll cover that in later videos (comprehensions, generators, etc)

The **while** loop also can be used with an **else** clause!!

The **else** is executed if the while loop terminated without hitting a **break** statement (we say the loop terminated **normally**)

Suppose we want to test if some value is present in some list, and if not we want to append it to the list (again there are better ways of doing this):

First, here's how we might do it without the benefit of the **else** clause:

```python
l = [1, 2, 3]
val = 10

found = False
idx = 0
while idx < len(l):
    if l[idx] == val:
        found = True
        break
    idx += 1
    
if not found:
    l.append(val)
print(l)
```

    [1, 2, 3, 10]

Using the **else** clause is easier:

```python
l = [1, 2, 3]
val = 10

idx = 0
while idx < len(l):
    if l[idx] == val:
        break
    idx += 1
else:
    l.append(val)

print(l)
```

    [1, 2, 3, 10]

```python
l = [1, 2, 3]
val = 3

idx = 0
while idx < len(l):
    if l[idx] == val:
        break
    idx += 1
else:
    l.append(val)

print(l)
```

    [1, 2, 3]

#### 05 - Break, Continue and the Try Statement

Recall that in a ``try`` statement, the ``finally`` clause always runs:

```python
a = 10
b = 1
try:
    a / b
except ZeroDivisionError:
    print('division by 0')
finally:
    print('this always executes')
```

    this always executes

```python
a = 10
b = 0
try:
    a / b
except ZeroDivisionError:
    print('division by 0')
finally:
    print('this always executes')
```

    division by 0
    this always executes

So, what happens when using a ``try`` statement within a ``while`` loop, and a ``continue`` or ``break`` statement is encountered?

```python
a = 0
b = 2

while a < 3:
    print('-------------')
    a += 1
    b -= 1
    try:
        res = a / b
    except ZeroDivisionError:
        print('{0}, {1} - division by 0'.format(a, b))
        res = 0
        continue
    finally:
        print('{0}, {1} - always executes'.format(a, b))
        
    print('{0}, {1} - main loop'.format(a, b))
```

    -------------
    1, 1 - always executes
    1, 1 - main loop
    -------------
    2, 0 - division by 0
    2, 0 - always executes
    -------------
    3, -1 - always executes
    3, -1 - main loop

As you can see in the above result, the ``finally`` code still executed, even though the current iteration was cut short with the ``continue`` statement. 

This works the same with a ``break`` statement:

```python
a = 0
b = 2

while a < 3:
    print('-------------')
    a += 1
    b -= 1
    try:
        res = a / b
    except ZeroDivisionError:
        print('{0}, {1} - division by 0'.format(a, b))
        res = 0
        break
    finally:
        print('{0}, {1} - always executes'.format(a, b))
        
    print('{0}, {1} - main loop'.format(a, b))
```

    -------------
    1, 1 - always executes
    1, 1 - main loop
    -------------
    2, 0 - division by 0
    2, 0 - always executes

We can even combine all this with the ``else`` clause:

```python
a = 0
b = 2

while a < 3:
    print('-------------')
    a += 1
    b -= 1
    try:
        res = a / b
    except ZeroDivisionError:
        print('{0}, {1} - division by 0'.format(a, b))
        res = 0
        break
    finally:
        print('{0}, {1} - always executes'.format(a, b))
        
    print('{0}, {1} - main loop'.format(a, b))
else:
    print('\n\nno errors were encountered!')
```

    -------------
    1, 1 - always executes
    1, 1 - main loop
    -------------
    2, 0 - division by 0
    2, 0 - always executes

```python
a = 0
b = 5

while a < 3:
    print('-------------')
    a += 1
    b -= 1
    try:
        res = a / b
    except ZeroDivisionError:
        print('{0}, {1} - division by 0'.format(a, b))
        res = 0
        break
    finally:
        print('{0}, {1} - always executes'.format(a, b))
        
    print('{0}, {1} - main loop'.format(a, b))
else:
    print('\n\nno errors were encountered!')
```

    -------------
    1, 4 - always executes
    1, 4 - main loop
    -------------
    2, 3 - always executes
    2, 3 - main loop
    -------------
    3, 2 - always executes
    3, 2 - main loop
        
    no errors were encountered!

#### 06 - The For Loop

In Python, an **iterable** is an **object** capable of returning values one at a time.

Many objects in Python are iterable: lists, strings, file objects and many more.

Note: Our definition of an iterable did not state it was a collection of values - we only said it is an object that can return values one at a time - that's a subtle difference that we'll examine when we look into iterators and generators.

The **for** keyword can be used to iterate an iterable.

If you come with a background in another programming language, you have probably seen **for** loops defined this way:

```python
for (int i=0; i < 5; i++) {
    //code block
}
```

This form of the **for** loop is simply a _repetition_, very similar to a **while** loop - in fact it is equivalent to what we could write in Python as follows:

```python
i = 0
while i < 5:
    #code block
    print(i)
    i += 1
i = None
```

    0
    1
    2
    3
    4

But that's **NOT** what the **for** statement does in Python - the **for** statement is a way to **iterate** over iterables, and has nothing to do with the **for** loop we just saw. The closest equivalent we have in Python is the **while** loop written as above.

To use the **for** loop in Python, we **require** an iterable object to work with.

A simple iterable object is generated via the ``range()`` function

```python
for i in range(5):
    print(i)
```

    0
    1
    2
    3
    4

Many objects are iterable in Python:

```python
for x in [1, 2, 3]:
    print(x)
```

    1
    2
    3

```python
for x in 'hello':
    print(x)
```

    h
    e
    l
    l
    o

```python
for x in ('a', 'b', 'c'):
    print(x)
```

    a
    b
    c

When we iterate over an iterable, each iteration returns the "next" value (or object) in the iterable:

```python
for x in [(1, 2), (3, 4), (5, 6)]:
    print(x)
```

    (1, 2)
    (3, 4)
    (5, 6)

We can even assign the individual tuple values to specific named variables:

```python
for i, j in [(1, 2), (3, 4), (5, 6)]:
    print(i, j)
```

    1 2
    3 4
    5 6

We will cover iterables in a lot more detail later in this course.

The **break** and **continue** statements work just as well in **for** loops as they do in **while** loops:

```python
for i in range(5):
    if i == 3:
        continue
    print(i)
```

    0
    1
    2
    4

```python
for i in range(5):
    if i == 3:
        break
    print(i)
```

    0
    1
    2

The **for** loop, like the **while** loop, also supports an **else** clause which is executed if and only if the loop terminates normally (i.e. did not exit because of a **break** statement)

```python
for i in range(1, 5):
    print(i)
    if i % 7 == 0:
        print('multiple of 7 found')
        break
else:
    print('No multiples of 7 encountered')
```

    1
    2
    3
    4
    No multiples of 7 encountered

```python
for i in range(1, 8):
    print(i)
    if i % 7 == 0:
        print('multiple of 7 found')
        break
else:
    print('No multiples of 7 encountered')
```

    1
    2
    3
    4
    5
    6
    7
    multiple of 7 found

Similarly to the **while** loop, **break** and **continue** work just the same in the context of a **try** statement's **finally** clause.

```python
for i in range(5):
    print('--------------------')
    try:
        10 / (i - 3)
    except ZeroDivisionError:
        print('divided by 0')
        continue
    finally:
        print('always runs')
    print(i)
```

    --------------------
    always runs
    0
    --------------------
    always runs
    1
    --------------------
    always runs
    2
    --------------------
    divided by 0
    always runs
    --------------------
    always runs
    4

There are a number of standard techniques to iterate over iterables:

```python
s = 'hello'
for c in s:
    print(c)
```

    h
    e
    l
    l
    o

But sometimes, for indexable iterable types (e.g. sequences), we want to also know the index of the item in the loop:

```python
s = 'hello'
i = 0
for c in s:
    print(i, c)
    i += 1
```

    0 h
    1 e
    2 l
    3 l
    4 o

Slightly better approach might be:

```python
s = 'hello'

for i in range(len(s)):
    print(i, s[i])

```

    0 h
    1 e
    2 l
    3 l
    4 o

or even better:

```python
s = 'hello'

for i, c in enumerate(s):
    print(i, c)
```

    0 h
    1 e
    2 l
    3 l
    4 o

We'll come back to all these iteration techniques in a lot more detail throughout this course.

#### 07 - Classes

We'll cover classes in a lot of detail in this course, but for now you should have at least some understanding of classes in Python and how to create them.

To create a custom class we use the `class` keyword, and we can initialize class attributes in the special method `__init__`.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
```

We create **instances** of the `Rectangle` class by calling it with arguments that are passed to the `__init__` method as the second and third arguments. The first argument (`self`) is automatically filled in by Python and contains the object being created.

Note that using `self` is just a convention (although a good one, and you shgoudl use it to make your code more understandable by others), you could really call it whatever (valid) name you choose.

But just because you can does not mean you should!

```python
r1 = Rectangle(10, 20)
r2 = Rectangle(3, 5)
```

```python
r1.width
```

    10

```python
r2.height
```

    5

`width` and `height` are attributes of the `Rectangle` class. But since they are just values (not callables), we call them **properties**.

Attributes that are callables are called **methods**.

You'll note that we were able to retrieve the `width` and `height` attributes (properties) using a dot notation, where we specify the object we are interested in, then a dot, then the attribute we are interested in.

We can add callable attributes to our class (methods), that will also be referenced using the dot notation.

Again, we will create instance methods, which means the method will require the first argument to be the object being used when the method is called.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(the_referenced_object):
        return 2 * (the_referenced_object.width + the_referenced_object.height)
```

```python
r1 = Rectangle(10, 20)
```

```python
r1.area()
```

    200

When we ran the above line of code, our object was `r1`, so when `area` was called, Python in fact called the method `area` in the Rectangle class automatically passing `r1` to the `self` parameter.

This is why we can use a name other than self, such as in the perimeter method:

```python
r1.perimeter()
```

    60

Again, I'm just illustrating a point, don't actually do that!

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
```

```python
r1 = Rectangle(10, 20)
```

Python defines a bunch of **special** methods that we can use to give our classes functionality that resembles functionality of built-in and standard library objects.

Many people refer to them as *magic* methods, but there's nothing magical about them - unlike magic, they are well documented and understood!!

These **special** methods provide us an easy way to overload operators in Python.

For example, we can obtain the string representation of an integer using the built-in `str` function:

```python
str(10)
```

    '10'

What happens if we try this with our Rectangle object?

```python
str(r1)
```

    '<__main__.Rectangle object at 0x000002375E7006A0>'

Not exactly what we might have expected. On the other hand, how is Python supposed to know how to display our rectangle as a string?

We could write a method in the class such as:

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def to_str(self):
        return 'Rectangle (width={0}, height={1})'.format(self.width, self.height)
```

So now we could get a string from our object as follows:

```python
r1 = Rectangle(10, 20)
r1.to_str()
```

    'Rectangle (width=10, height=20)'

But of course, using the built-in `str` function still does not work:

```python
str(r1)
```

    '<__main__.Rectangle object at 0x000002375E708DA0>'

Does this mean we are out of luck, and anyone who writes a class in Python will need to provide some method to do this, and probably come up with their own name for the method too, maybe `to_str`, `make_string`, `stringify`, and who knows what else.

Fortunately, this is where these special methods come in. When we call `str(r1)`, Python will first look to see if our class (`Rectangle`) has a special method called `__str__`.

If the `__str__` method is present, then Python will call it and return that value.

There's actually another one called `__repr__` which is related, but we'll just focus on `__str__` for now.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def __str__(self):
        return 'Rectangle (width={0}, height={1})'.format(self.width, self.height)
```

```python
r1 = Rectangle(10, 20)
```

```python
str(r1)
```

    'Rectangle (width=10, height=20)'

However, in Jupyter (and interactive console if you are using that), look what happens here:

```python
r1
```

    <__main__.Rectangle at 0x2375e716ef0>

As you can see we still get that default. That's because here Python is not converting `r1` to a string, but instead looking for a string *representation* of the object. It is looking for the `__repr__` method (which we'll come back to later).

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def __str__(self):
        return 'Rectangle (width={0}, height={1})'.format(self.width, self.height)
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
```

```python
r1 = Rectangle(10, 20)
```

```python
print(r1)  # uses __str__
```

    Rectangle (width=10, height=20)

```python
r1  # uses __repr__
```

    Rectangle(10, 20)

How about the comparison operators, such as `==` or `<`?

```python
r1 = Rectangle(10, 20)
r2 = Rectangle(10, 20)
```

```python
r1 == r2
```

    False

As you can see, Python does not consider `r1` and `r2` as equal (using the `==` operator). Again, how is Python supposed to know that two Rectangle objects with the same height and width should be considered equal?

We just need to tell Python how to do it, using the special method `__eq__`.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def __str__(self):
        return 'Rectangle (width={0}, height={1})'.format(self.width, self.height)
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
    
    def __eq__(self, other):
        print('self={0}, other={1}'.format(self, other))
        if isinstance(other, Rectangle):
            return (self.width, self.height) == (other.width, other.height)
        else:
            return False
```

```python
r1 = Rectangle(10, 20)
r2 = Rectangle(10, 20)
```

```python
r1 is r2
```

    False

```python
r1 == r2
```

    self=Rectangle (width=10, height=20), other=Rectangle (width=10, height=20)

    True

```python
r3 = Rectangle(2, 3)
```

```python
r1 == r3
```

    self=Rectangle (width=10, height=20), other=Rectangle (width=2, height=3)

    False

And if we try to compare our Rectangle to a different type:

```python
r1 == 100
```

    self=Rectangle (width=10, height=20), other=100

    False

Let's remove that print statement - I only put that in so you could see what the arguments were, in practice you should avoid side effects.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def __str__(self):
        return 'Rectangle (width={0}, height={1})'.format(self.width, self.height)
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
    
    def __eq__(self, other):
        if isinstance(other, Rectangle):
            return (self.width, self.height) == (other.width, other.height)
        else:
            return False
```

What about `<`, `>`, `<=`, etc.?

Again, Python has special methods we can use to provide that functionality.

These are methods such as `__lt__`, `__gt__`, `__le__`, etc.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
        
    def area(self):
        return self.width * self.height
    
    def perimeter(self):
        return 2 * (self.width + self.height)
    
    def __str__(self):
        return 'Rectangle (width={0}, height={1})'.format(self.width, self.height)
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
    
    def __eq__(self, other):
        if isinstance(other, Rectangle):
            return (self.width, self.height) == (other.width, other.height)
        else:
            return False
    
    def __lt__(self, other):
        if isinstance(other, Rectangle):
            return self.area() < other.area()
        else:
            return NotImplemented
```

```python
r1 = Rectangle(100, 200)
r2 = Rectangle(10, 20)
```

```python
r1 < r2
```

    False

```python
r2 < r1
```

    True

What about `>`?

```python
r1 > r2
```

    True

How did that work? We did not define a `__gt__` method.

Well, Python cleverly decided that since `r1 > r2` was not implemented, it would give 

`r2 < r1` 

a try. And since, `__lt__` **is** defined, it worked!

Of course, `<=` is not going to magically work!

```python
r1 <= r2
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-53-beabec6419b6> in <module>()
    ----> 1 r1 <= r2
    

    TypeError: '<=' not supported between instances of 'Rectangle' and 'Rectangle'

If you come from a Java background, you are probably thinking that using "bare" properties (direct access), such as `height` and `width` is a terrible design idea.

It is for Java, but not for Python.

Although you can use bare properties in Java, if you ever need to intercept the getting or setting of a property, you will need to write a method (such as `getWidth` and `setWidth`. The problem is that if you used a bare `width` property for example, a lot of your code might be using `obj.width` (as we have been doing here). The instant you make the `width` private and instead implement getters and setters, you break your code.
Hence one of the reasons why in Java we just write getters and setters for properties from the beginning.

With Python this is not the case - we can change any bare property into getters and setters without breaking the code that uses that bare property.

I'll show you a quick example here, but we'll come back to this topic in much more detail later.

Let's take our Rectangle class once again. I'll use a simplified version to keep the code short.

```python
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
```

```python
r1 = Rectangle(10, 20)
```

```python
r1.width
```

    10

```python
r1.width = 100
```

```python
r1
```

    Rectangle(100, 20)

As you saw we can *get* and *set* the `width` property directly.

But let's say after this code has been released for a while and users of our class have been using it (and specifically setting and getting the `width` and `height` attribute a lot), but now we want to make sure users cannot set a non-positive value (i.e. <= 0) for width (or height, but we'll focus on width as an example).

In a language like Java, we would implement `getWidth` and `setWidth` and make `width` private - which would break any code directly accessing the `width` property.

In Python we can use some special **decorators** (more on those later) to encapsulate our property getters and setters:

```python
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
    
    @property
    def width(self):
        return self._width
    
    @width.setter
    def width(self, width):
        if width <= 0:
            raise ValueError('Width must be positive.')
        self._width = width
    
    @property
    def height(self):
        return self._height
    
    @height.setter
    def height(self, height):
        if height <= 0:
            raise ValueError('Height must be positive.')
        self._height = height
```

```python
r1 = Rectangle(10, 20)
```

```python
r1.width
```

    10

```python
r1.width = 100
```

```python
r1
```

    Rectangle(100, 20)

```python
r1.width = -10
```

    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-64-5813452c3f38> in <module>()
    ----> 1 r1.width = -10
    

    <ipython-input-59-f23b29795658> in width(self, width)
         14     def width(self, width):
         15         if width <= 0:
    ---> 16             raise ValueError('Width must be positive.')
         17         self._width = width
         18 


    ValueError: Width must be positive.

There are more things we should do to properly implement all this, in particular we should also be checking the positive and negative values during the `__init__` phase. We do so by using the accessor methods for height and width:

```python
class Rectangle:
    def __init__(self, width, height):
        self._width = None
        self._height = None
        # now we call our accessor methods to set the width and height
        self.width = width
        self.height = height
    
    def __repr__(self):
        return 'Rectangle({0}, {1})'.format(self.width, self.height)
    
    @property
    def width(self):
        return self._width
    
    @width.setter
    def width(self, width):
        if width <= 0:
            raise ValueError('Width must be positive.')
        self._width = width
    
    @property
    def height(self):
        return self._height
    
    @height.setter
    def height(self, height):
        if height <= 0:
            raise ValueError('Height must be positive.')
        self._height = height
```

```python
r1 = Rectangle(0, 10)
```

    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-66-b60d030826a5> in <module>()
    ----> 1 r1 = Rectangle(0, 10)
    

    <ipython-input-65-4c1b43452381> in __init__(self, width, height)
          4         self._height = None
          5         # now we call our accessor methods to set the width and height
    ----> 6         self.width = width
          7         self.height = height
          8 


    <ipython-input-65-4c1b43452381> in width(self, width)
         17     def width(self, width):
         18         if width <= 0:
    ---> 19             raise ValueError('Width must be positive.')
         20         self._width = width
         21 


    ValueError: Width must be positive.

There more we should be doing, like checking that the width and height being passed in are numeric types, and so on. Especially during the `__init__` phase - we would rather raise an exception when the object is being created rather than delay things and raise an exception when the user calls some method like `area` - that way the exception will be on the line that creates the object - makes debugging much easier!

There are many more of these special methods, and we'll look in detail at them later in this course.

### 3. Variables and Memory

#### 01 - Variables are Memory References

We can find the memory address that a variable *references*, by using the `id()` function.

The `id()` function returns the memory address of its argument as a base-10 integer.

We can use the function `hex()` to convert the base-10 number to base-16.

```python
my_var = 10
print('my_var = {0}'.format(my_var))
print('memory address of my_var (decimal): {0}'.format(id(my_var)))
print('memory address of my_var (hex): {0}'.format(hex(id(my_var))))
```

    my_var = 10
    memory address of my_var (decimal): 1968827120
    memory address of my_var (hex): 0x7559eaf0

```python
greeting = 'Hello'
print('greeting = {0}'.format(greeting))
print('memory address of my_var (decimal): {0}'.format(id(greeting)))
print('memory address of my_var (hex): {0}'.format(hex(id(greeting))))
```

    greeting = Hello
    memory address of my_var (decimal): 1688681719264
    memory address of my_var (hex): 0x1892d4625e0

Note how the memory address of `my_var` is **different** from that of `greeting`.

Strictly speaking, `my_var` is not "equal" to 10. 

Instead `my_var` is a **reference** to an (*integer*) object (*containing the value 10*) located at the memory address `id(my_var)`

Similarly for the variable `greeting`.

#### 02 - Reference Counting

Method that returns the reference count for a given variable's memory address:

```python
import ctypes

def ref_count(address):
    return ctypes.c_long.from_address(address).value
```

Let's make a variable, and check it's reference count:

```python
my_var = [1, 2, 3, 4]
ref_count(id(my_var))
```

    1

There is another built-in function we can use to obtain the reference count:

```python
import sys
sys.getrefcount(my_var)
```

    2

But why is this returning 2, instead of the expected 1 we obtained with the previous function?

Answer: The *sys.getrefcount()* function takes **my_var** as an argument, this means it receives (and stores) a reference to **my_var**'s memory address **also** - hence the count is off by 1. So we will use *from_address()* instead.

We make another reference to the **same** reference as `my_var`:

```python
other_var = my_var
```

Let's look at the memory address of those two variables and the reference counts:

```python
print(hex(id(my_var)), hex(id(other_var)))
print(ref_count(id(my_var)))
```

    0x1e43f368388 0x1e43f368388
    2

Force one reference to go away:

```python
other_var = None
```

And we look at the reference count again:

```python
print(ref_count(id(my_var)))
```

    1

We see that the reference count has gone back to 1.

You'll probably never need to do anything like this in Python. Memory management is completely transparent - this is just to illustrate some of what is going behind the scenes as it helps to understand upcoming concepts.

#### 03 - Garbage Collection

```python
import ctypes
import gc
```

We use the same function that we used in the lesson on reference counting to calculate the number of references to a specified object (using its memory address to avoid creating an extra reference)

```python
def ref_count(address):
    return ctypes.c_long.from_address(address).value
```

We create a function that will search the objects in the GC for a specified id and tell us if the object was found or not:

```python
def object_by_id(object_id):
    for obj in gc.get_objects():
        if id(obj) == object_id:
            return "Object exists"
    return "Not found"
```

Next we define two classes that we will use to create a circular reference

Class A's constructor will create an instance of class B and pass itself to class B's constructor that will then store that reference in some instance variable.

```python
class A:
    def __init__(self):
        self.b = B(self)
        print('A: self: {0}, b:{1}'.format(hex(id(self)), hex(id(self.b))))
```

```python
class B:
    def __init__(self, a):
        self.a = a
        print('B: self: {0}, a: {1}'.format(hex(id(self)), hex(id(self.a))))
```

We turn off the GC so we can see how reference counts are affected when the GC does not run and when it does (by running it manually).

```python
gc.disable()
```

Now we create an instance of A, which will, in turn, create an instance of B which will store a reference to the calling A instance.

```python
my_var = A()
```

    B: self: 0x1fc1eae44e0, a: 0x1fc1eae4908
    A: self: 0x1fc1eae4908, b:0x1fc1eae44e0

As we can see A and B's constructors ran, and we also see from the memory addresses that we have a circular reference.

In fact `my_var` is also a reference to the same A instance:

```python
print(hex(id(my_var)))
```

    0x1fc1eae4908

Another way to see this:

```python
print('a: \t{0}'.format(hex(id(my_var))))
print('a.b: \t{0}'.format(hex(id(my_var.b))))
print('b.a: \t{0}'.format(hex(id(my_var.b.a))))
```

    a: 	0x1fc1eae4908
    a.b: 	0x1fc1eae44e0
    b.a: 	0x1fc1eae4908

```python
a_id = id(my_var)
b_id = id(my_var.b)
```

We can see how many references we have for `a` and `b`:

```python
print('refcount(a) = {0}'.format(ref_count(a_id)))
print('refcount(b) = {0}'.format(ref_count(b_id)))
print('a: {0}'.format(object_by_id(a_id)))
print('b: {0}'.format(object_by_id(b_id)))
```

    refcount(a) = 2
    refcount(b) = 1
    a: Object exists
    b: Object exists

As we can see the A instance has two references (one from `my_var`, the other from the instance variable `b` in the B instance)

The B instance has one reference (from the A instance variable `a`)

Now, let's remove the reference to the A instance that is being held by `my_var`:

```python
my_var= None
```

```python
print('refcount(a) = {0}'.format(ref_count(a_id)))
print('refcount(b) = {0}'.format(ref_count(b_id)))
print('a: {0}'.format(object_by_id(a_id)))
print('b: {0}'.format(object_by_id(b_id)))
```

    refcount(a) = 1
    refcount(b) = 1
    a: Object exists
    b: Object exists

As we can see, the reference counts are now both equal to 1 (a pure circular reference), and reference counting alone did not destroy the A and B instances - they're still around. If no garbage collection is performed this would result in a memory leak.

Let's run the GC manually and re-check whether the objects still exist:

```python
gc.collect()
print('refcount(a) = {0}'.format(ref_count(a_id)))
print('refcount(b) = {0}'.format(ref_count(b_id)))
print('a: {0}'.format(object_by_id(a_id)))
print('b: {0}'.format(object_by_id(b_id)))
```

    refcount(a) = 0
    refcount(b) = 0
    a: Not found
    b: Not found

#### 04 - Dynamic vs Static Typing

Python is dynamically typed.

This means that the type of a variable is simply the type of the object the variable name points to (references). The variable itself has no associated type.

```python
a = "hello"
```

```python
type(a)
```

    str

```python
a = 10
```

```python
type(a)
```

    int

```python
a = lambda x: x**2
```

```python
a(2)
```

    4

```python
type(a)
```

    function

As you can see from the above examples, the type of the variable ``a`` changed over time - in fact it was simply the type of the object ``a`` was referencing at that time. No type was ever attached to the variable name itself.



#### 05 - Variable Re-Assignment

Notice how the memory address of **a** is different every time.

```python
a = 10
hex(id(a))
```

    '0x7559eaf0'

```python
a = 15
hex(id(a))
```

    '0x7559eb90'

```python
a = 5
hex(id(a))
```

    '0x7559ea50'

```python
a = a + 1
hex(id(a))
```

    '0x7559ea70'

However, look at this:

```python
a = 10
b = 10
print(hex(id(a)))
print(hex(id(b)))
```

    0x7559eaf0
    0x7559eaf0

The memory addresses of both **a** and **b** are the same!! 

We'll revisit this in a bit to explain what is going on.

#### 06 - Object Mutability

Certain Python built-in object types (aka data types) are **mutable**.

That is, the internal contents (state) of the object in memory can be modified.

```python
my_list = [1, 2, 3]
print(my_list)
print(hex(id(my_list)))
```

    [1, 2, 3]
    0x1cf6ab5b208

```python
my_list.append(4)
print(my_list)
print(hex(id(my_list)))
```

    [1, 2, 3, 4]
    0x1cf6ab5b208

As you can see, the memory address of *my_list* has **not** changed.

But, the **contents** of *my_list* has changed from *[1, 2, 3]* to *[1, 2, 3, 4]*.

On the other hand, consider this:

```python
my_list_1 = [1, 2, 3]
print(my_list_1)
print(hex(id(my_list_1)))
```

    [1, 2, 3]
    0x1cf6abd55c8

```python
my_list_1 = my_list_1 + [4]
print(my_list_1)
print(hex(id(my_list_1)))
```

    [1, 2, 3, 4]
    0x1cf6ab56888

Notice here that the memory address of *my_list_1* **did** change.

This is because concatenating two lists objects *my_list_1* and *[4]* did not modify the contents of *my_list_1* - instead it created a new list object and re-assigned *my_list_1* to reference this new object.

Similarly with **dictionary** objects that are also **mutable** types.

```python
my_dict = dict(key1='value 1')
print(my_dict)
print(hex(id(my_dict)))
```

    {'key1': 'value 1'}
    0x1cf6abdcdc8

```python
my_dict['key1'] = 'modified value 1'
print(my_dict)
print(hex(id(my_dict)))
```

    {'key1': 'modified value 1'}
    0x1cf6abdcdc8

```python
my_dict['key2'] = 'value 2'
print(my_dict)
print(hex(id(my_dict)))
```

    {'key1': 'modified value 1', 'key2': 'value 2'}
    0x1cf6abdcdc8

Once again we see that while we are modifying the **contents** of the dictionary, the memory address of *my_dict* has not changed.

Now consider the immutable sequence type: **tuple**

The tuple is immutable, so elements cannot be added, removed or replaced.

```python
t = (1, 2, 3)
```

This tuple will **never** change at all. It has three elements, the integers 1, 2, and 3. This will remain the case as long as **t**'s reference is not changed.

But, consider the following tuple:

```python
a = [1, 2]
b = [3, 4]
t = (a, b)
```

Now, **t** is still immutable, i.e. it contains a reference to the object **a** and the object **b**. **That** will never change as long as **t**'s reference is not re-assigned.

**However**, the elements **a** and **b** are, themselves, mutable.

```python
a.append(3)
b.append(5)
print(t)
```

    ([1, 2, 3], [3, 4, 5])

Observe that the contents of **a** and **b** **did** change!

So immutability can be a little more subtle than just thinking something can never change. 

The tuple **t** did **not** change - it contains two elements, that are the references **a** and **b**. And that will not change. But, because the referenced elements are mutable themselves, it appears as though the tuple has changed.

It hasn't though - that distinction is subtle but important to understand!

#### 07 - Function Arguments and Mutability

Consider a function that receives a *string* argument, and changes the argument in some way:

```python
def process(s):
    print('initial s # = {0}'.format(hex(id(s))))
    s = s + ' world'
    print('s after change # = {0}'.format(hex(id(s))))
```

```python
my_var = 'hello'
print('my_var # = {0}'.format(hex(id(my_var))))
```

    my_var # = 0x1e7e96fc420

Note that when *s* is received, it is referencing the same object as *my_var*.

After we "modify" *s*, *s* is pointing to a new memory address:

```python
process(my_var)
```

    initial s # = 0x1e7e96fc420
    s after change # = 0x1e7e97153b0

And our own variable *my_var* is still pointing to the original memory address:

```python
print('my_var # = {0}'.format(hex(id(my_var))))
```

    my_var # = 0x1e7e96fc420

Let's see how this works with mutable objects:

```python
def modify_list(items):
    print('initial items # = {0}'.format(hex(id(items))))
    if len(items) > 0:
        items[0] = items[0] ** 2
    items.pop()
    items.append(5)
    print('final items # = {0}'.format(hex(id(items))))
```

```python
my_list = [2, 3, 4]
print('my_list # = {0}'.format(hex(id(my_list))))
```

    my_list # = 0x1e7e972d308

```python
modify_list(my_list)
```

    initial items # = 0x1e7e972d308
    final items # = 0x1e7e972d308

```python
print(my_list)
print('my_list # = {0}'.format(hex(id(my_list))))
```

    [4, 3, 5]
    my_list # = 0x1e7e972d308

As you can see, throughout all the code, the memory address referenced by *my_list* and *items* is always the **same** (shared) reference - we are simply modifying the contents (**internal state**) of the object at that memory address.

Now, even with immutable container objects we have to be careful, e.g. a tuple containing a list (the tuple is immutable, but the list element inside the tuple **is** mutable)

```python
def modify_tuple(t):
    print('initial t # = {0}'.format(hex(id(t))))
    t[0].append(100)
    print('final t # = {0}'.format(hex(id(t))))
```

```python
my_tuple = ([1, 2], 'a')
```

```python
hex(id(my_tuple))
```

    '0x1e7e9614288'

```python
modify_tuple(my_tuple)
```

    initial t # = 0x1e7e9614288
    final t # = 0x1e7e9614288

```python
my_tuple
```

    ([1, 2, 100], 'a')

As you can see, the first element of the tuple was mutated.

#### 08 - Shared References and Mutability

The following sets up a shared reference between the variables my_var_1 and my_var_2

```python
my_var_1 = 'hello'
my_var_2 = my_var_1
print(my_var_1)
print(my_var_2)
```

    hello
    hello

```python
print(hex(id(my_var_1)))
print(hex(id(my_var_2)))
```

    0x24c9144ca08
    0x24c9144ca08

```python
my_var_2 = my_var_2 + ' world!'
```

```python
print(hex(id(my_var_1)))
print(hex(id(my_var_2)))
```

    0x24c9144ca08
    0x24c9144fab0

Be careful if the variable type is mutable!

Here we create a list (*my_list_1*) and create a variable (*my_list_2*) referencing the same list object:

```python
my_list_1 = [1, 2, 3]
my_list_2 = my_list_1
print(my_list_1)
print(my_list_2)
```

    [1, 2, 3]
    [1, 2, 3]

As we can see they have the same memory address (shared reference):

```python
print(hex(id(my_list_1)))
print(hex(id(my_list_2)))
```

    0x24c9144fc48
    0x24c9144fc48

Now we modify the list referenced by *my_list_2*:

```python
my_list_2.append(4)
```

*my_list_2* has been modified:

```python
print(my_list_2)
```

    [1, 2, 3, 4]

And since my_list_1 references the same list object, it has also changed:

```python
print(my_list_1)
```

    [1, 2, 3, 4]

As you can see, both variables still share the same reference:

```python
print(hex(id(my_list_1)))
print(hex(id(my_list_2)))
```

    0x24c9144fc48
    0x24c9144fc48

##### Behind the scenes with Python's memory manager

Recall from a few lectures back:

```python
a = 10
b = 10
```

```python
print(hex(id(a)))
print(hex(id(b)))
```

    0x7559eaf0
    0x7559eaf0

Same memory address!!

This is safe for Python to do because integer objects are **immutable**. 

So, even though *a* and *b* initially shared the same memory address, we can never modify *a*'s value by "modifying" *b*'s value. 

The only way to change *b*'s value is to change it's reference, which will never affect *a*.

```python
b = 15
```

```python
print(hex(id(a)))
print(hex(id(b)))
```

    0x7559eaf0
    0x7559eb90

However, for mutable objects, Python's memory manager does not do this, since that would **not** be safe.

```python
my_list_1 = [1, 2, 3]
my_list_2 = [1, 2 , 3]
```

As you can see, although the two variables were assigned identical "contents", the memory addresses are not the same:

```python
print(hex(id(my_list_1)))
print(hex(id(my_list_2)))
```

    0x24c9146c5c8
    0x24c913c6848

#### 09 - Variable Equality

From the previous lecture we know that **a** and **b** will have a **shared** reference:

```python
a = 10
b = 10

print(hex(id(a)))
print(hex(id(b)))
```

    0x7559eaf0
    0x7559eaf0

When we use the **is** operator, we are comparing the memory address **references**:

```python
print("a is b: ", a is b)
```

    a is b:  True

But if we use the **==** operator, we are comparing the **contents**:

```python
print("a == b:", a == b)
```

    a == b: True

The following however, do not have a shared reference:

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(hex(id(a)))
print(hex(id(b)))
```

    0x27006f17288
    0x27006e968c8

Although they are not the same objects, they do contain the same "values":

```python
print("a is b: ", a is b)
print("a == b", a == b)
```

    a is b:  False
    a == b True

Python will attempt to compare values as best as possible, for example:

```python
a = 10
b = 10.0
```

These are **not** the same reference, since one object is an **int** and the other is a **float**

```python
print(type(a))
print(type(b))
```

    <class 'int'>
    <class 'float'>

```python
print(hex(id(a)))
print(hex(id(b)))
```

    0x7559eaf0
    0x270064b1870

```python
print('a is b:', a is b)
print('a == b:', a == b)
```

    a is b: False
    a == b: True

So, even though *a* is an integer 10, and *b* is a float 10.0, the values will still compare as equal.

In fact, this will also have the same behavior:

```python
c = 10 + 0j
print(type(c))
```

    <class 'complex'>

```python
print('a is c:', a is c)
print('a == c:', a == c)
```

    a is c: False
    a == c: True

##### The None Object

**None** is a built-in "variable" of type *NoneType*.

Basically the keyword **None** is a reference to an object instance of *NoneType*.

NoneType objects are immutable! Python's memory manager will therefore use shared references to the None object.

```python
print(None)
```

    None

```python
hex(id(None))
```

    '0x75576bc0'

```python
type(None)
```

    NoneType

```python
a = None
print(type(a))
print(hex(id(a)))
```

    <class 'NoneType'>
    0x75576bc0

```python
a is None
```

    True

```python
a == None
```

    True

```python
b = None
hex(id(b))
```

    '0x75576bc0'

```python
a is b
```

    True

```python
a == b
```

    True

```python
l = []
```

```python
type(l)
```

    list

```python
l is None
```

    False

```python
l == None
```

    False

#### 10 - Everything is an Object

```python
a = 10
```

**a** is an object of type **int**, i.e. **a** is an instance of the **int** class.

```python
print(type(a))
```

    <class 'int'>

If **int** is a class, we should be able to declare it using standard class instatiation:

```python
b = int(10)
```

```python
print(b)
print(type(b))
```

    10
    <class 'int'>

We can even request the class documentation:

```python
help(int)
```

    Help on class int in module builtins:
    
    class int(object)
     |  int(x=0) -> integer
     |  int(x, base=10) -> integer
     |  
     |  Convert a number or string to an integer, or return 0 if no arguments
     |  are given.  If x is a number, return x.__int__().  For floating point
     |  numbers, this truncates towards zero.
     |  
     |  If x is not a number or if base is given, then x must be a string,
     |  bytes, or bytearray instance representing an integer literal in the
     |  given base.  The literal can be preceded by '+' or '-' and be surrounded
     |  by whitespace.  The base defaults to 10.  Valid bases are 0 and 2-36.
     |  Base 0 means to interpret the base from the string as an integer literal.
     |  >>> int('0b100', base=0)
     |  4
     |  
     |  Methods defined here:
     |  
     |  __abs__(self, /)
     |      abs(self)
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __and__(self, value, /)
     |      Return self&value.
     |  
     |  __bool__(self, /)
     |      self != 0
     |  
     |  __ceil__(...)
     |      Ceiling of an Integral returns itself.
     |  
     |  __divmod__(self, value, /)
     |      Return divmod(self, value).
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __float__(self, /)
     |      float(self)
     |  
     |  __floor__(...)
     |      Flooring an Integral returns itself.
     |  
     |  __floordiv__(self, value, /)
     |      Return self//value.
     |  
     |  __format__(...)
     |      default object formatter
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getnewargs__(...)
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __hash__(self, /)
     |      Return hash(self).
     |  
     |  __index__(self, /)
     |      Return self converted to an integer, if self is suitable for use as an index into a list.
     |  
     |  __int__(self, /)
     |      int(self)
     |  
     |  __invert__(self, /)
     |      ~self
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __lshift__(self, value, /)
     |      Return self<<value.
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mod__(self, value, /)
     |      Return self%value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __neg__(self, /)
     |      -self
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __or__(self, value, /)
     |      Return self|value.
     |  
     |  __pos__(self, /)
     |      +self
     |  
     |  __pow__(self, value, mod=None, /)
     |      Return pow(self, value, mod).
     |  
     |  __radd__(self, value, /)
     |      Return value+self.
     |  
     |  __rand__(self, value, /)
     |      Return value&self.
     |  
     |  __rdivmod__(self, value, /)
     |      Return divmod(value, self).
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __rfloordiv__(self, value, /)
     |      Return value//self.
     |  
     |  __rlshift__(self, value, /)
     |      Return value<<self.
     |  
     |  __rmod__(self, value, /)
     |      Return value%self.
     |  
     |  __rmul__(self, value, /)
     |      Return value*self.
     |  
     |  __ror__(self, value, /)
     |      Return value|self.
     |  
     |  __round__(...)
     |      Rounding an Integral returns itself.
     |      Rounding with an ndigits argument also returns an integer.
     |  
     |  __rpow__(self, value, mod=None, /)
     |      Return pow(value, self, mod).
     |  
     |  __rrshift__(self, value, /)
     |      Return value>>self.
     |  
     |  __rshift__(self, value, /)
     |      Return self>>value.
     |  
     |  __rsub__(self, value, /)
     |      Return value-self.
     |  
     |  __rtruediv__(self, value, /)
     |      Return value/self.
     |  
     |  __rxor__(self, value, /)
     |      Return value^self.
     |  
     |  __sizeof__(...)
     |      Returns size in memory, in bytes
     |  
     |  __str__(self, /)
     |      Return str(self).
     |  
     |  __sub__(self, value, /)
     |      Return self-value.
     |  
     |  __truediv__(self, value, /)
     |      Return self/value.
     |  
     |  __trunc__(...)
     |      Truncating an Integral returns itself.
     |  
     |  __xor__(self, value, /)
     |      Return self^value.
     |  
     |  bit_length(...)
     |      int.bit_length() -> int
     |      
     |      Number of bits necessary to represent self in binary.
     |      >>> bin(37)
     |      '0b100101'
     |      >>> (37).bit_length()
     |      6
     |  
     |  conjugate(...)
     |      Returns self, the complex conjugate of any int.
     |  
     |  from_bytes(...) from builtins.type
     |      int.from_bytes(bytes, byteorder, *, signed=False) -> int
     |      
     |      Return the integer represented by the given array of bytes.
     |      
     |      The bytes argument must be a bytes-like object (e.g. bytes or bytearray).
     |      
     |      The byteorder argument determines the byte order used to represent the
     |      integer.  If byteorder is 'big', the most significant byte is at the
     |      beginning of the byte array.  If byteorder is 'little', the most
     |      significant byte is at the end of the byte array.  To request the native
     |      byte order of the host system, use `sys.byteorder' as the byte order value.
     |      
     |      The signed keyword-only argument indicates whether two's complement is
     |      used to represent the integer.
     |  
     |  to_bytes(...)
     |      int.to_bytes(length, byteorder, *, signed=False) -> bytes
     |      
     |      Return an array of bytes representing an integer.
     |      
     |      The integer is represented using length bytes.  An OverflowError is
     |      raised if the integer is not representable with the given number of
     |      bytes.
     |      
     |      The byteorder argument determines the byte order used to represent the
     |      integer.  If byteorder is 'big', the most significant byte is at the
     |      beginning of the byte array.  If byteorder is 'little', the most
     |      significant byte is at the end of the byte array.  To request the native
     |      byte order of the host system, use `sys.byteorder' as the byte order value.
     |      
     |      The signed keyword-only argument determines whether two's complement is
     |      used to represent the integer.  If signed is False and a negative integer
     |      is given, an OverflowError is raised.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  denominator
     |      the denominator of a rational number in lowest terms
     |  
     |  imag
     |      the imaginary part of a complex number
     |  
     |  numerator
     |      the numerator of a rational number in lowest terms
     |  
     |  real
     |      the real part of a complex number

As we see from the docs, we can even create an **int** using an overloaded constructor:

```python
b = int('10', base=2)
```

```python
print(b)
print(type(b))
```

    2
    <class 'int'>

##### Functions are Objects too

```python
def square(a):
    return a ** 2
```

```python
type(square)
```

    function

In fact, we can even assign them to a variable:

```python
f = square
```

```python
type(f)
```

    function

```python
f is square
```

    True

```python
f(2)
```

    4

```python
type(f(2))
```

    int

A function can return a function

```python
def cube(a):
    return a ** 3
```

```python
def select_function(fn_id):
    if fn_id == 1:
        return square
    else:
        return cube
```

```python
f = select_function(1)
print(hex(id(f)))
print(hex(id(square)))
print(hex(id(cube)))
print(type(f))
print('f is square: ', f is square)
print('f is cube: ', f is cube)
print(f)
print(f(2))
```

    0x21257457b70
    0x21257457b70
    0x21255fab8c8
    <class 'function'>
    f is square:  True
    f is cube:  False
    <function square at 0x0000021257457B70>
    4

```python
f = select_function(2)
print(hex(id(f)))
print(hex(id(square)))
print(hex(id(cube)))
print(type(f))
print('f is square: ', f is square)
print('f is cube: ', f is cube)
print(f)
print(f(2))
```

    0x21255fab8c8
    0x21257457b70
    0x21255fab8c8
    <class 'function'>
    f is square:  False
    f is cube:  True
    <function cube at 0x0000021255FAB8C8>
    8

We could even call it this way:


```python
select_function(1)(5)
```

    25

A Function can be passed as an argument to another function

(This example is pretty useless, but it illustrates the point effectively)

```python
def exec_function(fn, n):
    return fn(n)
```

```python
result = exec_function(cube, 2)
print(result)
```

    8

We will come back to functions as arguments **many** more times throughout this course!

#### 11 - Python Optimizations - Interning

Earlier, we saw shared references being created automatically by Python:

```python
a = 10
b = 10
print(id(a))
print(id(b))
```

    1968827120
    1968827120

Note how `a` and `b` reference the same object.

But consider the following example:

```python
a = 500
b = 500
print(id(a))
print(id(b))
```

    1935322088624
    1935322089008

As you can see, the variables `a` and `b` do **not** point to the same object!

This is because Python pre-caches integer objects in the range [-5, 256]

So for example:

```python
a = 256
b = 256
print(id(a))
print(id(b))
```

    1968834992
    1968834992

and

```python
a = -5
b = -5
print(id(a))
print(id(b))
```

    1968826640
    1968826640

do have the same reference.

This is called **interning**: Python **interns** the integers in the range [-5, 256].

The integers in the range [-5, 256] are essentially **singleton** objects.

```python
a = 10
b = int(10)
c = int('10')
d = int('1010', 2)
```

```python
print(a, b, c, d)
```

    10 10 10 10

```python
a is b
```

    True

```python
a is c
```

    True

```python
a is d
```

    True

As you can see, all these variables were created in different ways, but since the integer object with value 10 behaves like a singleton, they all ended up pointing to the **same** object in memory.

#### 12 - Python Optimizations - String Interning

Python will automatically intern *certain* strings.

In particular all the identifiers (variable names, function names, class names, etc) are interned (singleton objects created).

Python will also intern string literals that look like identifiers.

For example:

```python
a = 'hello'
b = 'hello'
print(id(a))
print(id(b))
```

    1342722069536
    1342722069536

But not the following:

```python
a = 'hello, world!'
b = 'hello, world!'
print(id(a))
print(id(b))
```

    1342722047024
    1342722170928

However, because the following literals resemble identifiers, even though they are quite long, Python will still automatically intern them:

```python
a = 'hello_world'
b = 'hello_world'
print(id(a))
print(id(b))
```

    1342722047856
    1342722047856

And even longer:

```python
a = '_this_is_a_long_string_that_could_be_used_as_an_identifier'
b = '_this_is_a_long_string_that_could_be_used_as_an_identifier'
print(id(a))
print(id(b))
```

    1342721886784
    1342721886784

Even if the string starts with a digit:

```python
a = '1_hello_world'
b = '1_hello_world'
print(id(a))
print(id(b))
```

    1342722046256
    1342722046256

That was interned (pointer is the same), but look at this one:

```python
a = '1 hello world'
b = '1 hello world'
print(id(a))
print(id(b))
```

    1342722046832
    1342722172592

Interning strings (making them singleton objects) means that testing for string equality can be done faster by comparing the memory address:

```python
a = 'this_is_a_long_string'
b = 'this_is_a_long_string'
print('a==b:', a == b)
print('a is b:', a is b)
```

    a==b: True
    a is b: True

##### Note: Remember, using `is` ONLY works if the strings were interned!

Here's where this technique fails:

```python
a = 'hello world'
b = 'hello world'
print('a==b:', a==b)
print('a is b:', a is b)
```

    a==b: True
    a is b: False

You *can* force strings to be interned (but only use it if you have a valid performance optimization need):

```python
import sys
```

```python
a = sys.intern('hello world')
b = sys.intern('hello world')
c = 'hello world'
print(id(a))
print(id(b))
print(id(c))
```

    1342722172080
    1342722172080
    1342722174896

Notice how `a` and `b` are pointing to the same object, but `c` is **NOT**.

So, since both `a` and `b` were interned we can use `is` to test for equality of the two strings:

```python
print('a==b:', a==b)
print('a is b:', a is b)
```

    a==b: True
    a is b: True

So, does interning really make a big speed difference?

Yes, but only if you are performing a *lot* of comparisons.

Let's run some quick and dirty benchmarks:

```python
def compare_using_equals(n):
    a = 'a long string that is not interned' * 200
    b = 'a long string that is not interned' * 200
    for i in range(n):
        if a == b:
            pass
```

```python
def compare_using_interning(n):
    a = sys.intern('a long string that is not interned' * 200)
    b = sys.intern('a long string that is not interned' * 200)
    for i in range(n):
        if a is b:
            pass
```

```python
import time

start = time.perf_counter()
compare_using_equals(10000000)
end = time.perf_counter()

print('equality: ', end-start)

```

    equality:  2.965451618090112

```python
start = time.perf_counter()
compare_using_interning(10000000)
end = time.perf_counter()

print('identity: ', end-start)
```

    identity:  0.28690104431129626

As you can see, the performance difference, especially for long strings, and for many comparisons, can be quite radical!

#### 13 - Python Optimizations - Peephole

Peephole optimizations refer to a certain class of optimization strategies Python employs during any compilation phases.

##### Constant Expressions

Let's see how Python reduces constant expressions for optimization purposes:

```python
def my_func():
    a = 24 * 60
    b = (1, 2) * 5
    c = 'abc' * 3
    d = 'ab' * 11
    e = 'the quick brown fox' * 10
    f = [1, 2] * 5

```

```python
my_func.__code__.co_consts
```

    (None,
     24,
     60,
     1,
     2,
     5,
     'abc',
     3,
     'ab',
     11,
     'the quick brown fox',
     10,
     1440,
     (1, 2),
     (1, 2, 1, 2, 1, 2, 1, 2, 1, 2),
     'abcabcabc')

As you can see in the example above, `24 * 60` was pre-calculated and cached as a constant (`1440`).

Similarly, `(1, 2) * 5` was cached as `(1, 2, 1, 2, 1, 2, 1, 2, 1, 2)` and `'abc' * 3` was cached as `abcabcabc`.

On the other hand, note how `'the quick brown fox' * 10` was **not** pre-calculated (too long).

Similarly `[1, 2] * 5` was not pre-calculated either since a list is *mutable*, and hence not a *constant*.

##### Membership Tests

In membership testing, optimizations are applied as can be seen below:

```python
def my_func():
    if e in [1, 2, 3]:
        pass
```

```python
my_func.__code__.co_consts
```

    (None, 1, 2, 3, (1, 2, 3))

As you can see, the mutable list `[1, 2, 3]` was converted to an immutable tuple. 

It is OK to do this here, since we are testing membership of the list **at that point in time**, hence it is safe to convert it to a tuple, which is more efficient than testing membership of a list.

In the same way, set membership will be converted to frozen set membership:

```python
def my_func():
    if e in {1, 2, 3}:
        pass
```

```python
my_func.__code__.co_consts
```

    (None, 1, 2, 3, frozenset({1, 2, 3}))

In general, when you are writing your code, if you can use **set** membership testing, prefer that over a list or tuple - it is quite a bit more efficient.

Let's do a small quick (and dirty) benchmark of this:

```python
import string
import time 

char_list = list(string.ascii_letters)
char_tuple = tuple(string.ascii_letters)
char_set = set(string.ascii_letters)

print(char_list)
print()
print(char_tuple)
print()
print(char_set)
```

    ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    
    ('a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z')
    
    {'l', 'p', 'x', 'R', 'j', 'S', 's', 'T', 'W', 'Y', 'Z', 'P', 'g', 'O', 'b', 'u', 'H', 'G', 'v', 'e', 'M', 'n', 'w', 't', 'Q', 'E', 'N', 'X', 'C', 'i', 'A', 'B', 'F', 'V', 'a', 'm', 'r', 'f', 'h', 'U', 'D', 'c', 'y', 'z', 'J', 'd', 'o', 'I', 'L', 'K', 'k', 'q'}

```python
def membership_test(n, container):
    for i in range(n):
        if 'p' in container:
            pass
```

```python
start = time.perf_counter()
membership_test(10000000, char_list)
end = time.perf_counter()
print('list membership: ', end-start)
```

    list membership:  2.6035404184015434

```python
start = time.perf_counter()
membership_test(10000000, char_tuple)
end = time.perf_counter()
print('tuple membership: ', end-start)
```

    tuple membership:  2.602491734651276

```python
start = time.perf_counter()
membership_test(10000000, char_set)
end = time.perf_counter()
print('set membership: ', end-start)
```

    set membership:  0.3743007599607324

As you can see, set membership tests run quite a bit faster - which is not surprising since they are basically dictionary-like objects, so hash maps are used for looking up an item to determine membership.

### 4. Numeric Types

#### 01 - Integers - Data Type

Integers are objects - instances of the ``int`` class.

```python
print(type(100))
```

    <class 'int'>

They are a variable length data type that can theoretically handle any integer magnitude. This will take up a variable amount of memory that depends on the particular size of the integer.

```python
import sys
```

Creating an integer object requires an overhead of 24 bytes:

```python
sys.getsizeof(0)
```

    24

Here we see that to store the number 1 required 4 bytes (32 bits) on top of the 24 byte overhead:

```python
sys.getsizeof(1)
```

    28

Larger numbers will require more storage space:

```python
sys.getsizeof(2**1000)
```

    160

Larger integers will also slow down calculations.

```python
import time
```

```python
def calc(a):
    for i in range(10000000):
        a * 2
```

We start with a small integer value for a (10):

```python
start = time.perf_counter()
calc(10)
end = time.perf_counter()
print(end - start)
```

    0.3565246949777869

Now we set a to something larger (2<sup>100</sup>):

```python
start = time.perf_counter()
calc(2**100)
end = time.perf_counter()
print(end - start)
```

    0.6125349575326144

Finally we set a to some really large value (2<sup>10,000</sup>):

```python
start = time.perf_counter()
calc(2**10000)
end = time.perf_counter()
print(end - start)
```

    5.023413039975091

#### 02 - Integers - Operations

Addition, subtraction, multiplication and exponentiation of integers always result in an integer. (In the case of exponentiation this holds only for positive integer exponents.)

```python
type(2 + 3)
```

    int

```python
type(3 - 10)
```

    int

```python
type(3 * 5)
```

    int

```python
type(3 ** 4)
```

    int

But the standard division operator `/` **always** results in a float value.

```python
type(2 / 3)
```

    float

```python
type(10 / 2)
```

    float

The `math.floor()` method will return the floor of any number.

```python
import math
```

For non-negative values (>= 0), the floor of the value is the same as the integer portion of the value (truncation)

```python
math.floor(3.15)
```

    3

```python
math.floor(3.9999999)
```

    3

However, this is not the case for negative values:

```python
math.floor(-3.15)
```

    -4

```python
math.floor(-3.0000001)
```

    -4

##### The Floor Division Operator

The floor division operator `a//b` is the floor of `a / b`

i.e. `a // b = math.floor(a / b)`

This is true whether `a` and `b` are positive or negative.

```python
a = 33
b = 16
print(a/b)
print(a//b)
print(math.floor(a/b))
```

    2.0625
    2
    2

For positive numbers, `a//b` is basically the same as truncating (taking the integer portion) of `a / b`.

But this is **not** the case for negative numbers.

```python
a = -33
b = 16
print('{0}/{1} = {2}'.format(a, b, a/b))
print('trunc({0}/{1}) = {2}'.format(a, b, math.trunc(a/b)))
print('{0}//{1} = {2}'.format(a, b, a//b))
print('floor({0}//{1}) = {2}'.format(a, b, math.floor(a/b)))
```

    -33/16 = -2.0625
    trunc(-33/16) = -2
    -33//16 = -3
    floor(-33//16) = -3

```python
a = 33
b = -16
print('{0}/{1} = {2}'.format(a, b, a/b))
print('trunc({0}/{1}) = {2}'.format(a, b, math.trunc(a/b)))
print('{0}//{1} = {2}'.format(a, b, a//b))
print('floor({0}//{1}) = {2}'.format(a, b, math.floor(a/b)))
```

    33/-16 = -2.0625
    trunc(33/-16) = -2
    33//-16 = -3
    floor(33//-16) = -3

##### The Modulo Operator

The modulo operator and the floor division operator will always satisfy the following equation:

``a = b * (a // b) + a % b``

```python
a = 13
b = 4
print('{0}/{1} = {2}'.format(a, b, a/b))
print('{0}//{1} = {2}'.format(a, b, a//b))
print('{0}%{1} = {2}'.format(a, b, a%b))
print(a == b * (a//b) + a%b)
```

    13/4 = 3.25
    13//4 = 3
    13%4 = 1
    True

```python
a = -13
b = 4
print('{0}/{1} = {2}'.format(a, b, a/b))
print('{0}//{1} = {2}'.format(a, b, a//b))
print('{0}%{1} = {2}'.format(a, b, a%b))
print(a == b * (a//b) + a%b)
```

    -13/4 = -3.25
    -13//4 = -4
    -13%4 = 3
    True

```python
a = 13
b = -4
print('{0}/{1} = {2}'.format(a, b, a/b))
print('{0}//{1} = {2}'.format(a, b, a//b))
print('{0}%{1} = {2}'.format(a, b, a%b))
print(a == b * (a//b) + a%b)
```

    13/-4 = -3.25
    13//-4 = -4
    13%-4 = -3
    True

```python
a = -13
b = -4
print('{0}/{1} = {2}'.format(a, b, a/b))
print('{0}//{1} = {2}'.format(a, b, a//b))
print('{0}%{1} = {2}'.format(a, b, a%b))
print(a == b * (a//b) + a%b)
```

    -13/-4 = 3.25
    -13//-4 = 3
    -13%-4 = -1
    True

#### 03 - Integers - Constructors and Bases

##### Constructors

The ``int`` class has two constructors

```python
help(int)
```

    Help on class int in module builtins:
    
    class int(object)
     |  int(x=0) -> integer
     |  int(x, base=10) -> integer
     |  
     |  Convert a number or string to an integer, or return 0 if no arguments
     |  are given.  If x is a number, return x.__int__().  For floating point
     |  numbers, this truncates towards zero.
     |  
     |  If x is not a number or if base is given, then x must be a string,
     |  bytes, or bytearray instance representing an integer literal in the
     |  given base.  The literal can be preceded by '+' or '-' and be surrounded
     |  by whitespace.  The base defaults to 10.  Valid bases are 0 and 2-36.
     |  Base 0 means to interpret the base from the string as an integer literal.
     |  >>> int('0b100', base=0)
     |  4
     |  
     |  Methods defined here:
     |  
     |  __abs__(self, /)
     |      abs(self)
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __and__(self, value, /)
     |      Return self&value.
     |  
     |  __bool__(self, /)
     |      self != 0
     |  
     |  __ceil__(...)
     |      Ceiling of an Integral returns itself.
     |  
     |  __divmod__(self, value, /)
     |      Return divmod(self, value).
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __float__(self, /)
     |      float(self)
     |  
     |  __floor__(...)
     |      Flooring an Integral returns itself.
     |  
     |  __floordiv__(self, value, /)
     |      Return self//value.
     |  
     |  __format__(...)
     |      default object formatter
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getnewargs__(...)
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __hash__(self, /)
     |      Return hash(self).
     |  
     |  __index__(self, /)
     |      Return self converted to an integer, if self is suitable for use as an index into a list.
     |  
     |  __int__(self, /)
     |      int(self)
     |  
     |  __invert__(self, /)
     |      ~self
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __lshift__(self, value, /)
     |      Return self<<value.
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mod__(self, value, /)
     |      Return self%value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __neg__(self, /)
     |      -self
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __or__(self, value, /)
     |      Return self|value.
     |  
     |  __pos__(self, /)
     |      +self
     |  
     |  __pow__(self, value, mod=None, /)
     |      Return pow(self, value, mod).
     |  
     |  __radd__(self, value, /)
     |      Return value+self.
     |  
     |  __rand__(self, value, /)
     |      Return value&self.
     |  
     |  __rdivmod__(self, value, /)
     |      Return divmod(value, self).
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __rfloordiv__(self, value, /)
     |      Return value//self.
     |  
     |  __rlshift__(self, value, /)
     |      Return value<<self.
     |  
     |  __rmod__(self, value, /)
     |      Return value%self.
     |  
     |  __rmul__(self, value, /)
     |      Return value*self.
     |  
     |  __ror__(self, value, /)
     |      Return value|self.
     |  
     |  __round__(...)
     |      Rounding an Integral returns itself.
     |      Rounding with an ndigits argument also returns an integer.
     |  
     |  __rpow__(self, value, mod=None, /)
     |      Return pow(value, self, mod).
     |  
     |  __rrshift__(self, value, /)
     |      Return value>>self.
     |  
     |  __rshift__(self, value, /)
     |      Return self>>value.
     |  
     |  __rsub__(self, value, /)
     |      Return value-self.
     |  
     |  __rtruediv__(self, value, /)
     |      Return value/self.
     |  
     |  __rxor__(self, value, /)
     |      Return value^self.
     |  
     |  __sizeof__(...)
     |      Returns size in memory, in bytes
     |  
     |  __str__(self, /)
     |      Return str(self).
     |  
     |  __sub__(self, value, /)
     |      Return self-value.
     |  
     |  __truediv__(self, value, /)
     |      Return self/value.
     |  
     |  __trunc__(...)
     |      Truncating an Integral returns itself.
     |  
     |  __xor__(self, value, /)
     |      Return self^value.
     |  
     |  bit_length(...)
     |      int.bit_length() -> int
     |      
     |      Number of bits necessary to represent self in binary.
     |      >>> bin(37)
     |      '0b100101'
     |      >>> (37).bit_length()
     |      6
     |  
     |  conjugate(...)
     |      Returns self, the complex conjugate of any int.
     |  
     |  from_bytes(...) from builtins.type
     |      int.from_bytes(bytes, byteorder, *, signed=False) -> int
     |      
     |      Return the integer represented by the given array of bytes.
     |      
     |      The bytes argument must be a bytes-like object (e.g. bytes or bytearray).
     |      
     |      The byteorder argument determines the byte order used to represent the
     |      integer.  If byteorder is 'big', the most significant byte is at the
     |      beginning of the byte array.  If byteorder is 'little', the most
     |      significant byte is at the end of the byte array.  To request the native
     |      byte order of the host system, use `sys.byteorder' as the byte order value.
     |      
     |      The signed keyword-only argument indicates whether two's complement is
     |      used to represent the integer.
     |  
     |  to_bytes(...)
     |      int.to_bytes(length, byteorder, *, signed=False) -> bytes
     |      
     |      Return an array of bytes representing an integer.
     |      
     |      The integer is represented using length bytes.  An OverflowError is
     |      raised if the integer is not representable with the given number of
     |      bytes.
     |      
     |      The byteorder argument determines the byte order used to represent the
     |      integer.  If byteorder is 'big', the most significant byte is at the
     |      beginning of the byte array.  If byteorder is 'little', the most
     |      significant byte is at the end of the byte array.  To request the native
     |      byte order of the host system, use `sys.byteorder' as the byte order value.
     |      
     |      The signed keyword-only argument determines whether two's complement is
     |      used to represent the integer.  If signed is False and a negative integer
     |      is given, an OverflowError is raised.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  denominator
     |      the denominator of a rational number in lowest terms
     |  
     |  imag
     |      the imaginary part of a complex number
     |  
     |  numerator
     |      the numerator of a rational number in lowest terms
     |  
     |  real
     |      the real part of a complex number
    
```python
int(10)
```

    10

```python
int(10.9)
```

    10

```python
int(-10.9)
```

    -10

```python
from fractions import Fraction
```

```python
a = Fraction(22, 7)
```

```python
a
```

    Fraction(22, 7)

```python
int(a)
```

    3

We can use the second constructor to generate integers (base 10) from strings in any base.

```python
int("10")
```

    10

```python
int("101", 2)
```

    5

```python
int("101", base=2)
```

    5

Python uses ``a-z`` for bases from 11 to 36.

Note that the letters are not case sensitive.

```python
int("F1A", base=16)
```

    3866

```python
int("f1a", base=16)
```

    3866

Of course, the string must be a valid number in whatever base you specify.

```python
int('B1A', base=11)
```

    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-28-d0cf8657e90a> in <module>()
    ----> 1 int('B1A', base=11)
    

    ValueError: invalid literal for int() with base 11: 'B1A'

```python
int('B1A', 12)
```

##### Base Representations

###### Built-ins

```python
bin(10)
```

```python
oct(10)
```

```python
hex(10)
```

Note the `0b`, `0o` and `0x` prefixes

You can use these in your own strings as well, and they correspond to prefixes used in integer literals as well.

```python
a = int('1010', 2)
b = int('0b1010', 2)
c = 0b1010
```

```python
print(a, b, c)
```

```python
a = int('f1a', 16)
b = int('0xf1a', 16)
c = 0xf1a
```

```python
print(a, b, c)
```

For literals, the ``a-z`` characters are not case-sensitive either

```python
a = 0xf1a
b = 0xF1a
c = 0xF1A
```

```python
print(a, b, c)
```

##### Custom Rebasing

Python only provides built-in function to rebase to base 2, 8 and 16.

For other bases, you have to provide your own algorithm (or leverage some 3rd party library of your choice)

```python
def from_base10(n, b):
    if b < 2:
        raise ValueError('Base b must be >= 2')
    if n < 0:
        raise ValueError('Number n must be >= 0')
    if n == 0:
        return [0]
    digits = []
    while n > 0:
        # m = n % b
        # n = n // b
        # which is the same as:
        n, m = divmod(n, b)
        digits.insert(0, m)
    return digits
```

```python
from_base10(10, 2)
```

```python
from_base10(255, 16)
```

Next we may want to encode the digits into strings using different characters for each digit in the base

```python
def encode(digits, digit_map):
    # we require that digit_map has at least as many
    # characters as the max number in digits
    if max(digits) >= len(digit_map):
        raise ValueError("digit_map is not long enough to encode digits")
    
    # we'll see this later, but the following would be better:
    encoding = ''.join([digit_map[d] for d in digits])
    return encoding
    
```

Now we can encode any list of digits:

```python
encode([1, 0, 1], "FT")
```

```python
encode([1, 10, 11], '0123456789AB')
```

And we can combine both functions into a single one for easier use:

```python
def rebase_from10(number, base):
    digit_map = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
    if base < 2 or base > 36:
        raise ValueError('Invalid base: 2 <= base <= 36')
    # we store the sign of number and make it positive
    # we'll re-insert the sign at the end
    sign = -1 if number < 0 else 1
    number *= sign
    
    digits = from_base10(number, base)
    encoding = encode(digits, digit_map)
    if sign == -1:
        encoding = '-' + encoding
    return encoding
```

```python
e = rebase_from10(10, 2)
print(e)
print(int(e, 2))
```

```python
e = rebase_from10(-10, 2)
print(e)
print(int(e, 2))
```

```python
rebase_from10(131, 11)
```

```python
rebase_from10(4095, 16)
```

```python
rebase_from10(-4095, 16)
```

#### 04 - Rational Numbers

```python
from fractions import Fraction
```

We can get some info on the Fraction class:

```python
help(Fraction)
```

    Help on class Fraction in module fractions:
    
    class Fraction(numbers.Rational)
     |  This class implements rational numbers.
     |  
     |  In the two-argument form of the constructor, Fraction(8, 6) will
     |  produce a rational number equivalent to 4/3. Both arguments must
     |  be Rational. The numerator defaults to 0 and the denominator
     |  defaults to 1 so that Fraction(3) == 3 and Fraction() == 0.
     |  
     |  Fractions can also be constructed from:
     |  
     |    - numeric strings similar to those accepted by the
     |      float constructor (for example, '-2.3' or '1e10')
     |  
     |    - strings of the form '123/456'
     |  
     |    - float and Decimal instances
     |  
     |    - other Rational instances (including integers)
     |  
     |  Method resolution order:
     |      Fraction
     |      numbers.Rational
     |      numbers.Real
     |      numbers.Complex
     |      numbers.Number
     |      builtins.object
     |  
     |  Methods defined here:
     |  
     |  __abs__(a)
     |      abs(a)
     |  
     |  __add__(a, b)
     |      a + b
     |  
     |  __bool__(a)
     |      a != 0
     |  
     |  __ceil__(a)
     |      Will be math.ceil(a) in 3.0.
     |  
     |  __copy__(self)
     |  
     |  __deepcopy__(self, memo)
     |  
     |  __eq__(a, b)
     |      a == b
     |  
     |  __floor__(a)
     |      Will be math.floor(a) in 3.0.
     |  
     |  __floordiv__(a, b)
     |      a // b
     |  
     |  __ge__(a, b)
     |      a >= b
     |  
     |  __gt__(a, b)
     |      a > b
     |  
     |  __hash__(self)
     |      hash(self)
     |  
     |  __le__(a, b)
     |      a <= b
     |  
     |  __lt__(a, b)
     |      a < b
     |  
     |  __mod__(a, b)
     |      a % b
     |  
     |  __mul__(a, b)
     |      a * b
     |  
     |  __neg__(a)
     |      -a
     |  
     |  __pos__(a)
     |      +a: Coerces a subclass instance to Fraction
     |  
     |  __pow__(a, b)
     |      a ** b
     |      
     |      If b is not an integer, the result will be a float or complex
     |      since roots are generally irrational. If b is an integer, the
     |      result will be rational.
     |  
     |  __radd__(b, a)
     |      a + b
     |  
     |  __reduce__(self)
     |      helper for pickle
     |  
     |  __repr__(self)
     |      repr(self)
     |  
     |  __rfloordiv__(b, a)
     |      a // b
     |  
     |  __rmod__(b, a)
     |      a % b
     |  
     |  __rmul__(b, a)
     |      a * b
     |  
     |  __round__(self, ndigits=None)
     |      Will be round(self, ndigits) in 3.0.
     |      
     |      Rounds half toward even.
     |  
     |  __rpow__(b, a)
     |      a ** b
     |  
     |  __rsub__(b, a)
     |      a - b
     |  
     |  __rtruediv__(b, a)
     |      a / b
     |  
     |  __str__(self)
     |      str(self)
     |  
     |  __sub__(a, b)
     |      a - b
     |  
     |  __truediv__(a, b)
     |      a / b
     |  
     |  __trunc__(a)
     |      trunc(a)
     |  
     |  limit_denominator(self, max_denominator=1000000)
     |      Closest Fraction to self with denominator at most max_denominator.
     |      
     |      >>> Fraction('3.141592653589793').limit_denominator(10)
     |      Fraction(22, 7)
     |      >>> Fraction('3.141592653589793').limit_denominator(100)
     |      Fraction(311, 99)
     |      >>> Fraction(4321, 8765).limit_denominator(10000)
     |      Fraction(4321, 8765)
     |  
     |  ----------------------------------------------------------------------
     |  Class methods defined here:
     |  
     |  from_decimal(dec) from abc.ABCMeta
     |      Converts a finite Decimal instance to a rational number, exactly.
     |  
     |  from_float(f) from abc.ABCMeta
     |      Converts a finite float to a rational number, exactly.
     |      
     |      Beware that Fraction.from_float(0.3) != Fraction(3, 10).
     |  
     |  ----------------------------------------------------------------------
     |  Static methods defined here:
     |  
     |  __new__(cls, numerator=0, denominator=None, *, _normalize=True)
     |      Constructs a Rational.
     |      
     |      Takes a string like '3/2' or '1.5', another Rational instance, a
     |      numerator/denominator pair, or a float.
     |      
     |      Examples
     |      --------
     |      
     |      >>> Fraction(10, -8)
     |      Fraction(-5, 4)
     |      >>> Fraction(Fraction(1, 7), 5)
     |      Fraction(1, 35)
     |      >>> Fraction(Fraction(1, 7), Fraction(2, 3))
     |      Fraction(3, 14)
     |      >>> Fraction('314')
     |      Fraction(314, 1)
     |      >>> Fraction('-35/4')
     |      Fraction(-35, 4)
     |      >>> Fraction('3.1415') # conversion from numeric string
     |      Fraction(6283, 2000)
     |      >>> Fraction('-47e-2') # string may include a decimal exponent
     |      Fraction(-47, 100)
     |      >>> Fraction(1.47)  # direct construction from float (exact conversion)
     |      Fraction(6620291452234629, 4503599627370496)
     |      >>> Fraction(2.25)
     |      Fraction(9, 4)
     |      >>> Fraction(Decimal('1.47'))
     |      Fraction(147, 100)
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  denominator
     |  
     |  numerator
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  __abstractmethods__ = frozenset()
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from numbers.Rational:
     |  
     |  __float__(self)
     |      float(self) = self.numerator / self.denominator
     |      
     |      It's important that this conversion use the integer's "true"
     |      division rather than casting one side to float before dividing
     |      so that ratios of huge integers convert without overflowing.
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from numbers.Real:
     |  
     |  __complex__(self)
     |      complex(self) == complex(float(self), 0)
     |  
     |  __divmod__(self, other)
     |      divmod(self, other): The pair (self // other, self % other).
     |      
     |      Sometimes this can be computed faster than the pair of
     |      operations.
     |  
     |  __rdivmod__(self, other)
     |      divmod(other, self): The pair (self // other, self % other).
     |      
     |      Sometimes this can be computed faster than the pair of
     |      operations.
     |  
     |  conjugate(self)
     |      Conjugate is a no-op for Reals.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from numbers.Real:
     |  
     |  imag
     |      Real numbers have no imaginary component.
     |  
     |  real
     |      Real numbers are their real component.
    
We can create Fraction objects in a variety of ways:

Using integers:

```python
Fraction(1)
```

    Fraction(1, 1)

```python
Fraction(1, 3)
```

    Fraction(1, 3)

Using rational numbers:

```python
x = Fraction(2, 3)
y = Fraction(3, 4)
# 2/3 / 3/4 --> 2/3 * 4/3 --> 8/9
Fraction(x, y)
```

    Fraction(8, 9)

Using floats:

```python
Fraction(0.125)
```

    Fraction(1, 8)


```python
Fraction(0.5)
```

    Fraction(1, 2)

Using strings:

```python
Fraction('10.5')
```

    Fraction(21, 2)

```python
Fraction('22/7')
```

    Fraction(22, 7)

Fractions are automatically reduced:

```python
Fraction(8, 16)
```

    Fraction(1, 2)

Negative sign is attached to the numerator:

```python
Fraction(1, -4)
```

    Fraction(-1, 4)

Standard arithmetic operators are supported:

```python
Fraction(1, 3) + Fraction(1, 3) + Fraction(1, 3)
```

    Fraction(1, 1)

```python
Fraction(1, 2) * Fraction(1, 4)
```

    Fraction(1, 8)

```python
Fraction(1, 2) / Fraction(1, 3)
```

    Fraction(3, 2)

We can recover the numerator and denominator (integers):

```python
x = Fraction(22, 7)
print(x.numerator)
print(x.denominator)
```

    22
    7

Since floats have **finite** precision, any float can be converted to a rational number:

```python
import math
x = Fraction(math.pi)
print(x)
print(float(x))
```

    884279719003555/281474976710656
    3.141592653589793

```python
x = Fraction(math.sqrt(2))
print(x)
```

    6369051672525773/4503599627370496

Note that these rational values are approximations to the irrational numbers $\pi$ and $\sqrt{2}$

**Beware!!**

Float number representations (as we will examine in future lessons) do not always have an exact representation.

The number 0.125 (1/8) **has** an exact representation:

```python
Fraction(0.125)
```

    Fraction(1, 8)

and so we see the expected equivalent fraction.

But, 0.3 (3/10) does **not** have an exact representation:

```python
Fraction(3, 10)
```

    Fraction(3, 10)

but

```python
Fraction(0.3)
```

    Fraction(5404319552844595, 18014398509481984)

We will study this in upcoming lessons.

But for now, let's just see a quick explanation:

```python
x = 0.3
```

```python
print(x)
```

    0.3

Everything looks ok here - why am I saying 0.3 (float) is just an approximation?

Python is trying to format the displayed value for readability - so it rounds the number for a better display format!

We can instead choose to display the value using a certain number of digits:

```python
format(x, '.5f')
```

    '0.30000'

At 5 digits after the decimal, we might still think 0.3 is an exact representation.

But let's display a few more digits:

```python
format(x, '.15f')
```

    '0.300000000000000'

Hmm... 15 digits and still looking good!

How about 25 digits...

```python
format(x, '.25f')
```

    '0.2999999999999999888977698'

Now we see that **x** is not quite 0.3...

In fact, we can quantify the delta this way:

```python
delta = Fraction(0.3) - Fraction(3, 10)
```

Theoretically, delta should be 0, but it's not:

```python
delta == 0
```

    False

```python
delta
```

    Fraction(-1, 90071992547409920)

**delta** is a very small number, the above fraction...

As a float:

```python
float(delta)
```

    -1.1102230246251566e-17

##### Constraining the denominator

```python
x = Fraction(math.pi)
print(x)
print(format(float(x), '.25f'))
```

    884279719003555/281474976710656
    3.1415926535897931159979635

```python
y = x.limit_denominator(10)
print(y)
print(format(float(y), '.25f'))
```

    22/7
    3.1428571428571427937015414

```python
y = x.limit_denominator(100)
print(y)
print(format(float(y), '.25f'))
```

    311/99
    3.1414141414141414365701621

```python
y = x.limit_denominator(500)
print(y)
print(format(float(y), '.25f'))
```

    355/113
    3.1415929203539825209645642

#### 05 - Floats - Internal Representation

The ``float`` class can be used to represent real numbers.

```python
help(float)
```

    Help on class float in module builtins:
    
    class float(object)
     |  float(x) -> floating point number
     |  
     |  Convert a string or number to a floating point number, if possible.
     |  
     |  Methods defined here:
     |  
     |  __abs__(self, /)
     |      abs(self)
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __bool__(self, /)
     |      self != 0
     |  
     |  __divmod__(self, value, /)
     |      Return divmod(self, value).
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __float__(self, /)
     |      float(self)
     |  
     |  __floordiv__(self, value, /)
     |      Return self//value.
     |  
     |  __format__(...)
     |      float.__format__(format_spec) -> string
     |      
     |      Formats the float according to format_spec.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getformat__(...) from builtins.type
     |      float.__getformat__(typestr) -> string
     |      
     |      You probably don't want to use this function.  It exists mainly to be
     |      used in Python's test suite.
     |      
     |      typestr must be 'double' or 'float'.  This function returns whichever of
     |      'unknown', 'IEEE, big-endian' or 'IEEE, little-endian' best describes the
     |      format of floating point numbers used by the C type named by typestr.
     |  
     |  __getnewargs__(...)
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __hash__(self, /)
     |      Return hash(self).
     |  
     |  __int__(self, /)
     |      int(self)
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mod__(self, value, /)
     |      Return self%value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __neg__(self, /)
     |      -self
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __pos__(self, /)
     |      +self
     |  
     |  __pow__(self, value, mod=None, /)
     |      Return pow(self, value, mod).
     |  
     |  __radd__(self, value, /)
     |      Return value+self.
     |  
     |  __rdivmod__(self, value, /)
     |      Return divmod(value, self).
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __rfloordiv__(self, value, /)
     |      Return value//self.
     |  
     |  __rmod__(self, value, /)
     |      Return value%self.
     |  
     |  __rmul__(self, value, /)
     |      Return value*self.
     |  
     |  __round__(...)
     |      Return the Integral closest to x, rounding half toward even.
     |      When an argument is passed, work like built-in round(x, ndigits).
     |  
     |  __rpow__(self, value, mod=None, /)
     |      Return pow(value, self, mod).
     |  
     |  __rsub__(self, value, /)
     |      Return value-self.
     |  
     |  __rtruediv__(self, value, /)
     |      Return value/self.
     |  
     |  __setformat__(...) from builtins.type
     |      float.__setformat__(typestr, fmt) -> None
     |      
     |      You probably don't want to use this function.  It exists mainly to be
     |      used in Python's test suite.
     |      
     |      typestr must be 'double' or 'float'.  fmt must be one of 'unknown',
     |      'IEEE, big-endian' or 'IEEE, little-endian', and in addition can only be
     |      one of the latter two if it appears to match the underlying C reality.
     |      
     |      Override the automatic determination of C-level floating point type.
     |      This affects how floats are converted to and from binary strings.
     |  
     |  __str__(self, /)
     |      Return str(self).
     |  
     |  __sub__(self, value, /)
     |      Return self-value.
     |  
     |  __truediv__(self, value, /)
     |      Return self/value.
     |  
     |  __trunc__(...)
     |      Return the Integral closest to x between 0 and x.
     |  
     |  as_integer_ratio(...)
     |      float.as_integer_ratio() -> (int, int)
     |      
     |      Return a pair of integers, whose ratio is exactly equal to the original
     |      float and with a positive denominator.
     |      Raise OverflowError on infinities and a ValueError on NaNs.
     |      
     |      >>> (10.0).as_integer_ratio()
     |      (10, 1)
     |      >>> (0.0).as_integer_ratio()
     |      (0, 1)
     |      >>> (-.25).as_integer_ratio()
     |      (-1, 4)
     |  
     |  conjugate(...)
     |      Return self, the complex conjugate of any float.
     |  
     |  fromhex(...) from builtins.type
     |      float.fromhex(string) -> float
     |      
     |      Create a floating-point number from a hexadecimal string.
     |      >>> float.fromhex('0x1.ffffp10')
     |      2047.984375
     |      >>> float.fromhex('-0x1p-1074')
     |      -5e-324
     |  
     |  hex(...)
     |      float.hex() -> string
     |      
     |      Return a hexadecimal representation of a floating-point number.
     |      >>> (-0.1).hex()
     |      '-0x1.999999999999ap-4'
     |      >>> 3.14159.hex()
     |      '0x1.921f9f01b866ep+1'
     |  
     |  is_integer(...)
     |      Return True if the float is an integer.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |  
     |  imag
     |      the imaginary part of a complex number
     |  
     |  real
     |      the real part of a complex number
    
The ``float`` class has a single constructor, which can take a number or a string and will attempt to convert it to a float.

```python
float(10)
```

    10.0

```python
float(3.14)
```

    3.14

```python
float('0.1')
```

    0.1

However, strings that represent fractions cannot be converted to floats, unlike the Fraction class we saw earlier.

```python
float('22/7')
```

    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-5-32cff4369993> in <module>()
    ----> 1 float('22/7')
    

    ValueError: could not convert string to float: '22/7'

If you really want to get a float from a string such as ``'22/7'``, you could first create a ``Fraction``, then create a ``float`` from that:

```python
from fractions import Fraction
```

```python
float(Fraction('22/7'))
```

Floats do not always have an exact representation:

```python
print(0.1)
```

Although this looks like ``0.1`` exactly, we need to reveal more digits after the decimal point to see what's going on:

```python
format(0.1, '.25f')
```

However, certain numbers can be represented exactly in a binary fraction expansion:

```python
format(0.125, '.25f')
```

This is because 0.125 is precisely 1/8, or 1/(2^3)

#### 06 - Floats - Equality Testing

Because not all real numbers have an exact ``float`` representation, equality testing can be tricky.

```python
x = 0.1 + 0.1 + 0.1
y = 0.3
x == y
```

    False

This is because ``0.1`` and ``0.3`` do not have exact representations:

```python
print('0.1 --> {0:.25f}'.format(0.1))
print('x --> {0:.25f}'.format(x))
print('y --> {0:.25f}'.format(y))
```

    0.1 --> 0.1000000000000000055511151
    x --> 0.3000000000000000444089210
    y --> 0.2999999999999999888977698

However, in some (limited) cases where all the numbers involved do have an exact representation, it will work:

```python
x = 0.125 + 0.125 + 0.125
y = 0.375
x == y
```

    True

```python
print('0.125 --> {0:.25f}'.format(0.125))
print('x --> {0:.25f}'.format(x))
print('y --> {0:.25f}'.format(y))
```

    0.125 --> 0.1250000000000000000000000
    x --> 0.3750000000000000000000000
    y --> 0.3750000000000000000000000

One simple way to get around this is to round to a specific number of digits and then compare

```python
x = 0.1 + 0.1 + 0.1
y = 0.3
round(x, 5) == round(y, 5)
```

    True

We can also use a more flexible technique implemented by the ``isclose`` method in the ``math`` module

```python
from math import isclose
```

```python
help(isclose)
```

    Help on built-in function isclose in module math:
    
    isclose(...)
        isclose(a, b, *, rel_tol=1e-09, abs_tol=0.0) -> bool
        
        Determine whether two floating point numbers are close in value.
        
           rel_tol
               maximum difference for being considered "close", relative to the
               magnitude of the input values
            abs_tol
               maximum difference for being considered "close", regardless of the
               magnitude of the input values
        
        Return True if a is close in value to b, and False otherwise.
        
        For the values to be considered close, the difference between them
        must be smaller than at least one of the tolerances.
        
        -inf, inf and NaN behave similarly to the IEEE 754 Standard.  That
        is, NaN is not close to anything, even itself.  inf and -inf are
        only close to themselves.
    
```python
x = 0.1 + 0.1 + 0.1
y = 0.3
isclose(x, y)
```

    True

The ``isclose`` method takes two optional parameters, ``rel_tol`` and ``abs_tol``.

``rel_tol`` is a relative tolerance that will be relative to the magnitude of the largest of the two numbers being compared. Useful when we want to see if two numbers are close to each other as a percentage of their magnitudes.

``abs_tol`` is an absolute tolerance that is independent of the magnitude of the numbers we are comparing - this is useful for numbers that are close to zero.

In this situation we might consider x and y to be close to each other:

```python
x = 123456789.01
y = 123456789.02
```

but not in this case:

```python
x = 0.01
y = 0.02
```

In both these cases the difference between the two numbers was ``0.01``, yet in one case we considered the numbers "equal" and in the other, not "equal". Relative tolerances are useful to handle these scenarios.

```python
isclose(123456789.01, 123456789.02, rel_tol=0.01)
```

    True

```python
isclose(0.01, 0.02, rel_tol=0.01)
```

    False

On the other hand, we have to be careful with relative tolerances when working with values that are close to zero:

```python
x = 0.0000001
y = 0.0000002
isclose(x, y, rel_tol=0.01)
```

    False

So, we could use an absolute tolerance here:

```python
isclose(x, y, abs_tol=0.0001, rel_tol=0)
```

    True

In general, we can combine the use of both relative and absolute tolerances in this way:

```python
x = 0.0000001
y = 0.0000002

a = 123456789.01
b = 123456789.02

print('x = y:', isclose(x, y, abs_tol=0.0001, rel_tol=0.01))
print('a = b:', isclose(a, b, abs_tol=0.0001, rel_tol=0.01))
```

    x = y: True
    a = b: True

#### 07 - Floats - Coercing to Integers

##### Truncation

```python
from math import trunc
```

```python
trunc(10.3), trunc(10.5), trunc(10.6)
```

    (10, 10, 10)

```python
trunc(-10.6), trunc(-10.5), trunc(-10.3)
```

    (-10, -10, -10)

The **int** constructor uses truncation when a float is passed in:

```python
int(10.3), int(10.5), int(10.6)
```

    (10, 10, 10)

```python
int(-10.5), int(-10.5), int(-10.4)
```

    (-10, -10, -10)

##### Floor

```python
from math import floor
```

```python
floor(10.4), floor(10.5), floor(10.6)
```

    (10, 10, 10)

```python
floor(-10.4), floor(-10.5), floor(-10.6)
```

    (-11, -11, -11)

##### Ceiling

```python
from math import ceil
```

```python
ceil(10.4), ceil(10.5), ceil(10.6)
```

    (11, 11, 11)

```python
ceil(-10.4), ceil(-10.5), ceil(-10.6)
```

    (-10, -10, -10)



#### 08 - Floats - Rounding

```python
help(round)

```

    Help on built-in function round in module builtins:
    
    round(...)
        round(number[, ndigits]) -> number
        
        Round a number to a given precision in decimal digits (default 0 digits).
        This returns an int when called with one argument, otherwise the
        same type as the number. ndigits may be negative.
    
##### n = 0

```python
a = round(1.5)
a, type(a)
```

    (2, int)

```python
a = round(1.5, 0)
a, type(b)
```

    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-6-356ec769b541> in <module>()
          1 a = round(1.5, 0)
    ----> 2 a, type(b)
    

    NameError: name 'b' is not defined

##### n > 0

```python
round(1.8888, 3), round(1.8888, 2), round(1.8888, 1), round(1.8888, 0)
```

##### n < 0

```python
round(888.88, 1), round(888.88, 0), \
round(888.88, -1), round(888.88, -2), \
round(888.88, -3)
```

##### Ties

```python
round(1.25, 1)
```

```python
round(1.35, 1)
```

This is rounding to nearest, with ties to nearest number with even least significant digit, aka Banker's Rounding.

Works similarly with **n** negative.

```python
round(15, -1)
```

```python
round(25, -1)
```

##### Rounding to closest, ties away from zero

This is traditionally the type of rounding taught in school, which is different from the Banker's Rounding implemented in Python (and in many other programming languages)

1.5 --> 2 <br>
2.5 --> 3 <br>

-1.5 --> -2 <br>
-2.5 --> -3 <br>

To do this type of rounding (to nearest 1) we can add (for positive numbers) or subtract (for negative numbers) 0.5 and then truncate the resulting number.

```python
def _round(x):
    from math import copysign
    return int(x + 0.5 * copysign(1, x))
```

```python
round(1.5), _round(1.5)
```

```python
round(2.5), _round(2.5)
```

#### 09 - Decimals

```python
import decimal
```

```python
from decimal import Decimal
```

Decimals have context, that can be used to specify rounding and precision (amongst other things)

Contexts can be local (temporary contexts) or global (default)

##### Global Context

```python
g_ctx  = decimal.getcontext()
```

```python
g_ctx.prec
```

    28

```python
g_ctx.rounding
```

    'ROUND_HALF_EVEN'

We can change settings in the global context:

```python
g_ctx.prec = 6
```

```python
g_ctx.rounding = decimal.ROUND_HALF_UP
```

And if we read this back directly from the global context:

```python
decimal.getcontext().prec
```

    6

```python
decimal.getcontext().rounding
```

    'ROUND_HALF_UP'

we see that the global context was indeed changed.

##### Local Context

The ``localcontext()`` function will return a context manager that we can use with a ``with`` statement:

```python
with decimal.localcontext() as ctx:
    print(ctx.prec)
    print(ctx.rounding)
```

    6
    ROUND_HALF_UP

Since no argument was specified in the ``localcontext()`` call, it provides us a context manager that uses a copy of the global context.

Modifying the local context has no effect on the global context

```python
with decimal.localcontext() as ctx:
    ctx.prec = 10
    print('local prec = {0}, global prec = {1}'.format(ctx.prec, g_ctx.prec))
```

    local prec = 10, global prec = 6

##### Rounding

```python
decimal.getcontext().rounding
```

    'ROUND_HALF_UP'

The rounding mechanism is ROUND_HALF_UP because we set the global context to that earlier in this notebook. Note that normally the default is ROUND_HALF_EVEN.

So we first reset our global context rounding to that:

```python
decimal.getcontext().rounding = decimal.ROUND_HALF_EVEN
```

```python
x = Decimal('1.25')
y = Decimal('1.35')
print(round(x, 1))
print(round(y, 1))
```

    1.2
    1.4

Let's change the rounding mechanism in the global context to ROUND_HALF_UP:

```python
decimal.getcontext().rounding = decimal.ROUND_HALF_UP
```

```python
x = Decimal('1.25')
y = Decimal('1.35')
print(round(x, 1))
print(round(y, 1))
```

    1.3
    1.4

As you may have realized, changing the global context is a pain if you need to constantly switch between different precisions and rounding algorithms. Also, it could introduce bugs if you forget that you changed the global context somewhere further up in your module.

For this reason, it is usually better to use a local context manager instead:

First we reset our global context rounding to the default:

```python
decimal.getcontext().rounding = decimal.ROUND_HALF_EVEN
```

```python
x = Decimal('1.25')
y = Decimal('1.35')
print(round(x, 1), round(y, 1))
with decimal.localcontext() as ctx:
    ctx.rounding = decimal.ROUND_HALF_UP
    print(round(x, 1), round(y, 1))
print(round(x, 1), round(y, 1))
```

    1.2 1.4
    1.3 1.4
    1.2 1.4

#### 10 - Decimals - Constructors and Contexts

The **Decimal** constructor can handle a variety of data types

```python
import decimal
from decimal import Decimal
```

##### Integers

```python
Decimal(10)
```

    Decimal('10')

```python
Decimal(-10)
```

    Decimal('-10')

##### Strings

```python
Decimal('0.1')
```

    Decimal('0.1')

```python
Decimal('-3.1415')
```

    Decimal('-3.1415')


##### Tuples

```python
Decimal ((0, (3,1,4,1,5), -4))
```

	Decimal('3.1415')

```python
Decimal((1, (1,2,3,4), -3))
```

    Decimal('-1.234')

```python
Decimal((0, (1,2,3), 3))
```

    Decimal('1.23E+5')

##### But don't use Floats

```python
format(0.1, '.25f')
```

    '0.1000000000000000055511151'

```python
Decimal(0.1)
```

    Decimal('0.1000000000000000055511151231257827021181583404541015625')

As you can see, since we passed an approximate binary float to the Decimal constructor it did it's best to represent that binary float **exactly**!!

So, instead, use strings or tuples in the Decimal constructor.

##### Context Precision and the Constructor

The context precision does nto affect the precision used when creating a Decimal object - those are independent of each other.

Let's set our global (default) context to a precision of 2

```python
decimal.getcontext().prec = 2
```

Now we can create decimal numbers of higher precision than that:

```python
a = Decimal('0.12345')
b = Decimal('0.12345')
```

```python
a
```

    Decimal('0.12345')

```python
b
```

    Decimal('0.12345')

But when we add those two numbers up, the context precision will matter:

```python
a+b
```

    Decimal('0.25')

As you can see, we ended up with a sum that was rounded to 2 digits after the decimal point (precision = 2)

##### Local and Global Contexts are Independent

```python
decimal.getcontext().prec = 6
```

```python
decimal.getcontext().rounding
```

    'ROUND_HALF_EVEN'

```python
a = Decimal('0.12345')
b = Decimal('0.12345')
print(a + b)
with decimal.localcontext() as ctx:
    ctx.prec = 2
    c = a + b
    print('c within local context: {0}'.format(c))
print('c within global context: {0}'.format(c))
```

    0.24690
    c within local context: 0.25
    c within global context: 0.25

Since **c** was created within the local context by adding **a** and **b**, and the local context had a precision of 2, **c** was rounded to 2 digits after the decimal point.

Once the local context is destroyed (after the **with** block), the variable **c** still exists, and its precision is **still** just 2 - it doesn't magically suddenly get the global context's precision of 6.

#### 11 - Decimals - Math Operations

##### Div and Mod

The // and % operators (and consequently, the divmod() function) behave differently for integers and Decimals.

This is because integer division for Decimals is performed differently, and results in a truncated division, whereas integers use a floored division.

These differences are only when negative numbers are involved. If all numbers involved are positive, then integer and Decimal div and mod operations are equal.

But in both cases the // and % operators satisfy the equation:

``n = d * (n // d) + (n % d)``

```python
import decimal
from decimal import Decimal
```

```python
x = 10
y = 3
print(x//y, x%y)
print(divmod(x, y))
print( x == y * (x//y) + x % y)
```

    3 1
    (3, 1)
    True

```python
a = Decimal('10')
b = Decimal('3')
print(a//b, a%b)
print(divmod(a, b))
print( a == b * (a//b) + a % b)
```

    3 1
    (Decimal('3'), Decimal('1'))
    True

As we can see, the // and % operators had the same result when both numbers were positive.


```python
x = -10
y = 3
print(x//y, x%y)
print(divmod(x, y))
print( x == y * (x//y) + x % y)
```

    -4 2
    (-4, 2)
    True

```python
a = Decimal('-10')
b = Decimal('3')
print(a//b, a%b)
print(divmod(a, b))
print( a == b * (a//b) + a % b)
```

    -3 -1
    (Decimal('-3'), Decimal('-1'))
    True

On the other hand, we see that in this case the // and % operators did not result in the same values, although the equation was satisfied in both instances.

##### Other Mathematical Functions

The Decimal class implements a variety of mathematical functions.

```python
a = Decimal('1.5')
print(a.log10())  # base 10 logarithm
print(a.ln())     # natural logarithm (base e)
print(a.exp())    # e**a
print(a.sqrt())   # square root
```

    0.1760912590556812420812890085
    0.4054651081081643819780131155
    4.481689070338064822602055460
    1.224744871391589049098642037

Although you can use the math function of the math module, be aware that the math module functions will cast the Decimal numbers to floats when it performs the various operations. So, if the precision is important (which it probably is if you decided to use Decimal numbers in the first place), choose the math functions of the Decimal class over those of the math module.

```python
x = 2
x_dec = Decimal(2)
```

```python
import math
```

```python
root_float = math.sqrt(x)
root_mixed = math.sqrt(x_dec)
root_dec = x_dec.sqrt()
```

```python
print(format(root_float, '1.27f'))
print(format(root_mixed, '1.27f'))
print(root_dec)
```

    1.414213562373095145474621859
    1.414213562373095145474621859
    1.414213562373095048801688724

```python
print(format(root_float * root_float, '1.27f'))
print(format(root_mixed * root_mixed, '1.27f'))
print(root_dec * root_dec)
```

    2.000000000000000444089209850
    2.000000000000000444089209850
    1.999999999999999999999999999

```python
x = 0.01
x_dec = Decimal('0.01')

root_float = math.sqrt(x)
root_mixed = math.sqrt(x_dec)
root_dec = x_dec.sqrt()

print(format(root_float, '1.27f'))
print(format(root_mixed, '1.27f'))
print(root_dec)
```

    0.100000000000000005551115123
    0.100000000000000005551115123
    0.1

```python
print(format(root_float * root_float, '1.27f'))
print(format(root_mixed * root_mixed, '1.27f'))
print(root_dec * root_dec)
```

    0.010000000000000001942890293
    0.010000000000000001942890293
    0.01

#### 12 - Decimals - Performance Considerations

##### Memory Footprint

Decimals take up a lot more memory than floats.

```python
import sys
from decimal import Decimal
```

```python
a = 3.1415
b = Decimal('3.1415')
```

```python
sys.getsizeof(a)
```

    24

24 bytes are used to store the float 3.1415

```python
sys.getsizeof(b)
```

    104

104 bytes are used to store the Decimal 3.1415

##### Computational Performance

Decimal arithmetic is also much slower than float arithmetic (on a CPU, and even more so if using a GPU)

We can do some rough timings to illustrate this.

First we look at the performance difference creating floats vs decimals:

```python
import time
from decimal import Decimal

def run_float(n=1):
    for i in range(n):
        a = 3.1415
        
def run_decimal(n=1):
    for i in range(n):
        a = Decimal('3.1415')

```

Timing float and Decimal operations:

```python
n = 10000000
```

```python
start = time.perf_counter()
run_float(n)
end = time.perf_counter()
print('float: ', end-start)

start = time.perf_counter()
run_decimal(n)
end = time.perf_counter()
print('decimal: ', end-start)
```

    float:  0.21406484986433047
    decimal:  2.1353148079910156

We make a slight variant here to see how addition compares between the two types:

```python
def run_float(n=1):
    a = 3.1415
    for i in range(n):
        a + a
        
def run_decimal(n=1):
    a = Decimal('3.1415')
    for i in range(n):
        a + a
        
start = time.perf_counter()
run_float(n)
end = time.perf_counter()
print('float: ', end-start)

start = time.perf_counter()
run_decimal(n)
end = time.perf_counter()
print('decimal: ', end-start)
```

    float:  0.1875864573764936
    decimal:  0.3911394302055555

How about square roots:

(We drop the n count a bit)

```python
n = 5000000

import math

def run_float(n=1):
    a = 3.1415
    for i in range(n):
        math.sqrt(a)
        
def run_decimal(n=1):
    a = Decimal('3.1415')
    for i in range(n):
        a.sqrt()
        
start = time.perf_counter()
run_float(n)
end = time.perf_counter()
print('float: ', end-start)

start = time.perf_counter()
run_decimal(n)
end = time.perf_counter()
print('decimal: ', end-start)
```

    float:  0.673833850211659
    decimal:  14.73112183459776

#### 13 - Complex Numbers

Python's built-in class provides support for complex numbers.

Complex numbers are defined in rectangular coordinates (real and imaginary parts) using either the constructor or a literal expression.

The complex number 1 + 2j can be defined in either of these ways:

```python
a = complex(1, 2)
b = 1 + 2j
```

```python
a == b
```

    True

Note that the real and imaginary parts are defined as floats, and can be retrieved as follows:

```python
a.real, type(a.real)
```

    (1.0, float)

```python
a.imag, type(a.imag)
```

    (2.0, float)

The complex conjugate can be calculated as follows:

```python
a.conjugate()
```

    (1-2j)

The standard arithmetic operatots are polymorphic and defined for complex numbers

```python
a = 1 + 2j
b = 3 - 4j
c = 5j
d = 10
```

```python
a + b
```

    (4-2j)

```python
b * c
```

    (20+15j)

```python
c / d
```

    0.5j

```python
d - a
```

    (9-2j)

The // and % operators, although also polymorphic, are not defined for complex numbers:

```python
a // b
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-11-d3400ddfd09e> in <module>()
    ----> 1 a // b
    

    TypeError: can't take floor of complex number.

```python
a % b
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-12-209a85c6b5ad> in <module>()
    ----> 1 a % b
    

    TypeError: can't mod complex numbers.

The == and != operators support complex numbers - but since the real and imaginary parts of complex numbers are floats, the same problems comparing floats using == and != also apply to complex numbers.

```python
a = 0.1j
a + a + a == 0.3j
```

    False

In addition, the standard comparison operators (<, <=, >, >=) are not defined for complex numbers.

```python
a = 1 + 1j
b = 100 + 100j
a < b
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-15-a9748a0ff9df> in <module>()
          1 a = 1 + 1j
          2 b = 100 + 100j
    ----> 3 a < b
    

    TypeError: '<' not supported between instances of 'complex' and 'complex'

##### Math Functions

The **cmath** module provides complex alternatives to the standard **math** functions.

In addition, the **cmath** module provides the complex implementation of the **isclose()** method available for floats.

```python
import cmath

a = 1 + 5j
print(cmath.sqrt(a))
```

    (1.7462845577958914+1.4316108957382214j)

The standard **math** module functions will not work with complex numbers:

```python
import math
print(math.sqrt(a))
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-18-77a8fdd31911> in <module>()
          1 import math
    ----> 2 print(math.sqrt(a))
    

    TypeError: can't convert complex to float

##### Polar / Rectangular Conversions

The **cmath.phase()** function can be used to return the phase (or argument) of  any complex number.

The standard **abs()** function supports complex numbers and will return the magnitude (euclidean norm) of the complex number.

```python
a = 1 + 1j
```

```python
r = abs(a)
phi = cmath.phase(a)
print('{0} = ({1},{2})'.format(a, r, phi))
```

    (1+1j) = (1.4142135623730951,0.7853981633974483)

Complex numbers in polar coordinates can be converted to rectangular coordinates using the **math.rect()** function:

```python
r = math.sqrt(2)
phi = cmath.pi/4
print(cmath.rect(r, phi))
```

    (1.0000000000000002+1.0000000000000002j)

##### Euler's Identity and the **isclose()** function

e<sup>i &pi;</sup> + 1 = 0

```python
RHS = cmath.exp(cmath.pi * 1j) + 1
print(RHS)
```

    1.2246467991473532e-16j

Which, because of limited precision is not quite zero.

However, the result is very close to zero.

We can use the **isclose()** method of the **cmath** module, which behaves similarly to the **math.isclose()** method. Since we are testing for closeness of two numbers close to zero, we need to make sure an absolute tolerance is also specified:

```python
cmath.isclose(RHS, 0, abs_tol=0.00001)
```

    True

If we had not specified an absolute tolerance:

```python
cmath.isclose(RHS, 0)
```

    False

#### 14 - Booleans

The **bool** class is used to represent boolean values.

The **bool** class inherits from the **int** class.

```python
issubclass(bool, int)
```

    True

Two built-in constants, **True** and **False** are singleton instances of the bool class with underlying int values of 1 and 0 respectively.

```python
type(True), id(True), int(True)
```

    (bool, 1658060976, 1)

```python
type(False), id(False), int(False)
```

    (bool, 1658061008, 0)

These two values are instances of the **bool** class, and by inheritance are also **int** objects.

```python
isinstance(True, bool)
```

    True

```python
isinstance(True, int)
```

    True

Since **True** and **False** are singletons, we can use either the **is** operator, or the **==** operator to compare them to **any** boolean expression.

```python
id(True), id(1 < 2)
```

    (1658060976, 1658060976)

```python
id(False), id(1 == 3)
```

    (1658061008, 1658061008)

```python
(1 < 2) is True, (1 < 2) == True
```

    (True, True)

```python
(1 == 2) is False, (1 == 2) == False
```

    (True, True)

Be careful with that last comparison, the parentheses are necessary!

```python
1 == 2 == False
```

    False

```python
(1 == 2) == False
```

    True

We'll look into this in detail later, but, for now, this happens because a chained comparison such as **a == b == c** is actually evaluated as **a == b and b == c**

So **1 == 2 == False ** is the same as **1 == 2 and 2 == False**

```python
1 == 2, 2 == False, 1==2 and 2==False
```

    (False, False, False)

But, 

```python
(1 == 2)
```

    False

So **(1 == 2) == False** evaluates to True

But since **False** is also **0**, we get the following:

```python
(1 == 2) == 0
```

    True

The underlying integer values of True and False are:

```python
int(True), int(False)
```

    (1, 0)

So, using an equality comparison:

```python
1 == True, 0 == False
```

    (True, True)

But, from an object perspective 1 and True are not the same (similarly with 0 and False)

```python
1 == True, 1 is True
```

    (True, False)

```python
0 == False, 0 is False
```

    (True, False)

Any integer can be cast to a boolean, and follows the rule:

bool(x) = True for any x except for zero which returns False

```python
bool(0)
```

    False

```python
bool(1), bool(100), bool(-1)
```

    (True, True, True)

Since booleans are subclassed from integers, they can behave like integers, and because of polymorphism all the standard integer operators, properties and methods apply

```python
True > False
```

    True

```python
True + 2
```

    3

```python
False // 2
```

    0

```python
True + True + True
```

    3

```python
(True + True + True) % 2
```

    1

```python
-True
```

    -1

```python
100 * False
```

    0

I certainly **do not** recommend you write code like that shown above, but be aware that it does work.

#### 15 - Booleans - Truth Values

All objects in Python have an associated **truth value**, or **truthyness**

We saw in a previous lecture that integers have an inherent truth value:

```python
bool(0)
```

    False

```python
bool(1), bool(-1), bool(100)
```

    (True, True, True)

This truthyness has nothing to do with the fact that **bool** is a subclass of **int**.

Instead, it has to do with the fact that the **int** class implements a `__bool__()` method:

```python
help(bool)
```

    Help on class bool in module builtins:
    
    class bool(int)
     |  bool(x) -> bool
     |  
     |  Returns True when the argument x is true, False otherwise.
     |  The builtins True and False are the only two instances of the class bool.
     |  The class bool is a subclass of the class int, and cannot be subclassed.
     |  
     |  Method resolution order:
     |      bool
     |      int
     |      object
     |  
     |  Methods defined here:
     |  
     |  __and__(self, value, /)
     |      Return self&value.
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __or__(self, value, /)
     |      Return self|value.
     |  
     |  __rand__(self, value, /)
     |      Return value&self.
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __ror__(self, value, /)
     |      Return value|self.
     |  
     |  __rxor__(self, value, /)
     |      Return value^self.
     |  
     |  __str__(self, /)
     |      Return str(self).
     |  
     |  __xor__(self, value, /)
     |      Return self^value.
     |  
     |  ----------------------------------------------------------------------
     |  Methods inherited from int:
     |  
     |  __abs__(self, /)
     |      abs(self)
     |  
     |  __add__(self, value, /)
     |      Return self+value.
     |  
     |  __bool__(self, /)
     |      self != 0
     |  
     |  __ceil__(...)
     |      Ceiling of an Integral returns itself.
     |  
     |  __divmod__(self, value, /)
     |      Return divmod(self, value).
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __float__(self, /)
     |      float(self)
     |  
     |  __floor__(...)
     |      Flooring an Integral returns itself.
     |  
     |  __floordiv__(self, value, /)
     |      Return self//value.
     |  
     |  __format__(...)
     |      default object formatter
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __getnewargs__(...)
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __hash__(self, /)
     |      Return hash(self).
     |  
     |  __index__(self, /)
     |      Return self converted to an integer, if self is suitable for use as an index into a list.
     |  
     |  __int__(self, /)
     |      int(self)
     |  
     |  __invert__(self, /)
     |      ~self
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __lshift__(self, value, /)
     |      Return self<<value.
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __mod__(self, value, /)
     |      Return self%value.
     |  
     |  __mul__(self, value, /)
     |      Return self*value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __neg__(self, /)
     |      -self
     |  
     |  __pos__(self, /)
     |      +self
     |  
     |  __pow__(self, value, mod=None, /)
     |      Return pow(self, value, mod).
     |  
     |  __radd__(self, value, /)
     |      Return value+self.
     |  
     |  __rdivmod__(self, value, /)
     |      Return divmod(value, self).
     |  
     |  __rfloordiv__(self, value, /)
     |      Return value//self.
     |  
     |  __rlshift__(self, value, /)
     |      Return value<<self.
     |  
     |  __rmod__(self, value, /)
     |      Return value%self.
     |  
     |  __rmul__(self, value, /)
     |      Return value*self.
     |  
     |  __round__(...)
     |      Rounding an Integral returns itself.
     |      Rounding with an ndigits argument also returns an integer.
     |  
     |  __rpow__(self, value, mod=None, /)
     |      Return pow(value, self, mod).
     |  
     |  __rrshift__(self, value, /)
     |      Return value>>self.
     |  
     |  __rshift__(self, value, /)
     |      Return self>>value.
     |  
     |  __rsub__(self, value, /)
     |      Return value-self.
     |  
     |  __rtruediv__(self, value, /)
     |      Return value/self.
     |  
     |  __sizeof__(...)
     |      Returns size in memory, in bytes
     |  
     |  __sub__(self, value, /)
     |      Return self-value.
     |  
     |  __truediv__(self, value, /)
     |      Return self/value.
     |  
     |  __trunc__(...)
     |      Truncating an Integral returns itself.
     |  
     |  bit_length(...)
     |      int.bit_length() -> int
     |      
     |      Number of bits necessary to represent self in binary.
     |      >>> bin(37)
     |      '0b100101'
     |      >>> (37).bit_length()
     |      6
     |  
     |  conjugate(...)
     |      Returns self, the complex conjugate of any int.
     |  
     |  from_bytes(...) from builtins.type
     |      int.from_bytes(bytes, byteorder, *, signed=False) -> int
     |      
     |      Return the integer represented by the given array of bytes.
     |      
     |      The bytes argument must be a bytes-like object (e.g. bytes or bytearray).
     |      
     |      The byteorder argument determines the byte order used to represent the
     |      integer.  If byteorder is 'big', the most significant byte is at the
     |      beginning of the byte array.  If byteorder is 'little', the most
     |      significant byte is at the end of the byte array.  To request the native
     |      byte order of the host system, use `sys.byteorder' as the byte order value.
     |      
     |      The signed keyword-only argument indicates whether two's complement is
     |      used to represent the integer.
     |  
     |  to_bytes(...)
     |      int.to_bytes(length, byteorder, *, signed=False) -> bytes
     |      
     |      Return an array of bytes representing an integer.
     |      
     |      The integer is represented using length bytes.  An OverflowError is
     |      raised if the integer is not representable with the given number of
     |      bytes.
     |      
     |      The byteorder argument determines the byte order used to represent the
     |      integer.  If byteorder is 'big', the most significant byte is at the
     |      beginning of the byte array.  If byteorder is 'little', the most
     |      significant byte is at the end of the byte array.  To request the native
     |      byte order of the host system, use `sys.byteorder' as the byte order value.
     |      
     |      The signed keyword-only argument determines whether two's complement is
     |      used to represent the integer.  If signed is False and a negative integer
     |      is given, an OverflowError is raised.
     |  
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from int:
     |  
     |  denominator
     |      the denominator of a rational number in lowest terms
     |  
     |  imag
     |      the imaginary part of a complex number
     |  
     |  numerator
     |      the numerator of a rational number in lowest terms
     |  
     |  real
     |      the real part of a complex number
    
If you scroll down in the documentation you shoudl reach a section that looks like this:

`` 
|  __bool__(self, /)
|      self != 0
``

So, when we write:

```python
bool(100)
```

    True

Python is actually calling 100.__bool__() and returning that:

```python
(100).__bool__()
```

    True

```python
(0).__bool__()
```

    False

Most objects will implement either the `__bool__()` or `__len__()` methods. If they don't, then their associated value will be **True** always.

##### Numeric Types

Any non-zero numeric value is truthy. Any zero numeric value is falsy:

```python
from fractions import Fraction
from decimal import Decimal
bool(10), bool(1.5), bool(Fraction(3, 4)), bool(Decimal('10.5'))
```

    (True, True, True, True)

```python
bool(0), bool(0.0), bool(Fraction(0,1)), bool(Decimal('0')), bool(0j)
```

    (False, False, False, False, False)

##### Sequence Types

An empty sequence type object is Falsy, a non-empty one is truthy:

```python
bool([1, 2, 3]), bool((1, 2, 3)), bool('abc'), bool(1j)
```

    (True, True, True, True)

```python
bool([]), bool(()), bool('')
```

    (False, False, False)

##### Mapping Types

Similarly, an empty mapping type will be falsy, a non-empty one truthy:

```python
bool({'a': 1}), bool({1, 2, 3})
```

    (True, True)

```python
bool({}), bool(set())
```

    (False, False)

##### The None Object

The singleton **None** object is always falsy:

```python
bool(None)
```

    False

##### One Application of Truth Values

Any conditional expression which involves objects other than **bool** types, will use the associated truth value as the result of the conditional expression.

```python
a = [1, 2, 3]
if a:
    print(a[0])
else:
    print('a is None, or a is empty')
```

    1

```python
a = []
if a:
    print(a[0])
else:
    print('a is None, or a is empty')
```

    a is None, or a is empty

```python
a = 'abc'
if a:
    print(a[0])
else:
    print('a is None, or a is empty')
```

    a

```python
a = ''
if a:
    print(a[0])
else:
    print('a is None, or a is empty')
```

    a is None, or a is empty

We could write this using a more lengthy expression:

```python
a = 'abc'
if a is not None and len(a) > 0:
    print(a[0])
else:
    print('a is None, or a is empty')
```

    a

Doing the following would break our code in some instances:

```python
a = 'abc'
if a is not None:
    print(a[0])
```

    a

works, but:

```python
a = ''
if a is not None:
    print(a[0])
```

    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-44-47991d9c7397> in <module>()
          1 a = ''
          2 if a is not None:
    ----> 3     print(a[0])
    

    IndexError: string index out of range

or even:

```python
a = None
if len(a) > 0:
    print(a[0])
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-45-92ec20435e20> in <module>()
          1 a = None
    ----> 2 if len(a) > 0:
          3     print(a[0])


    TypeError: object of type 'NoneType' has no len()


To be thorough we would need to write:

```python
a = None
if a is not None and len(a) > 0:
    print(a[0])
```

Also, the order of the boolean expressions matter here!

We'll discuss this and short-circuit evaluations in an upcoming video.

For example:

```python
a = None
if len(a) > 0 and a is not None:
    print(a[0])
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-47-0842480c6625> in <module>()
          1 a = None
    ----> 2 if len(a) > 0 and a is not None:
          3     print(a[0])


    TypeError: object of type 'NoneType' has no len()

#### 16 - Booleans - Precedence and Short-Circuiting

```python
True or True and False
```

    True

this is equivalent, because of ``and`` having higer precedence than ``or``, to:

```python
True or (True and False)
```

    True

This is not the same as:

```python
(True or True) and False
```

    False

##### Short-Circuiting

```python
a = 10
b = 2

if a/b > 2:
    print('a is at least double b')
```

    a is at least double b

```python
a = 10
b = 0

if a/b > 2:
    print('a is at least double b')
```

    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-12-98ac73a1accd> in <module>()
          2 b = 0
          3 
    ----> 4 if a/b > 2:
          5     print('a is at least double b')


    ZeroDivisionError: division by zero

```python
a = 10
b = 0

if b and a/b > 2:
    print('a is at least double b')
```

Can also be useful to deal with null or empty strings in a database:

```python
import string
```

```python
help(string)
```

    Help on module string:
    
    NAME
        string - A collection of string constants.
    
    DESCRIPTION
        Public module variables:
        
        whitespace -- a string containing all ASCII whitespace
        ascii_lowercase -- a string containing all ASCII lowercase letters
        ascii_uppercase -- a string containing all ASCII uppercase letters
        ascii_letters -- a string containing all ASCII letters
        digits -- a string containing all ASCII decimal digits
        hexdigits -- a string containing all ASCII hexadecimal digits
        octdigits -- a string containing all ASCII octal digits
        punctuation -- a string containing all ASCII punctuation characters
        printable -- a string containing all ASCII characters considered printable
    
    CLASSES
        builtins.object
            Formatter
            Template
        
        class Formatter(builtins.object)
         |  Methods defined here:
         |  
         |  check_unused_args(self, used_args, args, kwargs)
         |  
         |  convert_field(self, value, conversion)
         |  
         |  format(*args, **kwargs)
         |  
         |  format_field(self, value, format_spec)
         |  
         |  get_field(self, field_name, args, kwargs)
         |      # given a field_name, find the object it references.
         |      #  field_name:   the field being looked up, e.g. "0.name"
         |      #                 or "lookup[3]"
         |      #  used_args:    a set of which args have been used
         |      #  args, kwargs: as passed in to vformat
         |  
         |  get_value(self, key, args, kwargs)
         |  
         |  parse(self, format_string)
         |      # returns an iterable that contains tuples of the form:
         |      # (literal_text, field_name, format_spec, conversion)
         |      # literal_text can be zero length
         |      # field_name can be None, in which case there's no
         |      #  object to format and output
         |      # if field_name is not None, it is looked up, formatted
         |      #  with format_spec and conversion and then used
         |  
         |  vformat(self, format_string, args, kwargs)
         |  
         |  ----------------------------------------------------------------------
         |  Data descriptors defined here:
         |  
         |  __dict__
         |      dictionary for instance variables (if defined)
         |  
         |  __weakref__
         |      list of weak references to the object (if defined)
        
        class Template(builtins.object)
         |  A string class for supporting $-substitutions.
         |  
         |  Methods defined here:
         |  
         |  __init__(self, template)
         |      Initialize self.  See help(type(self)) for accurate signature.
         |  
         |  safe_substitute(*args, **kws)
         |  
         |  substitute(*args, **kws)
         |  
         |  ----------------------------------------------------------------------
         |  Data descriptors defined here:
         |  
         |  __dict__
         |      dictionary for instance variables (if defined)
         |  
         |  __weakref__
         |      list of weak references to the object (if defined)
         |  
         |  ----------------------------------------------------------------------
         |  Data and other attributes defined here:
         |  
         |  delimiter = '$'
         |  
         |  flags = <RegexFlag.IGNORECASE: 2>
         |  
         |  idpattern = '[_a-z][_a-z0-9]*'
         |  
         |  pattern = re.compile('\n    \\$(?:\n      (?P<escaped>\\$)..._a-z][_a-...
    
    FUNCTIONS
        capwords(s, sep=None)
            capwords(s [,sep]) -> string
            
            Split the argument into words using split, capitalize each
            word using capitalize, and join the capitalized words using
            join.  If the optional second argument sep is absent or None,
            runs of whitespace characters are replaced by a single space
            and leading and trailing whitespace are removed, otherwise
            sep is used to split and join the words.
    
    DATA
        __all__ = ['ascii_letters', 'ascii_lowercase', 'ascii_uppercase', 'cap...
        ascii_letters = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
        ascii_lowercase = 'abcdefghijklmnopqrstuvwxyz'
        ascii_uppercase = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
        digits = '0123456789'
        hexdigits = '0123456789abcdefABCDEF'
        octdigits = '01234567'
        printable = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTU...
        punctuation = '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
        whitespace = ' \t\n\r\x0b\x0c'
    
    FILE
        c:\users\fbapt\anaconda3\envs\deepdive\lib\string.py

```python
string.digits
```

    '0123456789'

```python
string.ascii_letters
```

    'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'

```python
name = ''
if name[0] in string.digits:
    print('Name cannot start with a digit!')
```

    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-19-b6d1fe6f1f39> in <module>()
          1 name = ''
    ----> 2 if name[0] in string.digits:
          3     print('Name cannot start with a digit!')


    IndexError: string index out of range

```python
name = ''
if name and name[0] in string.digits:
    print('Name cannot start with a digit!')
```

```python
name = None
if name and name[0] in string.digits:
    print('Name cannot start with a digit!')
```

```python
name = 'Bob'
if name and name[0] in string.digits:
    print('Name cannot start with a digit!')
```

```python
name = '1Bob'
if name and name[0] in string.digits:
    print('Name cannot start with a digit!')
```

    Name cannot start with a digit!



#### 17 - Booleans - Boolean Operators

Operator Precedence:

```
()
< > <= >= == != in is
not
and
or
```

The way the Boolean operators ``and``, ``or`` actually work is a littel different in Python:

##### or

``X or Y``: If X is falsy, returns Y, otherwise evaluates and returns X

```python
'' or 'abc'
```

    'abc'

```python
0 or 100
```

    100

```python
[] or [1, 2, 3]
```

    [1, 2, 3]

```python
[1, 2] or [1, 2, 3]
```

    [1, 2]

You should note that the truth value of ``Y`` is never even considered when evaluating the ``or`` result!

Only the left operand matters.

Of course, Y will be evaluated if it is being returned - but its truth value does not affect how the ``or`` is being calculated.

You probably will notice that this means ``Y`` is not evaluated if ``X`` is returned - short-circuiting!!!

We could (almost!) write the ``or`` operator ourselves in this way:

```python
def _or(x, y):
    if x:
        return x
    else:
        return y
```

```python
print(_or(0, 100) == (0 or 100))
print(_or(None, 'n/a') == (None or 'n/a'))
print(_or('abc', 'n/a') == ('abc' or 'n/a'))
```

    True
    True
    True

Why did I say almost?

Unlike the ``or`` operator, our ``_or`` function will always evaluate x and y (they are passed as arguments) - so we do not have short-circuiting!

```python
1 or 1/0
```

    1

```python
_or(1, 1/0)
```

    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-32-7b66dcdf3d9c> in <module>()
    ----> 1 _or(1, 1/0)
    

    ZeroDivisionError: division by zero

##### and

`X and Y`: If X is falsy, returns X, otherwise evaluates and returns Y

Once again, note that the truth value of Y is never considered when evaluating `and`, and that ``Y`` is only evaluated if it needs to be returned (short-circuiting)

```python
s1 = None
s2 = ''
s3 = 'abc'
```

```python
print(s1 and s1[0])
print(s2 and s2[0])
print(s3 and s3[0])
```

    None
    
    a

```python
print((s1 and s1[0]) or '')
print((s2 and s2[0]) or '')
print((s3 and s3[0]) or '')
```  
    
    a

This technique will also work to return any default value if ``s`` is an empty string or None:

```python
print((s1 and s1[0]) or 'n/a')
print((s2 and s2[0]) or 'n/a')
print((s3 and s3[0]) or 'n/a')
```

    n/a
    n/a
    a

The ``not`` function

```python
not 'abc'
```

    False

```python
not []
```

    True

```python
bool(None)
```

    False

```python
not None
```

    True

#### 18 - Comparison Operators

##### Identity and Membership Operators

The **is** and **is not** operators will work with any data type since they are comparing the memory addresses of the objects (which are integers)

```python
0.1 is (3+4j)
```

    False

```python
'a' is [1, 2, 3]
```

    False

The **in** and **not in** operators are used with iterables and test membership:

```python
1 in [1, 2, 3]
```

    True

```python
[1, 2] in [1, 2, 3]
```

    False

```python
[1, 2] in [[1,2], [2,3], 'abc']
```

    True

```python
'key1' in {'key1': 1, 'key2': 2}
```

    True

```python
1 in {'key1': 1, 'key2': 2}
```

    False

We'll come back to these operators in later sections on iterables and mappings.

##### Equality Operators

The **==** and **!=** operators are value comparison operators. 

They will work with mixed types that are comparable in some sense.

For example, you can compare Fraction and Decimal objects, but it would not make sense to compare string and integer objects.

```python
1 == '1'
```

    False

```python
from decimal import Decimal
from fractions import Fraction
```

```python
Decimal('0.1') == Fraction(1, 10)
```

    True

```python
1 == 1 + 0j
```

    True

```python
True == Fraction(2, 2)
```

    True

```python
False == 0j
```

    True

##### Ordering Comparisons

Many, but not all data types have an ordering defined.

For example, complex numbers do not.

```python
1 + 1j < 2 + 2j
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-16-82ffa8a7b757> in <module>()
    ----> 1 1 + 1j < 2 + 2j
    

    TypeError: '<' not supported between instances of 'complex' and 'complex'

Mixed type ordering comparisons is supported, but again, it needs to make sense:

```python
1 < 'a'
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-17-ca85dbce74b5> in <module>()
    ----> 1 1 < 'a'
    

    TypeError: '<' not supported between instances of 'int' and 'str'

```python
Decimal('0.1') < Fraction(1, 2)
```

    True

##### Chained Comparisons

It is possible to chain comparisons.

For example, in **a < b < c**, Python simply **ands** the pairwise comparisons: **a < b and b < c**

```python
1 < 2 < 3
```

    True

```python
1 < 2 > -5 < 50 > 4
```

    True

```python
1 < 2 == Decimal('2.0')
```

    True

```python
import string
'A' < 'a' < 'z' > 'Z' in string.ascii_letters 
```

    True

### 5. Function Parameters

#### 01 - Positional Arguments

```python
def my_func(a, b, c):
    print("a={0}, b={1}, c={2}".format(a, b, c))
```

```python
my_func(1, 2, 3)
```

    a=1, b=2, c=3

##### Default Values

```python
def my_func(a, b=2, c=3):
    print("a={0}, b={1}, c={2}".format(a, b, c))
```

Note that once a parameter is assigned a default value, **all** parameters thereafter **must** be asigned a default value too!

For example, this will not work:

```python
def fn(a, b=2, c):
    print(a, b, c)
```

      File "<ipython-input-4-2180ec769037>", line 1
        def fn(a, b=2, c):
              ^
    SyntaxError: non-default argument follows default argument

```python
def my_func(a, b=2, c=3):
    print("a={0}, b={1}, c={2}".format(a, b, c))
```

```python
my_func(10, 20, 30)
```

    a=10, b=20, c=30

```python
my_func(10, 20)
```

    a=10, b=20, c=3

```python
my_func(10)
```

    a=10, b=2, c=3

Since **a** does not have a default value, it **must** be specified:

```python
my_func()
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-9-d82eda95de40> in <module>()
    ----> 1 my_func()
    

    TypeError: my_func() missing 1 required positional argument: 'a'

##### Keyword Arguments (named arguments)

Positional arguments, can **optionally**, be specified using their corresponding parameter name.

This allows us to pass the arguments without using the positional assignment:

```python
def my_func(a, b=2, c=3):
    print("a={0}, b={1}, c={2}".format(a, b, c))
```

```python
my_func(c=30, b=20, a=10)
```

    a=10, b=20, c=30

```python
my_func(10, c=30, b=20)
```

    a=10, b=20, c=30

Note that once a keyword argument has been used, **all** arguments thereafter **must** also be named:

```python
my_func(10, b=20, 30)
```


      File "<ipython-input-13-ea05eeab2151>", line 1
        my_func(10, b=20, 30)
                         ^
    SyntaxError: positional argument follows keyword argument

However, if a parameter has a default value, it *can* be omitted from the argument list, named or not:

```python
my_func(10, c=30)
```

    a=10, b=2, c=30

```python
my_func(a=30, c=10)
```

    a=30, b=2, c=10

```python
my_func(c=10, a=30)
```

    a=30, b=2, c=10

#### 02 - Unpacking Iterables

##### Side Note on Tuples

This is a tuple:

```python
a = (1, 2, 3)
```

```python
type(a)
```

    tuple

This is also a tuple:

```python
a = 1, 2, 3
```

```python
type(a)
```

    tuple

In fact what defines a tuple is not **()**, but the **,** (comma)

To create a tuple with a single element:

```python
a = (1)
```

will not work!!

```python
type(a)
```

    int

Instead, we have to use a comma:

```python
a = (1,)
```

```python
type(a)
```

    tuple

And in fact, we don't even need the **()**:

```python
a = 1,
```

```python
type(a)
```

    tuple

The only exception is to create an empty tuple:

```python
a = ()
```

```python
type(a)
```

    tuple

Or we can use the tuple constructor:

```python
a = tuple()
```

```python
type(a)
```

    tuple

##### Unpacking

Unpacking is a way to split an iterable object into individual variables contained in a list or tuple: 

```python
l = [1, 2, 3, 4]
```

```python
a, b, c, d = l
```

```python
print(a, b, c, d)
```

    1 2 3 4

Strings are iterables too:

```python
a, b, c = 'XYZ'
print(a, b, c)
```

    X Y Z

##### Swapping Two Variables

Here's a quick application of unpacking to swap the values of two variables.

First we look at the "traditional" way you would have to do it in other languages such as Java:

```python
a = 10
b = 20
print("a={0}, b={1}".format(a, b))

tmp = a
a = b
b = tmp
print("a={0}, b={1}".format(a, b))
```

    a=10, b=20
    a=20, b=10

But using unpacking we can simplify this:

```python
a = 10
b = 20
print("a={0}, b={1}".format(a, b))

a, b = b, a
print("a={0}, b={1}".format(a, b))
```

    a=10, b=20
    a=20, b=10

In fact, we can even simplify the initial assignment of values to a and b as follows:

```python
a, b = 10, 20
print("a={0}, b={1}".format(a, b))

a, b = b, a
print("a={0}, b={1}".format(a, b))
```

    a=10, b=20
    a=20, b=10

##### Unpacking Unordered Objects

```python
dict1 = {'p': 1, 'y': 2, 't': 3, 'h': 4, 'o': 5, 'n': 6}
```

```python
dict1
```


    {'h': 4, 'n': 6, 'o': 5, 'p': 1, 't': 3, 'y': 2}

```python
for c in dict1:
    print(c)
```

    p
    y
    t
    h
    o
    n

```python
a, b, c, d, e, f = dict1
print(a)
print(b)
print(c)
print(d)
print(e)
print(f)
```

    p
    y
    t
    h
    o
    n

Note that this order is not guaranteed. You can always use an OrderedDict if that is a requirement.

The same applies to sets.

```python
s = {'p', 'y', 't', 'h', 'o', 'n'}
```

```python
type(s)
```

    set

```python
print(s)
```

    {'p', 't', 'y', 'n', 'o', 'h'}

```python
for c in s:
    print(c)
```

    p
    t
    y
    n
    o
    h

```python
a, b, c, d, e, f = s
```

```python
print(a)
print(b)
print(c)
print(d)
print(e)
print(f)
```

    p
    t
    y
    n
    o
    h

#### 03 - Extended Unpacking

Let's see how we might split a list into it's first element, and "everything else" using slicing:

```python
l = [1, 2, 3, 4, 5, 6]
```

```python
a = l[0]
b = l[1:]
print(a)
print(b)
```

    1
    [2, 3, 4, 5, 6]

We can even use unpacking to simplify this slightly:

```python
a, b = l[0], l[1:]
print(a)
print(b)
```

    1
    [2, 3, 4, 5, 6]

But we can use the **\*** operator to achieve the same result:

```python
a, *b = l
print(a)
print(b)
```

    1
    [2, 3, 4, 5, 6]

Note that the **\*** operator can only appear **once**!

Like standard unpacking, this extended unpacking will work with any iterable.

With tuples:

```python
a, *b = -10, 5, 2, 100
print(a)
print(b)
```

    -10
    [5, 2, 100]

With strings:

```python
a, *b = 'python'
print(a)
print(b)
```

    p
    ['y', 't', 'h', 'o', 'n']

What about extracting the first, second, last elements and *the rest*.

Again we can use slicing:

```python
s = 'python'

a, b, c, d = s[0], s[1], s[2:-1], s[-1]
print(a)
print(b)
print(c)
print(d)
```

    p
    y
    tho
    n

But we can just as easily do it this way using unpacking:

```python
a, b, *c, d = s
print(a)
print(b)
print(c)
print(d)
```

    p
    y
    ['t', 'h', 'o']
    n

As you can see though, **c** is a list of characters, not a string.

It that's a problem we can easily fix it this way:

```python
print(c)
c = ''.join(c)
print(c)
```

    ['t', 'h', 'o']
    tho

We can also use unpacking on the right hand side of an assignment expression:

```python
l1 = [1, 2, 3]
l2 = [4, 5, 6]
l = [*l1, *l2]
print(l)
```

    [1, 2, 3, 4, 5, 6]

```python
l1 = [1, 2, 3]
s = 'ABC'
l = [*l1, *s]
print(l)
```

    [1, 2, 3, 'A', 'B', 'C']

This unpacking works with unordered types such as sets and dictionaries as well.

The only thing is that it may not be very useful considering there is no particular ordering, so a first or last element has no real useful meaning.

```python
s = {10, -99, 3, 'd'}
```

```python
for c in s:
    print(c)
```

    10
    3
    d
    -99

As you can see, the order of the elements when we created the set was not retained!

```python
s = {10, -99, 3, 'd'}
a, b, *c = s
print(a)
print(b)
print(c)
```

    10
    3
    ['d', -99]

So unpacking this way is of limited use.

However consider this:

```python
s = {10, -99, 3, 'd'}
*a, = s
print(a)
```

    [10, 3, 'd', -99]

At first blush, this doesn't look terribly exciting - we simply unpacked the set values into a list.

But this is actually quite useful in both sets and dictionaries to combine things (although to be sure, there are alternative ways to do this as well - which we'll cover later in this course)

```python
s1 = {1, 2, 3}
s2 = {3, 4, 5}
```

How can we combine both these sets into a single merged set?

```python
s1 + s2
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-22-1659087814e1> in <module>()
    ----> 1 s1 + s2
    

    TypeError: unsupported operand type(s) for +: 'set' and 'set'

Well, **+** doesn't work...

We could use the built-in method for unioning sets:

```python
help(set)
```

    Help on class set in module builtins:
    
    class set(object)
     |  set() -> new empty set object
     |  set(iterable) -> new set object
     |  
     |  Build an unordered collection of unique elements.
     |  
     |  Methods defined here:
     |  
     |  __and__(self, value, /)
     |      Return self&value.
     |  
     |  __contains__(...)
     |      x.__contains__(y) <==> y in x.
     |  
     |  __eq__(self, value, /)
     |      Return self==value.
     |  
     |  __ge__(self, value, /)
     |      Return self>=value.
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __gt__(self, value, /)
     |      Return self>value.
     |  
     |  __iand__(self, value, /)
     |      Return self&=value.
     |  
     |  __init__(self, /, *args, **kwargs)
     |      Initialize self.  See help(type(self)) for accurate signature.
     |  
     |  __ior__(self, value, /)
     |      Return self|=value.
     |  
     |  __isub__(self, value, /)
     |      Return self-=value.
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __ixor__(self, value, /)
     |      Return self^=value.
     |  
     |  __le__(self, value, /)
     |      Return self<=value.
     |  
     |  __len__(self, /)
     |      Return len(self).
     |  
     |  __lt__(self, value, /)
     |      Return self<value.
     |  
     |  __ne__(self, value, /)
     |      Return self!=value.
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __or__(self, value, /)
     |      Return self|value.
     |  
     |  __rand__(self, value, /)
     |      Return value&self.
     |  
     |  __reduce__(...)
     |      Return state information for pickling.
     |  
     |  __repr__(self, /)
     |      Return repr(self).
     |  
     |  __ror__(self, value, /)
     |      Return value|self.
     |  
     |  __rsub__(self, value, /)
     |      Return value-self.
     |  
     |  __rxor__(self, value, /)
     |      Return value^self.
     |  
     |  __sizeof__(...)
     |      S.__sizeof__() -> size of S in memory, in bytes
     |  
     |  __sub__(self, value, /)
     |      Return self-value.
     |  
     |  __xor__(self, value, /)
     |      Return self^value.
     |  
     |  add(...)
     |      Add an element to a set.
     |      
     |      This has no effect if the element is already present.
     |  
     |  clear(...)
     |      Remove all elements from this set.
     |  
     |  copy(...)
     |      Return a shallow copy of a set.
     |  
     |  difference(...)
     |      Return the difference of two or more sets as a new set.
     |      
     |      (i.e. all elements that are in this set but not the others.)
     |  
     |  difference_update(...)
     |      Remove all elements of another set from this set.
     |  
     |  discard(...)
     |      Remove an element from a set if it is a member.
     |      
     |      If the element is not a member, do nothing.
     |  
     |  intersection(...)
     |      Return the intersection of two sets as a new set.
     |      
     |      (i.e. all elements that are in both sets.)
     |  
     |  intersection_update(...)
     |      Update a set with the intersection of itself and another.
     |  
     |  isdisjoint(...)
     |      Return True if two sets have a null intersection.
     |  
     |  issubset(...)
     |      Report whether another set contains this set.
     |  
     |  issuperset(...)
     |      Report whether this set contains another set.
     |  
     |  pop(...)
     |      Remove and return an arbitrary set element.
     |      Raises KeyError if the set is empty.
     |  
     |  remove(...)
     |      Remove an element from a set; it must be a member.
     |      
     |      If the element is not a member, raise a KeyError.
     |  
     |  symmetric_difference(...)
     |      Return the symmetric difference of two sets as a new set.
     |      
     |      (i.e. all elements that are in exactly one of the sets.)
     |  
     |  symmetric_difference_update(...)
     |      Update a set with the symmetric difference of itself and another.
     |  
     |  union(...)
     |      Return the union of sets as a new set.
     |      
     |      (i.e. all elements that are in either set.)
     |  
     |  update(...)
     |      Update a set with the union of itself and others.
     |  
     |  ----------------------------------------------------------------------
     |  Data and other attributes defined here:
     |  
     |  __hash__ = None
    
```python
print(s1)
print(s2)
s1.union(s2)
```

    {1, 2, 3}
    {3, 4, 5}

    {1, 2, 3, 4, 5}

What about joining 4 different sets?

```python
s1 = {1, 2, 3}
s2 = {3, 4, 5}
s3 = {5, 6, 7}
s4 = {7, 8, 9}
print(s1.union(s2).union(s3).union(s4))
print(s1.union(s2, s3, s4))
```

    {1, 2, 3, 4, 5, 6, 7, 8, 9}
    {1, 2, 3, 4, 5, 6, 7, 8, 9}

Or we could use unpacking in this way:

```python
{*s1, *s2, *s3, *s4}
```

    {1, 2, 3, 4, 5, 6, 7, 8, 9}

What we did here was to unpack each set directly into another set!

The same works for dictionaries - just remember that **\*** for dictionaries unpacks the keys only.

```python
d1 = {'key1': 1, 'key2': 2}
d2 = {'key2': 3, 'key3': 3}
[*d1, *d2]
```

    ['key1', 'key2', 'key2', 'key3']

So, is there anything to unpack the key-value pairs for dictionaries instead of just the keys?

Yes - we can use the **\*\*** operator:

```python
d1 = {'key1': 1, 'key2': 2}
d2 = {'key2': 3, 'key3': 3}

{**d1, **d2}
```

    {'key1': 1, 'key2': 3, 'key3': 3}

Notice what happened to the value of **key2**. The value for the second occurrence of **key2** was retained (overwritten).

In fact, if we write the unpacking reversing the order of d1 and d2:

```python
{**d2, **d1}
```

    {'key1': 1, 'key2': 2, 'key3': 3}

we see that the value of **key2** is now **2**, since it was the second occurrence.

Of course, we can unpack a dictionary into a dictionary as seen above, but we can mix in our own key-value pairs as well - it is just a dictionary literal after all.

```python
{'a': 1, 'b': 2, **d1, **d2, 'c':3}
```

    {'a': 1, 'b': 2, 'c': 3, 'key1': 1, 'key2': 3, 'key3': 3}

Again, if we have the same keys, only the "latest" value of the key is retained:

```python
{'key1': 100, **d1, **d2, 'key3': 200}
```

    {'key1': 1, 'key2': 3, 'key3': 200}

##### Nested Unpacking

Python even supports nested unpacking:

```python
a, b, (c, d) = [1, 2, ['X', 'Y']]
print(a)
print(b)
print(c)
print(d)
```

    1
    2
    X
    Y

In fact, since a string is an iterable, we can even write:

```python
a, b, (c, d) = [1, 2, 'XY']
print(a)
print(b)
print(c)
print(d)
```

    1
    2
    X
    Y

We can even write something like this:

```python
a, b, (c, d, *e) = [1, 2, 'python']
print(a)
print(b)
print(c)
print(d)
print(e)
```

    1
    2
    p
    y
    ['t', 'h', 'o', 'n']

Remember when we said that we can use a * only **once**...

How about this then?

```python
a, *b, (c, d, *e) = [1, 2, 3, 'python']
print(a)
print(b)
print(c)
print(d)
print(e)
```

    1
    [2, 3]
    p
    y
    ['t', 'h', 'o', 'n']

We can break down what happened here in multiple steps:

```python
a, *b, tmp = [1, 2, 3, 'python']
print(a)
print(b)
print(tmp)
```

    1
    [2, 3]
    python

```python
c, d, *e = tmp
print(c)
print(d)
print(e)
```

    p
    y
    ['t', 'h', 'o', 'n']
So putting it together we get our original line of code:

```python
a, *b, (c, d, *e) = [1, 2, 3, 'python']
print(a)
print(b)
print(c)
print(d)
print(e)
```

    1
    [2, 3]
    p
    y
    ['t', 'h', 'o', 'n']

If we wanted to do the same thing using slicing:

```python
l = [1, 2, 3, 'python']
l[0], l[1:-1], l[-1][0], l[-1][1], list(l[-1][2:])
```

    (1, [2, 3], 'p', 'y', ['t', 'h', 'o', 'n'])

```python
l = [1, 2, 3, 'python']
a, b, c, d, e = l[0], l[1:-1], l[-1][0], l[-1][1], list(l[-1][2:])
print(a)
print(b)
print(c)
print(d)
print(e)
```

    1
    [2, 3]
    p
    y
    ['t', 'h', 'o', 'n']

Of course, this works for arbitrary lengths and indexable sequence types:

```python
l = [1, 2, 3, 4, 'unladen swallow']
a, b, c, d, e = l[0], l[1:-1], l[-1][0], l[-1][1], list(l[-1][2:])
print(a)
print(b)
print(c)
print(d)
print(e)
```

    1
    [2, 3, 4]
    u
    n
    ['l', 'a', 'd', 'e', 'n', ' ', 's', 'w', 'a', 'l', 'l', 'o', 'w']

or even:

```python
l = [1, 2, 3, 4, ['a', 'b', 'c', 'd']]
a, b, c, d, e = l[0], l[1:-1], l[-1][0], l[-1][1], list(l[-1][2:])
print(a)
print(b)
print(c)
print(d)
print(e)
```

    1
    [2, 3, 4]
    a
    b
    ['c', 'd']

#### 04 - \*args

Recall from iterable unpacking:

```python
a, b, *c = 10, 20, 'a', 'b'
```

```python
print(a, b)
```

    10 20

```python
print(c)
```

    ['a', 'b']

We can use a similar concept in function definitions to allow for arbitrary numbers of **positional** parameters/arguments:

```python
def func1(a, b, *args):
    print(a)
    print(b)
    print(args)
```

```python
func1(1, 2, 'a', 'b')
```

    1
    2
    ('a', 'b')

A few things to note:

1. Unlike iterable unpacking, **\*args** will be a **tuple**, not a list.

2. The name of the parameter **args** can be anything you prefer

3. You cannot specify positional arguments **after** the **\*args** parameter - this does something different that we'll cover in the next lecture.

```python
def func1(a, b, *my_vars):
    print(a)
    print(b)
    print(my_vars)
```

```python
func1(10, 20, 'a', 'b', 'c')
```

    10
    20
    ('a', 'b', 'c')

```python
def func1(a, b, *c, d):
    print(a)
    print(b)
    print(c)
    print(d)
```

```python
func1(10, 20, 'a', 'b', 100)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-18-50a3343cf093> in <module>()
    ----> 1 func1(10, 20, 'a', 'b', 100)
    

    TypeError: func1() missing 1 required keyword-only argument: 'd'

Let's see how we might use this to calculate the average of an arbitrary number of parameters.

```python
def avg(*args):
    count = len(args)
    total = sum(args)
    return total/count
```

```python
avg(2, 2, 4, 4)
```

    3.0

But watch what happens here:

```python
avg()
```

    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-21-867ab4243063> in <module>()
    ----> 1 avg()
    

    <ipython-input-19-03b621c670aa> in avg(*args)
          2     count = len(args)
          3     total = sum(args)
    ----> 4     return total/count
    

    ZeroDivisionError: division by zero

The problem is that we passed zero arguments.

We can fix this in one of two ways:

```python
def avg(*args):
    count = len(args)
    total = sum(args)
    if count == 0:
        return 0
    else:
        return total/count
```

```python
avg(2, 2, 4, 4)
```

    3.0

```python
avg()
```

    0

But we may not want to allow specifying zero arguments, in which case we can split our parameters into a required (non-defaulted) positional argument, and the rest:

```python
def avg(a, *args):
    count = len(args) + 1
    total = a + sum(args)
    return total/count
```

```python
avg(2, 2, 4, 4)
```

    3.0

```python
avg()
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-27-867ab4243063> in <module>()
    ----> 1 avg()
    

    TypeError: avg() missing 1 required positional argument: 'a'

As you can see, an exception occurs if we do not specify at least one argument.

##### Unpacking an iterable into positional arguments

```python
def func1(a, b, c):
    print(a)
    print(b)
    print(c)
```

```python
l = [10, 20, 30]
```

This will **not** work:

```python
func1(l)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-30-3255f48773bf> in <module>()
    ----> 1 func1(l)
    

    TypeError: func1() missing 2 required positional arguments: 'b' and 'c'

The function expects three positional arguments, but we only supplied a single one (albeit a list).

But we could unpack the list, and **then** pass it to as the function arguments:

```python
*l,
```

    (10, 20, 30)

```python
func1(*l)
```

    10
    20
    30

What about mixing positional and keyword arguments with this?

```python
def func1(a, b, c, *d):
    print(a)
    print(b)
    print(c)
    print(d)
```

```python
func1(10, c=20, b=10, 'a', 'b')
```

      File "<ipython-input-34-f5236a91cb18>", line 1
        func1(10, c=20, b=10, 'a', 'b')
                             ^
    SyntaxError: positional argument follows keyword argument

Recall that once a keyword argument is used in a function call, we **cannot** use positional arguments after that. 

However, in the next lecture we'll look at how to address this issue.

#### 05 - Keyword Arguments

Recall from iterable unpacking:

```python
a, b, *c = 10, 20, 'a', 'b'
```

```python
print(a, b)
```

    10 20

```python
print(c)
```

    ['a', 'b']

We can use a similar concept in function definitions to allow for arbitrary numbers of **positional** parameters/arguments:

```python
def func1(a, b, *args):
    print(a)
    print(b)
    print(args)
```

```python
func1(1, 2, 'a', 'b')
```

    1
    2
    ('a', 'b')

A few things to note:

1. Unlike iterable unpacking, **\*args** will be a **tuple**, not a list.

2. The name of the parameter **args** can be anything you prefer

3. You cannot specify positional arguments **after** the **\*args** parameter - this does something different that we'll cover in the next lecture.

```python
def func1(a, b, *my_vars):
    print(a)
    print(b)
    print(my_vars)
```

```python
func1(10, 20, 'a', 'b', 'c')
```

    10
    20
    ('a', 'b', 'c')

```python
def func1(a, b, *c, d):
    print(a)
    print(b)
    print(c)
    print(d)
```

```python
func1(10, 20, 'a', 'b', 100)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-18-50a3343cf093> in <module>()
    ----> 1 func1(10, 20, 'a', 'b', 100)
    

    TypeError: func1() missing 1 required keyword-only argument: 'd'


Let's see how we might use this to calculate the average of an arbitrary number of parameters.

```python
def avg(*args):
    count = len(args)
    total = sum(args)
    return total/count
```

```python
avg(2, 2, 4, 4)
```

    3.0

But watch what happens here:

```python
avg()
```

    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-21-867ab4243063> in <module>()
    ----> 1 avg()
    

    <ipython-input-19-03b621c670aa> in avg(*args)
          2     count = len(args)
          3     total = sum(args)
    ----> 4     return total/count
    
    ZeroDivisionError: division by zero

The problem is that we passed zero arguments.

We can fix this in one of two ways:

```python
def avg(*args):
    count = len(args)
    total = sum(args)
    if count == 0:
        return 0
    else:
        return total/count
```

```python
avg(2, 2, 4, 4)
```

    3.0

```python
avg()
```

    0

But we may not want to allow specifying zero arguments, in which case we can split our parameters into a required (non-defaulted) positional argument, and the rest:

```python
def avg(a, *args):
    count = len(args) + 1
    total = a + sum(args)
    return total/count
```

```python
avg(2, 2, 4, 4)
```

    3.0

```python
avg()
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-27-867ab4243063> in <module>()
    ----> 1 avg()
    

    TypeError: avg() missing 1 required positional argument: 'a'

As you can see, an exception occurs if we do not specify at least one argument.

##### Unpacking an iterable into positional arguments

```python
def func1(a, b, c):
    print(a)
    print(b)
    print(c)
```

```python
l = [10, 20, 30]
```

This will **not** work:

```python
func1(l)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-30-3255f48773bf> in <module>()
    ----> 1 func1(l)
    
    TypeError: func1() missing 2 required positional arguments: 'b' and 'c'

The function expects three positional arguments, but we only supplied a single one (albeit a list).

But we could unpack the list, and **then** pass it to as the function arguments:

```python
*l,
```

    (10, 20, 30)

```python
func1(*l)
```

    10
    20
    30

What about mixing positional and keyword arguments with this?

```python
def func1(a, b, c, *d):
    print(a)
    print(b)
    print(c)
    print(d)
```

```python
func1(10, c=20, b=10, 'a', 'b')
```

      File "<ipython-input-34-f5236a91cb18>", line 1
        func1(10, c=20, b=10, 'a', 'b')
                             ^
    SyntaxError: positional argument follows keyword argument

Recall that once a keyword argument is used in a function call, we **cannot** use positional arguments after that. 

However, in the next lecture we'll look at how to address this issue.

Recall: positional parameters defined in functions can also be passed as named (keyword) arguments.

```python
def func1(a, b, c):
    print(a, b, c)
```

```python
func1(10, 20, 30)
```

    10 20 30

```python
func1(b=20, c=30, a=10)
```

    10 20 30

```python
func1(10, c=30, b=20)
```

    10 20 30

Using a named argument is optional and up to the caller.

What if we wanted to force calls to our function to use named arguments?

We can do so by **exhausting** all the positional arguments, and then adding some additional parameters in teh function definition:

```python
def func1(a, b, *args, d):
    print(a, b, args, d)
```

Now we will need at least two positional arguments, an optional (possibly even zero) number of additional arguments, and this extra argument which is supposed to go into **d**. This argument can **only** be passed to the function using a named (keyword) argument:

So, this will not work:

```python
func1(10, 20, 'a', 'b', 100)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-6-50a3343cf093> in <module>()
    ----> 1 func1(10, 20, 'a', 'b', 100)
    

    TypeError: func1() missing 1 required keyword-only argument: 'd'

But this will:

```python
func1(10, 20, 'a', 'b', d=100)
```

As you can see, **d** took the keyword argument, while the remaining arguments were handled as positional parameters.

We can even define a function that has only optional positional arguments and mandatory keyword arguments:

```python
def func1(*args, d):
    print(args)
    print(d)
```

```python
func1(1, 2, 3, d='hello')
```

We can of course, not pass any positional arguments:

```python
func1(d='hello')
```

but the positional argument is mandatory (since no default was provided in the function definition):

```python
func1()
```

To make the keyword argument optional, we just need to specify a default value in the function definition:

```python
def func1(*args, d='n/a'):
    print(args)
    print(d)
```

```python
func1(1, 2, 3)
```

```python
func1()
```

Sometimes we want **only** keyword arguments, in which case we still have to exhaust the positional arguments first - but we can use the following syntax if we do not want any positional parameters passed in:

```python
def func1(*, d='hello'):
    print(d)
```

```python
func1(10, d='bye')
```

```python
func1(d='bye')
```

Of course, if we do not provide a default value for the keyword argument, then we effectively are forcing the caller to provide the keyword argument:

```python
def func1(*, a, b):
    print(a)
    print(b)
```

```python
func1(a=10, b=20)
```

but, the following would not work:

```python
func1(10, 20)
```

Unlike positional parameters, keyword arguments do not have to be defined with non-defaulted and then defaulted arguments:

```python
def func1(a, *, b='hello', c):
    print(a, b, c)
```

```python
func1(5, c='bye')
```

We can also include positional non-defaulted (first), positional defaulted (after positional non-defaulted) followed lastly (after exhausting positional arguments) by keyword args (defaulted or non-defaulted in any order)

```python
def func1(a, b=20, *args, d=0, e='n/a'):
    print(a, b, args, d, e)
```

```python
func1(5, 4, 3, 2, 1, d=0, e='all engines running')
```

```python
func1(0, 600, d='goooood morning', e='python!')
```

```python
func1(11, 'm/s', 24, 'mph', d='unladen', e='swallow')
```

As you can see, defining parameters and passing arguments is extremely flexible in Python! Even more so, when you account for the fact that the parameters are not statically typed!

In the next video, we'll look at one more thing we can do with function parameters!

#### 06 - \*\*kwargs

```python
def func(**kwargs):
    print(kwargs)
```

```python
func(x=100, y=200)
```

    {'x': 100, 'y': 200}

We can also use it in conjunction with **\*args**: 

```python
def func(*args, **kwargs):
    print(args)
    print(kwargs)
```

```python
func(1, 2, a=100, b=200)
```

    (1, 2)
    {'a': 100, 'b': 200}

Note: You cannot do the following:

```python
def func(*, **kwargs):
    print(kwargs)
```

      File "<ipython-input-9-330c63b7f22e>", line 1
        def func(*, **kwargs):
                   ^
    SyntaxError: named arguments must follow bare *

There is no need to even do this, since **\*\*kwargs** essentially indicates no more positional arguments.

```python
def func(a, b, **kwargs):
    print(a)
    print(b)
    print(kwargs)
```

```python
func(1, 2, x=100, y=200)
```

    1
    2
    {'x': 100, 'y': 200}

Also, you cannot specify parameters **after** **\*\*kwargs** has been used:

```python
def func(a, b, **kwargs, c):
    pass
```


      File "<ipython-input-12-ffdc3153243b>", line 1
        def func(a, b, **kwargs, c):
                                 ^
    SyntaxError: invalid syntax

If you want to specify both specific keyword-only arguments and **\*\*kwargs** you will need to first get to a point where you can define a keyword-only argument (i.e. exhaust the positional arguments, using either **\*args** or just **\***)

```python
def func(*, d, **kwargs):
    print(d)
    print(kwargs)
```

```python
func(d=1, x=100, y=200)
```

    1
    {'x': 100, 'y': 200}

#### 07 - Putting it all Together

Positionals Only: no extra positionals, no defaults (all positionals required)

```python
def func(a, b):
    print(a, b)
```

```python
func('hello', 'world')
```

    hello world

```python
func(b='world', a='hello')
```

    hello world

Positionals Only: no extra positionals, defaults (some positionals optional)

```python
def func(a, b='world', c=10):
    print(a, b, c)
```

```python
func('hello')
```

    hello world 10

```python
func('hello', c='!')
```

    hello world !

Positionals Only: extra positionals, no defaults (all positionals required)

```python
def func(a, b, *args):
    print(a, b, args)
```

```python
func(1, 2, 'x', 'y', 'z')
```

    1 2 ('x', 'y', 'z')

Note that we cannot call the function this way:

```python
func(b=2, a=1, 'x', 'y', 'z')
```

      File "<ipython-input-9-f1b0ffb3b67d>", line 1
        func(b=2, a=1, 'x', 'y', 'z')
                      ^
    SyntaxError: positional argument follows keyword argument

Keywords Only: no positionals, no defaults (all keyword args required)

```python
def func(*, a, b):
    print(a, b)
```

```python
func(a=1, b=2)
```

    1 2

Keywords Only: no positionals, some defaults (not all keyword args required)

```python
def func(*, a=1, b):
    print(a, b)
```

```python
func(a=10, b=20)
```

    10 20

```python
func(b=2)
```

    1 2

Keywords and Positionals: some positionals (no defaults), keywords (no defaults)

```python
def func(a, b, *, c, d):
    print(a, b, c, d)
```

```python
func(1, 2, c=3, d=4)
```

    1 2 3 4

```python
func(1, 2, d=4, c=3)
```

    1 2 3 4

```python
func(1, c=3, d=4, b=2)
```

    1 2 3 4

Keywords and Positionals: some positional defaults

```python
def func(a, b=2, *, c, d=4):
    print(a, b, c, d)
```

```python
func(1, c=3)
```

    1 2 3 4

```python
func(c=3, a=1)
```

    1 2 3 4

```python
func(1, 2, c=3, d=4)
```

    1 2 3 4

```python
func(c=3, a=1, b=2, d=4)
```

    1 2 3 4

Keywords and Positionals: extra positionals

```python
def func(a, b=2, *args, c=3, d):
    print(a, b, args, c, d)
```

```python
func(1, 2, 'x', 'y', 'z', c=3, d=4)
```

    1 2 ('x', 'y', 'z') 3 4

Note that if we are going to use the extra arguments, then we cannot actually use a default value for b:

```python
func(1, 'x', 'y', 'z', c=3, d=4)
```

    1 x ('y', 'z') 3 4

as you can see, **b** was assigned the value **x**

Keywords and Positionals: no extra positionals, extra keywords

```python
def func(a, b, *, c, d=4, **kwargs):
    print(a, b, c, d, kwargs)
```

```python
func(1, 2, c=3, x=100, y=200, z=300)
```

    1 2 3 4 {'x': 100, 'y': 200, 'z': 300}

```python
func(x=100, y=200, z=300, c=3, b=2, a=1)
```

    1 2 3 4 {'x': 100, 'y': 200, 'z': 300}

Keywords and Positionals: extra positionals, extra keywords

```python
def func(a, b, *args, c, d=4, **kwargs):
    print(a, b, args, c, d, kwargs)
```

```python
func(1, 2, 'x', 'y', 'z', c=3, d=5, x=100, y=200, z=300)
```

    1 2 ('x', 'y', 'z') 3 5 {'x': 100, 'y': 200, 'z': 300}

Keywords and Positionals: only extra positionals and extra keywords

```python
def func(*args, **kwargs):
    print(args, kwargs)
```

```python
func(1, 2, 3, x=100, y=200, z=300)
```

    (1, 2, 3) {'x': 100, 'y': 200, 'z': 300}

##### The Print Function

```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    
```python
print(1, 2, 3)
```

    1 2 3

```python
print(1, 2, 3, sep='--')
```

    1--2--3

```python
print(1, 2, 3, end='***\n')
```

    1 2 3***

```python
print(1, 2, 3, sep='\t', end='\t***\t')
print(4, 5, 6, sep='\t', end='\t***\n')
```

    1	2	3	***	4	5	6	***

##### Another Use Case

```python
def calc_hi_lo_avg(*args, log_to_console=False):
    hi = int(bool(args)) and max(args)
    lo = int(bool(args)) and min(args)
    avg = (hi + lo)/2
    if log_to_console:
        print("high={0}, low={1}, avg={2}".format(hi, lo, avg))
    return avg
```

```python
avg = calc_hi_lo_avg(1, 2, 3, 4, 5)
print(avg)
```

    3.0

```python
avg = calc_hi_lo_avg(1, 2, 3, 4, 5, log_to_console=True)
print(avg)
```

    high=5, low=1, avg=3.0
    3.0

#### 08 - Simple Function Timer

We want to create a simple function that can time how fast a function runs.

We want this function to be generic in the sense that it can be used to time any function (along with it's positional and keyword arguments), as well as specifying the number of the times the function should be timed, and the returns the average of the timings.

We'll call our function **time_it**, and it will need to have the following parameters:

* the function we want to time
* the positional arguments of the function we want to time (if any)
* the keyword-only arguments of the function we want to time (if any)
* the number of times we want to run this function

```python
import time
```

```python
def time_it(fn, *args, rep=5, **kwargs):
    print(args, rep, kwargs)
```

Now we could the function this way:

```python
time_it(print, 1, 2, 3, sep='-')
```

    (1, 2, 3) 5 {'sep': '-'}

Let's modify our function to actually run the print function with any positional and keyword args (except for rep) passed to it:

```python
def time_it(fn, *args, rep=5, **kwargs):
    for i in range(rep):
        fn(*args, **kwargs)
```

```python
time_it(print, 1, 2, 3, sep='-')
```

    1-2-3
    1-2-3
    1-2-3
    1-2-3
    1-2-3

As you can see **1, 2, 3** was passed to the **print** function's positional parameters, and the keyword_only arg **sep** was also passed to it. 

We can even add more arguments:

```python
time_it(print, 1, 2, 3, sep='-', end=' *** ', rep=3)
```

    1-2-3 *** 1-2-3 *** 1-2-3 *** 

Now all that's really left for us to do is to time the function and return the average time:

```python
def time_it(fn, *args, rep=5, **kwargs):
    start = time.perf_counter()
    for i in range(rep):
        fn(*args, **kwargs)
    end = time.perf_counter()
    return (end - start) / rep
```

Let's write a few functions we might want to time:

We'll create three functions that all do the same thing: calculate powers of n**k for k in some range of integer values

```python
def compute_powers_1(n, *, start=1, end):
    # using a for loop
    results = []
    for i in range(start, end):
        results.append(n**i)
    return results
```

```python
def compute_powers_2(n, *, start=1, end):
    # using a list comprehension
    return [n**i for i in range(start, end)]
```

```python
def compute_powers_3(n, *, start=1, end):
    # using a generator expression
    return (n**i for i in range(start, end))
```

Let's run these functions and see the results:

```python
compute_powers_1(2, end=5)
```

    [2, 4, 8, 16]

```python
compute_powers_2(2, end=5)
```

    [2, 4, 8, 16]

```python
list(compute_powers_3(2, end=5))
```

    [2, 4, 8, 16]

Finally let's run these functions through our **time_it** function and see the results:

```python
time_it(compute_powers_1, n=2, end=20000, rep=4)
```

    2.5798198230283234

```python
time_it(compute_powers_2, 2, end=20000, rep=4)
```

    2.3151767636341347

```python
time_it(compute_powers_3, 2, end=20000, rep=4)
```

    3.0854032573301993e-06

Although the **compute_powers_3** function appears to be **much** faster than the other two, it doesn't quite do the same thing! 

We'll cover generators in detail later in this course.

#### 09 - Parameter Defaults - Beware

```python
from datetime import datetime
```

```python
print(datetime.utcnow())
```

    2017-08-22 04:04:17.700303

```python
def log(msg, *, dt=datetime.utcnow()):
    print('{0}: {1}'.format(dt, msg))
```

```python
log('message 1')
```

    2017-08-22 04:04:18.406943: message 1

```python
log('message 2', dt='2001-01-01 00:00:00')
```

    2001-01-01 00:00:00: message 2

```python
log('message 3')
```

    2017-08-22 04:04:18.406943: message 3

```python
log('message 4')
```

    2017-08-22 04:04:18.406943: message 4

As you can see, the default for **dt** is calculated when the function is **defined** and is **NOT** re-evaluated when the function is called.

##### Solution Pattern

Here is one pattern we can use to achieve the desired result:

We actually set the default to None - this makes the argument optional, and we can then test for None **inside** the function and default to the current time if it is None.

```python
def log(msg, *, dt=None):
    dt = dt or datetime.utcnow()
    # above is equivalent to:
    #if not dt:
    #    dt = datetime.utcnow()
    print('{0}: {1}'.format(dt, msg))    
```

```python
log('message 1')
```

    2017-08-22 04:15:11.797640: message 1

```python
log('message 2')
```

    2017-08-22 04:15:14.529496: message 2

```python
log('message 3', dt='2001-01-01 00:00:00')
```

    2001-01-01 00:00:00: message 3

```python
log('message 4')
```

    2017-08-22 04:15:18.045607: message 4

#### 10 - Parameter Defaults - Beware Again

Another gotcha with parameter defaults comes with mutable types, and is an easy trap to fall into.

Again, you have to remember that function parameter defaults are evaluated once, when the function is defined (i.e. when the module is loaded, or in this Jupyter notebook, when we "execute" the function definition), and not every time the function is called.

Consider the following scenario.

We are creating a grocery list, and we want our list to contain consistently formatted data with name, quantity and measurement unit:

``
bananas (2 units)
grapes (1 bunch)
milk (1 liter)
python (1 medium-rare)
``

To make sure the data is consistent, we want to use a function that we can call to add the item to our list.

So we'll need to provide it our current grocery list as well as the item information to be added:

```python
def add_item(name, quantity, unit, grocery_list):
    item_fmt = "{0} ({1} {2})".format(name, quantity, unit)
    grocery_list.append(item_fmt)
    return grocery_list
```

We have two stores we want to visit, so we set up two grocery lists:

```python
store_1 = []
store_2 = []
```

```python
add_item('bananas', 2, 'units', store_1)
add_item('grapes', 1, 'bunch', store_1)
add_item('python', 1, 'medium-rare', store_2)
```

    ['python (1 medium-rare)']

```python
store_1
```

    ['bananas (2 units)', 'grapes (1 bunch)']

```python
store_2
```

    ['python (1 medium-rare)']

Ok, working great. But let's make the function a little easier to use - if the user does not supply an existing grocery list to append the item to, let's just go ahead and default our `grocery_list` to an empty list hence starting a new shopping list:

```python
def add_item(name, quantity, unit, grocery_list=[]):
    item_fmt = "{0} ({1} {2})".format(name, quantity, unit)
    grocery_list.append(item_fmt)
    return grocery_list
```

```python
store_1 = add_item('bananas', 2, 'units')
add_item('grapes', 1, 'bunch', store_1)
```

    ['bananas (2 units)', 'grapes (1 bunch)']

```python
store_1
```

    ['bananas (2 units)', 'grapes (1 bunch)']

OK, so that seems to be working as expected.

Let's start our second list:

```python
store_2 = add_item('milk', 1, 'gallon')
```

```python
print(store_2)
```

    ['bananas (2 units)', 'grapes (1 bunch)', 'milk (1 gallon)']

??? What's going on? Our second list somehow contains the items that are in the first list.

What happened is that the returned value in the first call we made was the default grocery list - but remember that the list was created once and for all when the function was **created** not called. So everytime we call the function, that is the **same** list being used as the default. 

When we started out first list, we were adding item to that default list.

When we started our second list, we were adding items to the **same** default list (since it is the same object).

We can avoid this problem using the same pattern as in the previous example we had with the default date time value. We use None as a default value instead, and generate a new empty list (hence starting a new list) if none was provided.

```python
def add_item(name, quantity, unit, grocery_list=None):
    if not grocery_list:
        grocery_list = []
    item_fmt = "{0} ({1} {2})".format(name, quantity, unit)
    grocery_list.append(item_fmt)
    return grocery_list
```

```python
store_1 = add_item('bananas', 2, 'units')
add_item('grapes', 1, 'bunch', store_1)
```

    ['bananas (2 units)', 'grapes (1 bunch)']

```python
store_2 = add_item('milk', 1, 'gallon')
store_2
```

    ['milk (1 gallon)']

Issue resolved!

However, there are legitimate use cases (well, almost legitimate, often we're better off using a different approach that we'll see when we look at closures), but here's a simple one.

We want our function to cache results, so that we don't recalculate something more than once.

Let's say we have a factorial function, that can be defined recursively as:

`n! = n * (n-1)!`

```python
def factorial(n):
    if n < 1:
        return 1
    else:
        print('calculating {0}!'.format(n))
        return n * factorial(n-1)
```

```python
factorial(3)
```

    calculating 3!
    calculating 2!
    calculating 1!

    6

```python
factorial(3)
```

    calculating 3!
    calculating 2!
    calculating 1!

    6

As you can see we had to recalculate all those factorials the second time around.

Let's cache the results leveraging what we saw in the previous example:

```python
def factorial(n, cache={}):
    if n < 1:
        return 1
    elif n in cache:
        return cache[n]
    else:
        print('calculating {0}!'.format(n))
        result = n * factorial(n-1)
        cache[n] = result
        return result
```

```python
factorial(3)
```

    calculating 3!
    calculating 2!
    calculating 1!

    6

```python
factorial(3)
```

    6

Now as you can see, the second time around we did not have to recalculate all the factorials. In fact, to calculate higher factorials, you'll notice that we don't need to re-run *all* the recursive calls:

```python
factorial(5)
```

    calculating 5!
    calculating 4!

    120

`5!` and `4!` was calculated since they weren't cached, but since `3!` was already cached we didn't have to recalculate it - it was a quick lookup instead.

This technique is something called memoization, and we'll come back to it in much more detail when we discuss closures and decorators.

### 6. First-Class Functions

#### 01 - Docstrings and Annotation

##### Docstrings

When we call **help()** on a class, function, module, etc, Python will typically display some information:

```python
help(print)
```

    Help on built-in function print in module builtins:
    
    print(...)
        print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
        
        Prints the values to a stream, or to sys.stdout by default.
        Optional keyword arguments:
        file:  a file-like object (stream); defaults to the current sys.stdout.
        sep:   string inserted between values, default a space.
        end:   string appended after the last value, default a newline.
        flush: whether to forcibly flush the stream.
    
We can define such help using docstrings and annotations.

```python
def my_func(a, b):
    return a*b
```

```python
help(my_func)
```

    Help on function my_func in module __main__:
    
    my_func(a, b)
    
Pretty bare! So let's add some additional help:

```python
def my_func(a, b):
    'Returns the product of a and b'
    return a*b
```

```python
help(my_func)
```

    Help on function my_func in module __main__:
    
    my_func(a, b)
        Returns the product of a and b
    
Docstrings can span multiple lines using a multi-line string literal:

```python
def fact(n):
    '''Calculates n! (factorial function)
    
    Inputs:
        n: non-negative integer
    Returns:
        the factorial of n
    '''
    
    if n < 0:
        '''Note that this is not part of the docstring!'''
        return 1
    else:
        return n * fact(n-1)
    
    
```

```python
help(fact)
```

    Help on function fact in module __main__:
    
    fact(n)
        Calculates n! (factorial function)
        
        Inputs:
            n: non-negative integer
        Returns:
            the factorial of n
    
Docstrings, when found, are simply attached to the function in the `__doc__` property:

```python
fact.__doc__
```

    'Calculates n! (factorial function)\n    \n    Inputs:\n        n: non-negative integer\n    Returns:\n        the factorial of n\n    '

And the Python **help()** function simply returns the contents of `__doc__`

##### Annotations

We can also add metadata annotations to a function's parameters and return. These metadata annotations can be any **expression** (string, type, function call, etc)

```python
def my_func(a:'annotation for a', 
            b:'annotation for b')->'annotation for return':
    
    return a*b
```

```python
help(my_func)
```

    Help on function my_func in module __main__:
    
    my_func(a:'annotation for a', b:'annotation for b') -> 'annotation for return'
    
The annotations can be any expression, not just strings:

```python
x = 3
y = 5
def my_func(a: str) -> 'a repeated ' + str(max(3, 5)) + ' times':
	return a*max(x, y)
```

```python
help(my_func)
```

    Help on function my_func in module __main__:
    
    my_func(a:str) -> 'a repeated 5 times'
    
Note that these annotations do **not** force a type on the parameters or the return value - they are simply there for documentation purposes within Python and **may** be used by external applications and modules, such as IDE's.

Just like docstrings are stored in the `__doc__` property, annotations are stored in the `__annotations__` property - a dictionary whose keys are the parameter names, and values are the annotation.

```python
my_func.__annotations__
```

    {'a': str, 'return': 'a repeated 5 times'}

Of course we can combine both docstrings and annotations:

```python
def fact(n: 'int >= 0')->int:
    '''Calculates n! (factorial function)
    
    Inputs:
        n: non-negative integer
    Returns:
        the factorial of n
    '''
    
    if n < 0:
        '''Note that this is not part of the docstring!'''
        return 1
    else:
        return n * fact(n-1)
```

```python
help(fact)
```

    Help on function fact in module __main__:
    
    fact(n:'int >= 0') -> int
        Calculates n! (factorial function)
        
        Inputs:
            n: non-negative integer
        Returns:
            the factorial of n
    
Annotations will work with default parameters too: just specify the default **after** the annotation:

```python
def my_func(a:str='a', b:int=1)->str:
    return a*b
```

```python
help(my_func)
```

    Help on function my_func in module __main__:
    
    my_func(a:str='a', b:int=1) -> str

```python
my_func()
```

    'a'

```python
my_func('abc', 3)
```

    'abcabcabc'

```python
def my_func(a:int=0, *args:'additional args'):
    print(a, args)
```

```python
my_func.__annotations__
```

    {'a': int, 'args': 'additional args'}

```python
help(my_func)
```

    Help on function my_func in module __main__:
    
    my_func(a:int=0, *args:'additional args')
    
#### 02 - Lambda Expressions

```python
lambda x: x**2
```

    <function __main__.<lambda>>

As you can see, the above expression just created a function.

##### Assigning to a Variable

```python
func = lambda x: x**2
```

```python
type(func)
```

    function

```python
func(3)
```

    9

We can specify arguments for lambdas just like we would for any function created using **def**, except for annotations:

```python
func_1 = lambda x, y=10: (x, y)
```

```python
func_1(1, 2)
```

    (1, 2)

```python
func_1(1)
```

    (1, 10)

We can even use \* and \*\*:

```python
func_2 = lambda x, *args, y, **kwargs: (x, *args, y, {**kwargs})
```

```python
func_2(1, 'a', 'b', y=100, a=10, b=20)
```

    (1, 'a', 'b', 100, {'a': 10, 'b': 20})

##### Passing as an Argument

Lambdas are functions, and can therefore be passed to any other function as an argument (or returned from another function)

```python
def apply_func(x, fn):
    return fn(x)
```

```python
apply_func(3, lambda x: x**2)
```

    9

```python
apply_func(3, lambda x: x**3)
```

    27

Of course we can make this even more generic:

```python
def apply_func(fn, *args, **kwargs):
    return fn(*args, **kwargs)
```

```python
apply_func(lambda x, y: x+y, 1, 2)
```

    3

```python
apply_func(lambda x, *, y: x+y, 1, y=2)
```

    3

```python
apply_func(lambda *args: sum(args), 1, 2, 3, 4, 5)
```

    15

Of course in the example above, we really did not need to create a lambda!

```python
apply_func(sum, (1, 2, 3, 4, 5))
```

    15

Of course, we don't have to use lambdas when calling **apply_func**, we can also pass in a function defined using a **def** statement:

```python
def multiply(x, y):
    return x * y
```

```python
apply_func(multiply, 'a', 5)
```

    'aaaaa'

```python
apply_func(lambda x, y: x*y, 'a', 5)
```

    'aaaaa'

#### 03 - Lambdas and Sorting

Python has a built-in **sorted** method that can be used to sort any iterable. It will use the default ordering of the particular items, but sometimes you may want to (or need to) specify a different criteria for sorting.

Let's start with a simple list:

```python
l = ['a', 'B', 'c', 'D']
```

```python
sorted(l)
```

    ['B', 'D', 'a', 'c']

As you can see there is a difference between upper and lower-case characters when sorting strings.

What if we wanted to make a case-insensitive sort?

Python's **sorted** function has a keyword-only argument that allows us to modify the values that are used to sort the list.

```python
sorted(l, key=str.upper)
```

    ['a', 'B', 'c', 'D']

We could have used a lambda here (but you should not, this is just to illustrate using a lambda in this case):

```python
sorted(l, key = lambda s: s.upper())
```

    ['a', 'B', 'c', 'D']

Let's look at how we might create a sorted list from a dictionary:

```python
d = {'def': 300, 'abc': 200, 'ghi': 100}
```

```python
d
```

    {'abc': 200, 'def': 300, 'ghi': 100}

```python
sorted(d)
```

    ['abc', 'def', 'ghi']

What happened here? 

Remember that iterating dictionaries actually iterates the keys - so we ended up with tyhe keys sorted alphabetically.

What if we want to return the keys sorted by their associated value instead?

```python
sorted(d, key=lambda k: d[k])
```

    ['ghi', 'abc', 'def']

Maybe we want to sort complex numbers based on their distance from the origin:

```python
def dist(x):
    return (x.real)**2 + (x.imag)**2
```

```python
l = [3+3j, 1+1j, 0]
```

Trying to sort this list directly won't work since Python does not have an ordering defined for complex numbers:

```python
sorted(l)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-11-5ed0ddfda5a6> in <module>()
    ----> 1 sorted(l)
    

    TypeError: '<' not supported between instances of 'complex' and 'complex'

Instead, let's try to specify the key using the distance:

```python
sorted(l, key=dist)
```

    [0, (1+1j), (3+3j)]

Of course, if we're only going to use the **dist** function once, we can just do the same thing this way:

```python
sorted(l, key=lambda x: (x.real)**2 + (x.imag)**2)
```

    [0, (1+1j), (3+3j)]

And here's another example where we want to sort a list of strings based on the **last character** of the string:

```python
l = ['Cleese', 'Idle', 'Palin', 'Chapman', 'Gilliam', 'Jones']
```

```python
sorted(l)
```

    ['Chapman', 'Cleese', 'Gilliam', 'Idle', 'Jones', 'Palin']

```python
sorted(l, key=lambda s: s[-1])
```

    ['Cleese', 'Idle', 'Gilliam', 'Palin', 'Chapman', 'Jones']

#### 04 - Challenge - Randomizing using Sorted

```python
import random
```

```python
help(random.random)
```

    Help on built-in function random:
    
    random(...) method of random.Random instance
        random() -> x in the interval [0, 1).
    
```python
random.random()
```

    0.8655691916467607

```python
l = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

```python
sorted(l, key=lambda x: random.random())
```

    [5, 7, 2, 1, 3, 10, 9, 6, 8, 4]

Of course, this works for any iterable:

```python
sorted('abcdefg', key = lambda x: random.random())
```

    ['b', 'd', 'g', 'e', 'a', 'c', 'f']

And to get a string back instead of just a list:

```python
''.join(sorted('abcdefg', key = lambda x: random.random()))
```

    'adfegbc'

#### 05 - Function Introspection

```python
def fact(n: "some non-negative integer") -> "n! or 0 if n < 0":
    """Calculates the factorial of a non-negative integer n
    
    If n is negative, returns 0.
    """
    if n < 0:
        return 0
    elif n <= 1:
        return 1
    else:
        return n * fact(n-1)
```

Since functions are objects, we can add attributes to a function:

```python
fact.short_description = "factorial function"
```

```python
print(fact.short_description)
```

    factorial function

We can see all the attributes that belong to a function using the **dir** function:

```python
dir(fact)
```

    ['__annotations__',
     '__call__',
     '__class__',
     '__closure__',
     '__code__',
     '__defaults__',
     '__delattr__',
     '__dict__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__get__',
     '__getattribute__',
     '__globals__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__kwdefaults__',
     '__le__',
     '__lt__',
     '__module__',
     '__name__',
     '__ne__',
     '__new__',
     '__qualname__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'short_description']

We can see our **short_description** attribute, as well as some attributes we have seen before: **__annotations__** and **__doc__**:

```python
fact.__doc__
```

    'Calculates the factorial of a non-negative integer n\n    \n    If n is negative, returns 0.\n    '

```python
fact.__annotations__
```

    {'n': 'some non-negative integer', 'return': 'n! or 0 if n < 0'}

We'll revisit some of these attributes later in this course, but let's take a look at a few here:

```python
def my_func(a, b=2, c=3, *, kw1, kw2=2, **kwargs):
    pass
```

Let's assign my_func to another variable:

```python
f = my_func
```

The **__name__** attribute holds the function's name:

```python
my_func.__name__
```

    'my_func'

```python
f.__name__
```

    'my_func'

The **__defaults__** attribute is a tuple containing any positional parameter defaults:

```python
my_func.__defaults__
```

    (2, 3)

```python
my_func.__kwdefaults__
```

    {'kw2': 2}

Let's create a function with some local variables:

```python
def my_func(a, b=1, *args, **kwargs):
    i = 10
    b = min(i, b)
    return a * b
```

```python
my_func('a', 100)
```

    'aaaaaaaaaa'

The **__code__** attribute contains a **code** object:

```python
my_func.__code__
```

    <code object my_func at 0x0000016640E71300, file "<ipython-input-13-785cf1a800f4>", line 1>

This **code** object itself has various properties:

```python
dir(my_func.__code__)
```

    ['__class__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__le__',
     '__lt__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'co_argcount',
     'co_cellvars',
     'co_code',
     'co_consts',
     'co_filename',
     'co_firstlineno',
     'co_flags',
     'co_freevars',
     'co_kwonlyargcount',
     'co_lnotab',
     'co_name',
     'co_names',
     'co_nlocals',
     'co_stacksize',
     'co_varnames']

Attribute **__co_varnames__** is a tuple containing the parameter names and local variables:

```python
my_func.__code__.co_varnames
```

    ('a', 'b', 'args', 'kwargs', 'i')

Attribute **co_argcount** returns the number of arguments (minus any \* and \*\* args)

```python
my_func.__code__.co_argcount
```

    2

##### The **inspect** module

It is much easier to use the **inspect** module!

```python
import inspect
```

```python
inspect.isfunction(my_func)
```

    True

By the way, there is a difference between a function and a method! A method is a function that is bound to some object:

```python
inspect.ismethod(my_func)
```

    False

```python
class MyClass:
    def f_instance(self):
        pass
    
    @classmethod
    def f_class(cls):
        pass
    
    @staticmethod
    def f_static():
        pass
```

**Instance methods** are bound to the **instance** of a class (not the class itself)

**Class methods** are bound to the **class**, not instances

**Static methods** are no bound either to the class or its instances

```python
inspect.isfunction(MyClass.f_instance), inspect.ismethod(MyClass.f_instance)
```

    (True, False)

```python
inspect.isfunction(MyClass.f_class), inspect.ismethod(MyClass.f_class)
```

    (False, True)

```python
inspect.isfunction(MyClass.f_static), inspect.ismethod(MyClass.f_static)
```

    (True, False)

```python
my_obj = MyClass()
```

```python
inspect.isfunction(my_obj.f_instance), inspect.ismethod(my_obj.f_instance)
```

    (False, True)

```python
inspect.isfunction(my_obj.f_class), inspect.ismethod(my_obj.f_class)
```

    (False, True)

```python
inspect.isfunction(my_obj.f_static), inspect.ismethod(my_obj.f_static)
```

    (True, False)

If you just want to know if something is a function or method:

```python
inspect.isroutine(my_func)
```

    True

```python
inspect.isroutine(MyClass.f_instance)
```

    True

```python
inspect.isroutine(my_obj.f_class)
```

    True

```python
inspect.isroutine(my_obj.f_static)
```

    True

We'll revisit this in more detail in section on OOP.

##### Introspecting Callable Code

We can get back the source code of our function using the **getsource()** method:

```python
inspect.getsource(fact)
```

    'def fact(n: "some non-negative integer") -> "n! or 0 if n < 0":\n    """Calculates the factorial of a non-negative integer n\n    \n    If n is negative, returns 0.\n    """\n    if n <= 1:\n        return 1\n    else:\n        return n * fact(n-1)\n'

```python
print(inspect.getsource(fact))
```

    def fact(n: "some non-negative integer") -> "n! or 0 if n < 0":
        """Calculates the factorial of a non-negative integer n
        
        If n is negative, returns 0.
        """
        if n <= 1:
            return 1
        else:
            return n * fact(n-1)
    
```python
inspect.getsource(MyClass.f_instance)
```

    '    def f_instance(self):\n        pass\n'

```python
inspect.getsource(my_obj.f_instance)
```

    '    def f_instance(self):\n        pass\n'

We can also find out where the function was defined:

```python
inspect.getmodule(fact)
```

    <module '__main__'>

```python
inspect.getmodule(print)
```

    <module 'builtins' (built-in)>

```python
import math
```

```python
inspect.getmodule(math.sin)
```

    <module 'math' (built-in)>

```python
# setting up variable
i = 10

# comment line 1
# comment line 2
def my_func(a, b=1):
    # comment inside my_func
    pass
```

```python
inspect.getcomments(my_func)
```

    '# comment line 1\n# comment line 2\n'

```python
print(inspect.getcomments(my_func))
```

    # comment line 1
    # comment line 2
    
##### Introspecting Callable Signatures

```python
# TODO: Provide implementation
def my_func(a: 'a string', 
            b: int = 1, 
            *args: 'additional positional args', 
            kw1: 'first keyword-only arg', 
            kw2: 'second keyword-only arg' = 10,
            **kwargs: 'additional keyword-only args') -> str:
    """does something
       or other"""
    pass
```

```python
inspect.signature(my_func)
```

    <Signature (a:'a string', b:int=1, *args:'additional positional args', kw1:'first keyword-only arg', kw2:'second keyword-only arg'=10, **kwargs:'additional keyword-only args') -> str>

```python
type(inspect.signature(my_func))
```

    inspect.Signature

```python
sig = inspect.signature(my_func)
```

```python
dir(sig)
```

    ['__class__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__le__',
     '__lt__',
     '__module__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__setattr__',
     '__setstate__',
     '__sizeof__',
     '__slots__',
     '__str__',
     '__subclasshook__',
     '_bind',
     '_bound_arguments_cls',
     '_hash_basis',
     '_parameter_cls',
     '_parameters',
     '_return_annotation',
     'bind',
     'bind_partial',
     'empty',
     'from_builtin',
     'from_callable',
     'from_function',
     'parameters',
     'replace',
     'return_annotation']

```python
for param_name, param in sig.parameters.items():
    print(param_name, param)
```

    a a:'a string'
    b b:int=1
    args *args:'additional positional args'
    kw1 kw1:'first keyword-only arg'
    kw2 kw2:'second keyword-only arg'=10
    kwargs **kwargs:'additional keyword-only args'

```python
def print_info(f: "callable") -> None:
    print(f.__name__)
    print('=' * len(f.__name__), end='\n\n')
    
    print('{0}\n{1}\n'.format(inspect.getcomments(f), 
                              inspect.cleandoc(f.__doc__)))
    
    print('{0}\n{1}'.format('Inputs', '-'*len('Inputs')))
    
    sig = inspect.signature(f)
    for param in sig.parameters.values():
        print('Name:', param.name)
        print('Default:', param.default)
        print('Annotation:', param.annotation)
        print('Kind:', param.kind)
        print('--------------------------\n')
        
    print('{0}\n{1}'.format('\n\nOutput', '-'*len('Output')))
    print(sig.return_annotation)
```

```python
print_info(my_func)
```

    my_func
    =======
    
    # TODO: Provide implementation
    
    does something
    or other
    
    Inputs
    ------
    Name: a
    Default: <class 'inspect._empty'>
    Annotation: a string
    Kind: POSITIONAL_OR_KEYWORD
    --------------------------
    
    Name: b
    Default: 1
    Annotation: <class 'int'>
    Kind: POSITIONAL_OR_KEYWORD
    --------------------------
    
    Name: args
    Default: <class 'inspect._empty'>
    Annotation: additional positional args
    Kind: VAR_POSITIONAL
    --------------------------
    
    Name: kw1
    Default: <class 'inspect._empty'>
    Annotation: first keyword-only arg
    Kind: KEYWORD_ONLY
    --------------------------
    
    Name: kw2
    Default: 10
    Annotation: second keyword-only arg
    Kind: KEYWORD_ONLY
    --------------------------
    
    Name: kwargs
    Default: <class 'inspect._empty'>
    Annotation: additional keyword-only args
    Kind: VAR_KEYWORD
    -------------------------- 
    
    Output
    ------
    <class 'str'>

##### A Side Note on Positional Only Arguments

Some built-in callables have arguments that are positional only (i.e. cannot be specified using a keyword).

However, Python does not currently have any syntax that allows us to define callables with positional only arguments.

In general, the documentation uses a **/** character to indicate that all preceding arguments are positional-only. But not always :-(

```python
help(divmod)
```

    Help on built-in function divmod in module builtins:
    
    divmod(x, y, /)
        Return the tuple (x//y, x%y).  Invariant: div*y + mod == x.
    
Here we see that the **divmod** function takes two positional-only parameters:

```python
divmod(10, 3)
```

    (3, 1)

```python
divmod(x=10, y=3)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-55-c637b01eef33> in <module>()
    ----> 1 divmod(x=10, y=3)
    

    TypeError: divmod() takes no keyword arguments

Similarly, the string **replace** function also takes positional-only arguments, however, the documentation does not indicate this!

```python
help(str.replace)
```

    Help on method_descriptor:
    
    replace(...)
        S.replace(old, new[, count]) -> str
        
        Return a copy of S with all occurrences of substring
        old replaced by new.  If the optional argument count is
        given, only the first count occurrences are replaced.
    
```python
'abcdefg'.replace('abc', 'xyz')
```

    'xyzdefg'

```python
'abcdefg'.replace(old='abc', new='xyz')
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-58-9d61ac657cae> in <module>()
    ----> 1 'abcdefg'.replace(old='abc', new='xyz')
    

    TypeError: replace() takes no keyword arguments

#### 06 - Callables

A callable is an object that can be called (using the **()** operator), and always returns a value.

We can check if an object is callable by using the built-in function **callable**

##### Functions and Methods are callable

```python
callable(print)
```

    True

```python
callable(len)
```

    True

```python
l = [1, 2, 3]
callable(l.append)
```

    True

```python
s = 'abc'
callable(s.upper)
```

    True

##### Callables **always** return a value:

```python
result = print('hello')
print(result)
```

    hello
    None

```python
l = [1, 2, 3]
result = l.append(4)
print(result)
print(l)
```

    None
    [1, 2, 3, 4]

```python
s = 'abc'
result = s.upper()
print(result)
```

    ABC

##### Classes are callable:

```python
from decimal import Decimal
```

```python
callable(Decimal)
```

    True

```python
result = Decimal('10.5')
print(result)
```

    10.5

##### Class instances may be callable:

```python
class MyClass:
    def __init__(self):
        print('initializing...')
        self.counter = 0
    
    def __call__(self, x=1):
        self.counter += x
        print(self.counter)
```

```python
my_obj = MyClass()
```

    initializing...

```python
callable(my_obj.__init__)
```

    True

```python
callable(my_obj.__call__)
```

    True

```python
my_obj()
```

    1

```python
my_obj()
```

    2

```python
my_obj(10)
```

    12

#### 07 - Map, Filter, Zip and List Comprehensions

**Definition**: A function that takes a function as an argument, and/or returns a function as its return value

For example, the **sorted** function is a higher-order function as we saw in an earlier video.

##### Map

The **map** built-in function is a higher-order function that applies a function to an iterable type object:

```python
help(map)
```

    Help on class map in module builtins:
    
    class map(object)
     |  map(func, *iterables) --> map object
     |  
     |  Make an iterator that computes the function using arguments from
     |  each of the iterables.  Stops when the shortest iterable is exhausted.
     |  
     |  Methods defined here:
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __next__(self, /)
     |      Implement next(self).
     |  
     |  __reduce__(...)
     |      Return state information for pickling.
    
```python
def fact(n):
    return 1 if n < 2 else n * fact(n-1)
```

```python
fact(3)
```

    6

```python
fact(4)
```

    24

```python
map(fact, [1, 2, 3, 4, 5])
```

    <map at 0x23b123a3978>

The **map** function returns a **map** object, which is an **iterable** - we can either convert that to a list or enumerate it:

```python
l = list(map(fact, [1, 2, 3, 4, 5]))
print(l)
```

    [1, 2, 6, 24, 120]

We can also use it this way:

```python
l1 = [1, 2, 3, 4, 5]
l2 = [10, 20, 30, 40, 50]

f = lambda x, y: x+y

m = map(f, l1, l2)
list(m)
```

    [11, 22, 33, 44, 55]

##### Filter

```python
help(filter)
```

    Help on class filter in module builtins:
    
    class filter(object)
     |  filter(function or None, iterable) --> filter object
     |  
     |  Return an iterator yielding those items of iterable for which function(item)
     |  is true. If function is None, return the items that are true.
     |  
     |  Methods defined here:
     |  
     |  __getattribute__(self, name, /)
     |      Return getattr(self, name).
     |  
     |  __iter__(self, /)
     |      Implement iter(self).
     |  
     |  __new__(*args, **kwargs) from builtins.type
     |      Create and return a new object.  See help(type) for accurate signature.
     |  
     |  __next__(self, /)
     |      Implement next(self).
     |  
     |  __reduce__(...)
     |      Return state information for pickling.   

The **filter** function is a function that filters an iterable based on the truthyness of the elements, or the truthyness of the elements after applying a function to them. Like the **map** function, the **filter** function returns an iterable that we can view by generating a list from it, or simply enumerating in a for loop.

```python
l = [0, 1, 2, 3, 4, 5, 6]
for e in filter(None, l):
    print(e)
```

    1
    2
    3
    4
    5
    6

Notice how **0** was eliminated from the list, since **0** is **falsy**.

We can use a function for this filtering.

Suppose we want to filter out all odd values, only retaining even values:

We could first define a function to return True if the value is even, and False otherwise:

```python
def is_even(n):
    return n % 2 == 0
```

```python
l = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result = filter(is_even, l)
print(list(result))
```

    [2, 4, 6, 8]

Of course, we could just use a lambda expression instead:

```python
l = [1, 2, 3, 4, 5, 6, 7, 8, 9]
result = filter(lambda x: x % 2 == 0, l)
print(list(result))
```

    [2, 4, 6, 8]

##### Alternatives to **map** and **filter** using Comprehensions

We'll cover comprehensions in much more detail later, but, for now, just be aware that we can use comprehensions instead of the **map** and **filter** functions - you decide which one you find more readable and enjoyable to write.

###### Map using a list comprehension:

* factorial example

```python
l = [1, 2, 3, 4, 5]
result = [fact(i) for i in l]
print(result)
```

    [1, 2, 6, 24, 120]

* two iterables example

Before we do this example we need to know about the **zip** function.

The **zip** built-in function will take one or more iterables, and generate an iterable of tuples where each tuple contains one element from each iterable:

```python
l1 = 1, 2, 3
l2 = 'a', 'b', 'c'
list(zip(l1, l2))
```

    [(1, 'a'), (2, 'b'), (3, 'c')]

```python
l1 = 1, 2, 3
l2 = [10, 20, 30]
l3 = ('a', 'b', 'c')
list(zip(l1, l2, l3))
```

    [(1, 10, 'a'), (2, 20, 'b'), (3, 30, 'c')]

```python
l1 = [1, 2, 3]
l2 = (10, 20, 30)
l3 = 'abc'
list(zip(l1, l2, l3))
```

    [(1, 10, 'a'), (2, 20, 'b'), (3, 30, 'c')]

```python
l1 = range(100)
l2 = 'python'
list(zip(l1, l2))
```

    [(0, 'p'), (1, 'y'), (2, 't'), (3, 'h'), (4, 'o'), (5, 'n')]

Using the **zip** function we can now add our two lists element by element as follows:

```python
l1 = [1, 2, 3, 4, 5]
l2 = [10, 20, 30, 40, 50]
result = [i + j for i,j in zip(l1,l2)]
print(result)
```

    [11, 22, 33, 44, 55]

###### Filtering using a comprehension

We can very easily filter an iterable using a comprehension as follows:

```python
l = [1, 2, 3, 4, 5, 6, 7, 8, 9]

result = [i for i in l if i % 2 == 0]
print(result)
```

    [2, 4, 6, 8]

As you can see, we did not even need a lambda expression!

##### Combining **map** and **filter**

```python
list(filter(lambda y: y < 25, map(lambda x: x**2, range(10))))
```

    [0, 1, 4, 9, 16]

Alternatively, we can use a list comprehension to do the same thing:

```python
[x**2 for x in range(10) if x**2 < 25]
```

    [0, 1, 4, 9, 16]

We will come back, in more detail, to comprehensions and generators later in this course.

#### 08 - Reducing Functions

##### Maximum and Minimum

Suppose we want to find the maximum value in a list:

```python
l = [5, 8, 6, 10, 9]
```

We can solve this problem using a **for** loop.

First we define a function that returns the maximum of two arguments:

```python
_max = lambda a, b: a if a > b else b
```

```python
def max_sequence(sequence):
    result = sequence[0]
    for x in sequence[1:]:
        result = _max(result, x)
    return result
```

```python
max_sequence(l)
```

    10

To calculate the minimum, all we need to do is to change the function that is repeatedly applied:

```python
_min = lambda a, b: a if a < b else b
```

```python
def min_sequence(sequence):
    result = sequence[0]
    for x in sequence[1:]:
        result = _min(result, x)
    return result
```

```python
print(l)
print(min_sequence(l))
```

    [5, 8, 6, 10, 9]
    5

In general we could write it like this:

```python
def _reduce(fn, sequence):
    result = sequence[0]
    for x in sequence[1:]:
        result = fn(result, x)
    return result
```

```python
_reduce(_max, l)
```

    10

```python
_reduce(_min, l)
```

    5

We could even just use a lambda directly in the call to **\_reduce**:

```python
_reduce(lambda a, b: a if a > b else b, l)
```

    10

```python
_reduce(lambda a, b: a if a < b else b, l)
```

    5

Using the same approach, we could even add all the elements of a sequence together:

```python
print(l)
```
    [5, 8, 6, 10, 9]

```python
_reduce(lambda a, b: a + b, l)
```

    38

Python actually implements a reduce function, which is found in the **functools** module. Unlike our **\_reduce** function, it can handle any iterable, not just sequences.

```python
from functools import reduce
```

```python
l
```

    [5, 8, 6, 10, 9]

```python
reduce(lambda a, b: a if a > b else b, l)
```

    10

```python
reduce(lambda a, b: a if a < b else b, l)
```

    5

```python
reduce(lambda a, b: a + b, l)
```

    38

Finding the max and min of an iterable is such a common thing that Python provides a built-in function to do just that:

```python
max(l), min(l)
```

    (10, 5)

Finding the sum of all the elements in an iterable is also common enough that Python implements the **sum** function:

```python
sum(l)
```

    38

##### The **any** and **all** built-ins

Python provides two additional built-in reducing functions: **any** and **all**.

The **any** function will return **True** if any element in the iterable is truthy:

```python
l = [0, 1, 2]
any(l)
```

    True

```python
l = [0, 0, 0]
any(l)
```

    False

On the other hand, **all** will return True if **every** element of the iterable is truthy:

```python
l = [0, 1, 2]
all(l)
```

    False

```python
l = [1, 2, 3]
all(l)
```

    True

We can implement these functions ourselves using **reduce** if we choose to - simply use the Boolean **or** or **and** operators as the function passed to **reduce** to implement **any** and **all** respectively.

##### any

```python
l = [0, 1, 2]
reduce(lambda a, b: bool(a or b), l)
```

    True

```python
l = [0, 0, 0]
reduce(lambda a, b: bool(a or b), l)
```

    False

##### all

```python
l = [0, 1, 2]
reduce(lambda a, b: bool(a and b), l)
```

    False

```python
l = [1, 2, 3]
reduce(lambda a, b: bool(a and b), l)
```

    True

##### Products

Sometimes we may want to find the product of every element of an iterable.

Python does not provide us a built-in method to do this, so we have to either use a procedural approach, or we can use the **reduce** function.

We start by defining a function that multiplies two arguments together:

```python
def mult(a, b):
    return a * b
```

Then we can use the **reduce** function:

```python
l = [2, 3, 4]
reduce(mult, l)
```

    24

Remember what this did:

    step 1: result = 2
    step 2: result = mult(result, 3) = mult(2, 3) = 6
    step 3: result = mult(result, 4) = mult(6, 4) = 24
    step 4: l exhausted, return result --> 24

Of course, we can also just use a lambda:

```python
reduce(lambda a, b: a * b, l)
```

    24

##### Factorials

A special case of the product we just did would be calculating the factorial of some number (**n!**):

Recall:

    n! = 1 * 2 * 3 * ... * n

In other words, we are calculating the product of a sequence containing consecutive integers from 1 to n (inclusive)

We can easily write this using a simple for loop:

```python
def fact(n):
    if n <= 1:
        return 1
    else:
        result = 1
        for i in range(2, n+1):
            result *= i
        return result
```

```python
fact(1), fact(2), fact(3), fact(4), fact(5)
```

    (1, 2, 6, 24, 120)

We could also write this using a recursive function:

```python
def fact(n):
    if n <=1:
        return 1
    else:
        return n * fact(n-1)
```

```python
fact(1), fact(2), fact(3), fact(4), fact(5)
```

    (1, 2, 6, 24, 120)

Finally we can also write this using **reduce** as follows:

```python
n = 5
reduce(lambda a, b: a * b, range(1, n+1))
```

    120

As you can see, the **reduce** approach, although concise, is sometimes more difficult to understand than the plain loop or recursive approach.

##### **reduce** initializer

Suppose we want to provide some sort of default when we claculate the product of the elements of an iterable if that iterable is empty:

```python
l = [1, 2, 3]
reduce(lambda x, y: x*y, l)
```
    6

but if **l** is empty:

```python
l = []
reduce(lambda x, y: x*y, l)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-39-09fa1e2b48dc> in <module>()
          1 l = []
    ----> 2 reduce(lambda x, y: x*y, l)

    TypeError: reduce() of empty sequence with no initial value

To fix this, we can provide an initializer. In this case, we will use **1** since that will not affect the result of the product, and still allow us to return a value for an empty iterable.

```python
l = []
reduce(lambda x, y: x*y, l, 1)
```

    1

#### 09 - Partial Functions

```python
from functools import partial
```

```python
def my_func(a, b, c):
    print(a, b, c)
```

```python
f = partial(my_func, 10)
```

```python
f(20, 30)
```

    10 20 30

We could have done this using another function (or a lambda) as well:

```python
def partial_func(b, c):
    return my_func(10, b, c)
```

```python
partial_func(20, 30)
```

    10 20 30

or, using a lambda:

```python
fn = lambda b, c: my_func(10, b, c)
```

```python
fn(20, 30)
```

    10 20 30

Any of these ways is fine, but sometimes partial is just a cleaner more consise way to do it.

Also, it is quite flexible with parameters:

```python
def my_func(a, b, *args, k1, k2, **kwargs):
    print(a, b, args, k1, k2, kwargs)
```

```python
f = partial(my_func, 10, k1='a')
```

```python
f(20, 30, 40, k2='b', k3='c')
```

    10 20 (30, 40) a b {'k3': 'c'}

We can of course do the same thing using a regular function too:

```python
def f(b, *args, k2, **kwargs):
    return my_func(10, b, *args, k1='a', k2=k2, **kwargs)
```

```python
f(20, 30, 40, k2='b', k3='c')
```

    10 20 (30, 40) a b {'k3': 'c'}

As you can see in this case, using **partial** seems a lot simpler.

Also, you are not stuck having to specify the first argument in your partial:

```python
def power(base, exponent):
    return base ** exponent
```

```python
power(2, 3)
```

    8

```python
square = partial(power, exponent=2)
```

```python
square(4)
```

    16

```python
cube = partial(power, exponent=3)
```

```python
cube(2)
```

    8

You can even call it this way:

```python
cube(base=3)
```

    27

##### Caveat

We can certainly use variables instead of literals when creating partials, but we have to be careful.

```python
def my_func(a, b, c):
    print(a, b, c)
```

```python
a = 10
f = partial(my_func, a)
```

```python
f(20, 30)
```

    10 20 30

Now let's change the value of the variable **a** and see what happens:

```python
a = 100
```

```python
f(20, 30)
```

    10 20 30

As you can see, the value for **a** is fixed once the partial has been created.

In fact, the memory address of **a** is baked in to the partial, and **a** is immutable.

If we use a mutable object, things are different:

```python
a = [10, 20]
f = partial(my_func, a)
```

```python
f(100, 200)
```

    [10, 20] 100 200

```python
a.append(30)
```

```python
f(100, 200)
```

    [10, 20, 30] 100 200

##### Use Cases

We tend to use partials in situation where we need to call a function that actually requires more parameters than we can supply.

Often this is because we are working with exiting libraries or code, and we have a special case.

For example, suppose we have points (represented as tuples), and we want to sort them based on the distance of the point from some other fixed point:

```python
origin = (0, 0)
```

```python
l = [(1,1), (0, 2), (-3, 2), (0,0), (10, 10)]
```

```python
dist2 = lambda x, y: (x[0]-y[0])**2 + (x[1]-y[1])**2
```

```python
dist2((0,0), (1,1))
```

    2

```python
sorted(l, key = lambda x: dist2((0,0), x))
```

    [(0, 0), (1, 1), (0, 2), (-3, 2), (10, 10)]

```python
sorted(l, key=partial(dist2, (0,0)))
```

    [(0, 0), (1, 1), (0, 2), (-3, 2), (10, 10)]

Another use case is when using **callback** functions. Usually these are used when running asynchronous operations, and you provide a callable to another callable which will be called when the first callable completes its execution.

Very often, the asynchronous callable will specify the number of variables that the callback function must have - this may not be what we want, maybe we want to add some additional info.

We'll look at asynchronous processing later in this course.

Often we can also use partial functions to make our life a bit easier.

Consider a situation where we have some generic `email()` function that can be used to notify someone when various things happen in our application. But depending on what is happening we may want to notify different people. Let's see how we may do this:

```python
def sendmail(to, subject, body):
    # code to send email
    print('To:{0}, Subject:{1}, Body:{2}'.format(to, subject, body))
```

Now, we may haver different email adresses we want to send notifications to, maybe defined in a config file in our app. Here, I'll just use hardcoded variables:

```python
email_admin = 'palin@python.edu'
email_devteam = 'idle@python.edu;cleese@python.edu'
```

Now when we want to send emails we would have to write things like:

```python
sendmail(email_admin, 'My App Notification', 'the parrot is dead.')
sendmail(';'.join((email_admin, email_devteam)), 'My App Notification', 'the ministry is closed until further notice.')
```

    To:palin@python.edu, Subject:My App Notification, Body:the parrot is dead.
    To:palin@python.edu;idle@python.edu;cleese@python.edu, Subject:My App Notification, Body:the ministry is closed until further notice.

We could simply our life a little using partials this way:

```python
send_admin = partial(sendmail, email_admin, 'For you eyes only')
send_dev = partial(sendmail, email_devteam, 'Dear IT:')
send_all = partial(sendmail, ';'.join((email_admin, email_devteam)), 'Loyal Subjects')
```

```python
send_admin('the parrot is dead.')
send_all('the ministry is closed until further notice.')
```

    To:palin@python.edu, Subject:For you eyes only, Body:the parrot is dead.
    To:palin@python.edu;idle@python.edu;cleese@python.edu, Subject:Loyal Subjects, Body:the ministry is closed until further notice.

Finally, let's make this a little more complex, with a mixture of positional and keyword-only arguments:

```python
def sendmail(to, subject, body, *, cc=None, bcc=email_devteam):
    # code to send email
    print('To:{0}, Subject:{1}, Body:{2}, CC:{3}, BCC:{4}'.format(to, 
                                                                  subject, 
                                                                  body, 
                                                                  cc, 
                                                                  bcc))
```

```python
send_admin = partial(sendmail, email_admin, 'General Admin')
send_admin_secret = partial(sendmail, email_admin, 'For your eyes only', cc=None, bcc=None)
```

```python
send_admin('and now for something completely different')
```

    To:palin@python.edu, Subject:General Admin, Body:and now for something completely different, CC:None, BCC:idle@python.edu;cleese@python.edu

```python
send_admin_secret('the parrot is dead!')
```

    To:palin@python.edu, Subject:For your eyes only, Body:the parrot is dead!, CC:None, BCC:None

```python
send_admin_secret('the parrot is no more!', bcc=email_devteam)
```

    To:palin@python.edu, Subject:For your eyes only, Body:the parrot is no more!, CC:None, BCC:idle@python.edu;cleese@python.edu

```python
def pow(base, exponent):
    return base ** exponent
```

```python
cube = partial(pow, exponent=3)
```

```python
cube(2)
```

    8

```python
cube(2, 4)
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-54-725d549b8104> in <module>()
    ----> 1 cube(2, 4)
    

    TypeError: pow() got multiple values for argument 'exponent'

```python
cube(2, exponent=4)
```

    16



#### 10 - The operator Module

```python
import operator
```

```python
dir(operator)
```

    ['__abs__',
     '__add__',
     '__all__',
     '__and__',
     '__builtins__',
     '__cached__',
     '__concat__',
     '__contains__',
     '__delitem__',
     '__doc__',
     '__eq__',
     '__file__',
     '__floordiv__',
     '__ge__',
     '__getitem__',
     '__gt__',
     '__iadd__',
     '__iand__',
     '__iconcat__',
     '__ifloordiv__',
     '__ilshift__',
     '__imatmul__',
     '__imod__',
     '__imul__',
     '__index__',
     '__inv__',
     '__invert__',
     '__ior__',
     '__ipow__',
     '__irshift__',
     '__isub__',
     '__itruediv__',
     '__ixor__',
     '__le__',
     '__loader__',
     '__lshift__',
     '__lt__',
     '__matmul__',
     '__mod__',
     '__mul__',
     '__name__',
     '__ne__',
     '__neg__',
     '__not__',
     '__or__',
     '__package__',
     '__pos__',
     '__pow__',
     '__rshift__',
     '__setitem__',
     '__spec__',
     '__sub__',
     '__truediv__',
     '__xor__',
     '_abs',
     'abs',
     'add',
     'and_',
     'attrgetter',
     'concat',
     'contains',
     'countOf',
     'delitem',
     'eq',
     'floordiv',
     'ge',
     'getitem',
     'gt',
     'iadd',
     'iand',
     'iconcat',
     'ifloordiv',
     'ilshift',
     'imatmul',
     'imod',
     'imul',
     'index',
     'indexOf',
     'inv',
     'invert',
     'ior',
     'ipow',
     'irshift',
     'is_',
     'is_not',
     'isub',
     'itemgetter',
     'itruediv',
     'ixor',
     'le',
     'length_hint',
     'lshift',
     'lt',
     'matmul',
     'methodcaller',
     'mod',
     'mul',
     'ne',
     'neg',
     'not_',
     'or_',
     'pos',
     'pow',
     'rshift',
     'setitem',
     'sub',
     'truediv',
     'truth',
     'xor']

##### Arithmetic Operators

A variety of arithmetic operators are implemented.

```python
operator.add(1, 2)
```

    3

```python
operator.mul(2, 3)
```

    6

```python
operator.pow(2, 3)
```

    8

```python
operator.mod(13, 2)
```

    1

```python
operator.floordiv(13, 2)
```

    6

```python
operator.truediv(3, 2)
```

    1.5

These would have been very handy in our previous section:

```python
from functools import reduce
```

```python
reduce(lambda x, y: x*y, [1, 2, 3, 4])
```

    24

Instead of defining a lambda, we could simply use **operator.mul**:

```python
reduce(operator.mul, [1, 2, 3, 4])
```

    24

##### Comparison and Boolean Operators

Comparison and Boolean operators are also implemented as functions:

```python
operator.lt(10, 100)
```

    True

```python
operator.le(10, 10)
```

    True

```python
operator.is_('abc', 'def')
```

    False

We can even get the truthyness of an object:

```python
operator.truth([1,2])
```

    True

```python
operator.truth([])
```

    False

```python
operator.and_(True, False)
```

    False

```python
operator.or_(True, False)
```

    True

##### Element and Attribute Getters and Setters

We generally select an item by index from a sequence by using **[n]**:

```python
my_list = [1, 2, 3, 4]
my_list[1]
```

    2

We can do the same thing using:

```python
operator.getitem(my_list, 1)
```

    2

If the sequence is mutable, we can also set or remove items:

```python
my_list = [1, 2, 3, 4]
my_list[1] = 100
del my_list[3]
print(my_list)
```

    [1, 100, 3]

```python
my_list = [1, 2, 3, 4]
operator.setitem(my_list, 1, 100)
operator.delitem(my_list, 3)
print(my_list)
```

    [1, 100, 3]

We can also do the same thing using the **operator** module's **itemgetter** function.

The difference is that this returns a callable:

```python
f = operator.itemgetter(2)
```

Now, **f(my_list)** will return **my_list[2]**

```python
f(my_list)
```

    3

```python
x = 'python'
f(x)
```

    't'

Furthermore, we can pass more than one index to **itemgetter**:

```python
f = operator.itemgetter(2, 3)
```

```python
my_list = [1, 2, 3, 4]
f(my_list)
```

    (3, 4)

```python
x = 'pytyhon'
f(x)
```

    ('t', 'y')

Similarly, **operator.attrgetter** does the same thing, but with object attributes.

```python
class MyClass:
    def __init__(self):
        self.a = 10
        self.b = 20
        self.c = 30
        
    def test(self):
        print('test method running...')
```

```python
obj = MyClass()
```

```python
obj.a, obj.b, obj.c
```

    (10, 20, 30)

```python
f = operator.attrgetter('a')
```

```python
f(obj)
```

    10

```python
my_var = 'b'
operator.attrgetter(my_var)(obj)
```

    20

```python
my_var = 'c'
operator.attrgetter(my_var)(obj)
```

    30

```python
f = operator.attrgetter('a', 'b', 'c')
```

```python
f(obj)
```

    (10, 20, 30)

Of course, attributes can also be methods.

In this case, **attrgetter** will return the object's **test** method - a callable that can then be called using **()**:

```python
f = operator.attrgetter('test')
```

```python
obj_test_method = f(obj)
```

```python
obj_test_method()
```

    test method running...

Just like lambdas, we do not need to assign them to a variable name in order to use them:

```python
operator.attrgetter('a', 'b')(obj)
```

    (10, 20)

```python
operator.itemgetter(2, 3)('python')
```

    ('t', 'h')

Of course, we can achieve the same thing using functions or lambdas:

```python
f = lambda x: (x.a, x.b, x.c)
```

```python
f(obj)
```

    (10, 20, 30)

```python
f = lambda x: (x[2], x[3])
```

```python
f([1, 2, 3, 4])
```

    (3, 4)

```python
f('python')
```

    ('t', 'h')

###### Use Case Example: Sorting

Suppose we want to sort a list of complex numbers based on the real part of the numbers:

```python
a = 2 + 5j
a.real
```

    2.0

```python
l = [10+1j, 8+2j, 5+3j]
sorted(l, key=operator.attrgetter('real'))
```

    [(5+3j), (8+2j), (10+1j)]

Or if we want to sort a list of string based on the last character of the strings:

```python
l = ['aaz', 'aad', 'aaa', 'aac']
sorted(l, key=operator.itemgetter(-1))
```

    ['aaa', 'aac', 'aad', 'aaz']

Or maybe we want to sort a list of tuples based on the first item of each tuple:

```python
l = [(2, 3, 4), (1, 2, 3), (4, ), (3, 4)]
sorted(l, key=operator.itemgetter(0))
```

    [(1, 2, 3), (2, 3, 4), (3, 4), (4,)]

##### Slicing

```python
l = [1, 2, 3, 4]
```

```python
l[0:2]
```

    [1, 2]

```python
l[0:2] = ['a', 'b', 'c']
print(l)
```

    ['a', 'b', 'c', 3, 4]

```python
del l[3:5]
print(l)
```

    ['a', 'b', 'c']

We can do the same thing this way:

```python
l = [1, 2, 3, 4]
```

```python
operator.getitem(l, slice(0,2))
```

    [1, 2]

```python
operator.setitem(l, slice(0,2), ['a', 'b', 'c'])
print(l)
```

    ['a', 'b', 'c', 3, 4]

```python
operator.delitem(l, slice(3, 5))
print(l)
```

    ['a', 'b', 'c']

##### Calling another Callable

```python
x = 'python'
x.upper()
```

    'PYTHON'

```python
operator.methodcaller('upper')('python')
```

    'PYTHON'

Of course, since **upper** is just an attribute of the string object **x**, we could also have used:

```python
operator.attrgetter('upper')(x)()
```

    'PYTHON'

If the callable takes in more than one parameter, they can be specified as additional arguments in **methodcaller**:

```python
class MyClass:
    def __init__(self):
        self.a = 10
        self.b = 20
    
    def do_something(self, c):
        print(self.a, self.b, c)
```

```python
obj = MyClass()
```

```python
obj.do_something(100)
```

    10 20 100

```python
operator.methodcaller('do_something', 100)(obj)
```

    10 20 100

```python
class MyClass:
    def __init__(self):
        self.a = 10
        self.b = 20
    
    def do_something(self, *, c):
        print(self.a, self.b, c)
```

```python
obj.do_something(c=100)
```

    10 20 100

```python
operator.methodcaller('do_something', c=100)(obj)
```

    10 20 100

More information on the **operator** module can be found here:

https://docs.python.org/3/library/operator.html

### 7. Scopes, Closures and Decorators

#### 01 - Global and Local Scopes

In Python the **global** scope refers to the **module** scope.

The scope of a variable is normally defined by **where** it is (lexically) defined in the code.

```python
a = 10
```

In this case, **a** is defined inside the main module, so it is a global variable.

```python
def my_func(n):
    c = n ** 2
    return c
```

In this case, **c** was defined inside the function **my_func**, so it is **local** to the function **my_func**. In this example, **n** is also **local** to **my_func**

Global variables can be accessed from any inner scope in the module, for example:

```python
def my_func(n):
    print('global:', a)
    c = a ** n
    return c
```

```python
my_func(2)
```

    global: 10

    100

As you can see, **my_func** was able to reference the global variable **a**.

But remember that the scope of a variable is determined by where it is assigned. In particular, any variable defined (i.e. assigned a value) inside a function is local to that function, even if the variable name happens to be global too!

```python
def my_func(n):
    a = 2
    c = a ** 2
    return c
```

```python
print(a)
print(my_func(3))
print(a)
```

    10
    4
    10

In order to change the value of a global variable within an inner scope, we can use the **global** keyword as follows:

```python
def my_func(n):
    global a
    a = 2
    c = a ** 2
    return c
```

```python
print(a)
print(my_func(3))
print(a)
```

    10
    4
    2

As you can see, the value of the global variable **a** was changed from within **my_func**.

In fact, we can **create** global variables from within an inner function - Python will simply create the variable and place it in the **global** scope instead of the **local scope**:

```python
def my_func(n):
    global var
    var = 'hello world'
    return n ** 2
```

Now, **var** does not exist yet, since the function has not run:

```python
print(var)
```

    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-10-571cba235a7f> in <module>()
    ----> 1 print(var)
    

    NameError: name 'var' is not defined

Once we call the function though, it will create that global **var**:

```python
my_func(2)
```

    4

```python
print(var)
```

    hello world

##### Beware!!

Remember that whenever you assign a value to a variable without having specified the variable as **global**, it is **local** in the current scope. **Moreover**, it does not matter **where** the assignment in the code takes place, the variable is considered local in the **entire** scope - Python determines the scope of objects at compile-time, not at run-time.

Let's see an example of this:

```python
a = 10
b = 100
```

```python
def my_func():
    print(a)
    print(b)
    
```

```python
my_func()
```

    10
    100

So, this works as expected - **a** and **b** are taken from the global scope since they are referenced **before** being assigned a value in the local scope.

But now consider the following example:

```python
a = 10
b = 100

def my_func():
    print(a)
    print(b)
    b = 1000
```

```python
my_func()
```

    10

    ---------------------------------------------------------------------------

    UnboundLocalError                         Traceback (most recent call last)

    <ipython-input-17-d82eda95de40> in <module>()
    ----> 1 my_func()
    

    <ipython-input-16-a2b60f95cac1> in my_func()
          4 def my_func():
          5     print(a)
    ----> 6     print(b)
          7     b = 1000


    UnboundLocalError: local variable 'b' referenced before assignment

As you can see, **b** in the line ``print(b)`` is considered a **local** variable - that's because the **next** line **assigns** a value to **b** - hence **b** is scoped as local by Python for the **entire** function.

Of course, functions are also objects, and scoping applies equally to function objects too. For example, we can "mask" the built-in `print` Python function:

```python
print = lambda x: 'hello {0}!'.format(x)

def my_func(name):
	return print(name)

my_func('world')

```

    'hello world!'

You may be wondering how we get our **real** ``print`` function back!

```python
del print
```

```python
print('hello')
```

    hello

Yay!!

If you have experience in some other programming languages you may be wondering if loops and other code "blocks" have their own local scope too. For example in Java, the following would not work:

``for (int i=0; i<10; i++) {
    int x = 2 * i;
}
system.out.println(x);
``

But in Python it works perfectly fine:

```python
for i in range(10):
    x = 2 * i
print(x)
```

    18

In this case, when we assigned a value to `x`, Python put it in the global (module) scope, so we can reference it after the `for` loop has finished running.

#### 02 - Nonlocal Scopes

Functions defined inside anther function can reference variables from that enclosing scope, just like functions can reference variables from the global scope.

```python
def outer_func():
    x = 'hello'
    
    def inner_func():
        print(x)
    
    inner_func()
```

```python
outer_func()
```

    hello

In fact, any level of nesting is supported since Python just keeps looking in enclosing scopes until it finds what it needs (or fails to find it by the time it finishes looking in the built-in scope, in which case a runtime error occurrs.)

```python
def outer_func():
    x = 'hello'
    def inner1():
        def inner2():
            print(x)
        inner2()
    inner1()
```

```python
outer_func()
```

    hello

But if we **assign** a value to a variable, it is considered part of the local scope, and potentially **masks** enclsogin scope variable names:

```python
def outer():
    x = 'hello'
    def inner():
        x = 'python'
    inner()
    print(x)
```

```python
outer()
```

    hello

As you can see, **x** in **outer** was not changed.

To achieve this, we can use the **nonlocal** keyword:

```python
def outer():
    x = 'hello'
    def inner():
        nonlocal x
        x = 'python'
    inner()
    print(x)
```

```python
outer()
```

    python

Of course, this can work at any level as well:

```python
def outer():
    x = 'hello'
    
    def inner1():
        def inner2():
            nonlocal x
            x = 'python'
        inner2()
    inner1()
    print(x)
```

```python
outer()
```

    python

How far Python looks up the chain depends on the first occurrence of the variable name in an enclosing scope.

Consider the following example:

```python
def outer():
    x = 'hello'
    def inner1():
        x = 'python'
        def inner2():
            nonlocal x
            x = 'monty'
        print('inner1 (before):', x)
        inner2()
        print('inner1 (after):', x)
    inner1()
    print('outer:', x)
```

```python
outer()
```

    inner1 (before): python
    inner1 (after): monty
    outer: hello

What happened here, is that `x` in `inner1` **masked** `x` in `outer`. But `inner2` indicated to Python that `x` was nonlocal, so the first local variable up in the enclosing scope chain Python found was the one in `inner1`, hence `x` in `inner2` is actually referencing `x` that is local to `inner1`

We can change this behavior by making the variable `x` in `inner` nonlocal as well:

```python
def outer():
    x = 'hello'
    def inner1():
        nonlocal x
        x = 'python'
        def inner2():
            nonlocal x
            x = 'monty'
        print('inner1 (before):', x)
        inner2()
        print('inner1 (after):', x)
    inner1()
    print('outer:', x)
```

```python
outer()
```

    inner1 (before): python
    inner1 (after): monty
    outer: monty

```python
x = 100
def outer():
    x = 'python'  # masks global x
    def inner1():
        nonlocal x  # refers to x in outer
        x = 'monty' # changed x in outer scope
        def inner2():
            global x  # refers to x in global scope
            x = 'hello'
        print('inner1 (before):', x)
        inner2()
        print('inner1 (after):', x)
    inner1()
    print('outer', x)    
```

```python
outer()
print(x)
```

    inner1 (after): monty
    outer monty
    100

But this will not work. In `inner` Python is looking for a local variable called `x`. `outer` has a label called `x`, but it is a global variable, not a local one - hence Python does not find a local variable in the scope chain.

```python
x = 100
def outer():
    global x
    x = 'python'
    
    def inner():
        nonlocal x
        x = 'monty'
    inner()
```

      File "<ipython-input-17-3ccaec905318>", line 7
        nonlocal x
        ^
    SyntaxError: no binding for nonlocal 'x' found

#### 03 - Closures

Let's examine that concept of a cell to create an indirect reference for variables that are in multiple scopes.

```python
def outer():
    x = 'python'
    def inner():
        print(x)
    return inner
```

```python
fn = outer()
```

```python
fn.__code__.co_freevars
```

    ('x',)

As we can see, `x` is a free variable in the closure.

```python
fn.__closure__
```

    (<cell at 0x0000015F5299B4C8: str object at 0x0000015F51092068>,)

Here we see that the free variable x is actually a reference to a cell object that is itself a reference to a string object.

Let's see what the memory address of `x` is in the outer function and the inner function. To be sure string interning does not play a role, I am going to use an object that we know Python will not automatically intern, like a list.

```python
def outer():
    x = [1, 2, 3]
    print('outer:', hex(id(x)))
    def inner():
        print('inner:', hex(id(x)))
        print(x)
    return inner
```

```python
fn = outer()
```

    outer: 0x15f52907988

```python
fn.__closure__
```

    (<cell at 0x0000015F5299B768: list object at 0x0000015F52907988>,)

```python
fn()
```

    inner: 0x15f52907988
    [1, 2, 3]

As you can see, each the memory address of `x` in `outer`, `inner` and the cell all point to the same object.

##### Modifying the Free Variable

We know we can modify nonlocal variables by using the `nonlocal` keyword. So the following will work:

```python
def counter():
    count = 0 # local variable
    
    def inc():
        nonlocal count  # this is the count variable in counter
        count += 1
        return count
    return inc
```

```python
c = counter()
```

```python
c()
```

    1

```python
c()
```

    2

###### Shared Extended Scopes

As we saw in the lecture, we can set up nonlocal variables in different inner functionsd that reference the same outer scope variable, i.e. we have a free variable that is shared between two closures. This works because both non local variables and the outer local variable all point back to the same cell object.

```python
def outer():
    count = 0
    def inc1():
        nonlocal count
        count += 1
        return count
    
    def inc2():
        nonlocal count
        count += 1
        return count
    
    return inc1, inc2
```

```python
fn1, fn2 = outer()
```

```python
fn1.__closure__, fn2.__closure__
```

    ((<cell at 0x0000015F5299B738: int object at 0x00000000506FEC50>,),
     (<cell at 0x0000015F5299B738: int object at 0x00000000506FEC50>,))

As you can see here, the `count` label points to the same cell.

```python
fn1()
```

    1

```python
fn1()
```

    2

```python
fn2()
```

    3

##### Multiple Instances of Closures

Recall that **every** time a function is called, a **new** local scope is created.

```python
from time import perf_counter

def func():
    x = perf_counter()
    print(x, id(x))
```

```python
func()
```

    2.7089464582150425e-07 1508916709680

```python
func()
```

    0.011222623387093279 1508916709680

The same thing happens with closures, they have their own extended scope every time the closure is created:

```python
def pow(n):
    # n is local to pow
    def inner(x):
        # x is local to inner
        return x ** n
    return inner
```

In this example, `n`, in the function `inner` is a free variable, so we have a closure that contains `inner` and the free variable `n`

```python
square = pow(2)
```

```python
square(5)
```

    25

```python
cube = pow(3)
```

```python
cube(5)
```

    125

We can see that the cell used for the free variable in both cases is **different**:

```python
square.__closure__
```

    (<cell at 0x0000015F5299B8B8: int object at 0x00000000506FEC90>,)

```python
cube.__closure__
```

    (<cell at 0x0000015F5299BAC8: int object at 0x00000000506FECB0>,)

In fact, these functions (`square` and `cube`) are **not** the same functions, even though they were "created" from the same `power` function:

```python
id(square), id(cube)
```

    (1508919294560, 1508919295784)

##### Beware!

Remember when I said the captured variable is a reference established when the closure is created, but the value is looked up only once the function is called?

This can create very subtle bugs in your program.

Consider the following example where we want to create some functions that can add 1, 2, 3, 4 and to whatever is passed to them.

We could do the following:

```python
def adder(n):
    def inner(x):
        return x + n
    return inner
```

```python
add_1 = adder(1)
add_2 = adder(2)
add_3 = adder(3)
add_4 = adder(4)
```

```python
add_1(10), add_2(10), add_3(10), add_4(10)
```

    (11, 12, 13, 14)

But suppose we want to get a little fancier and do it as follows:

```python
def create_adders():
    adders = []
    for n in range(1, 5):
        adders.append(lambda x: x + n)
    return adders
```

```python
adders = create_adders()
```

Now technically we have 4 functions in the `adders` list:

```python
adders
```

    [<function __main__.create_adders.<locals>.<lambda>>,
     <function __main__.create_adders.<locals>.<lambda>>,
     <function __main__.create_adders.<locals>.<lambda>>,
     <function __main__.create_adders.<locals>.<lambda>>]

The first one should add 1 to the value we pass it, the second should add 2, and so on.

```python
adders[3](10)
```

    14

Yep, that works for the 4th function.

```python
adders[0](10)
```

    14

Uh Oh - what happened? In fact we get the same behavior from every one of those functions:

```python
adders[0](10), adders[1](10), adders[2](10), adders[3](10)
```

    (14, 14, 14, 14)

Remember what I said about when the variable is captured and when the value is looked up?

When the lambdas are **created** their `n` is the `n` used in the loop - the **same** `n`!!

```python
adders[0].__code__.co_freevars
```

    ('n',)

```python
adders[0].__closure__
```

    (<cell at 0x0000015F5299B3D8: int object at 0x00000000506FECD0>,)

```python
adders[1].__closure__
```

    (<cell at 0x0000015F5299B3D8: int object at 0x00000000506FECD0>,)

```python
adders[2].__closure__
```

    (<cell at 0x0000015F5299B3D8: int object at 0x00000000506FECD0>,)

```python
adders[3].__closure__
```

    (<cell at 0x0000015F5299B3D8: int object at 0x00000000506FECD0>,)

So, by the time we call `adder[i]`, the free variable `n` (shared between all adders) is set to 4.

```python
hex(id(4))
```

    '0x506fecd0'

As we can see the memory address of the singleton integer 4, is what that cell is pointint to.

If you want to use a loop to do this and not end up using the same cell for each of the free variables, we can use a simple trick that forces the evaluation of `n` at the time the closure is **created**, instead of when the closure function is evaluated.

We can do this by creating a parameter for `n` in our lambda whose default value is the current value of `n` - remember from an earlier video that parameter defaults are avaluated when the function is created, not called.

```python
def create_adders():
    adders = []
    for n in range(1, 5):
        adders.append(lambda x, step=n: x + step)
    return adders
```

```python
adders = create_adders()
```

```python
adders[0].__closure__
```

Why aren't we getting anything in the closure? What about free variables?

```python
adders[0].__code__.co_freevars
```

    ()

Hmm, nothing either... Why?

Well, look at the lambda in that loop. Does it reference the variable `n` (other than in the default value)? No. Hence, `n` is **not** a free variable in this case, and our lambda is just a plain lambda, not a closure.

And this code will now work as expected:

```python
adders[0](10)
```

    11

```python
adders[1](10)
```

    12

```python
adders[2](10)
```

    13

```python
adders[3](10)
```

    14

You just need to understand that since the default values are evaluated when the function (lambda in this case) is **created**, the then-current `n` value is assigned to the local variable `step`. So `step` will not change every time the lambda is called, and since n is not referenced inside the function (and therefore evaluated when the lambda is called), `n` is not a free variable.

##### Nested Closures

We can also nest closures, as can be seen in this example:

```python
def incrementer(n):
    def inner(start):
        current = start
        def inc():
            a = 10  # local var
            nonlocal current
            current += n
            return current
        return inc
    return inner
        
```

```python
fn = incrementer(2)
```

```python
fn
```

    <function __main__.incrementer.<locals>.inner>

```python
fn.__code__.co_freevars
```

    ('n',)

```python
fn.__closure__
```

    (<cell at 0x0000015F5299B798: int object at 0x00000000506FEC90>,)

```python
inc_2 = fn(100)
```

```python
inc_2
```

    <function __main__.incrementer.<locals>.inner.<locals>.inc>

```python
inc_2.__code__.co_freevars
```

    ('current', 'n')

```python
inc_2.__closure__
```

    (<cell at 0x0000015F5299B318: int object at 0x00000000506FF8D0>,
     <cell at 0x0000015F5299B798: int object at 0x00000000506FEC90>)

Here you can see that the second free variable `n`, is pointing to the same cell as the free variable in `fn`.

Note that **a** is a local variable, and is not considered a free variable.

And we can call the closures as follows:

```python
inc_2()
```

    102

```python
inc_2()
```

    104

```python
inc_3 = incrementer(3)(200)
```

```python
inc_3()
```

    203

```python
inc_3()
```

    206




#### 04 - Closure Applications - Part 1

In this example we are going to build an averager function that can average multiple values.

The twist is that we want to simply be able to feed numbers to that function and get a running average over time, not average a list which requires performing the same calculations (sum and count) over and over again.

```python
class Averager:
    def __init__(self):
        self.numbers = []
    
    def add(self, number):
        self.numbers.append(number)
        total = sum(self.numbers)
        count = len(self.numbers)
        return total / count
```

```python
a = Averager()
```

```python
a.add(10)
```

    10.0

```python
a.add(20)
```

    15.0

```python
a.add(30)
```

    20.0

We can do this using a closure as follows:

```python
def averager():
    numbers = []
    def add(number):
        numbers.append(number)
        total = sum(numbers)
        count = len(numbers)
        return total / count
    return add
```

```python
a = averager()
```

```python
a(10)
```

    10.0

```python
a(20)
```

    15.0

```python
a(30)
```

    20.0

Now, instead of storing a list and reclaculating `total` and `count` every time wer need the new average, we are going to store the running total and count and update each value each time a new value is added to the running average, and then return `total / count`.

Let's start with a class approach first, where we will use instance variables to store the running total and count and provide an instance method to add a new number and return the current average.

```python
class Averager:
    def __init__(self):
        self._count = 0
        self._total = 0
    
    def add(self, value):
        self._total += value
        self._count += 1
        return self._total / self._count
```

```python
a = Averager()
```

```python
a.add(10)
```

    10.0

```python
a.add(20)
```

    15.0

```python
a.add(30)
```

    20.0

Now, let's see how we might use a closure to achieve the same thing.

```python
def averager():
    total = 0
    count = 0
    
    def add(value):
        nonlocal total, count
        total += value
        count += 1
        return 0 if count == 0 else total / count
    
    return add
        
```

```python
a = averager()
```

```python
a(10)
```

    10.0

```python
a(20)
```

    15.0

```python
a(30)
```

    20.0

##### Generalizing this example

We saw that we were essentially able to convert a class to an equivalent functionality using closures. This is actually true in a much more general sense - very often, classes that define a single method (other than initializers) can be implemented using a closure instead.

Let's look at another example of this.

Suppose we want something that can keep track of the running elapsed time in seconds.

```python
from time import perf_counter
```

```python
class Timer:
    def __init__(self):
        self._start = perf_counter()
    
    def __call__(self):
        return (perf_counter() - self._start)
```

```python
a = Timer()
```

Now wait a bit before running the next line of code:

```python
a()
```

    0.011695334544051804

Let's start another "timer":

```python
b = Timer()
```

```python
print(a())
print(b())
```

    0.03528294403966765
    0.011656054820407689

Now let's rewrite this using a closure instead:

```python
def timer():
    start = perf_counter()
    
    def elapsed():
        # we don't even need to make start nonlocal 
        # since we are only reading it
        return perf_counter() - start
    
    return elapsed
```

```python
x = timer()
```

```python
x()
```

    0.011068213438975016

```python
y = timer()
```

```python
print(x())
print(y())
```

    0.03419096772236116
    0.01164738619174141

```python
print(a())
print(b())
print(x())
print(y())
```

    0.10822159832175349
    0.08475345336494494
    0.0462381944113351
    0.023573252079387305

#### 05 - Closure Applications - Part 2

##### Example 1

Let's write a small function that can increment a counter for us - we don't have an incrementor in Python (the ++ operator in Java or C++ for example):

```python
def counter(initial_value):
    # initial_value is a local variable here
    
    def inc(increment=1):
        nonlocal initial_value
        # initial_value is a nonlocal (captured) variable here
        initial_value += increment
        return initial_value
    
    return inc
```

```python
counter1 = counter(0)
```

```python
print(counter1(0))
```

    0

```python
print(counter1())
```

    1

```python
print(counter1())
```

    2

```python
print(counter1(8))
```

    10

```python
counter2 = counter(1000)
```

```python
print(counter2(0))
```

    1000

```python
print(counter2(1))
```

    1001

```python
print(counter2())
```

    1002

```python
print(counter2(220))
```

    1222

As you can see, each closure maintains a reference to the **initial_value** variable that was created when the **counter** function was **called** - each time that function was called, a new local variable **initial_value** was created (with a value assigned from the argument), and it became a nonlocal (captured) variable in the inner scope.

##### Example 2

Let's modify this example to now build something that can run, and maintain a count of how many times we have run some function.

```python
def counter(fn):
    cnt = 0  # initially fn has been run zero times
    
    def inner(*args, **kwargs):
        nonlocal cnt
        cnt = cnt + 1
        print('{0} has been called {1} times'.format(fn.__name__, cnt))
        return fn(*args, **kwargs)
    
    return inner
```

```python
def add(a, b):
    return a + b
```

```python
counted_add = counter(add)
```

And the free variables are:

```python
counted_add.__code__.co_freevars
```

    ('cnt', 'fn')

We can now call the `counted_add` function:

```python
counted_add(1, 2)
```

    add has been called 1 times

    3

```python
counted_add(2, 3)
```

    add has been called 2 times

    5

```python
def mult(a, b, c):
    return a * b * c
```

```python
counted_mult = counter(mult)
```

```python
counted_mult(1, 2, 3)
```

    mult has been called 1 times

    6

```python
counted_mult(2, 3, 4)
```

    mult has been called 2 times

    24

##### Example 3

Let's take this one step further, and actually store the function name and the number of calls in a global dictionary instead of just printing it out all the time.

```python
counters = dict()

def counter(fn):
    cnt = 0  # initially fn has been run zero times
    
    def inner(*args, **kwargs):
        nonlocal cnt
        cnt = cnt + 1
        counters[fn.__name__] = cnt  # counters is global
        return fn(*args, **kwargs)
    
    return inner
```

```python
counted_add = counter(add)
counted_mult = counter(mult)
```

Note that `counters` is a **global** variable, and therefore **not** a free variable:

```python
counted_add.__code__.co_freevars
```

    ('cnt', 'fn')

```python
counted_mult.__code__.co_freevars
```

    ('cnt', 'fn')

We can now call out functions:

```python
counted_add(1, 2)
```

    3

```python
counted_add(2, 3)
```

    5

```python
counted_mult(1, 2, 'a')
```

    'aa'

```python
counted_mult(2, 3, 'b')
```

    'bbbbbb'

```python
counted_mult(1, 1, 'abc')
```

    'abc'

```python
print(counters)
```

    {'add': 2, 'mult': 3}

Of course this relies on us creating the **counters** global variable first and making sure we are naming it that way, so instead, we're going to pass it as an argument to the **counter** function:

```python
def counter(fn, counters):
    cnt = 0  # initially fn has been run zero times
    
    def inner(*args, **kwargs):
        nonlocal cnt
        cnt = cnt + 1
        counters[fn.__name__] = cnt  # counters is nonlocal
        return fn(*args, **kwargs)
    
    return inner
```

```python
func_counters = dict()
counted_add = counter(add, func_counters)
counted_mult = counter(mult, func_counters)
```

```python
counted_add.__code__.co_freevars
```

    ('cnt', 'counters', 'fn')

As you can see, `counters` is now a free variable.

We can now call our functions:

```python
for i in range(5):
    counted_add(i, i)

for i in range(10):
    counted_mult(i, i, i)
```

```python
print(func_counters)
```

    {'add': 5, 'mult': 10}

Of course, we don't have to assign the "counted" version of our functions a new name - we can simply assign it to the same name!

```python
def fact(n):
    product = 1
    for i in range(2, n+1):
        product *= i
    return product
```

```python
fact = counter(fact, func_counters)
```

```python
fact(0)
```

    1

```python
fact(3)
```

    6

```python
fact(4)
```

    24

```python
print(func_counters)
```

    {'add': 5, 'mult': 10, 'fact': 3}

Notice, how we essentially **added** some functionality to our `fact` function, without modifying what the `fact` function actually returns.

This leads us straight into our next topic: decorators!

#### 06 - Decorators - Part 1

Recall the example in the last section where we wrote a simple closure to count how many times a function had been run:

```python
def counter(fn):
    count = 0
    
    def inner(*args, **kwargs):
        nonlocal count
        count += 1
        print('Function {0} was called {1} times'.format(fn.__name__, count))
        return fn(*args, **kwargs)
    return inner
```

```python
def add(a, b=0):
    """
    returns the sum of a and b
    """
    return a + b
```

```python
help(add)
```

    Help on function add in module __main__:
    
    add(a, b=0)
        returns the sum of a and b
    

Here's the memory address that `add` points to:

```python
id(add)
```

    2352389334696

Now we create a closure using the `add` function as an argument to the `counter` function:

```python
add = counter(add)
```

And you'll note that `add` is no longer the same function as before. Indeed the memory address `add` points to is no longer the same:

```python
id(add)
```

    2352404346128

```python
add(1, 2)
```

    Function add was called 1 times

    3

```python
add(2, 2)
```

    Function add was called 2 times

    4

What happened is that we put our **add** function 'through' the **counter** function - we usually say that we **decorated** our function **add**.

And we call that **counter** function a **decorator**.

There is a shorthand way of decorating our function without having to type:

``func = counter(func)``

```python
@counter
def mult(a: float, b: float=1, c: float=1) -> float:
    """
    returns the product of a, b, and c
    """
    return a * b * c
```

```python
mult(1, 2, 3)
```

    Function mult was called 1 times

    6

```python
mult(2, 2, 2)
```

    Function mult was called 2 times

    8

Let's do a little bit of introspection on our two decorated functions:

```python
add.__name__
```

    'inner'

```python
mult.__name__
```

    'inner'

As you can see, the name of the function is no longer **add** or **mult**, but instead it is the name of that **inner** function in our decorator.

```python
help(add)
```

    Help on function inner in module __main__:
    
    inner(*args, **kwargs)
    

```python
help(mult)
```

    Help on function inner in module __main__:
    
    inner(*args, **kwargs)
    

As you can see, we've also lost our docstring and parameter annotations!

What about introspecting the parameters of **add** and **mult**:

```python
import inspect
```

```python
inspect.getsource(add)
```

    "    def inner(*args, **kwargs):\n        nonlocal count\n        count += 1\n        print('Function {0} was called {1} times'.format(fn.__name__, count))\n        return fn(*args, **kwargs)\n"

```python
inspect.getsource(mult)
```

    "    def inner(*args, **kwargs):\n        nonlocal count\n        count += 1\n        print('Function {0} was called {1} times'.format(fn.__name__, count))\n        return fn(*args, **kwargs)\n"

Even the signature is gone:

```python
inspect.signature(add)
```

    <Signature (*args, **kwargs)>

```python
inspect.signature(mult)
```

    <Signature (*args, **kwargs)>

Even the parameter defaults documentation is are gone:

```python
inspect.signature(add).parameters
```

    mappingproxy({'args': <Parameter "*args">, 'kwargs': <Parameter "**kwargs">})

In general, when we create decorated functions, we end up "losing" a lot of the metadata of our original function!

However, we **can** put that information back in - it can get quite complicated.

Let's see how we might be able to do that for some simple things, like the docstring and the function name.

```python
def counter(fn):
    count = 0
    
    def inner(*args, **kwargs):
        nonlocal count
        count += 1
        print("{0} was called {1} times".format(fn.__name__, count))
    inner.__name__ = fn.__name__
    inner.__doc__ = fn.__doc__
    return inner
```

```python
@counter
def add(a: int, b: int=10) -> int:
    """
    returns sum of two integers
    """
    return a + b
```

```python
help(add)
```

    Help on function add in module __main__:
    
    add(*args, **kwargs)
        returns sum of two integers

```python
add.__name__
```

    'add'

At least we have the docstring and function name back... But what about the parameters? Our real **add** function takes two positional parameters, but because the closure used a generic way of accepting **\*args** and **\*\*kwargs**, we lose this information

We can use a special function in the **functools** module, called **wraps**. In fact, that function is a decorator itself!

```python
from functools import wraps
```

```python
def counter(fn):
    count = 0
    
    @wraps(fn)
    def inner(*args, **kwargs):
        nonlocal count
        count += 1
        print("{0} was called {1} times".format(fn.__name__, count))

    return inner
```

```python
@counter
def add(a: int, b: int=10) -> int:
    """
    returns sum of two integers
    """
    return a + b
```

```python
help(add)
```

    Help on function add in module __main__:
    
    add(a:int, b:int=10) -> int
        returns sum of two integers
    

Yay!!! Everything is back to normal.

```python
inspect.getsource(add)
```

    '@counter\ndef add(a: int, b: int=10) -> int:\n    """\n    returns sum of two integers\n    """\n    return a + b\n'

```python
inspect.signature(add)
```

    <Signature (a:int, b:int=10) -> int>

```python
inspect.signature(add).parameters
```

    mappingproxy({'a': <Parameter "a:int">, 'b': <Parameter "b:int=10">})

#### 07 - Decorator Application - Timer

Here we go back to an example we have seen in the past - timing how long it takes to run a certain function.

```python
def timed(fn):
    from time import perf_counter
    from functools import wraps
    
    @wraps(fn)
    def inner(*args, **kwargs):
        start = perf_counter()
        result = fn(*args, **kwargs)
        end = perf_counter()
        elapsed = end - start
        
        args_ = [str(a) for a in args]
        kwargs_ = ['{0}={1}'.format(k, v) for (k, v) in kwargs.items()]
        all_args = args_ + kwargs_
        args_str = ','.join(all_args)
        print('{0}({1}) took {2:.6f}s to run.'.format(fn.__name__, 
                                                         args_str,
                                                         elapsed))
        return result
    
    return inner
```

Let's write a function that calculates the n-th Fibonacci number:

`1, 1, 2, 3, 5, 8, ...`

We will implement this using three different methods:
1. recursion
2. a loop
3. functional programming (reduce)

We use a 1-based system, e.g. first Fibonnaci number has index 1, etc.

##### Using Recursion

```python
def calc_recursive_fib(n):
    if n <=2:
        return 1
    else:
        return calc_recursive_fib(n-1) + calc_recursive_fib(n-2)
```

```python
calc_recursive_fib(3)
```

    2

```python
calc_recursive_fib(6)
```

    8

```python
@timed
def fib_recursed(n):
    return calc_recursive_fib(n)
```

```python
fib_recursed(33)
```

    fib_recursed(33) took 1.060477s to run.

    3524578

```python
fib_recursed(34)
```

    fib_recursed(34) took 1.715229s to run.

    5702887

```python
fib_recursed(35)
```

    fib_recursed(35) took 2.773638s to run.

    9227465

There's a reason we did not decorate our recursive function directly!

```python
@timed
def fib_recursed_2(n):
    if n <=2:
        return 1
    else:
        return fib_recursed_2(n-1) + fib_recursed_2(n-2)
```

```python
fib_recursed_2(10)
```

    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000001s to run.
    fib_recursed_2(3) took 0.000409s to run.
    fib_recursed_2(2) took 0.000001s to run.
    fib_recursed_2(4) took 0.000460s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000038s to run.
    fib_recursed_2(5) took 0.000535s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000038s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000075s to run.
    fib_recursed_2(6) took 0.000646s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(2) took 0.000001s to run.
    fib_recursed_2(4) took 0.000071s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000035s to run.
    fib_recursed_2(5) took 0.000143s to run.
    fib_recursed_2(7) took 0.000837s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000001s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000072s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(5) took 0.000142s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000037s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000073s to run.
    fib_recursed_2(6) took 0.000251s to run.
    fib_recursed_2(8) took 0.001125s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000041s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000076s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000035s to run.
    fib_recursed_2(5) took 0.000146s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000001s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000072s to run.
    fib_recursed_2(6) took 0.000253s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000001s to run.
    fib_recursed_2(3) took 0.000048s to run.
    fib_recursed_2(2) took 0.000001s to run.
    fib_recursed_2(4) took 0.000085s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(5) took 0.000156s to run.
    fib_recursed_2(7) took 0.000444s to run.
    fib_recursed_2(9) took 0.001604s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000001s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(2) took 0.000001s to run.
    fib_recursed_2(4) took 0.000071s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(5) took 0.000142s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000071s to run.
    fib_recursed_2(6) took 0.000248s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000040s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000075s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000036s to run.
    fib_recursed_2(5) took 0.000145s to run.
    fib_recursed_2(7) took 0.000429s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000035s to run.
    fib_recursed_2(2) took 0.000001s to run.
    fib_recursed_2(4) took 0.000075s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000035s to run.
    fib_recursed_2(5) took 0.000145s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(1) took 0.000000s to run.
    fib_recursed_2(3) took 0.000041s to run.
    fib_recursed_2(2) took 0.000000s to run.
    fib_recursed_2(4) took 0.000076s to run.
    fib_recursed_2(6) took 0.000256s to run.
    fib_recursed_2(8) took 0.000720s to run.
    fib_recursed_2(10) took 0.002367s to run.

    55

Since we are calling the function recursively, we are actually calling the **decorated** function recursively. In this case I wanted the total time to calculate the n-th number, not the time for each recursion.

You will notice from the above how inefficient the recursive method is: the same fibonacci numbers are calculated repeatedly! This is why as the value of `n` start increasing beyond 30 we start seeing considerable slow downs.

##### Using a Loop

```python
@timed
def fib_loop(n):
    fib_1 = 1
    fib_2 = 1
    for i in range(3, n+1):
        fib_1, fib_2 = fib_2, fib_1 + fib_2
    return fib_2               
```

```python
fib_loop(3)
```

    fib_loop(3) took 0.000003s to run.

    2

```python
fib_loop(6)
```

    fib_loop(6) took 0.000002s to run.

    8

```python
fib_loop(34)
```

    fib_loop(34) took 0.000004s to run.

    5702887

```python
fib_loop(35)
```

    fib_loop(35) took 0.000005s to run.

    9227465

As you can see this method is much more efficient!

##### Using  Reduce

We first need to understand how we are going to calculate the Fibonnaci sequence using reduce: 

<pre>
n=1:
(1, 0) --> (1, 1)

n=2:
(1, 0) --> (1, 1) --> (1 + 1, 1) = (2, 1)  : result = 2 

n=3
(1, 0) --> (1, 1) --> (2, 1) --> (2+1, 2) = (3, 2)  : result = 3

n=4
(1, 0) --> (1, 1) --> (2, 1) --> (3, 2) --> (5, 3)  : result = 5
</pre>

In general each step in the reduction is as follows:

<pre>
previous value = (a, b)
new value = (a+b, a)
</pre>

If we start our reduction with an initial value of `(1, 0)`, we need to run our "loop" n times.

We therefore use a "dummy" sequence of length `n` to create `n` steps in our reduce.

```python
from functools import reduce

@timed
def fib_reduce(n):
    initial = (1, 0)
    dummy = range(n-1)
    fib_n = reduce(lambda prev, n: (prev[0] + prev[1], prev[0]), 
                   dummy, 
                   initial)
    return fib_n[0]                  
```

```python
fib_reduce(3)
```

    fib_reduce(3) took 0.000004s to run.

    2

```python
fib_reduce(6)
```

    fib_reduce(6) took 0.000005s to run.

    8

```python
fib_reduce(34)
```

    fib_reduce(34) took 0.000013s to run.

    5702887

```python
fib_reduce(35)
```

    fib_reduce(35) took 0.000014s to run.

    9227465

Now we can run a quick comparison between the various timed implementations:

```python
fib_recursed(35)
fib_loop(35)
fib_reduce(35)
```

    fib_recursed(35) took 2.771373s to run.
    fib_loop(35) took 0.000007s to run.
    fib_reduce(35) took 0.000013s to run.

    9227465

Even though the recursive algorithm is by far the easiest to understand, it is also the slowest. We'll see how to fix this in an upcoming video using a technique called **memoization**.

First let's focus on the loop and reduce variants. Our timing is not very effective since we only time a single calculation for each - there could be some variance if we run these tests multiple times:

```python
for i in range(10):
    result =  fib_loop(10000)
```

    fib_loop(10000) took 0.002114s to run.
    fib_loop(10000) took 0.002109s to run.
    fib_loop(10000) took 0.002072s to run.
    fib_loop(10000) took 0.002072s to run.
    fib_loop(10000) took 0.002075s to run.
    fib_loop(10000) took 0.002078s to run.
    fib_loop(10000) took 0.002049s to run.
    fib_loop(10000) took 0.002064s to run.
    fib_loop(10000) took 0.002533s to run.
    fib_loop(10000) took 0.002109s to run.

```python
for i in range(10):
    result = fib_reduce(10000)
```

    fib_reduce(10000) took 0.004234s to run.
    fib_reduce(10000) took 0.003961s to run.
    fib_reduce(10000) took 0.004363s to run.
    fib_reduce(10000) took 0.004459s to run.
    fib_reduce(10000) took 0.003895s to run.
    fib_reduce(10000) took 0.003847s to run.
    fib_reduce(10000) took 0.004342s to run.
    fib_reduce(10000) took 0.003908s to run.
    fib_reduce(10000) took 0.003970s to run.
    fib_reduce(10000) took 0.003970s to run.

In general it is better to time the same function call multiple times and generate and average of the run times.

We'll see in an upcoming video how we can do this from within our decorator.

In the meantime observe that the simple loop approach seems to perform about twice as fast as the reduce approach!!

The moral of this side note is that simply because you **can** do something in  Python using some fancy or cool technique does not mean you **should**!

We technically could write our reduce-based function as a one liner:

```python
from functools import reduce 

fib_1 = timed(lambda n: reduce(lambda prev, n: (prev[0] + prev[1], prev[0]),
                               range(n), 
                               (0, 1))[0])
```

```python
fib_loop(100)
```

    fib_loop(100) took 0.000009s to run.

    354224848179261915075

```python
fib_1(100)
```

    <lambda>(100) took 0.000031s to run.

    354224848179261915075

So yes, it's cool that you can write this using a single line of code, but consider two things here:
1. Is it as efficient as another method?
2. Is the code **readable**?

Code readability is something I cannot emphasize enough. Given similar efficiencies (cpu / memory), give preference to code that is more easily understandable!

Sometimes, if the efficiency is not greatly impacted (or does not matter in absolute terms), I might even give preference to less efficient, but more readable (i.e. understanbdable), code.

But enough of the soapbox already :-)

#### 08 - Decorator Application - Logger, Stacked

In this example we're going to create a utility decorator that will log function calls (to the console, but in practice you would be writing your logs to a file (e.g. using Python's built-in logger), or to a database, etc.

```python
def logged(fn):
    from functools import wraps
    from datetime import datetime, timezone
    
    @wraps(fn)
    def inner(*args, **kwargs):
        run_dt = datetime.now(timezone.utc)
        result = fn(*args, **kwargs)
        print('{0}: called {1}'.format(fn.__name__, run_dt))
        return result
        
    return inner
```

```python
@logged
def func_1():
    pass
```

```python
@logged
def func_2():
    pass
```

```python
func_1()
```

    func_1: called 2017-12-10 00:09:19.443657+00:00

```python
func_2()
```

    func_2: called 2017-12-10 00:09:19.460691+00:00

Now we may additionaly also want to time the function. We can certainly include the code to do so in our `logged` decorator, but we could also just use the `@timed` decorator we already wrote by **stacking** our decorators.

```python
def timed(fn):
    from functools import wraps
    from time import perf_counter
    
    @wraps(fn)
    def inner(*args, **kwargs):
        start = perf_counter()
        result = fn(*args, **kwargs)
        end = perf_counter()
        print('{0} ran for {1:.6f}s'.format(fn.__name__, end-start))
        return result
    
    return inner
```

```python
@timed
@logged
def factorial(n):
    from operator import mul
    from functools import reduce
    
    return reduce(mul, range(1, n+1))
```

```python
factorial(10)
```

    factorial: called 2017-12-10 00:09:19.496762+00:00
    factorial ran for 0.000130s

    3628800

Note that the order in which we stack the decorators can make a difference!

Remember that this is because our stacked decorators essentially amounted to:

```python
def factorial(n):
    from operator import mul
    from functools import reduce
    
    return reduce(mul, range(1, n+1))

factorial = timed(logged(factorial))
```

So in this case the `timed` decorator will be called first, followed by the `logged` decorator.

You may wonder why the printed output seems reversed. Look at how the decorators were defined - they first ran the function passed in, and **then** printed the result.

So in the above example, a simplified look at what happens in each decorator:

* `timed(fn)(*args, **kwargs)`:
    1. calls `fn(*args, **kwargs)`
    2. prints timing
    
    
* `logged(fn)(*args, **kwargs)`:
    1. calls `fn(*args, **kwargs)`
    2. prints log info

So, calling
`factorial = timed(logged(factorial))`

is equivalent to:

<pre>
fn = logged(factorial)
factorial = timed(fn)

factorial(n) --> call timed(fn)(n)
             --> call fn(n), then print timing
             --> call logged(original_factorial)(n), then print timing
             --> call original_factorial(n), then log, then print timing
</pre>

So as you can see, the `timed` decorator ran first, but it called the logged decorated function first, then printed the result - hence why the print output seems reversed.

```python
factorial(10)
```

    factorial: called 2017-12-10 00:09:19.525820+00:00
    factorial ran for 0.000147s

    3628800

But in the following case, the `logged` decorator will run first, followed by the `timed` decorator:

```python
def factorial(n):
    from operator import mul
    from functools import reduce
    
    return reduce(mul, range(1, n+1))

factorial = logged(timed(factorial))
```

```python
factorial(10)
```

    factorial ran for 0.000015s
    factorial: called 2017-12-10 00:09:19.547866+00:00

    3628800

Or, using the **@** notation:

```python
@logged
@timed
def factorial(n):
    from operator import mul
    from functools import reduce
    
    return reduce(mul, range(1, n+1))
```

```python
factorial(10)
```

    factorial ran for 0.000016s
    factorial: called 2017-12-10 00:09:19.572914+00:00

    3628800

```python
@timed
@logged
def factorial(n):
    from operator import mul
    from functools import reduce
    
    return reduce(mul, range(1, n+1))
```

```python
factorial(10)
```

    factorial: called 2017-12-10 00:09:19.608237+00:00
    factorial ran for 0.000153s

    3628800

To make this clearer, let's write two very simple decorators as follows:

```python
def dec_1(fn):
    def inner():
        print('running dec_1')
        return fn()
    return inner
```

```python
def dec_2(fn):
    def inner():
        print('running dec_2')
        return fn()
    return inner
```

```python
@dec_1
@dec_2
def my_func():
    print('running my_func')
```

```python
my_func()
```

    running dec_1
    running dec_2
    running my_func

But if we change the order of the decorators:

```python
@dec_2
@dec_1
def my_func():
    print('running my_func')
```

```python
my_func()
```

    running dec_2
    running dec_1
    running my_func

You may wonder whether this really matters in practice. And yes, it can.

Consider an API that contains various functions that can be called. However, endpoints are secured and can only be run by authenticated users who have some specific role(s). If they do not have the role you want to return an unauthorized error. But if they do, then you want to log that they called the endpoint.

In this case you may have one decorator that is used to check authentication and permissions (and immediately return an unauthorized error from the API if applicable), and the other to log the call. 

If you decorated it this way:

<pre>
@log
@authorize
def my_endpoint():
    pass
</pre>

then the call would always be logged.

But, in this instance:

<pre>
@authorize
@log
def my_endpoint():
    pass
</pre>

your endpoint would only get logged if the user passed the `authorize` test.

#### 09 - Decorator Application - Memoization

Let's go back to our Fibonacci example:

```python
def fib(n):
    print ('Calculating fib({0})'.format(n))
    return 1 if n < 3 else fib(n-1) + fib(n-2)
```

When we run this, we see that it is quite inefficient, as the same Fibonacci numbers get calculated multiple times:

```python
fib(6)
```

    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)
    Calculating fib(2)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)
    Calculating fib(4)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)
    Calculating fib(2)

    8

It would be better if we could somehow "store" these results, so if we have calculated `fib(4)` and `fib(3)` before, we could simply recall the these values when calculating `fib(5) = fib(4) + fib(3)` instead of recalculating them.

This concept of improving the efficiency of our code by caching pre-calculated values so they do not need to be re-calcualted every time, is called "memoization"

We can approach this using a simple class and a dictionary that stores any Fibonacci number that's already been calculated:

```python
class Fib:
    def __init__(self):
        self.cache = {1: 1, 2: 1}
    
    def fib(self, n):
        if n not in self.cache:
            print('Calculating fib({0})'.format(n))
            self.cache[n] = self.fib(n-1) + self.fib(n-2)
        return self.cache[n]
```

```python
f = Fib()
```

```python
f.fib(1)
```

    1

```python
f.fib(6)
```

    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)

    8

```python
f.fib(7)
```

    Calculating fib(7)

    13

Let's see how we could rewrite this using a closure:

```python
def fib():
    cache = {1: 1, 2: 2}
    
    def calc_fib(n):
        if n not in cache:
            print('Calculating fib({0})'.format(n))
            cache[n] = calc_fib(n-1) + calc_fib(n-2)
        return cache[n]
    
    return calc_fib
```

```python
f = fib()
```

```python
f(10)
```

    Calculating fib(10)
    Calculating fib(9)
    Calculating fib(8)
    Calculating fib(7)
    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)

    89

Now let's see how we would implement this using a decorator:

```python
from functools import wraps

def memoize_fib(fn):
    cache = dict()
    
    @wraps(fn)
    def inner(n):
        if n not in cache:
            cache[n] = fn(n)
        return cache[n]
    
    return inner
```

```python
@memoize_fib
def fib(n):
    print ('Calculating fib({0})'.format(n))
    return 1 if n < 3 else fib(n-1) + fib(n-2)
```

```python
fib(3)
```

    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)

    2

```python
fib(10)
```

    Calculating fib(10)
    Calculating fib(9)
    Calculating fib(8)
    Calculating fib(7)
    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)

    55

```python
fib(6)
```

    8

As you can see, we are hitting the cache when the values are available.

Now, we made our memoization decorator "hardcoded" to single argument functions - we could make it more generic.

For example, to handle an arbitrary number of positional arguments and keyword-only arguments we could do the following:

```python
def memoize(fn):
    cache = dict()
    
    @wraps(fn)
    def inner(*args):
        if args not in cache:
            cache[args] = fn(*args)
        return cache[args]
    
    return inner
```

```python
@memoize
def fib(n):
    print ('Calculating fib({0})'.format(n))
    return 1 if n < 3 else fib(n-1) + fib(n-2)
```

```python
fib(6)
```

    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)

    8

```python
fib(7)
```

    Calculating fib(7)

    13

Of course, with this rather generic memoization decorator we can memoize other functions too:

```python
def fact(n):
    print('Calculating {0}!'.format(n))
    return 1 if n < 2 else n * fact(n-1)
```

```python
fact(5)
```

    Calculating 5!
    Calculating 4!
    Calculating 3!
    Calculating 2!
    Calculating 1!

    120

```python
fact(5)
```

    Calculating 5!
    Calculating 4!
    Calculating 3!
    Calculating 2!
    Calculating 1!

    120

And memoizing it:

```python
@memoize
def fact(n):
    print('Calculating {0}!'.format(n))
    return 1 if n < 2 else n * fact(n-1)
```

```python
fact(6)
```

    Calculating 6!
    Calculating 5!
    Calculating 4!
    Calculating 3!
    Calculating 2!
    Calculating 1!

    720

```python
fact(6)
```

    720

Our simple memoizer has a drawback however:
* the cache size is unbounded - probably not a good thing! In general we want to limit the cache to a certain number of entries, balancing computational efficiency vs memory utilization.
* we are not handling **kwargs

Memoization is such a common thing to do that Python actually has a memoization decorator built for us!

It's in the, you guessed it, **functools** module, and is called **lru_cache** and is going to be quite a bit more efficient compared to the rudimentary memoization example we did above.

[LRU Cache = Least Recently Used caching: since the cache is not unlimited, at some point cached entries need to be discarded, and the least recently used entries are discarded first]

```python
from functools import lru_cache
```

```python
@lru_cache()
def fact(n):
    print("Calculating fact({0})".format(n))
    return 1 if n < 2 else n * fact(n-1)
```

```python
fact(5)
```

    Calculating fact(5)
    Calculating fact(4)
    Calculating fact(3)
    Calculating fact(2)
    Calculating fact(1)

    120

```python
fact(4)
```

    24

As you can see, `fact(4)` was returned via a cached entry!

Same thing with our Fibonacci function:

```python
@lru_cache()
def fib(n):
    print("Calculating fib({0})".format(n))
    return 1 if n < 3 else fib(n-1) + fib(n-2)
```

```python
fib(6)
```

    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)

    8

```python
fib(5)
```

    5

Recall from a few videos back that we timed the calculation for Fibonacci numbers. Calculating fib(35) took several seconds - every time...

```python
from time import perf_counter
```

```python
def fib_no_memo(n):
    return 1 if n < 3 else fib_no_memo(n-1) + fib_no_memo(n-2)
```

```python
start = perf_counter()
result = fib_no_memo(35)
print("result={0}, elapsed: {1}s".format(result, perf_counter() - start))
```

    result=9227465, elapsed: 2.939012289158911s

```python
@lru_cache()
def fib_memo(n):
    return 1 if n < 3 else fib_memo(n-1) + fib_memo(n-2)
```

```python
start = perf_counter()
result = fib_memo(35)
print("result={0}, elapsed: {1}s".format(result, perf_counter() - start))
```

    result=9227465, elapsed: 9.83349429017899e-05s

And if we make the calls again:

```python
start = perf_counter()
result = fib_no_memo(35)
print("result={0}, elapsed: {1}s".format(result, perf_counter() - start))
```

    result=9227465, elapsed: 2.782454120518548s

```python
start = perf_counter()
result = fib_memo(35)
print("result={0}, elapsed: {1}s".format(result, perf_counter() - start))
```

    result=9227465, elapsed: 5.6617088337596044e-05s

You may have noticed that the `lru_cache` decorator was implemented using `()` - we'll see more on this later, but that's because decorators can themselves have parameters (beyond the function being decorated).

One of the arguments to the `lru_cache` decorator is the size of the cache - it defaults to 128 items, but we can easily change this - for performance reasons use powers of 2 for the cache size (or None for unbounded cache):

```python
@lru_cache(maxsize=8)
def fib(n):
    print("Calculating fib({0})".format(n))
    return 1 if n < 3 else fib(n-1) + fib(n-2)
```

```python
fib(10)
```

    Calculating fib(10)
    Calculating fib(9)
    Calculating fib(8)
    Calculating fib(7)
    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)

    55

```python
fib(20)
```

    Calculating fib(20)
    Calculating fib(19)
    Calculating fib(18)
    Calculating fib(17)
    Calculating fib(16)
    Calculating fib(15)
    Calculating fib(14)
    Calculating fib(13)
    Calculating fib(12)
    Calculating fib(11)

    6765

```python
fib(10)
```

    Calculating fib(10)
    Calculating fib(9)
    Calculating fib(8)
    Calculating fib(7)
    Calculating fib(6)
    Calculating fib(5)
    Calculating fib(4)
    Calculating fib(3)
    Calculating fib(2)
    Calculating fib(1)

    55

You'll not how Python had to recalculate `fib` for `10, 9,` etc. This is because the cache can only contain 10 items, so when we calculated `fib(20)`, it stored fib for `20, 19, ..., 11` (10 items) and therefore the oldest items fib `10, 9, ..., 1` were removed from the cache to make space.

#### 10 - Decorators - Part 2

We have seen how to create some simple and not so simple decorators.

However we have also been using built-in decorators that can accept parameters, such as `wraps` and `lru_cache`.

This can be quite useful and we can accomplish the same thing ourselves.

First recall our original timer decorator from an earlier video (Decorator Application - Timer):

```python
def timed(fn):
    from time import perf_counter
    
    def inner(*args, **kwargs):
        start = perf_counter()
        result = fn(*args, **kwargs)
        end = perf_counter()
        elapsed = end - start
        print('Run time: {0:.6f}s'.format(elapsed))
        return result
    
    return inner
```

```python
def calc_fib_recurse(n):
    return 1 if n < 3 else calc_fib_recurse(n-1) + calc_fib_recurse(n-2)

def fib(n):
    return calc_fib_recurse(n)
```

We can decorate our Fibonacci function using the **@** syntax, or the longer syntax as follows:

```python
fib = timed(fib)
```

```python
fib(30)
```

    Run time: 0.255260s

    832040

Let's modify this so the timer runs the function multiple times and calculates the average run time:

```python
def timed(fn):
    from time import perf_counter

    def inner(*args, **kwargs):
        total_elapsed = 0
        for i in range(10):
            start = perf_counter()
            result = fn(*args, **kwargs)
            end = perf_counter()
            total_elapsed += (perf_counter() - start)
        avg_elapsed = total_elapsed / 10
        print('Avg Run time: {0:.6f}s'.format(avg_elapsed))
        return result
    
    return inner
```

And again we decorate it using the long syntax:

```python
def fib(n):
    return calc_fib_recurse(n)

fib = timed(fib)
```

```python
fib(28)
```

    Avg Run time: 0.098860s

    317811

But that value of 10 has been hardcoded. Let's make it a parameter instead.

```python
def timed(fn, num_reps):
    from time import perf_counter
    
    def inner(*args, **kwargs):
        total_elapsed = 0
        for i in range(num_reps):
            start = perf_counter()
            result = fn(*args, **kwargs)
            end = perf_counter()
            total_elapsed += (perf_counter() - start)
        avg_elapsed = total_elapsed / num_reps
        print('Avg Run time: {0:.6f}s ({1} reps)'.format(avg_elapsed,
                                                        num_reps))
        return result
    
    return inner
```

Now to decorate our Fibonacci function we **have** to use the long syntax (as we saw in the lecture, the **@** syntax will not work):

```python
def fib(n):
    return calc_fib_recurse(n)

fib = timed(fib, 5)
```

```python
fib(28)
```

    Avg Run time: 0.095708s (5 reps)

    317811

The problem is that we cannot use the `@` decorator syntax because when using that syntax Python passes a **single** argument to the decorator: the function we are decorating - nothing else.

Of course we could just use what we did above, but the decorator syntax is kind of neat, so it would be nice to retain the ability to use it.

We just need to change our thinking a little bit to do this:

First, when we see the following syntax:

`
@dec
def my_func():
    pass
`

we see that `dec` must be a function that takes a single argument, the function being decorated.

You'll note that `dec` is just a function, but we do not **call** `dec` when we decorate `my_func`, we simply use the label `dec`.

Then Python does:

`
my_func = dec(my_func)
`

Let's try a concrete example:

```python
def dec(fn):
    print ("running dec")
    
    def inner(*args, **kwargs):
        print("running inner")
        return fn(*args, **kwargs)
              
    return inner
```

```python
@dec
def my_func():
    print('running my_func')
```

    running dec

As we can see, when we decorated `my_func`, the `dec` function was **called** at that time.

(Because Python did this: 

`my_func = dec(my_func)` 

so `dec` was called)

And when we now call `my_func`, we see that the `inner` function is called, followed by the original `my_func`

```python
my_func()
```

    running inner
    running my_func

But what if `dec` was not the decorator itself, but instead created and returned a decorator?

Let's see how we might do this:

```python
def dec_factory():
    print('running dec_factory')
    def dec(fn):
        print('running dec')
        def inner(*args, **kwargs):
            print('running inner')
            return fn(*args, **kwargs)
        return inner
    return dec
```

So as you can see, calling `dec_generator()` will return that `dec` function which is our decorator:

```python
@dec_factory()
def my_func(a, b):
    print(a, b)
```

    running dec_factory
    running dec

You can see that both `dec_generator` and `dec` were already called.

```python
my_func(10, 20)
```

    running inner
    10 20

And there you go, all we did is basically create a decorator by calling a function (`dec_factory`) and use the return value of that call (the `dec` function) as our actual decorator.

We could have done the decoration this way too:

```python
dec = dec_factory()
```

    running dec_factory

```python
@dec
def my_func():
    print('running my_func')
```

    running dec

```python
my_func()
```

    running inner
    running my_func

Or even this way:

```python
dec = dec_factory()

def my_func():
    print('running my_func')

my_func = dec(my_func)
```

    running dec_factory
    running dec

```python
my_func()
```

    running inner
    running my_func

Of course we could even decorate it this way using a single statement:

```python
def my_func():
    print('running my_func')

my_func = dec_factory()(my_func)
```

    running dec_factory
    running dec

```python
my_func()
```

    running inner
    running my_func

OK, so now we have decorated our function using, not a decorator, but a decorator factory as follows:

```python
def dec_factory():
    def dec(fn):
        def inner(*args, **kwargs):
            print('running decorator inner')
            return fn(*args, **kwargs)
        return inner
    return dec
```

```python
@dec_factory()
def my_func(a, b):
    return a + b
```

```python
my_func(10, 20)
```

    running decorator inner

    30

You should note that in this approach, we are **calling** `dec_factory()`, [note the parentheses `()`], and **then** using the return value (a decorator) to decorate our function.

So, we could pass arguments as we do so without affecting the final outcome. In fact we can even access them from anywhere inside `dec_factory`, including any of the nested functions! 

Let's try this:

```python
def dec_factory(a, b):
    def dec(fn):
        def inner(*args, **kwargs):
            print('running decorator inner')
            print('free vars: ', a, b)  # a and b are free variables!
            return fn(*args, **kwargs)
        return inner
    return dec
```

```python
@dec_factory(10, 20)
def my_func():
    print('python rocks')
```

```python
my_func()
```

    running decorator inner
    free vars:  10 20
    python rocks

And this is how we can create decorators with parameters. We do not directly create a decorator, instead we use an outer function that returns a decorator when called, and pass arguments to that outer function, which the decorator and its inner function can of course access as nonlocal (free) variables.

So now, let's go back to our original problem where we wanted our timing decorator to run a number of loops which could be specified as a parameter when decorating the function we want to time.

Here it is again:

```python
def timed(fn, num_reps):
    from time import perf_counter
    
    def inner(*args, **kwargs):
        total_elapsed = 0
        for i in range(num_reps):
            start = perf_counter()
            result = fn(*args, **kwargs)
            end = perf_counter()
            total_elapsed += (perf_counter() - start)
        avg_elapsed = total_elapsed / num_reps
        print('Avg Run time: {0:.6f}s ({1} reps)'.format(avg_elapsed,
                                                        num_reps))
        return result
    
    return inner
```

So, all we need to do is create an outer function around our timed decorator, and pass the `num_reps` argument to that outer function instead:

```python
def timed_factory(num_reps=1):
    def timed(fn):
        from time import perf_counter

        def inner(*args, **kwargs):
            total_elapsed = 0
            for i in range(num_reps):
                start = perf_counter()
                result = fn(*args, **kwargs)
                end = perf_counter()
                total_elapsed += (perf_counter() - start)
            avg_elapsed = total_elapsed / num_reps
            print('Avg Run time: {0:.6f}s ({1} reps)'.format(avg_elapsed,
                                                            num_reps))
            return result
        return inner
    return timed    
```

```python
@timed_factory(5)
def fib(n):
    return calc_fib_recurse(n)
```

```python
fib(30)
```

    Avg Run time: 0.249934s (5 reps)

    832040

Just to put the finishing touch on this, we probably don't want to have our outer function named the way it is (`timed_factory`). Instead we probably just want to call it `timed`. So lets just do this final part:

```python
from functools import wraps

def timed(num_reps=1):
    def decorator(fn):
        from time import perf_counter

        @wraps(fn)
        def inner(*args, **kwargs):
            total_elapsed = 0
            for i in range(num_reps):
                start = perf_counter()
                result = fn(*args, **kwargs)
                end = perf_counter()
                total_elapsed += (perf_counter() - start)
            avg_elapsed = total_elapsed / num_reps
            print('Avg Run time: {0:.6f}s ({1} reps)'.format(avg_elapsed,
                                                            num_reps))
            return result
        return inner
    return decorator  
```

```python
@timed(5)
def fib(n):
    return calc_fib_recurse(n)
```

```python
fib(30)
```

    Avg Run time: 0.253744s (5 reps)

    832040

##### RECAP:

"So hopefully this explains quite clearly how parameterized decorators work. We don't actually parameterize the decorators. What we do is we create a decorator factory. That has the parameters and then that is able to be referenced from the decorator, so that will now be a closure itself, within the decorator factory. That then gets returned and applied to whatever function we're decorating."



#### 11 - Decorator Application - Decorator Class

If you recall how we wrote a parameterized decorator, we had to write a decorator factory that took in the arguments for our decorator and then returned the decorator (which could reference the arguments as free variables).

Very simply:

```python
def my_dec(a, b):
    def dec(fn):
        def inner(*args, **kwargs):
            print('decorated function called: a={0}, b={1}'.format(a, b))
            return fn(*args, **kwargs)
        return inner
    return dec
```

```python
@my_dec(10, 20)
def my_func(s):
    print('hello {0}'.format(s))
```

```python
my_func('world')
```

    decorated function called: a=10, b=20
    hello world

So, our decorator factory was passed some arguments, and returned a callable which took one single parameter, the function being decorated, but also had access to the arguments passed to the factory.

Now, recall that we can make our class instances callable, simply by implementing the `__call__` method.

Here's a simple example:

```python
class MyClass:
    def __init__(self, a, b):
        self.a = a
        self.b = b
        
    def __call__(self):
        print('MyClass instance called: a={0}, b={1}'.format(self.a, self.b))
```

```python
my_class = MyClass(10, 20)
```

```python
my_class()
```

    MyClass instance called: a=10, b=20

So let's modify this just a bit, and have the `__call__` method be our decorator!

```python
class MyClass:
    def __init__(self, a, b):
        self.a = a
        self.b = b
        
    def __call__(self, fn):
        def inner(*args, **kwargs):
            print('MyClass instance called: a={0}, b={1}'.format(self.a, self.b))
            return fn(*args, **kwargs)
        return inner
```

So, we can decorate our functions this way:

```python
@MyClass(10, 20)
def my_func(s):
    print('Hello {0}!'.format(s))
```

Remember that `@MyClass(10, 20)` returned an object of type `MyClass`. But  that object is itself callable, so we could do something like:

``
my_func = MyClass(10, 20)(my_func)
``

or, more simply

``
@MyClass(10, 20)
def my_func(s):
    print(s)
``

```python
my_func('Python')
```

    MyClass instance called: a=10, b=20
    Hello Python!

So as you can see, we can also use callable classes to decorate functions!

#### 12 - Decorator Application (Decorating Classes)

We have so far worked with decorating functions. This means we can decorate functions defined with a `def` statement (we can use the `@` syntax, or the long form). Since class methods are functions, they can be decorated too. Lambda expressions can also be decorated (using the long form).

But if you think about how our decorators work, they take a single parameter, a function, and return some other function - usually a closure that uses the original function that was passed as an argument.

We could use the same concept to accept, not a function, but a class instead. We could reference that class inside our decorator, modify it, and then return that modified class.

First we look at something called **monkey patching**. It boils down to modifying or extending our code at **run time**.

For example we can modify or add attributes to classes at run time. Modules too.

In Python, many of the classes we use can be modified at run time 
(built-ins like strings, lists, and so on, cannot).

But classes written in Python, such as the ones we write, and even library classes, as long as they are written in Python, not C, can. For example `Fraction` in the `fractions` module can be monkey patched.

Just because we can do something however, does not mean we should! Monkey patching can be extremely useful, but don't do it just because you can - as always there should be a real reason to do it, as we'll see in a bit.

Also, in general it is a bad idea to monkey patch the special methods `__???__` (such as `__len__`) as this will often not work due to how these methods are searched for by Python.

```python
from fractions import Fraction
```

```python
Fraction.speak = lambda self: 'This is a late parrot.'
```

```python
f = Fraction(2, 3)
```

```python
f
```

    Fraction(2, 3)

```python
f.speak()
```

    'This is a late parrot.'

Yes, this is obviously nonsense, but you get the idea that you can add attributes to classes even if you do not have direct control over the class, or after your class has been defined.

If you want a more useful method, how about one that tells us if the Fraction is an integral number? (i.e. denominator is `1`)

```python
Fraction.is_integral = lambda self: self.denominator == 1
```

```python
f1 = Fraction(1, 2)
f2 = Fraction(10, 5)
```

```python
f1.is_integral()
```

    False

```python
f2.is_integral()
```

    True

Now, we can make this change to the class by calling a function to do it instead:

```python
def dec_speak(cls):
    cls.speak = lambda self: 'This is a very late parrot.'
    return cls
```

```python
Fraction = dec_speak(Fraction)
```

_(Hopefully the above code reminds you of decorators.)_

```python
f = Fraction(10, 2)
```

```python
f.speak()
```

    'This is a very late parrot.'

We can use that function to decorate our custom classes too, using the short **@** syntax too.

```python
@dec_speak
class Parrot:
    def __init__(self):
        self.state = 'late'
```

```python
polly = Parrot()
```

```python
polly.speak()
```

    'This is a very late parrot.'

Using this technique we could for example add a useful *reciprocal* attribute to the Fraction class, but of course since it would probably be a one time kind of thing (how many Fraction classes are there that you will want to add a reciprocal to after all), there's no need for decorators. Decorators  are useful when they are able to be reused in more general ways.

```python
Fraction.recip = lambda self: Fraction(self.denominator, self.numerator)
```

```python
f = Fraction(2,3)
```

```python
f
```

    Fraction(2, 3)

```python
f.recip()
```

    Fraction(3, 2)

These example are quite trivial, and not very useful. 

So why bring this up? 

Because this same technique can be used for more interesting things.

As a first example, let's say you typically like to inspect various properties of an object for debugging purposes, maybe the memory address, it's current state (property values), and the time at which the debug info was generated.

```python
from datetime import datetime, timezone
```

```python
def debug_info(cls):
    def info(self):
        results = []
        results.append('time: {0}'.format(datetime.now(timezone.utc)))
        results.append('class: {0}'.format(self.__class__.__name__))
        results.append('id: {0}'.format(hex(id(self))))
        
        if vars(self):
            for k, v in vars(self).items():
                results.append('{0}: {1}'.format(k, v))
        
        # we have not covered lists, the extend method and generators,
        # but note that a more Pythonic way to do this would be:
        #if vars(self):
        #    results.extend('{0}: {1}'.format(k, v) 
        #                   for k, v in vars(self).items())
        
        return results
    
    cls.debug = info
    
    return cls
```

```python
@debug_info
class Person:
    def __init__(self, name, birth_year):
        self.name = name
        self.birth_year = birth_year
        
    def say_hi():
        return 'Hello there!'
```

```python
p1 = Person('John', 1939)
```

```python
p1.debug()
```

    ['time: 2018-02-09 04:44:02.893951+00:00',
     'class: Person',
     'id: 0x2dfe29a4630',
     'name: John',
     'birth_year: 1939']

And of course we can decorate other classes this way too, not just a single class:

```python
@debug_info
class Automobile:
    def __init__(self, make, model, year, top_speed_mph):
        self.make = make
        self.model = model
        self.year = year
        self.top_speed_mph = top_speed_mph
        self.current_speed = 0
    
    @property
    def speed(self):
        return self.current_speed
    
    @speed.setter
    def speed(self, new_speed):
        self.current_speed = new_speed
```

```python
s = Automobile('Ford', 'Model T', 1908, 45)
```

```python
s.debug()
```

    ['time: 2018-02-09 04:44:03.562898+00:00',
     'class: Automobile',
     'id: 0x2dfe29b3a58',
     'make: Ford',
     'model: Model T',
     'year: 1908',
     'top_speed_mph: 45',
     'current_speed: 0']

```python
s.speed = 20
```

```python
s.debug()
```

    ['time: 2018-02-09 04:44:03.898085+00:00',
     'class: Automobile',
     'id: 0x2dfe29b3a58',
     'make: Ford',
     'model: Model T',
     'year: 1908',
     'top_speed_mph: 45',
     'current_speed: 20']

Let's look at another example where decorating an entire class could be useful.

```python
from math import sqrt
```

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    def __abs__(self):
        return sqrt(self.x**2 + self.y**2)
    
    def __repr__(self):
        return 'Point({0},{1})'.format(self.x, self.y)
```

```python
p1, p2, p3 = Point(2, 3), Point(2, 3), Point(0,0)
```

```python
abs(p1)
```

    3.605551275463989

```python
p1, p2
```

    (Point(2,3), Point(2,3))

```python
p1 == p2
```

    False

Hmm, we probably would have expected `p1` to be equal to `p2` since it has the same coordinates. But by default Python will compare memory addresses, since our class does not implement the `__eq__` method used for `==` comparisons.

```python
p2, p3
```

    (Point(2,3), Point(0,0))

```python
p2 > p3
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-38-b46639986960> in <module>()
    ----> 1 p2 > p3
    

    TypeError: '>' not supported between instances of 'Point' and 'Point'

So, that class does not support the comparison operators such as `<`, `<=`, etc. 

Even `==` does not work as expected - it will use the memory address instead of using a comparison of the `x` and `y` coordinates as we might probably expect.

For the `<` operator, we need our class to implement the `__lt__` method, and for `==` we need the `__eq__` method.

Other comparison operators are supported by implementing a variety of functions such as `__le__` (`<=`), `__gt__` (`>`), `__ge__` (`>=`).

We are going to add the `__lt__` and `__eq__` methods to our Point class.

We will consider a Point object to be smaller than another one if it is closer to the origin (i.e. smaller magnitude).

```python
del Point

class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    def __abs__(self):
        return sqrt(self.x**2 + self.y**2)
    
    def __eq__(self, other):
        if isinstance(other, Point):
            return self.x == other.x and self.y == other.y
        else:
            return NotImplemented
            
    def __lt__(self, other):
        if isinstance(other, Point):
            return abs(self) < abs(other)
        else:
            return NotImplemented
        
    def __repr__(self):
        return '{0}({1},{2})'.format(self.__class__.__name__, self.x, self.y)
```

```python
p1, p2, p3 = Point(2, 3), Point(2, 3), Point(0,0)
```

```python
p1, p2, p1==p2
```

    (Point(2,3), Point(2,3), True)

```python
p2, p3, p2==p3
```

    (Point(2,3), Point(0,0), False)

As we can see, `==` now works as expected

```python
p4 = Point(1, 2)
```

```python
abs(p1), abs(p4), p1 < p4
```

    (3.605551275463989, 2.23606797749979, False)

Great, so now we have `<` and `==` implemented. What about the rest of the operators: `<=`, `>`, `>=`?

```python
p1 > p4
```

    True

Ooh, since we have implemented `<` and `==`, does this mean Python magically implemented a `>` operator (i.e. not < and not ==)?

Not exactly! What happened is that since `p1` and `p4` are both points, running the comparison `p1 > p4` is really the same as evaluating `p4 < p1` - and Python did do that automatically for us.

But it has not implemented any of the others, such as `>=` and `<=`:

```python
p1 <= p4
```

    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-46-80f9ea228203> in <module>()
    ----> 1 p1 <= p4
    

    TypeError: '<=' not supported between instances of 'Point' and 'Point'

Now, although we could proceed in a similar way and define `>=`, `<=` and `>` using the same technique, observe that if `<` and `==` is defined then:

* `a <= b` iff `a < b or a == b`
* `a > b` iff `not(a<b) and a != b`
* `a >= b` iff `not(a<b)`

So, to be quite generic we could create a decorator that will implement these last three operators as long as `==` and `<` are defined. We could then decorate **any** class that implements just those two operators.

```python
def complete_ordering(cls):
    if '__eq__' in dir(cls) and '__lt__' in dir(cls):
        cls.__le__ = lambda self, other: self < other or self == other
        cls.__gt__ = lambda self, other: not(self < other) and not (self == other)
        cls.__ge__ = lambda self, other: not (self < other)
    return cls
```

In reality, the code above is **NOT** a good implementation at all. We are not checking that the types are compatible and returning a `NotImplemented` result if appropriate. I am also using inline operators (`<` and `==`) instead of the dunder functions (`__lt__` and `__eq__`). I just kept it simple because we'll use a better alternative in a bit.

For example, a better way to implement `__ge__` would be as follows:

```python
def ge_from_lt(self, other):
    # self >= other iff not(other < self)
    result = self.__lt__(other)
    if result is NotImplemented:
        return NotImplemented
    else:
        return not result
```

You may be wondering why I used `__lt__` instead of just using the `<` operator. This is because I want to actually look at the result of the operation without raising an exception if the operation is not implemented. The way I have the total ordering decorator implemented could cause an infinite loop because when I evaluate `self < other`, if an exception is raised, Python will reflect the evaluation to `other > self`, and if that raises an error as well, Python will try to reflect that operation too, and we get into an infinite loop (which eventually terminates in a stack overflow). This was actually a bug in Python's standard library implementation of a `complete_ordering` decorator (called `total_ordering`) that was resolved in 3.4.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    def __abs__(self):
        return sqrt(self.x**2 + self.y**2)
    
    def __eq__(self, other):
        if isinstance(other, Point):
            return self.x == other.x and self.y == other.y
        else:
            return NotImplemented
            
    def __lt__(self, other):
        if isinstance(other, Point):
            return abs(self) < abs(other)
        else:
            return NotImplemented
        
    def __repr__(self):
        return '{0}({1},{2})'.format(self.__class__, self.x, self.y)
```

```python
Point = complete_ordering(Point)        
```

```python
p1, p2, p3 = Point(1, 1), Point(3, 4), Point(3, 4)
```

```python
abs(p1), abs(p2), abs(p3)
```

    (1.4142135623730951, 5.0, 5.0)

```python
p1 < p2, p1 <= p2, p1 > p2, p1 >= p2, p2 > p2, p2 >= p3
```

    (True, True, False, False, False, True)

Now the `complete_ordering` decorator can also be directly applied to any class that defines `__eq__` and `__lt__`.

```python
@complete_ordering
class Grade:
    def __init__(self, score, max_score):
        self.score = score
        self.max_score = max_score
        self.score_percent = round(score / max_score * 100)
     
    def __repr__(self):
        return 'Grade({0}, {1})'.format(self.score, self.max_score)
    
    def __eq__(self, other):
        if isinstance(other, Grade):
            return self.score_percent == other.score_percent
        else:
            return NotImplemented
    
    def __lt__(self, other):
        if isinstance(other, Grade):
            return self.score_percent < other.score_percent
        else:
            return NotImplemented
        
```

```python
g1 = Grade(10, 100)
g2 = Grade(20, 30)
g3 = Grade(5, 50)
```

```python
g1 <= g2, g1 == g3, g2 > g3
```

    (True, True, True)

Often, given the `==` operator and just **one** of the other comparison operators (`<`, `<=`, `>`, `>=`), then all the rest can be derived.

Our decorator insisted on `==` and `<`. but we could make it better by insisting on `==` and any one of the other operators. This will of course make our decorator more complicated, and in fact, Python has this precise functionality built in to the, you guessed it, `functools` module!

It is a decorator called `total_ordering`. 

Let's see it in action:

```python
from functools import total_ordering
```

```python
@total_ordering
class Grade:
    def __init__(self, score, max_score):
        self.score = score
        self.max_score = max_score
        self.score_percent = round(score / max_score * 100)
     
    def __repr__(self):
        return 'Grade({0}, {1})'.format(self.score, self.max_score)
    
    def __eq__(self, other):
        if isinstance(other, Grade):
            return self.score_percent == other.score_percent
        else:
            return NotImplemented
    
    def __lt__(self, other):
        if isinstance(other, Grade):
            return self.score_percent < other.score_percent
        else:
            return NotImplemented
```

```python
g1, g2 = Grade(80, 100), Grade(60, 100)
```

```python
g1 >= g2, g1 > g2
```

    (True, True)

Or we could also do it this way:

```python
@total_ordering
class Grade:
    def __init__(self, score, max_score):
        self.score = score
        self.max_score = max_score
        self.score_percent = round(score / max_score * 100)
     
    def __repr__(self):
        return 'Grade({0}, {1})'.format(self.score, self.max_score)
    
    def __eq__(self, other):
        if isinstance(other, Grade):
            return self.score_percent == other.score_percent
        else:
            return NotImplemented
    
    def __gt__(self, other):
        if isinstance(other, Grade):
            return self.score_percent > other.score_percent
        else:
            return NotImplemented
```

```python
g1, g2 = Grade(80, 100), Grade(60, 100)
```

```python
g1 >= g2, g1 > g2, g1 <= g2, g1 < g2
```

    (True, True, False, False)

#### 13 - Decorator Application - Single Dispatch

Consider an application where we want to provide similar functionality but that varies slightly depending on the argument types passed in.

In this set of examples we consider this problem where functionality differs based on a single argument's type (hence single dispatch) instead of the type of multiple arguments (which would be multi dispatch)

If you have a background in some other OO languages such as Java or C#, you'll know that we can easily do something like this by basically **overloading** functions: using a different data type for the function parameter, hence changing the function signature. Then although the name of the function is the same, calling `do_something(100)` and `do_something('java')` would call a different function, the first one would call the `do_something(int)` function, and the second would call the `do_something(String)` function.

Of course, Python is not statically typed, so even if Python had function overloading built-in, we would not be able to make such a distinction in our function signatures since there is nothing that says that a parameter must be of a specific type, so in a best case scenario we would have to "distinguish" functions with the same name only by the number of parameters they take. And then we'd have to somehow deal with variable numbers of positional and keyword arguments too... Uuugh!
In any event, single dispatch could never work.

Instead we have to come up with a different solution.

Let's say we want to display various data types in html format, with different presentations for integers (we want both base 10 and hex values), floats (we always want it rounded to 2 decimal points), strings (we want the string html-escaped, and all newline characters replaced by `<br/>`), lists and tuples should be implemented using bulleted lists, and the same with dictionaries except we want the name/value pair to be displayed in the bulleted list.

For starters, let's just implement individual functions to do each of those things.

I am going to keep the functions very simple, but in practice you should handle situations like None objects, empty lists and dictionaries, possibly the wrong type being passed to the function, etc.

```python
from html import escape

def html_escape(arg):
    return escape(str(arg))
                      
def html_int(a):
    return '{0}(<i>{1}</i)'.format(a, str(hex(a)))

def html_real(a):
    return '{0:.2f}'.format(round(a, 2))
                                  
def html_str(s):
    return html_escape(s).replace('\n', '<br/>\n')
                                  
def html_list(l):
    items = ('<li>{0}</li>'.format(html_escape(item)) 
             for item in l)
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
                                  
def html_dict(d):
    items = ('<li>{0}={1}</li>'.format(html_escape(k), html_escape(v)) 
             for k, v in d.items())    
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
```

```python
print(html_str("""this is 
a multi line string
with special characters: 10 < 100"""))
```

    this is <br/>
    a multi line string<br/>
    with special characters: 10 &lt; 100

```python
print(html_int(255))
```

    255(<i>0xff</i)

```python
print(html_escape(3+10j))
```

    (3+10j)

Ideally we would want to just have to call a single function, maybe `htmlize` that would figure out which particular flavor of the `html_xxx` function to call depending on the argument type.

We could try it as follows:

```python
from decimal import Decimal

def htmlize(arg):
    if isinstance(arg, int):
        return html_int(arg)
    elif isinstance(arg, float) or isinstance(arg, Decimal):
        return html_real(arg)
    elif isinstance(arg, str):
        return html_str(arg)
    elif isinstance(arg, list) or isinstance(arg, tuple):
        return html_list(arg)
    elif isinstance(arg, dict):
        return html_dict(arg)
    else:
        # default behavior - just html escape string representation
        return html_escape(str(arg))
```

Now we can essentially use the same function call to handle different types - the `htmlize` function is a dispatcher - it dispatches the request to a different function based on the argument type. (There's a much better way to do some of this, but we'll have to wait until we cover abstract base classes to do so).

```python
print(htmlize([1, 2, 3]))
```

    <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    </ul>

```python
print(htmlize(dict(key1=1, key2=2)))
```

    <ul>
    <li>key1=1</li>
    <li>key2=2</li>
    </ul>

```python
print(htmlize(255))
```

    255(<i>0xff</i)

But there are a number of shortcomings here:

```python
print(htmlize(["""first element is 
a multi-line string""", (1, 2, 3)]))
```

    <ul>
    <li>first element is 
    a multi-line string</li>
    <li>(1, 2, 3)</li>
    </ul>

As you can see, the multi-line string did not get the newline characters replaced, the tuple was not rendered as an html list, and the integers do not have their hex representation.

So we just need to redefine the `html_list` and `html_dict` functions to use the `htmlize` function:

```python
def html_list(l):
    items = ['<li>{0}</li>'.format(htmlize(item)) for item in l]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
```

```python
def html_dict(d):
    items = ['<li>{0}={1}</li>'.format(html_escape(k), htmlize(v)) for k, v in d.items()]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
```

```python
print(htmlize(["""first element is 
a multi-line string""", (1, 2, 3)]))
```

    <ul>
    <li>first element is <br/>
    a multi-line string</li>
    <li><ul>
    <li>1(<i>0x1</i)</li>
    <li>2(<i>0x2</i)</li>
    <li>3(<i>0x3</i)</li>
    </ul></li>
    </ul>

Much better, but hopefully you spotted something that might seem problematic!

Do we not have a circular reference?

In order to define `html_list` and `html_dict` we needed to call `htmlize`, but in order to define `htmlize` we needed to call `html_list` and `html_dict`.

Remember that in Python we can reference a function **inside** the body of another function **before** the function has been defined, as long as by the time we **call** the first function, the second one has been defined. SO this is actually OK.

If you don't believe me and want to make sure of this yourself, go ahead and reset your Kernel (click on the Kernel | Restart menu option), and run the following code without running anything prior to this.

The `htmlize` function body makes calls to other functions such as `html_escape`, `html_int`, etc that have not actually been defined yet

```python
from html import escape
from decimal import Decimal

def htmlize(arg):
    if isinstance(arg, int):
        return html_int(arg)
    elif isinstance(arg, float) or isinstance(arg, Decimal):
        return html_real(arg)
    elif isinstance(arg, str):
        return html_str(arg)
    elif isinstance(arg, list) or isinstance(arg, tuple) or isinstance(arg, set):
        return html_list(arg)
    elif isinstance(arg, dict):
        return html_dict(arg)
    else:
        # default behavior - just html escape string representation
        return html_escape(str(arg))
```

Now we define all the functions that `htmlize` uses before we actually call `htmlize` and all is good:

```python
def html_escape(arg):
    return escape(str(arg))
                      
def html_int(a):
    return '{0}(<i>{1}</i)'.format(a, str(hex(a)))

def html_real(a):
    return '{0:.2f}'.format(round(a, 2))
                                  
def html_str(s):
    return html_escape(s).replace('\n', '<br/>\n')
                                  
def html_list(l):
    items = ['<li>{0}</li>'.format(htmlize(item)) for item in l]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
                                  
def html_dict(d):
    items = ['<li>{0}={1}</li>'.format(html_escape(k), htmlize(v)) for k, v in d.items()]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
```

```python
print(htmlize(["""first element is 
a multi-line string""", (1, 2, 3)]))
```

    <ul>
    <li>first element is <br/>
    a multi-line string</li>
    <li><ul>
    <li>1(<i>0x1</i)</li>
    <li>2(<i>0x2</i)</li>
    <li>3(<i>0x3</i)</li>
    </ul></li>
    </ul>

As you can see this works just fine.

But we still have something undesirable. You'll notice that the dispatch function `htmlize` needs to have this big `if...elif...else` statement that will just keep growing as we need to handle more and more types (including potentially custom types).

This will just get unwieldy, and not very flexible (every time someone creates a new type that has to have a special html representation they will need to go into the `htmlize` function and modify it.

So instead, we are going to try a more flexible approach using decorators.

The way we are going to approach this is to create a dispatcher function, and then separately "register" each type-specific function with the dispatcher.

First, we are going to create a decorator that will do something that may seem kind of silly - it is going to take the decorated function and store it in a dictionary, using a key consisting of the **type** `object`.

Then when the returned closure is called, the closure will call the function stored in that dictionary.

```python
def singledispatch(fn):
    registry = dict()
    registry[object] = fn
    
    def inner(arg):
        return registry[object](arg)

    return inner
```

```python
@singledispatch
def htmlizer(arg):
    return escape(str(arg))
```

```python
htmlizer('a < 10')
```

    'a &lt; 10'

Next, we are going to add some functions to that `registry` dictionary, and modify our inner function to choose the correct function from the registry, or pick a default based on the type of the argument:

```python
def singledispatch(fn):
    registry = dict()
    
    registry[object] = fn
    registry[int] = lambda arg: '{0}(<i>{1}</i)'.format(arg, str(hex(arg)))
    registry[float] = lambda arg: '{0:.2f}'.format(round(arg, 2))
    
    def inner(arg):
        fn = registry.get(type(arg), registry[object])
        return fn(arg)
    return inner
```

```python
@singledispatch
def htmlize(a):
    return escape(str(a))
```

```python
htmlize(10)
```

    '10(<i>0xa</i)'

```python
htmlize(3.1415)
```

    '3.14'

Now, we want a way to add the specialized functions to the `registry` dictionary from **outside** the `singledispatch` function - to do so we will create a parametrized decorator that will (1) take the type as a parameter, and (2) return a closure that will decorate the function associated with the type:

```python
def singledispatch(fn):
    registry = dict()
    
    registry[object] = fn
    
    def register(type_):
        def inner(fn):
            registry[type_] = fn
        return inner
        
    
    def decorator(arg):
        fn = registry.get(type(arg), registry[object])
        return fn(arg)
    
    return decorator
```

But of course this is not good enough - how do we get a hold of the `register` function from outside `singledispatch`? Remember, `singledispatch` is a decorator that returns the `decorated` closure, not the `register` closure.

We can do this by adding the `register` function as an **attribute** of the `decorated` function before we return it. 

While we're at it we're also going to:

* add the `registry` dictionary as an attribute as so we can look into it to see what it contains.

* add another function that given a type will return the function associated with that type (or the default function if the type is not found in the dictionary)

```python
def singledispatch(fn):
    registry = dict()
    
    registry[object] = fn
    
    def register(type_):
        def inner(fn):
            registry[type_] = fn
            return fn  # we do this so we can stack register decorators!
        return inner
   
    def decorator(arg):
        fn = registry.get(type(arg), registry[object])
        return fn(arg)
    
    def dispatch(type_):
        return registry.get(type_, registry[object])

    decorator.register = register
    decorator.registry = registry.keys()
    decorator.dispatch = dispatch
    return decorator
```

```python
@singledispatch
def htmlize(arg):
    return escape(str(arg))
```

And we can see that `htmlize` (that returned `inner`) function has an attribute called `register`:

```python
htmlize.register
```

    <function __main__.singledispatch.<locals>.register>

as well as that `registry` attribute that we put in just we could see what keys are in the `registry` dictionary:

```python
htmlize.registry
```

    dict_keys([<class 'object'>])

We can also ask it what function it is going to use for any specific type (currently we only have one registered, the default, for the most general `object` type):

```python
htmlize.dispatch(str)
```

    object

And you'll note that the extended scope of `register` and `dispatch` is the same as the extended scope of `htmlize`.

So now we can register some functions (it will store the function with associated data type in the `registry` dictionary):

```python
@htmlize.register(int)
def html_int(a):
    return '{0}(<i>{1}</i)'.format(a, str(hex(a)))
```

We can peek into the registered types:

```python
htmlize.registry
```

    dict_keys([<class 'object'>, <class 'int'>])

and we can ask the decorated `htmlize` function what function it is going to use for the `int` type:

```python
htmlize.dispatch(int)
```

    <function __main__.html_int>

and we can actually call it as well:

```python
htmlize(100)
```

    '100(<i>0x64</i)'

The huge advantage now is that we can keep registering new handlers from anywhere in our module, or even from outside our module!

```python
@htmlize.register(float)
def html_real(a):
    return '{0:.2f}'.format(round(a, 2))

@htmlize.register(str)
def html_str(s):
    return escape(s).replace('\n', '<br/>\n')

@htmlize.register(tuple)
@htmlize.register(list)
def html_list(l):
    items = ['<li>{0}</li>'.format(htmlize(item)) for item in l]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'

@htmlize.register(dict)
def html_dict(d):
    items = ['<li>{0}={1}</li>'.format(htmlize(k), htmlize(v)) for k, v in d.items()]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
```

```python
htmlize.registry
```

    dict_keys([<class 'object'>, <class 'int'>, <class 'float'>, <class 'str'>, <class 'list'>, <class 'tuple'>, <class 'dict'>])

```python
print(htmlize([1, 2, 3]))
```

    <ul>
    <li>1(<i>0x1</i)</li>
    <li>2(<i>0x2</i)</li>
    <li>3(<i>0x3</i)</li>
    </ul>

```python
print(htmlize((1, 2, 3)))
```

    <ul>
    <li>1(<i>0x1</i)</li>
    <li>2(<i>0x2</i)</li>
    <li>3(<i>0x3</i)</li>
    </ul>

```python
print(htmlize("""this
is a multi line string with
a < 10"""))
```

    this<br/>
    is a multi line string with<br/>
    a &lt; 10

Our single dispatch decorator works quite well - but it has some limitations. For example it cannot handle functions that take in more than one argument (in which case dispatching would be based on the type of the **first** argument), and we also are not allowing for types based on parent classes - for example, integers and booleans are both integral numbers - i.e. they both inherit from the Integral base class. Similarly lists and tuples are both more generic Sequence types. We'll see this in more detail when we get to the topic of abstract base classes (ABC's).

```python
from numbers import Integral
```

```python
isinstance(100, Integral)
```

    True

```python
isinstance(True, Integral)
```

    True

```python
isinstance(100.5, Integral)
```

    False

```python
type(100) is Integral
```

    False

```python
type(True) is Integral
```

    False

```python
(100).__class__
```

    int

```python
(True).__class__
```

    bool

The way we have implement our decorator, if we register an Integral generic function, it won't pick up either integers or Booleans.

We can certainly fix this shortcoming ourselves, but of course...

We can can use Python's built-in single dispatch support, in ...

you guessed it!

the `functools` module.

```python
from functools import singledispatch
from numbers import Integral
from collections.abc import Sequence
```

```python
@singledispatch
def htmlize(a):
    return escape(str(a))
```

The `singledispatch` returned closure has a few attributes we can use:
1. A `register` decorator (just like ours did)
2. A `registry` property that is the registry dictionary
3. A `dispatch` function that can be used to determine which registry key (registered type) it will use for the specified type.

```python
@htmlize.register(Integral)
def htmlize_int(a):
    return '{0}(<i>{1}</i)'.format(a, str(hex(a))) 
```

```python
htmlize.dispatch(int)
```

    <function __main__.htmlize_int>

```python
htmlize.dispatch(bool)
```

    <function __main__.htmlize_int>

```python
htmlize(100)
```

    '100(<i>0x64</i)'

```python
htmlize(True)
```

    'True(<i>0x1</i)'

```python
@htmlize.register(Sequence)
def html_sequence(l):
    items = ['<li>{0}</li>'.format(htmlize(item)) for item in l]
    return '<ul>\n' + '\n'.join(items) + '\n</ul>'
```

```python
htmlize.dispatch(list)
```

    <function __main__.html_sequence>

```python
htmlize.dispatch(tuple)
```

    <function __main__.html_sequence>

```python
htmlize.dispatch(str)
```

    <function __main__.html_sequence>

You'll note that a string is also a sequence type, hence our dispatcher will call the `html_sequence` function on a string.

In fact, at this point things would not even run properly.

If we were to call

`htmlize('abc')`

we'd get an infinite recursion!

The call to `htmlize` the string `abc` would treat it as a sequence, which would call `htmlize` character by character. But each character is itself just a string of length 1, so it will `htmlize` for that single character, which would treat it as a sequence, which would call `htmlize` for that single character again, and so on, in an infinite loop. 

```python
htmlize('abc')
```

    ---------------------------------------------------------------------------

    RecursionError                            Traceback (most recent call last)

    <ipython-input-57-d6479a8af936> in <module>()
    ----> 1 htmlize('abc')
    

    D:\Users\fbapt\Anaconda3\envs\deepdive\lib\functools.py in wrapper(*args, **kw)
        801 
        802     def wrapper(*args, **kw):
    --> 803         return dispatch(args[0].__class__)(*args, **kw)
        804 
        805     registry[object] = func


    <ipython-input-53-50c13b0d81b3> in html_sequence(l)
          1 @htmlize.register(Sequence)
          2 def html_sequence(l):
    ----> 3     items = ['<li>{0}</li>'.format(htmlize(item)) for item in l]
          4     return '<ul>\n' + '\n'.join(items) + '\n</ul>'


    <ipython-input-53-50c13b0d81b3> in <listcomp>(.0)
          1 @htmlize.register(Sequence)
          2 def html_sequence(l):
    ----> 3     items = ['<li>{0}</li>'.format(htmlize(item)) for item in l]
          4     return '<ul>\n' + '\n'.join(items) + '\n</ul>'


    ... last 3 frames repeated, from the frame below ...


    D:\Users\fbapt\Anaconda3\envs\deepdive\lib\functools.py in wrapper(*args, **kw)
        801 
        802     def wrapper(*args, **kw):
    --> 803         return dispatch(args[0].__class__)(*args, **kw)
        804 
        805     registry[object] = func

    RecursionError: maximum recursion depth exceeded

Instead, we are going to register a string handler specifically - that way we will avoid that problem entirely:

```python
@htmlize.register(str)
def html_str(s):
    return escape(s).replace('\n', '<br/>\n')
```

```python
htmlize.dispatch(str)
```

    <function __main__.html_str>

So, even though a string is both an `str` instance and in general a sequence type, the "closest" type will be picked by the dispatcher (again something our own implementation did not do).

This means, we have something for generic sequences, but something specific for more specialized strings.

```python
htmlize('abc')
```

    'abc'

We can do the same thing with sequences - right now `html_sequence` will be used for both lists and tuples. 

But suppose we want slightly different handling of tuples:

```python
@htmlize.register(tuple)
def html_tuple(t):
    items = [escape(str(item)) for item in t]
    return '({0})'.format(', '.join(items))
```

```python
htmlize.dispatch(list)
```

    <function __main__.html_sequence>

```python
htmlize.dispatch(tuple)
```

    <function __main__.html_tuple>

```python
print(htmlize(['a', 100, 3.14]))
```

    <ul>
    <li>a</li>
    <li>100(<i>0x64</i)</li>
    <li>3.14</li>
    </ul>

```python
print(htmlize(('a', 100, 3.14)))
```

    (a, 100, 3.14)

One thing of note is that we started our decoration with a `@singledispatch` decorator - you'll notice that no specific type was indicated here - and in fact this means the dispatcher will use the generic `object` type.

This means that any object type not specifically handled by our dispatcher will fall back on that `object` key - hence you can think of it as the default for the dispatcher.

```python
type(None)
```

    NoneType

```python
htmlize.dispatch(type(None))
```

    <function __main__.htmlize>

```python
type(1+1j)
```

    complex

```python
htmlize.dispatch(complex)
```

    <function __main__.htmlize>

```python
type(3)
```

    int

```python
htmlize.dispatch(int)
```

    <function __main__.htmlize_int>

Lastly, because the name of the individual specialized functions does not really matter to us (the dispatcher will pick the appropriate function), it is quite common for an underscore character ( \_ ) to be used for the function name - the memory address of each specialized function will be stored in the `registry` dictionary, and the function name does not matter - in fact we can even add lambdas to the registry.

```python
@singledispatch
def htmlize(a):
    return escape(str(a))
```

```python
@htmlize.register(int)
def _(a):
    return '{0}({1})'.format(a, str(hex(a)))
```

```python
@htmlize.register(str)
def _(s):
    return escape(s).replace('\n', '<br/>\n')
```

```python
htmlize.register(float)(lambda f: '{0:.2f}'.format(f))
```

    <function __main__.<lambda>>

```python
htmlize.registry
```

    mappingproxy({object: <function __main__.htmlize>,
                  int: <function __main__._>,
                  str: <function __main__._>,
                  float: <function __main__.<lambda>>})

But note that the `__main__._` function for `int` and `str` are not the same functions (even tough they have the same name):

```python
id(htmlize.registry[str])
```

    3104966916432

```python
id(htmlize.registry[int])
```

    3104967451784

And everything works as expected:

```python
htmlize(100)
```

    '100(0x64)'

```python
htmlize(3.1415)
```

    '3.14'

```python
print(htmlize("""this
is a multi-line string
a < 10"""))
```

    this<br/>
    is a multi-line string<br/>
    a &lt; 10

If this same name but different function thing has you confused, look at it this way:

```python
def my_func():
    print('my_func initial')
```

```python
id(my_func)
```

    3104966916296

```python
f = my_func
```

```python
id(f)
```

    3104966916296

So, `f` and `my_func` point to the same function in memory.

Let's go ahead and "redefine" the function `my_func`:

```python
def my_func():
    print('second my_func')
```

In fact, we did not "redefine" the previous `my_func`, it still exists in memory (and `f` still points to it). Instead we have re-assigned the function that `my_func` points to:

```python
id(my_func)
```

    3104966914800

But the original `my_func` is still around, and 'f' still has a reference to it:

```python
id(f)
```

    3104966916296

So, we can call each one:

```python
f()
```

    my_func initial

```python
my_func()
```

    second my_func

But the function `__name__` have the same value:

```python
f.__name__
```

    'my_func'

```python
my_func.__name__
```

    'my_func'

Just always keep in mind that labels point to something in memory, it is not the object itself. So in this case we have two distinct objects (functions) which happen to have the same name, but are two very different objects - `f` points to the first one we created, and `my_func` points to the second.

### 8. Tuples as Data Structures and Named Tuples
### 9. Modules, Packages and Namespaces
### 10. Extras

## Python 3: Deep Dive (Part 2 - Iteration, Generators)

### Introduction
### Sequence Types
### Project 1
### Iterables and Iterators
### Project 2
### Generators
### Project 3
### Iteration Tools
### Project 4
### Context Managers
### Project 5
### Generators as Coroutines
### Project 6

## Python 3: Deep Dive (Part 3 - Hash Maps)

### Introduction
### Associative Arrays
### Dictionaries
### Coding Exercises
### Sets
### Project 1
### Serialization and Deserialization
### Coding Exercises
### Specialized Dictionaries
### Coding Exercises

## Python 3: Deep Dive (Part 4 - OOP)

### Introduction
### Classes
### Project 1
### Polymorphism and Special Methods
### Project 2
### Single Inheritance
### Project 3
### Descriptors
### Project 4
### Enumerations
### Project 5
### Exceptions (Single Inheritance)
### Project 6


