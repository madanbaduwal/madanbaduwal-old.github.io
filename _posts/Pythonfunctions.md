---
jupyter:
  jupytext:
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.11.3
  kernelspec:
    display_name: Python 3
    name: python3
---

<!-- #region id="8Zd-VusP5pM-" -->
In this lessons, we'll learn about the basics of Python function. 
<!-- #endregion -->

<!-- #region id="CB9O_JhPxBEb" -->
#All about the Function in python
<!-- #endregion -->

<!-- #region id="pgYnhC8U6Inp" -->
A function is a sequence of statements that performs some kind of task. We use functions to eliminate code duplication.
<!-- #endregion -->

<!-- #region id="8nNJrZO6JvQ8" -->
We will learn different types of function in these lessons as shown figure below:
<!-- #endregion -->

<!-- #region id="EVTfa1AcFmn-" -->

| ![space-1.jpg](https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2018/01/Python-Functions.jpg) | 
|:--:| 
| *Type of Functions in Python : [Source](https://d2h0cx97tjks2p.cloudfront.net/blogs/wp-content/uploads/sites/2/2018/01/Python-Functions.jpg)* |



<!-- #endregion -->

<!-- #region id="VVOWd6j5xcC-" -->
Before starting the function we need to recall the function name, arguments, and parameters.


```
def function_name(parameters):
  statement
  statement
  ...
  return value

return_value = function_name(arguments)
```


<!-- #endregion -->

<!-- #region id="g979LMnra2cu" -->
## Defining Function
<!-- #endregion -->

<!-- #region id="5DfsPh2CCjo3" -->
We can define a function with the def keyword.
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="h8GXc1cJa8gL" outputId="4445895f-330b-4510-bb5c-13175062e3e8"
def print_hello():
  print(f"Hello")

print_hello()
```

<!-- #region id="2ugnfDOAeDns" -->
### More on defining function
<!-- #endregion -->

<!-- #region id="i71my2D0eooM" -->
We can define a function with a variable number of arguments.
<!-- #endregion -->

<!-- #region id="B5O1DmVMeqWK" -->
#### Default Argument Values
<!-- #endregion -->

```python id="rWU7ZK3_fc3t"
# Defining function with default arguments
def sum(x , y=2, z=3):
  print(f"Sum of x, y, and z is:{x+y+z}")
```

<!-- #region id="_B5LimG8i8hU" -->
Calling a function in different ways:



<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="xXGIOecHhcbq" outputId="fc6d1a2d-d63e-4977-f64b-5c705d942656"
# giving only the mendatory argument
sum(1)
```

```python colab={"base_uri": "https://localhost:8080/"} id="iRZGk2dYhE35" outputId="275cbf22-1e92-41be-ebaf-be2aca44afa0"
# Giving one of the option arguments
sum(3,4)
```

```python colab={"base_uri": "https://localhost:8080/"} id="oPGl6I7skCP8" outputId="b3c3acba-89d8-4a9f-b40c-99be62e1e92d"
# Giving all arguments
sum(3,4,5)
```

<!-- #region id="XGp7n3i_kSnI" -->
Note1 : The default values are evaluated at the point of function defination in the defining scope, so that
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="YqEst4YCkdwj" outputId="06859d0d-4aff-4397-d0f0-d00aec4056e8"
a = 10
# The default value for variable arg is set at the time of function definition
def function(arg=a):
  print(arg)

a = 15
function()
```

<!-- #region id="7EapxZvKlNsR" -->
Note2: The default value is evaluated only once. This makes a difference when the default is a mutable object such as a list, dictionary, or instances of most classes. For example, the following function accumulates the arguments passed to it on subsequent calls:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="yW4tuMEClV2Y" outputId="ff750ad5-531c-41de-f23f-6b4ae6262080"
# The default value is evaluated only once but in the case of mutable(list, dictionary...) we can evaluate many times.
def append(a,L={}):
  L[a]=a
  return L

print(append(1))
print(append(2))
print(append(3))
```

<!-- #region id="8O2yCnnyhKIg" -->
* Note: Order matter while calling in a default argument values function.
<!-- #endregion -->

<!-- #region id="nGBiD_xVoSfW" -->
#### Keyword Arguments
<!-- #endregion -->

<!-- #region id="OdKnQU6sqAqy" -->
Functions can also be called using keyword arguments of the form kwarg=value. For instance, the following function:
<!-- #endregion -->

```python id="gyNw2fS8qZtl"
def add(x,y=2,z=3):
  print(f"Sum of x, y, and z is:{x+y+z}")
```

<!-- #region id="6hVQtxKdrEEp" -->
Calling a function in different ways:

<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="A1LiTVjJrFeb" outputId="b7942b2e-4800-4853-cedb-ea1fbea0afe6"
add(1)
```

```python colab={"base_uri": "https://localhost:8080/"} id="GWouumQdraFr" outputId="97b47d4b-0989-4499-e150-b9da12620333"
add(x=2)
```

```python colab={"base_uri": "https://localhost:8080/"} id="tz2uD9rqtD5e" outputId="fc0b5e3a-086b-4b72-f260-c2822682de5f"
add(x=2,y=4)
```

```python colab={"base_uri": "https://localhost:8080/"} id="Ip8URNfbtKHb" outputId="f38d27db-bf7c-41c5-f6c7-cc40df10a5a3"
add(1,2,3)
```

```python colab={"base_uri": "https://localhost:8080/"} id="GDjA5RyctOyU" outputId="887fa248-c1f9-4640-9717-90cf47b833ab"
add(1,2,z=8)
```

<!-- #region id="XVLCm1IQtWN2" -->
But some following calls are invalid:
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 163} id="fqqP--ERtiyK" outputId="8c7efcde-f844-48c7-ffd8-96fff203d1e9"
add()
```

```python colab={"base_uri": "https://localhost:8080/", "height": 129} id="RdPGRGCItpWM" outputId="69140284-17e6-4553-98a4-c27826eabe30"
add(x=1,2)
```

```python colab={"base_uri": "https://localhost:8080/", "height": 163} id="Q1buEYJotwLm" outputId="eb9cea54-da2a-4105-fd64-8f3fa0738d08"
add(5,x=2)
```

```python colab={"base_uri": "https://localhost:8080/", "height": 163} id="wML5Qs8RuBRp" outputId="d3babaf8-b666-4c63-bab0-896fb7219378"
add(k=2)
```

<!-- #region id="mmsDr_pgu_G1" -->
#### Special parameters
<!-- #endregion -->

<!-- #region id="KOYt_Uej0e88" -->
Developer needs only look at the function definition to determine if items are passed by position, by position or keyword, or by keyword.
<!-- #endregion -->

<!-- #region id="vu5QjMhL4I9g" -->
A function definition may look like:


```
def f(pos1, pos2, /, pos_or_kwd, *, kwd1, kwd2):
      -----------    ----------     ----------
        |             |                  |
        |        Positional or keyword   |
        |                                - Keyword only
         -- Positional only
```


<!-- #endregion -->

<!-- #region id="y3eXZdq-4oRc" -->
where / and * are optional. If used, these symbols indicate the kind of parameter by how the arguments may be passed to the function: positional-only, positional-or-keyword, and keyword-only. Keyword parameters are also referred to as named parameters.
<!-- #endregion -->

<!-- #region id="--lxFD0G43OK" -->
##### Positional-or-Keyword Arguments
<!-- #endregion -->

<!-- #region id="W4CPDrF_5Ctl" -->
If / and * are not present in the function definition, arguments may be passed to a function by position or by keyword.
<!-- #endregion -->

<!-- #region id="W_ULHFJD5zDV" -->
##### Positional-Only Parameters
<!-- #endregion -->

<!-- #region id="K-Q7FQUr5-NL" -->
```
def f(pos1, pos2, /):
      -----------    ----------     ----------
        |
         -- Positional only
```
<!-- #endregion -->

<!-- #region id="uGYMTijHE8lr" -->


```
# This is formatted as code
```


<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 129} id="ZCPi4VzH6J1x" outputId="98c72c2d-6570-4cdb-a06a-0cda644c87eb"
def pos_only_arg(arg,/):
  print(arg)
```

<!-- #region id="vpkzrNdGCm0Y" -->
Note: poition only support 3.8
<!-- #endregion -->

<!-- #region id="Y-ciLl3mYhh7" -->
```
>>> pos_only_arg(1)
1

>>> pos_only_arg(arg=1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: pos_only_arg() got an unexpected keyword argument 'arg'

```
<!-- #endregion -->

<!-- #region id="2JBtXG5PXLvj" -->
##### Keyword-Only Parameters
<!-- #endregion -->

```python id="qy0Hk0BOYb0E"
def kwd_only_arg(*, arg):
    print(arg)
```

```python colab={"base_uri": "https://localhost:8080/", "height": 197} id="lTKBz3mMYy5s" outputId="6bbee308-602f-4b58-b0d3-dcb4e9eb3314"
kwd_only_arg(3)
```

```python colab={"base_uri": "https://localhost:8080/"} id="GqSyT7bHY4Fb" outputId="74845dd8-6a70-4c0d-f2af-52695b66ccce"
kwd_only_arg(arg=3)
```

<!-- #region id="0zFzA4PoZHmV" -->
#### Arbitrary Argument 

<!-- #endregion -->

<!-- #region id="FacO-o93bclW" -->
Function can be call with an arbitrary number of arguments. 
<!-- #endregion -->

<!-- #region id="LcD3rQd-i4fF" -->
##### Arbitrary Argument tuples
<!-- #endregion -->

```python id="gghfDMEXcSSf"
def arbitrary_argument(*args):
  return args
```

```python colab={"base_uri": "https://localhost:8080/"} id="gSmnVn5ycYDl" outputId="cb18ca87-c945-409f-cae7-3f28849f771e"
print(arbitrary_argument("hi","iam","madan"))
```

<!-- #region id="oiKnHbWjc5Ky" -->
Note: From above we can see that  arguments are wrapped up in a tuple (see Tuples and Sequences)
<!-- #endregion -->

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
```

<!-- #region id="r-t5oDBFDMvr" -->
calling lambda function
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="2Kg0qsocDOZQ" outputId="43ddce58-09bb-4120-fc57-87a7ea6f2813"
_(1,2) # Note _  call recent run things
```

```python colab={"base_uri": "https://localhost:8080/", "height": 35} id="yrZXWc58DtaQ" outputId="d01c5501-2f2c-48af-e251-77549d2a77ab"
_ #last output value
```

```python colab={"base_uri": "https://localhost:8080/"} id="5J6IXq_0Dzof" outputId="9e690298-6815-4c16-a4bf-279595d46446"
(lambda a,b:a*b)(2,3)# call lambda function
```

```python colab={"base_uri": "https://localhost:8080/"} id="TTXrSAfrD-Ok" outputId="ac87a7dd-955c-4dea-f9eb-eb17b0172464"
divide = lambda a,b: a/b

divide(4,2) # calling lambda function
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
```

<!-- #region id="sPDPsu8N9VsY" -->
However, Python provides a much easier way for us to apply decorators. We simply use the @ symbol before the function we'd like to decorate. 
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/", "height": 35} id="cNGETaP_9W8l" outputId="fbeea845-b18c-406d-d366-95dcdf07cded"
@uppercase_decorator
def say_hi():
    return 'hello there'

say_hi()
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
```

<!-- #region id="_xITGSDwMGfI" -->
From above we can say that yield statement suspends function’s execution and sends a value back to the caller, but retains enough state to enable function to resume where it is left off. 
<!-- #endregion -->

```python colab={"base_uri": "https://localhost:8080/"} id="IQA8KjLY8Ea5" outputId="71661c1b-0edd-4e04-d01e-375c563fcac3"
g = my_gen(3)

print(type(g))

for x in g:
    print(x)
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
```

<!-- #region id="a_Pc2D_c46FK" -->
# References

* https://python-textbok.readthedocs.io/en/1.0/

* https://realpython.com/python3-object-oriented-programming/


<!-- #endregion -->
