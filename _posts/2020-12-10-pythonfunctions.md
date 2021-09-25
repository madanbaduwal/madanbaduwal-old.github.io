---
title: "Python functions"
date: 2020-12-10T00:00-00:00
last_modified_at: 2021-07-08T00:00:00-00:00
categories:
  - Python
permalink: /pythonfunctions/
classes: wide
excerpt : Learn all about the python functions. From basic what is function to advance decorator and generator.
header:
  og_image: /images/Python-Functions.jpg
  teaser: /images/Python-Functions.jpg
---

In this lessons, we'll learn about the basics of Python function. A function is a sequence of statements that performs some kind of task. We use functions to eliminate code duplication.

We will learn different types of function in these lessons as shown figure below:


| ![space-1.jpg](https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2018/01/Python-Functions.jpg) | 
|:--:| 
| *Type of Functions in Python : [Source](https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2018/01/Python-Functions.jpg)* |





Before starting the function we need to recall the function name, arguments, and parameters.


```python
def function_name(parameters):
  statement
  statement
  ...
  return value

return_value = function_name(arguments)
```



## Defining Function

We can define a function with the def keyword.
```python
def print_hello():
  print(f"Hello")

print_hello()

>>> Hello
```

### More on defining function

We can define a function with a variable number of arguments.

#### Default Argument Values

```python
# Defining function with default arguments
def sum(x , y=2, z=3):
  print(f"Sum of x, y, and z is:{x+y+z}")
```

Calling a function in different ways:

```python
# giving only the mendatory argument
sum(1)
>>> Sum of x, y, and z is:6
```

```python
# Giving one of the option arguments
sum(3,4)
>>> Sum of x, y, and z is:10
```
```python
# Giving all arguments
sum(3,4,5)
>>> Sum of x, y, and z is:12
```

Note1 : The default values are evaluated at the point of function defination in the defining scope, so that
```python
a = 10
# The default value for variable arg is set at the time of function definition
def function(arg=a):
  print(arg)

a = 15
function()
>>> 10
```

Note2: The default value is evaluated only once. This makes a difference when the default is a mutable object such as a list, dictionary, or instances of most classes. For example, the following function accumulates the arguments passed to it on subsequent calls:
```python
# The default value is evaluated only once but in the case of mutable(list, dictionary...) we can evaluate many times.
def append(a,L={}):
  L[a]=a
  return L

print(append(1))
print(append(2))
print(append(3))

>>> {1: 1}
>>> {1: 1, 2: 2}
>>> {1: 1, 2: 2, 3: 3}
```

* Note: Order matter while calling in a default argument values function.

#### Keyword Arguments

Functions can also be called using keyword arguments of the form kwarg=value. For instance, the following function:
```python
def add(x,y=2,z=3):
  print(f"Sum of x, y, and z is:{x+y+z}")
```

Calling a function in different ways:

```python
add(1)
>>> Sum of x, y, and z is:6
```

```python
add(x=2)
>>> Sum of x, y, and z is:7
```
```python
add(x=2,y=4)
>>> Sum of x, y, and z is:9
```
```python
add(1,2,3)
>>> Sum of x, y, and z is:6
```
```python
add(1,2,z=8)
>>> Sum of x, y, and z is:11
```

But some following calls are invalid:
```python
add()
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-33-d5d29de3ed94> in <module>()
----> 1 add()

TypeError: add() missing 1 required positional argument: 'x'
```
```python
add(x=1,2)
>>> File "<ipython-input-34-ea0ca97f0446>", line 1
    add(x=1,2)
           ^
SyntaxError: positional argument follows keyword argument
```
```python
add(5,x=2)
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-37-cf0a26e4ab05> in <module>()
----> 1 add(5,x=2)

TypeError: add() got multiple values for argument 'x'
```
```python
add(k=2)
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-38-4063630c747d> in <module>()
----> 1 add(k=2)

TypeError: add() got an unexpected keyword argument 'k'
```

#### Special parameters

Developer needs only look at the function definition to determine if items are passed by position, by position or keyword, or by keyword.

A function definition may look like:


```python
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```



where / and * are optional. If used, these symbols indicate the kind of parameter by how the arguments may be passed to the function: positional-only, positional-or-keyword, and keyword-only. Keyword parameters are also referred to as named parameters.

##### Positional-or-Keyword Arguments

If / and * are not present in the function definition, arguments may be passed to a function by position or by keyword.

##### Positional-Only Parameters

```python
def f(pos1, pos2, /):
      -----------    ----------     ----------
        |
         -- Positional only
```

```python
def pos_only_arg(arg,/):
  print(arg)
```

Note: poition only support 3.8

```python
pos_only_arg(1)
>>> 1

pos_only_arg(arg=1)
>>> Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: pos_only_arg() got an unexpected keyword argument 'arg'

```

##### Keyword-Only Parameters
```python
def kwd_only_arg(*, arg):
    print(arg)
```
```python
kwd_only_arg(3)
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-8-896c53ef896c> in <module>()
----> 1 kwd_only_arg(3)

TypeError: kwd_only_arg() takes 0 positional arguments but 1 was given
```
```python
kwd_only_arg(arg=3)
>>> 3
```

#### Arbitrary Argument 


Function can be call with an arbitrary number of arguments. 

##### Arbitrary Argument tuples

```python
def arbitrary_argument(*args):
  return args
```
```python
print(arbitrary_argument("hi","iam","madan"))

>>> ('hi', 'iam', 'madan')
```

Note: From above we can see that  arguments are wrapped up in a tuple (see Tuples and Sequences)

##### Arbitrary Argument lists

```python
def arbitrary_argument(*args):
  L = list(args)
  return L
```

```python
print(arbitrary_argument("hi","iam","madan"))
>>> ['hi', 'iam', 'madan']
```

##### Arbitrary Argument dictionaries

In the same fashion, dictionaries can deliver keyword arguments with the **-operator:
```python
def arbitrary_argument(**args):
  return args
```
```python
print(arbitrary_argument(hi="hi",iam="iam",Madan="Madan"))
>>> {'hi': 'hi', 'iam': 'iam', 'Madan': 'Madan'}

```

Note: for dictionary we need to pass "key":"value" into key="value" this formate.

#### Lambda Expressions 


Small anonymous functions can be created with the lambda keyword. 

* `lambda arguments : expression`

**Arguments:**

-Positional arguments

-Named arguments (sometimes called keyword arguments)

-Variable list of arguments (often referred to as varargs)

-Variable list of keyword arguments

-Keyword-only arguments

```python
lambda a,b:a+b
>>> <function __main__.<lambda>>

```

calling lambda function
```python
_(1,2) # Note _  call recent run things
>>> 3
```
```python
_ #last output value
>>> 3
```
```python
(lambda a,b:a*b)(2,3)# call lambda function
>>> 6
```
```python
divide = lambda a,b: a/b

divide(4,2) # calling lambda function
>>> 2.0
```

#### Recursion



We can make a function call itself. This is known as recursion.
```python
def facto(n):
  if n==1:
    return 1
  return n*facto(n-1) 
```
```python
facto(5)
>>> 120
```

How does it work?

We already know the return keyword return value.

first step:  value = 5*facto(4)

second step: value = 5* 4 * facto(3)

third step: value = 5* 4*  3 * facto(2)

fourth step: value = 5 * 4 * 3 * 2 *facto(1)

fifth step: value = 5 * 4 * 3 * 2 * 1

#### Decorators

Decorators are very powerful and useful tool in Python since it allows programmers to modify the behavior of function or class.
```python
def uppercase_decorator(function): # Pass function as an argument
    def wrapper():
        func = function()
        make_uppercase = func.upper()
        return make_uppercase # return function as value

    return wrapper # return function as value
```

Our decorator function takes a function as an argument, and we shall, therefore, define a function and pass it to our decorator.
```python
def say_hi():
    return 'hello there'

decorate = uppercase_decorator(say_hi)
decorate()
>>> HELLO THERE
```

However, Python provides a much easier way for us to apply decorators. We simply use the @ symbol before the function we'd like to decorate. 
```python
@uppercase_decorator
def say_hi():
    return 'hello there'

say_hi()
>>> HELLO THERE
```

#### Generator functions and yield

Consider this simple function which returns a range of numbers as a list:

```python
def my_list(n):
    i = 0
    l = []

    while i < n:
        l.append(i)
        i += 1

    return l
```

This function builds the full list of numbers and returns it. We can change this function into a generator function while preserving a very similar syntax, like this:
```python
def my_gen(n):
    i = 0

    while i < n:
        yield i  #  Yield le value return gardain , state retun garxa
        i += 1
```
```python
my_gen(3) 
>>> <generator object my_gen at 0x7f06035b3c50>

```

From above we can say that yield statement suspends function’s execution and sends a value back to the caller, but retains enough state to enable function to resume where it is left off. 
```python
g = my_gen(3)

print(type(g))

for x in g:
    print(x)
    
>>>  <class 'generator'>
0
1
2
```

How yield keyword work?

* After the yield statement is executed, execution of the function does not end – when the next value is requested from the generator, it will go back to the beginning of the function and execute it again.

* The yield keyword in python works like a return with the only
difference is that instead of returning a value, it gives back a generator object to the caller.


#### Documentation Strings
```python
def my_function():
    """Do nothing, but document it.          # First latter capital and end with period
                                             # Second line is blank if there is multiple line for documentation string.
     No, really, it doesn't do anything.     # Indentation determine by first line open quote
     """
    pass
```
```python
print(my_function.__doc__)

>>> Do nothing, but document it.         # first latter capital and end with period
                                            # second line is blank if there is multiple line for documentation string.
     No, really, it doesn't do anything.     # indentation determine by first line open quote
     
```
#### Callback Function

**What is a Callback Function?**

A callback is a function that is passed as an argument to other function. This other function is expected to call this callback function in its definition. The point at which other function calls our callback function depends on the requirement and nature of other function.

Callback Functions are generally used with asynchronous functions.

Example for Callback Function: Callback Function can be passed to a function to print out the size of file after the function reads given text file.

```python
def callbackFunc(s):
    print('Length of the text file is : ', s)

def printFileLength(path, callback):
    f = open(path, "r")
    length = len(f.read())
    f.close()
    callback(length)

```
```python
printFileLength("test.txt", callbackFunc)

>>> Output : Length of the text file is : 40
```

#### Function Annotations
```python
def bio(name: str, address: str='address')->str: # colon (:) paxiko annotation ho and -> paxiko return type janauna
  print("ANnotation",bio.__annotations__)   
  return 'and'+address
```
```python
bio(10)
>>> ANnotation {'name': <class 'str'>, 'address': <class 'str'>, 'return': <class 'str'>}
'andaddress'
```

# References

* [Readthedocs](https://python-textbok.readthedocs.io/en/1.0/)

* [Realpython](https://realpython.com/python3-object-oriented-programming/)
