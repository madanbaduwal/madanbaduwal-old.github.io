---
title: "Python functions"
date: 2021-07-08T00:00-00:00
last_modified_at: 2021-07-08T00:00:00-00:00
permalink: /Python/
categories:
  - Python
permalink: /Python/
permalink: /Pythonfunctions/
classes: wide
excerpt: Python functions. 
---

In this lessons, we'll learn about the basics of Python function. 

# All about the Function in python

A function is a sequence of statements that performs some kind of task. We use functions to eliminate code duplication.

We will learn different types of function in these lessons as shown figure below:


| ![space-1.jpg](https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2018/01/Python-Functions.jpg) | 
|:--:| 
| *Type of Functions in Python : [Source](https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2018/01/Python-Functions.jpg)* |





Before starting the function we need to recall the function name, arguments, and parameters.


```
def function_name(parameters):
  statement
  statement
  ...
  return value

return_value = function_name(arguments)
```



## Defining Function

We can define a function with the def keyword.
```
def print_hello():
  print(f"Hello")

print_hello()

>>> Hello
```

### More on defining function

We can define a function with a variable number of arguments.

#### Default Argument Values

```
# Defining function with default arguments
def sum(x , y=2, z=3):
  print(f"Sum of x, y, and z is:{x+y+z}")
```

Calling a function in different ways:

```
# giving only the mendatory argument
sum(1)
>>> Sum of x, y, and z is:6
```

```
# Giving one of the option arguments
sum(3,4)
>>> Sum of x, y, and z is:10
```
```
# Giving all arguments
sum(3,4,5)
>>> Sum of x, y, and z is:12
```

Note1 : The default values are evaluated at the point of function defination in the defining scope, so that
```
a = 10
# The default value for variable arg is set at the time of function definition
def function(arg=a):
  print(arg)

a = 15
function()
>>> 10
```

Note2: The default value is evaluated only once. This makes a difference when the default is a mutable object such as a list, dictionary, or instances of most classes. For example, the following function accumulates the arguments passed to it on subsequent calls:
```
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
```
def add(x,y=2,z=3):
  print(f"Sum of x, y, and z is:{x+y+z}")
```

Calling a function in different ways:

```
add(1)
>>> Sum of x, y, and z is:6
```

```
add(x=2)
>>> Sum of x, y, and z is:7
```
```
add(x=2,y=4)
>>> Sum of x, y, and z is:9
```
```
add(1,2,3)
>>> Sum of x, y, and z is:6
```
```
add(1,2,z=8)
>>> Sum of x, y, and z is:11
```

But some following calls are invalid:
```
add()
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-33-d5d29de3ed94> in <module>()
----> 1 add()

TypeError: add() missing 1 required positional argument: 'x'
```
```
add(x=1,2)
>>> File "<ipython-input-34-ea0ca97f0446>", line 1
    add(x=1,2)
           ^
SyntaxError: positional argument follows keyword argument
```
```
add(5,x=2)
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-37-cf0a26e4ab05> in <module>()
----> 1 add(5,x=2)

TypeError: add() got multiple values for argument 'x'
```
```
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


```
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

```
def f(pos1, pos2, /):
      -----------    ----------     ----------
        |
         -- Positional only
```

```
def pos_only_arg(arg,/):
  print(arg)
```

Note: poition only support 3.8

```
pos_only_arg(1)
>>> 1

pos_only_arg(arg=1)
>>> Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: pos_only_arg() got an unexpected keyword argument 'arg'

```

##### Keyword-Only Parameters
```
def kwd_only_arg(*, arg):
    print(arg)
```
```
kwd_only_arg(3)
>>> -
TypeError                                 Traceback (most recent call last)
<ipython-input-8-896c53ef896c> in <module>()
----> 1 kwd_only_arg(3)

TypeError: kwd_only_arg() takes 0 positional arguments but 1 was given
```
```
kwd_only_arg(arg=3)
>>> 3
```

#### Arbitrary Argument 


Function can be call with an arbitrary number of arguments. 

##### Arbitrary Argument tuples

```
def arbitrary_argument(*args):
  return args
```
```
print(arbitrary_argument("hi","iam","madan"))

>>> ('hi', 'iam', 'madan')
```

Note: From above we can see that  arguments are wrapped up in a tuple (see Tuples and Sequences)

<!-- #region id="hFXd9vRTmSFx" -->
##### Arbitrary Argument lists
<!-- #endregion -->

```python id="vfufUwkJmUUb"
def arbitrary_argument(*args):
  L = list(args)
  return L
```

```python id="SNDEspDsmamJ" colab={"base_uri": "https://localhost:8080/"} outputId="d1984795-6e34-45b9-f55a-8ef23b5a32b0"
print(arbitrary_argument("hi","iam","madan"))
>>> ['hi', 'iam', 'madan']
```

<!-- #region id="N1xzf-PsjB5w" -->
##### Arbitrary Argument dictionaries
<!-- #endregion -->

<!-- #region id="GqIs7hfNiHL0" -->
In the same fashion, dictionaries can deliver keyword arguments with the **-operator:
<!-- #endregion -->

```python id="5A4_rWgmfBo6"
def arbitrary_argument(**args):
  return args
```

```python colab={"base_uri": "https://localhost:8080/"} id="ZGBo9UwdfLsm" outputId="a988aff5-f631-4839-a179-37f2fae0cc5d"
print(arbitrary_argument(hi="hi",iam="iam",Madan="Madan"))
>>> {'hi': 'hi', 'iam': 'iam', 'Madan': 'Madan'}

```

<!-- #region id="FjHOuuL6CZVW" -->
Note: for dictionary we need to pass "key":"value" into key="value" this formate.
<!-- #endregion -->

<!-- #region id="mqdUN3psp4H4" -->
#### Lambda Expressions 

<!-- #endregion -->

<!-- #region id="Ti4uXLvVve0z" -->
Small anonymous functions can be created with the lambda keyword. 

* `lambda arguments : expression`

**Arguments:**

-Positional arguments

-Named arguments (sometimes called keyword arguments)

-Variable list of arguments (often referred to as varargs)

-Variable list of keyword arguments

-Keyword-only arguments

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="MDakTa4bvf34" outputId="c2e7b166-a65b-4840-9b3b-89bcd8f03660"
lambda a,b:a+b
>>> <function __main__.<lambda>>

```

<!-- #region id="r-t5oDBFDMvr" -->
calling lambda function
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="2Kg0qsocDOZQ" outputId="43ddce58-09bb-4120-fc57-87a7ea6f2813"
_(1,2) # Note _  call recent run things
>>> 3
```

```python colab={"base_uri": "https://localhost:8080/", "height": 35} id="yrZXWc58DtaQ" outputId="d01c5501-2f2c-48af-e251-77549d2a77ab"
_ #last output value
>>> 3
```

```python colab={"base_uri": "https://localhost:8080/"} id="5J6IXq_0Dzof" outputId="9e690298-6815-4c16-a4bf-279595d46446"
(lambda a,b:a*b)(2,3)# call lambda function
>>> 6
```

```python colab={"base_uri": "https://localhost:8080/"} id="TTXrSAfrD-Ok" outputId="ac87a7dd-955c-4dea-f9eb-eb17b0172464"
divide = lambda a,b: a/b

divide(4,2) # calling lambda function
>>> 2.0
```

<!-- #region id="7zKWMUpL5d2l" -->
#### Recursion


<!-- #endregion -->

<!-- #region id="bZPMk9455qmH" -->
We can make a function call itself. This is known as recursion.
<!-- #endregion -->

```python id="e5A7GV3_Ephy"
def facto(n):
  if n==1:
    return 1
  return n*facto(n-1) 
```

```python colab={"base_uri": "https://localhost:8080/"} id="bMhYhcJKEt1b" outputId="14e724e9-55b3-488a-bee8-fa5cc9535442"
facto(5)
>>> 120
```

<!-- #region id="QOnaCVs7E6y_" -->
How does it work?

We already know the return keyword return value.

first step:  value = 5*facto(4)

second step: value = 5* 4 * facto(3)

third step: value = 5* 4*  3 * facto(2)

fourth step: value = 5 * 4 * 3 * 2 *facto(1)

fifth step: value = 5 * 4 * 3 * 2 * 1
<!-- #endregion -->

<!-- #region id="sq-aYXuw7Nl4" -->
#### Decorators
<!-- #endregion -->

<!-- #region id="Lr3kkh337TU2" -->
Decorators are very powerful and useful tool in Python since it allows programmers to modify the behavior of function or class.
<!-- #endregion -->

```python id="Gjl7ZmIC9AER"
def uppercase_decorator(function): # Pass function as an argument
    def wrapper():
        func = function()
        make_uppercase = func.upper()
        return make_uppercase # return function as value

    return wrapper # return function as value
```

<!-- #region id="IddoCMHf9Nbz" -->
Our decorator function takes a function as an argument, and we shall, therefore, define a function and pass it to our decorator.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 35} id="vNnoeLsd9EU1" outputId="46c3d033-7dd8-4e3e-bc8d-afc8fd907e5a"
def say_hi():
    return 'hello there'

decorate = uppercase_decorator(say_hi)
decorate()
>>> HELLO THERE
```

<!-- #region id="sPDPsu8N9VsY" -->
However, Python provides a much easier way for us to apply decorators. We simply use the @ symbol before the function we'd like to decorate. 
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 35} id="cNGETaP_9W8l" outputId="fbeea845-b18c-406d-d366-95dcdf07cded"
@uppercase_decorator
def say_hi():
    return 'hello there'

say_hi()
>>> HELLO THERE
```

<!-- #region id="7_mnf8lI7hqF" -->
#### Generator functions and yield
<!-- #endregion -->

<!-- #region id="l72V7ua47y7N" -->
Consider this simple function which returns a range of numbers as a list:

<!-- #endregion -->

```python id="TPjvLVsn7wPb"
def my_list(n):
    i = 0
    l = []

    while i < n:
        l.append(i)
        i += 1

    return l
```

<!-- #region id="ARb9JuEt75uC" -->
This function builds the full list of numbers and returns it. We can change this function into a generator function while preserving a very similar syntax, like this:
<!-- #endregion -->

```python id="wXhQMz3V77pF"
def my_gen(n):
    i = 0

    while i < n:
        yield i  #  Yield le value return gardain , state retun garxa
        i += 1
```

```python colab={"base_uri": "https://localhost:8080/"} id="wQ6rJOWzLry7" outputId="d314d267-95c2-4bb5-af9d-c270b0c523b4"
my_gen(3) 
>>> <generator object my_gen at 0x7f06035b3c50>

```

<!-- #region id="_xITGSDwMGfI" -->
From above we can say that yield statement suspends function’s execution and sends a value back to the caller, but retains enough state to enable function to resume where it is left off. 
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="IQA8KjLY8Ea5" outputId="71661c1b-0edd-4e04-d01e-375c563fcac3"
g = my_gen(3)

print(type(g))

for x in g:
    print(x)
    
>>>  <class 'generator'>
0
1
2
```

<!-- #region id="O8wEAri98Iy_" -->
How yield keyword work?

* After the yield statement is executed, execution of the function does not end – when the next value is requested from the generator, it will go back to the beginning of the function and execute it again.

* The yield keyword in python works like a return with the only
difference is that instead of returning a value, it gives back a generator object to the caller.

<!-- #endregion -->

<!-- #region id="zgamVWnISUIy" -->
#### Documentation Strings
<!-- #endregion -->

```python id="-GBSKSwkSbKa"
def my_function():
    """Do nothing, but document it.          # First latter capital and end with period
                                             # Second line is blank if there is multiple line for documentation string.
     No, really, it doesn't do anything.     # Indentation determine by first line open quote
     """
    pass
```

```python id="GG1_ft6WVSY8" colab={"base_uri": "https://localhost:8080/", "height": 85} outputId="6b6a00ad-99aa-4e1d-db53-447664095379"
print(my_function.__doc__)

>>> Do nothing, but document it.         # first latter capital and end with period
                                            # second line is blank if there is multiple line for documentation string.
     No, really, it doesn't do anything.     # indentation determine by first line open quote
     
```

<!-- #region id="AwC7z756XqtK" -->
#### Function Annotations
<!-- #endregion -->

```python id="3a-3RNHbXwBa"
def bio(name: str, address: str='address')->str: # colon (:) paxiko annotation ho and -> paxiko return type janauna
  print("ANnotation",bio.__annotations__)   
  return 'and'+address
```

```python id="ENjLAER_YR3-" colab={"base_uri": "https://localhost:8080/", "height": 52} outputId="19742e3e-bc71-44f4-b38a-85bfb06aebc9"
bio(10)
>>> ANnotation {'name': <class 'str'>, 'address': <class 'str'>, 'return': <class 'str'>}
'andaddress'
```

<!-- #region id="a_Pc2D_c46FK" -->
# References

* https://python-textbok.readthedocs.io/en/1.0/

* https://realpython.com/python3-object-oriented-programming/


<!-- #endregion -->
