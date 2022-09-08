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

+++ {"lang": "en", "slideshow": {"slide_type": "slide"}}

**Programming Course** - ***Master 1 PSL - Science et Génie des Matériaux / Énergie*** 

---------------

# Variables and control structures

**Basile Marchand (Centre des Matériaux- Mines ParisTech / CNRS / PSL University)**

<div>
<a href="https://twitter.com/BasileMarchand?ref_src=twsrc%5Etfw" class="twitter-follow-button" data-size="large" data-text="Follow me on Twitter" data-show-count="false">Follow @BasileMarchand</a><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

## Define and manipulate variables

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

### Concretely, what is a variable?

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

In general, in computer science, a variable is a symbol associated with a value. The value in question can be of any type. Depending on the programming language considered, a variable can be typed (i.e. when it is declared it has an immutable type) or not (i.e. the value associated with the variable can change its type during the execution of the program). Python is a non-typed programming language. In other words if you declare a variable A that contains a string you can later in the program associate it with a number instead for example.

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

The Python language, compared to low level languages such as C, greatly simplifies the manipulation of variables. Indeed, to create a variable, we usually distinguish the declaration operation from the assignment operation. Typically in C++ the first step is to declare a variable A with its type. And in a second step using the `=` operator we assign to this variable a value of the corresponding type. For example to define an integer in C++ :   
```c
int value;
value = 1;
```

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

In Python the declaration step is included in the assignment. Indeed since variables are not typed in Python they can't be declared in advance. In all rigor this is possible but is strictly useless given the internal mechanisms of the language.

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

The question we can then ask ourselves is where the value associated with the variable is actually located in the computer? In a file? 

No, it is located in the RAM memory. How it works: 

When in a Python code we create a variable A associated to a value of a certain type (floating number for example) the mechanism of the language will automatically ask the computer to give it a box in the memory (the size of the box depends on the type of the value we want to store). The Python language then retrieves a pointer to the allocated memory slot (a memory address) and associates the variable to be manipulated with this memory address. 
The Python language is called high level because of this process of creating variables in memory which is automated and transparent for the user. Contrary to low level languages, like C or FORTRAN for example, where the programmer must explicitly ask for the allocation of a memory cell before storing a value.

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

*Tip:* to know the address in memory of a variable in Python you just have to do :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_variable = 12.4    # we define a variable named my_variable and we associate the value 12.4
hex(id(my_variable))  # request the memory address in hexadecimal
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

### How do you define a variable? Can we define everything as a variable?

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

In Python, as in a number of other languages, the assignment of a value to a variable (which in Python creates the variable if it does not exist) is done with the **=** symbol
The syntax for all types is the following: 

```python
variable_name = associated_value
```

For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
var1 = 1.3
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Note on variable naming: the **PEP8**

The naming of variables is an important element, whatever the programming language. Indeed a bad choice in the naming of variables does not affect the functioning of the code but it generates : 
* Programming errors.
* A code that is difficult to read and understand. 
* A code that is difficult to maintain and to evolve.

The first and most important point is therefore that variables must always be named in such a way that you know from the name what it refers to. 

There are "official" recommendations for Python concerning the naming of variables, it is the [PEP8](https://www.python.org/dev/peps/pep-0008/). 

Among the various recommendations contained in PEP8, the one concerning the naming of variables stipulates that : 

* Variable names begin with a lower case letter
* If the name consists of more than one word, the words are separated by **_**

```python
my_variable
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

*Tip:* to know the type of a variable just use

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
type(my_variable)
```

+++ {"lang": "en", "slideshow": {"slide_type": "slide"}}

## The basic types (so not the only ones possible)!

We will now review the different basic types available in Python. We will see later in the course that Python allows to define new additional types. We will also see that the use of modules makes it possible to handle other types such as matrices for example.

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

### Numbers: integers, floats and complexes

Like any computer language, Python allows the manipulation of numbers of all types, integers, floats and complexes. 

**Integers** are objects of type **int** (for integer).

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
un_entier = 127
## ou bien 
un_entier = int(127)

un_entier, un_autre = 128,25
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

All the usual operations addition, subtraction, multiplication, division and raising to the power are already defined and usable on integers.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

**Warning**: In Python 2.X the **/** division of two integers actually returns the integer division while in Python 3.X it is indeed a floating-point division.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
%%python2
a = 1 
b = 3
print("a/b = {}".format( a/b ))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The **real** are objects of type **float** for floating

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Floats are defined in Python following the same logic as integers, note that the comma is represented by a dot.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = 1.2387
## or 
a = float(1.2387)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We can also define $0.000123$ by $1.23 e^{-4}$ as follows

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
1.23e-4
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

As for integers, all the usual operations are defined and usable in Python

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = 1.24
b = 2.45

print(a+b) ## Addition
print(a-b) ## Subtraction
print(a*b) ## Multiplication
print(a/b) ## Division
print(a**b) ## a power b
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

When mixing types within expressions Python automatically takes care of converting the operands into the appropriate type. 

For example the sum of an integer and a float returns a float

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = 2
print(type(a))
b = 2.
print(type(b))
c = a + b
print(c)
print(type(c))

a = 0.1
b = 0.2
c=a+b
print(a)
print(b)
print(c)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The **complexes** are defined by a doublet of two numbers the real part and the imaginary part. In Python the definition of this doublet can be done in two different ways

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
## Using the "complex" constructor
un_complex = complex(1,1) # corresponds to 1+1i
## Use of the constant "j
un_complex = 1+1j
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

*Caution* : there is no __*__ operator between the 1 and the j if you try to put this operator in the definition of a complex it will lead to an error

+++ {"slideshow": {"slide_type": "fragment"}}

```python 
>>> x=1
>>> y=2
>>> c = x+y*j

---------------------------------------------------------------------------
NameError Traceback (most recent call last)
<ipython-input-26-b894b6a64e03> in <module>()
      1 x=1
      2 y=2
----> 3 c = x+y*j

NameError: name 'j' is not defined
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

*Tip: If you want to manipulate complexes involving variables without having to rewrite the **complex** command each time, the easiest way is to proceed as follows

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
i = 1j
x = 1
y = 2

c = x+i*y
print(c)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Of course the basic operations on complex numbers already exist in Python.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
c1 = 1+1j
c2 = 2+3.45j

print(c1+c2)
print(c1-c2)
print(c1*c2)
print(c1/c2)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

But there are also other specific operations available

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(c1.real) ## Real part
print(c1.imag) ## Imaginary part
print(c1.conjugate()) ## Conjugate of c1
print(abs(c1)) ## Module of c1
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Booleans

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

The **boolean** type is used in Python for writing logical expressions, tests. The boolean type can only take two values **True** or **False**.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
un_true = True
un_false = False
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In order to build logical expressions we have the following logical operators in Python: 
* Comparison operators (applicable to integers and floats): >,>=,<,<=,==,!=
* Connectors: and, or, not, == or is, in

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Below are some examples of logical expressions:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = 2.3
b = 10

print( a <= b)
print( a >= b)
print( (a <= b) is True )
print( (a <= b) == False )
print( (a <= b) or (a > b) )
print( ( (a <= b) or (a > b) ) and ( a>b ) )
print( not (b>10.))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Strings of characters

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

The last native type in Python is the **string** type for strings. Strings in Python can be defined in three different ways.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
une_string = "Hell World"
### or 
une_string = 'Hello World'
### or
une_string = """Hello World"""
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

These three definition methods all have an interest. The first one allows to define strings containing apostrophes. The second one allows to define strings containing quotation marks. The last one allows to keep the formatting of the string when displaying it with the **print** command for example

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
one_chain_without_formatting = "Hello everyone, how are you?"
print( one_chain_without_formatting )
one_chain_with_formatting = """Hello everyone, 
how are you? """
print( one_chain_with_formatting )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

*Note:* the last method of writing a string, based on triple quotes, also allows you to define comment blocks.

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

**String manipulation** {"lang": "en", "slideshow": {"slide_type": "subslide"}}

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We will now see how we can manipulate strings. This may seem secondary but for the processing of experimental data a large part of the work is the processing of files and thus of strings representing their contents. It is therefore essential to know how to process strings quickly and efficiently. Here are some elementary operations on strings.

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
string_a = "start"
string_b = "end"
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

*Concatenation of strings :*

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
res = string_a + string_b 
print(res)
res = string_a + " " + string_b
print(res)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

*Formatting a string:*

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_string = "A string with an integer {} a float {} and a boolean {}".format(1,2.34,False)
print( my_string )
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_string = "A string with an integer {2} a float {1} and a boolean {0}".format(False,2.34,1)
print( my_string )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Since Python 3.6 it is possible to format a string more concisely using the following syntax: 

```python 

f"a string {variable} and/or {python expression}"

```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
pi=3.14
print( f"pi={pi} and pi*pi={pi*pi}")
```

+++ {"slideshow": {"slide_type": "fragment"}}

And since Python 3.8 you can :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print( f"{pi=}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

*Find if a substring is in a string :*

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
sub_string = "ar"
print( sub_string in string_a )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

*Separate a string into a set of strings at a given character level:*

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
res = string_a + "_" + string_b
print(res)
after_split = res.split("_")
print(after_split)
print(after_split[0])
print(after_split[1])
```

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

_Join a list of strings with a given delimiter :_

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(after_split)
"-".join(after_split)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

*Know the size of a string*

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(string_a) 
len(string_a)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

*Extract a subpart (slice)*

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
string_a[1:3]
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
string_a[::2]
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

***Slicing in general***

In general, the syntax for extracting a slice is of the form:

    start:end:step
    

With by default : 

    start=0
    end=len(obj)
    step=1
    
    
> **Warning**  
> In the slice the value of `end` is **excluded**.

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

## Control structures

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Principle
The last point addressed in this first part is what is called in computer science the control structures. 
We have seen previously that we can easily write logical expressions about variables. What we have not seen for the moment is what the result of these logical expressions can be used for in the code and this is where the control structures come in. 
Indeed the interest of a computer program is generally to carry out a certain number of tasks/actions. But according to the input values of the program the actions to be performed are potentially not the same, so we need to set up logical expressions associated to the control structures in order to **direct** the program and the processing flow. 

Concretely, let's imagine that I make a program which, according to grades, tells me automatically if a student validates my module or if he has to go for a re-take. Once the grade has been calculated, I have to test if it is greater than or equal to 10 or if it is less than 10, because depending on the case, the program should not display the same message. This is what the use of control structures is all about.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### if ... elif ... else

In Python the only commands that allow you to direct the flow of a program are **if**, **elif** and **else**. Which you may have guessed can be translated as **if**, **if**, **if**. 


```python
if a_first_condition:
    action_associated_with_the_first_condition
elif another_condition:
    action_associated_with_the_second_condition
else:
    action_performed_by_default
```

Of course the syntax allows you to have as many **elif** as necessary, meaning from __0 to N__. You can only have one **else** and you must start with a **if**. The condition objects/variables must be of type *boolean* or *integer*. Indeed Python can assimilate an integer to a boolean according to the following rule if the integer is **0** it is associated to **False**, if it is different from 0 it is associated to **True**.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

> **Important** : syntax rule   
> You may have noticed it :
> * at the end of each line if, elif, else there is the character "**:**"
> * there is no keyword to specify the end of the control structure (no endif)
> the command lines located within the control structure (under the if, elif, else commands) are indented.  
>

This is a fundamental concept in Python, all instruction blocks start with the character "**:**" and are delimited by the indentation level of the code. For example: 
```python 
if une_condition:
    ## Start of statements executed if the condition "a_condition" is true
    a = 2
    print(a)
    b = 3
    print(b)
    ## End of the instructions contained in the if
### Resume the executed code whether we pass in the if or not
a = 234
b = a**3
print( b )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

By following this indentation rule it is quite possible to nest several blocks of if, elif, else statements within each other. For example: 

```python
if condition_1:
    if sub_condition_11:
        an_action
    elif sub_condition_12:
        an_other_action
    else:
        yet_an_other_action
elif condition_2:
    if sub_condition_21:
        pass
    elif:
        one_action
else:
    one_action
```    

You can see the keyword `pass` appearing. This keyword in fact serves no purpose, since it does not perform any action. Its only interest is to allow to respect the syntax rules. In the previous case it allows to define a **elif** block associated to a **if** block which does not perform any action.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

*Comment on the indentation :*  
For indentations in your code you can use :

* The tab key 
* An arbitrary number of spaces (usually 4)  

However, be careful not to mix tabs and spaces in your code, otherwise you will get an error when you run the code. Most text editors automatically replace tabs with 4 spaces. However, some editors under Windows in particular do not do this, which can lead to errors. The error message returned by Python is quite explicit and is of the form


```python
TabError : inconsistent use of tabs and spaces in indentation
```
