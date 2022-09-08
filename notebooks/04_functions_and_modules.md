---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.1
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

# Functions and modules

**Basile Marchand (Centre des Matériaux - Mines ParisTech/CNRS/Université PSL)**

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

## Let's organize this!

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Organize your code in functions

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In the previous parts we have seen how to manipulate basic Python objects, how to repeat operations, etc ... However you have seen with the different exercises (I guess) your Python files tend to become a bit messy and you can quickly get confused. Moreover, as we have seen in the part about loops, a big part of a computer program consists in repeating a series of instructions a lot of times. The ideal way to have a clear and easily exploitable code is to divide the different series of instructions into functions and this is what we will do.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### What is a function?

In mathematics we define a function $f$ as an application which to an input $x$ living in a certain space $x\in E$ associates an output $y$ living in a certain space $y\in V$. 

$$ x \rightarrow y = f(x) $$

Well, in computer science it is the same thing, the only difference is in the vocabulary. Indeed we can define a function `f` in computer science as being an instruction which has an argument `x` of a certain type (int, float, list, dict, ...) and an output `y` of a certain type.   

```python
y = f(x)
```

In the same way, just as there are functions of several variables in mathematics, computer functions can also take several arguments as input. 

```python
y = f(x,y,z)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

How do you define functions in Python ? It's very simple, it's done with the `def` statement. The syntax is the following: 

```python
def function_name(arg1, arg2, ..., argN):
    instruction_1
    instruction_2
    ret = ...
    return ret
```

For example if we want to define the function `sum` taking as input a list and returning the sum of its elements we can write :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
## Function definition 
def sum(my_list):
    s = 0
    for x in my_list:
        s += x
    return s

a_list = [ x+100 for x in range(10) ]
the_sum = sum( a_list ) ## Call the function 
print("the_sum = {}".format(the_sum))
print("the_sum = {}")
print(f "the_sum = { the_sum}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

__Many remarks :__
* You must distinguish between the phase of *defining the function* (part of the code where you define the function by specifying the series of instructions that it will perform) and the phase of *calling the function* (part of the code where you execute the series of instructions contained in the function). 
* The name of the `my_list` argument in the function definition is completely independent of the variable name I give when I call the function. The name `my_list` only serves as an identifier to manipulate my input variable within the function

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Writing a function with several variables follows the same logic as above. For example, if we want to implement a function `mean_ponderee` we can proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def weight_average( values, weightings ):
    s = 0
    s_w = 0
    for x, w in zip(values, weightings):
        s += w*x
        s_w += w
    return s/s_w

scores = [12,9,17,15]
weight = [1, 2, 2, 3]

s = weighted_average(notes, weight)
print("The weighted average is: {}".format(s))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Function and variable the same thing or not?

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
mean_weight = weight_average
s_bis = mean_weight(grades, weight)
print("The weighted average is: {}".format(s_bis))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We get the same result because if we look at the memory address of the functions, they are the same in both cases.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print("""Address of mean_weight : {}
Address of mean_weight: {}
""".format(hex(id(mean_ponderee)), hex(id(mean_weight))))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

So functions and variables have common aspects, so this implies that you can also pass a function as an argument to another function!!!

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def square(x):
    return x*x


def for_each(func, iterable):
    res = []
    for x in iterable:
        res.append( func(x) )

    return res

inp = [ x**0.5 for x in range(10) ]
inp2 = for_each( square, inp )
print(inp)
print(inp2)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

A question you may or may not be asking yourself is what to do if I want the function I'm defining to return multiple variables as output? The answer is simple, you just have to return a tuple in which you store the different variables you want to retrieve. For example, if in the previous example I want to retrieve the result list and its size (no interest you may say), I just have to modify the `for_each` function as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def for_each2(func, iterable):
    res = []
    for x in iterable:
        res.append( func(x) )

    return res, len(res)

inp = [ x**0.5 for x in range(4) ]
out = for_each2( square, inp )
print(out[0])
print(out[1])
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Now you want to tell me it's not necessarily practical to have to manipulate a tuple afterwards. And I can only agree with you and even add that it harms the readability of the code. 
But don't worry because Python is quite well thought out. Indeed you can automatically split a tuple into several variables as soon as you exit the function. You just have to call the function as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
ret, size = for_each2(square, inp)
print("list = {} size = {}".format(ret, size))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

However **careful** the number of variable must be consistent between what is in the `return` of the function and what you put to the left of the `=` when calling the function. If this is not the case, Python will interpret this as an error

+++ {"slideshow": {"slide_type": "fragment"}}

```python 
>>> ret, size, variable_in_trop = for_each2(square, inp)
---------------------------------------------------------------------------
ValueError Traceback (most recent call last)
<ipython-input-52-ae3d4eb02d50> in <module>()
----> 1 ret, size, variable_in_trop = for_each2(square, inp)

ValueError: not enough values to unpack (expected 3, got 2)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

In the same spirit, we can ask ourselves what to do if we want to define a function with arguments having default values. To do this, you simply have to give a value to the arguments in question when defining the function. For example if we want to create a function `increment` which by default increments a number by **1** but can also increment it by another value specified by the user, we just have to proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def increment(x, incr=1):    
    return x+incr

a = 1
print(increment(a))
print(increment(a, 100))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

**Warning:** syntax rule
Arguments with default values must necessarily be placed last when defining the function. For example the following syntax is wrong :

+++ {"slideshow": {"slide_type": "fragment"}}

```python
>>> def increment_error(incr=1, x):
>>> return x+incr
    
def incremente_error(incr=1, x):
SyntaxError: non-default argument follows default argument

```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

When you have multiple arguments with default values, the rule for calling the function when you want to specify one or more arguments at a value other than its default value is as follows:
> The values of the arguments must be given in the same order as the one established for the function definition   
**or**  
> The argument values must be preceded by the name of the argument followed by the **=** symbol

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def formula(x, a=1, b=0):
    return a*x + b

# If we specify all arguments 

print( formula( 1.876, 10., 2.) )
# or 
print( formula( 1.876, a=10., b=2.) )

# Partial specification 
print( formula( 1.876, 2.) )
print( formula( 1.876, b=2.) )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

To finish with the subject of functions, there is only one point left to discuss, namely how to define functions taking a variable number of arguments. Indeed it can be useful sometimes to define such functions. To do this there is a first solution, which does not require any particular syntax and which is to define your function as taking as input a tuple in which before calling your function you will put all your arguments. This would give for example :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def function_arg_variable( args ):
    print("The function is called with {} arguments that have values {}".format( len(args), args))
    
one_variable = 1
an_other = False
yet_an_other = [1,2,3]
func_args = (one_variable, one_other, one_other_)
function_arg_variable( func_args )
func_args_2 = (one_variable, another_variable)
function_arg_variable( func_args_2 )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

You could then tell me that yes it does the expected work but it's still not very practical because you have to define by hand a tuple before each call of the function. And you would be right to tell me that. That's why there is in Python the `*args` syntax which will allow us to have the same behavior as before while doing without the step of defining a tuple. If we take the previous example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def function_arg_variable_star( *args ):
    print("The function is called with {} arguments that have {} values".format( len(args), args))
    
one_variable = 1
an_other = False
again_an_other = [1,2,3]
### We call directly the function with the arguments
### without creating a tuple
function_arg_variable_star( one_variable, one_other, one_other_ again )
function_arg_variable_star( one_variable, another_variable )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Finally there is another way to define a function with a variable number of arguments : the `**kwargs` syntax. This second syntax solves a problem associated with `*args` which is that when calling a function defined using `*args` it is necessary to give the arguments in the direction provided in the definition of the function so that the latter has the expected behavior. Illustration:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def function_args(exponent, *args):
    """ The function is implemented such that :
        exponent -> a float 
        args[1] -> a boolean 
        args[2:] -> floats 
    """
    if len(args) < 1:
        return exponent**exponent
    if args[0] is True:
        s = 0
        for x in args[1:]:
            s += x**exponent
        return s
    else:
        s=0
        for x in args[1:]:
            s += x**(1./exponent)
        return s

### Call the function with only positional argument
print( function_args(2.) )
### Call the function with all arguments (in the right direction so correct behavior)
print( function_args(2., True, 1.,2.,3.,4.) )
### Call the function with all the arguments (the first two are inverted so the behavior is incorrect)
print( function_args(True, 2., 1.,2.,3.,4.) )
    
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The use of the `kwargs` syntax is as illustrated below:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def function_arg_variable_names( **kwargs ):
    print("The function is called with {} arguments that have values {}".format( len(kwargs), kwargs))
    print("kwargs is of type : {}".format(type(kwargs)))
    
one_variable = 1
an_other = False
again_an_other = [1,2,3]
### We call directly the function with the arguments
### without creating a tuple
function_arg_variable_names( my_arg_1=one_variable, my_arg_2=another, my_arg_3=another)
function_arg_variable_nommes( my_arg_1=a_variable, my_arg_3=also_an_other )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We can then see that the object `kwargs` is a dictionary whose keys are in fact the names given to the variables when the function is called.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Anonymous functions

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

There is in fact a second way to define functions in Python, it is called anonymous functions or lambda functions. The syntax for defining these anonymous functions is as follows: 

```python
my_anonymous_function = lambda arg1, arg2, arg3: return_value
```

It can be seen that the syntax is relatively different from that of the keyword `def`. The use of this type of function is the definition of short functions and essentially mathematical functions. We can see that with this syntax we are very close to what we could write on a paper.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

For example, if we program the function `rms` (for Root Mean Square) of three variables which is expressed mathematically as :
$$ rms(x,y,z) = \left( \frac{1}{3} \left[ x^2 + y^2 + z^2 \right] \right)^{\frac{1}{2}} $$

we can write an anonymous function:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
rms = lambda x,y,z: (1./3. * (x**2+y**2+z**2) )**(1./2.)

print(rms(1,2,1))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### The scope of variables 

To finish this presentation of the syntax and the rules for defining a function in Python we will see what we call the scope of variables. First of all we can see in the following example that a variable defined in a function is only usable within the function. To the outside world it does not exist.

+++ {"slideshow": {"slide_type": "subslide"}}

```python

>>> def add_2(a):
>>> b = 2 ### The variable b is created in the function 
>>> c = a + b
>>> print( "c = {}".format(c) )
    
>>> one_value = 1.

>>> add_2( one_value )

c = 3.0

>>> print( b ) ### Error : outside the function b does not exist

---------------------------------------------------------------------------
NameError Traceback (most recent call last)
<ipython-input-53-7c321ed8f944> in <module>()
      9 add_2( a_value )
     10 
---> 11 print( b ) ### Error: outside the function b does not exist

NameError: name 'b' is not defined

```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The following example illustrates the fact that within a function, Python sees the set of variables being defined in the statement block calling the function in question.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def add_3(a):
    c = a + d
    print("c = {}".format(c))
    
a_value = 1
```

+++ {"slideshow": {"slide_type": "fragment"}}

```python 
    
>>> add_3(one_value)

---------------------------------------------------------------------------
NameError Traceback (most recent call last)
<ipython-input-54-43a5a1054963> in <module>()
      4 
      5 one_value = 1
----> 6 add_3(one_value)

<ipython-input-54-43a5a1054963> in add_3(a)
      1 def add_3(a):
----> 2 c = a + d
      3 print("c = {}".format(c))
      4 
      5 one_value = 1

NameError: name 'd' is not defined

```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

If we define outside the code the variable `d` before the call to the `add_3` function, we can see that there is no more error during the execution of the code.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
d = 10
add_3(one_value)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

On the other hand Python cannot modify the value associated with variables defined outside the function. It can only see them in read-only mode. In the following example we can see that trying to modify `e` gives an error when executing the code.

+++ {"slideshow": {"slide_type": "fragment"}}

```python 

def add_4(a):
    c = a + e
    print("c = {}".format(c))
    e = 0


e = 10
add_4(a_value)
print(e)

---------------------------------------------------------------------------
UnboundLocalError Traceback (most recent call last)
<ipython-input-56-703da7c8669b> in <module>()
      6 
      7 e = 10
----> 8 add_4(one_value)
      9 print(e)

<ipython-input-56-703da7c8669b> in add_4(a)
      1 def add_4(a):
----> 2 c = a + e
      3 print("c = {}".format(c))
      4 e = 0
      5 

UnboundLocalError: local variable 'e' referenced before assignment

```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

> **Note:** 
> There is a `global` keyword in Python which allows you to override the variable scope rules presented above. We won't talk about the `global` operation here because its use is strongly discouraged because it generates messy codes, very complicated to maintain and evolve and especially with a potentially unpredictable behavior.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Let's go further and arrange the functions

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

So we have just seen how we can organize our code into functions in order to have a simple and reusable program. For small single-use codes this is quite sufficient. On the other hand you can easily imagine that for a complex program with many functions it is necessary to push further the organization and the architecture of the code. 

To go further in the organization of the code the idea is to arrange your functions in files. Moreover the principle is to make an "integrated" distribution of your functions by category. For example a file for all the calculation/data processing functions, a file for all the output writing functions, a file for all the display and visualization functions, etc.

To distribute your functions in files is very simple. You just have to create a file with the extension `.py` and put inside it the definitions of your functions. 

> **Warning :** 
> For the naming of your files there are some rules to respect. First of all it is absolutely forbidden to use spaces and special characters (é, è, à, !, ?, ...) in your file names. 
> Secondly, the PEP8 convention recommends naming files with a name starting with a lower case letter. 


For example, let's create a file `myFunctions.py` in which we will store a number of Python functions.

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
%%file mesFonctions.py

##### File: mesFonctions.py 

def function_calcul():
    return None


##### end of file test.py 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
!ls 
!cat mesFonctions.py
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Now the question we can ask ourselves is how do we tell Python that there is a `myFunctions.py` file containing a set of functions that I want to use in my main program? The answer is simple, just use the `import` keyword. The `import` keyword has four modes of use: 

The first one is the syntax below. In this case it is necessary to specify the name `myFunctions` each time you want to use a function contained in the `myFunctions.py` file 

```python 
import myFunctions
...
myFunctions.aFunctionFromFile( args )
```

The second possible syntax is directly related to the fact that in general a developer is lazy and tries to write as few characters as possible. For this reason we can rename the function modules. 

```python 
import mesFunctions as mf
...
mf.aFileFunction( args )
```

The third syntax allows us to specify at import time which functions we are going to use, and thus only load those functions. 

```python 
from myFunctions import oneFileFunction, oneOtherFunction
...
aFileFunction( args )
...
anOtherFunction( args2 )
```

Finally, the last possible syntax is the one that allows you to import all the functions contained in a file and use them afterwards without needing to put the file prefix in front. 
```python 
from myFunctions import *
...
aFunctionFromFile( args )
...
anOtherFunction( args2 )

```

> **Caution:** although the last mode of use may seem convenient it is a bad idea to use it. A simple example is if in two files there is a function with the same name but not doing the same thing. If you use the syntax `from ... import *` then one of the two functions will be overwritten by the other and therefore inaccessible.

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

In order to use the `import` keyword without problems, you have to be careful where the `mesFunctions.py` file is located in relation to the main file, i.e. the one where the `import` line is written.

If the two files are side by side there is no problem, the `import` will run smoothly (provided there is no syntax error in the `mesFunction.py` file. 

On the other hand, if the `myFunctions.py` file is not in the same folder as the `main_script.py` file, if you do nothing the `import` will fail. Indeed you have to help Python to find the `myFunctions.py` file if it is not located next to it. To do this it is necessary to extend the `PYTHONPATH`.

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

Under Linux or Mac OS a simple way to extend the PYTHONPATH is to use environment variables. To do this, type the following command line in a console:

```bash
export PYTHONPATH=/path/to/folder:$PYTHONPATH
```

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

Another, perhaps easier solution, is to extend your PATH within your main Python program. This is done as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
import sys

sys.path.append("/path/to/folder/")
```

+++ {"lang": "en", "slideshow": {"slide_type": "slide"}}

## Python modules

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### What is a module and where to find them ?

We have seen in the previous part that we can distribute Python code in files. So of course people started to do that and to redistribute their code on the Internet and this way modules were born. So a module is a set of additional features that you can import into a Python code, using the `import` command. And so over the years a huge library of Open Source modules has been developed thanks to a very active Python user community. 

Among all the available modules it is necessary to distinguish two categories: 
* The modules of the standard Python library, it is a restricted set installed by default with Python whatever your installation. 
* Other modules which are not available by default and need to be installed for you to use them.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### The standard Python library

The standard Python library gathers more than 100 modules of all kinds, to have the list of available modules you can go on the official site of [Python](https://docs.python.org/3/library/index.html). Of course we will not talk about all of them, especially since many of them will not be useful to us. We will only focus on the few modules of the standard library that can be used in everyday life.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

___The math and cmath modules___.

The first module that will most likely be useful to you one day is the `math` module. As its name indicates it is a module defining a certain number of mathematical functions. The loading of this module is of course done with the `import` command following one of the 4 syntaxes presented in the previous section. 

Among the functions defined there are `sin`, `cos`, `log`, `exp` and many others. For an exhaustive list of functions contained in the `math` module you can : 
* go to https://docs.python.org/3/library/math.html
* type `help(math)` in a Python or Notebook prompt. 

```python 
import math
help(math)
```

The `math` module also defines a number of mathematical constants:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
import math
print("math.pi : {}".format(math.pi))
print("math.e : {}".format(math.e))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

There is a variant of the `math` module dedicated to the treatment of complex numbers, it is the `cmath` module.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

___The os___ module

The `os` module allows to interact with the computer's operating system. The great thing about this module is that it has been designed so that no matter what operating system you use (Windows, Mac OS or Linux) the functions of the module are the same (although at a lower level this is not the case at all). This makes it possible to design programs that are cross-platform. Among the useful functions of the module there are among others: 

* `os.listdir` which allows you to list all the files/folders in a directory. 
* `os.isdir` which allows to test if the given path is a folder or not.
* `os.mkdir` which allows to create a folder
* and many others ...

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Among the useful features available in the `os` module there are those related to path management. To use these features you need to load the `os.path` submodule. Why bother with file paths you may ask. It is always for reasons of compatibility between operating systems. Indeed on Linux and Mac OS (based on a Linux) the file/folder paths are of the form `/here/here/a/path`. While on Windows the paths are of the form `C:\a\path\in\windows`. The most used function of the `os.path` module is the `join` function. Below is an example of its use.

```{code-cell} ipython3
---
lang: en
slideshow:
  slide_type: fragment
---
import os.path

un_path = os.path.join("part_1", "part_2")

print( un_path )

path, file = os.path.split("/one/path/to/one_file.txt")
print(path)
print(file)
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

### And many other things

This is only a very brief review of all the possibilities offered by the standard Python library. I strongly invite you, if you are curious of course, to have a look at [https://docs.python.org/3/library/](https://docs.python.org/3/library/) to have a more global vision of the possibilities offered by the language. You will find there modules for graphical interfaces, for setting up a tcp server, for managing input arguments of a program, ....
