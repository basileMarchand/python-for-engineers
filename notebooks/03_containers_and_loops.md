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

# Containers and loops

***Basile Marchand (Centre des Matériaux - Mines ParisTech/CNRS/Université PSL)***

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

## Containers --- because a variable is good but a big package is better

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### In practice - a variable containing other variables

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We have seen previously that we can easily define variables of type number, boolean or string with Python. This is good but it is far from being enough to automate tasks or to do numerical calculations. That's why we will now look at containers. As its name indicates, a container is a variable in which we will store a set of variables. For example, in order to store all the notes that you will have for the course project, I will need a list. 

We will see that there is not only one type of container in Python but several, in the Python that I will call basic they are four in number: 
* Tuples
* Lists
* Dictionaries
* Sets

In this course we will only be interested in the first three, the last one being of little interest for our applications. Of course, if several containers exist, it is because each one has its own particularities and limits that we will present.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Tuples 

This is the first Python container and probably the most used. You have already used it without realizing it. In english we could translate the notion of tuple to that of n-uplet. It is a set of values (homogeneous or not), that is to say that a tuple can store objects of different types. 

The syntax for defining a tuple is as follows: 

```python
tuple_name = (value1, value2, ..., valueN)
```

To access the value of a tuple you just have to use the **[]** operator with the index of the element you want to access between brackets.

> Caution :**
> In all Python containers the indices start at **zero** ! This means that to access the first element of a tuple you have to ask for the element with index 0.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
un_tuple = (10, "une_string", 1.e-5, False)
print(un_tuple[0])
print(un_tuple[1])
print(un_tuple[2])
print(un_tuple[3])
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

Subtuples can also be extracted by specifying **i:j:s** between brackets where: 
* **i** is the index of the first element we want to retrieve
* **j** is the index of the last element we want to retrieve __+1__ * **s** is the step between
* **s** is the step between each element that we extract

If you don't specify **i** by default Python takes i=0, if you don't specify j it takes j=tuple size and if you don't specify __s__ it takes __s=1__

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(un_tuple)
print(un_tuple[1:3])
print(un_tuple[:3])
print(un_tuple[2:])
print(un_tuple[::2])
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Finally, if you want to know the size of a tuple, just use the **len** command

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(un_tuple)
print(len(un_tuple))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

*Note*: we have not seen in this part how to modify a value in a tuple and this is normal because it is not possible. 
One of the particularities of tuples is that they are immutable variables, i.e. once defined it is no longer possible to modify them. The major interest that this can have is if you want to make sure that values will be constant throughout the execution of your code. 

To have variables that look like tuples but can be modified you have to use lists.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Lists

Lists are the second basic container that can be used in Python. Like tuples, they are a set of values (homogeneous or not) that can be modified later. The definition of a list in Python is very similar to the construction of a tuple except that brackets are used instead of parentheses.

```python
list_name = [value1, value2, ..., valueN]
```
Accessing the value of a list is done in the same way as for tuples, i.e. using the **[]** operators. And similarly, a sub-list can be retrieved using the **i:j:s** notation.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
une_liste = [10, "une_string", 1.e-05, False]
print(type(a_list))
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(a_list[0])
print(a_list[2])
print(a_list[2:])
print(a_list[::2])
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

To know the size of a list you just have to use the same command as for tuples, namely **len**

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(len(a_list))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Among the other actions that can be performed on lists and that can make life easier, there is the use of the **in** keyword that allows you to test if an element is in the list or not

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print( 3 in une_liste )
print( "une_string" in une_liste )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

To access the index of an element in a list, use the **index** command

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
une_liste.index("une_string")
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

We can also concatenate lists using the **+** operator. Remember that the sum of two lists does not return the term-by-term sum of the two lists but the concatenation.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
list_a = [1,2,3]
list_b = [4,5,6]
print( list_a + list_b )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Finally we will see how to modify the values within a list. To do this we use the **[]** operator again, but we follow it with an assignment operation, i.e. it is followed by a __=__ a value. We can also modify sublists using the **i:j:s** notation.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(a_list)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a_list[0] = -1
print(one_list)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
a_list[3] = [0,1]
print(one_list)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a_list[:2] = [0,1]
print(one_list)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

However you may have noticed that for now we have only changed the values in the list without changing its size. To add elements to a list by enlarging it you need to use the functions :
* append which adds an element to the end of the list 
* insert which adds an element at a given position

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(a_list)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
one_list.append( 10000 )
print(one_list)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
help(a_list.insert)
a_list.insert(2, "new_item")
print(a_list)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

And if you want to delete elements of a list you can use the **remove** command or the **del** keyword for delete.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
one_list.remove(1.e-5)
print(one_list)
 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
del une_liste[1]
print(a_list)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

**Caution :**
You have to be very careful with lists, when you copy a list if you don't do it in the right way you won't have the expected behavior and you will potentially take a long time to find the source of the problem. This "problem" is related to the fact that in Python everything is done by passing by reference, we will see later in the course what this means. 

Illustration:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
list_a = [1,2,3,4,5]
list_b = list_a ### We think of making a copy of list_a in list_b 
list_b[0] = 10
print(list_b)
print(list_a)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

We can see that the modification we made in list_b is also reflected in list_a. And this is quite normal, because if we look at the memory addresses of each of the variables list_a and list_b we see that they are identical.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(hex(id(liste_a)))
print(hex(id(liste_b)))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Why this strange behavior? Because for Python when you write 

```python
list_b = list_a
```

It includes, created for me, a variable named list_b pointing to the same memory area as list_a and so when you use the variable list_b you are actually accessing the same memory box as list_a. 

If you don't want this behavior, you have to be a little more explicit and do it like this:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
list_a = [1,2,3,4,5]
list_b = list_a.copy()
## or 
list_b = list_a[:]
list_b[0] = 10
print(list_b)
print(list_a)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Dictionaries

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We will now look at the last natively available container in Python that we are studying in this course, namely dictionaries. 

Dictionaries are quite different from lists and tuples in the sense that they are not ordered and there is no notion of index. The access to the elements is done with a key. Indeed Python dictionaries are based on doublets (key, value). Each key of a dictionary must be unique and of type **int** or **string**. The syntax to define a dictionary is the following: 

```python
un_dictionary = {key1: value, key2:value, ...}
```
Accessing the values of a dictionary is done by using the **[]** operator to which we provide the key of the element we want to retrieve.

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
un_dict = {"cle1": 1, "cle2": 2, 1035: False}
print(un_dict)
print(un_dict["cle1"])
print(un_dict[1035])
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

The interest of dictionaries is multiple and its applications are numerous. The modification of an element of the dictionary is done simply by making the considered element of an assignment operation with the new value.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(un_dict)
un_dict["cle1"] = 18
print(un_dict)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

If you want to add new entries to a dictionary the thing is very simple. It is enough to proceed as for the modification of a value since if the key which one gives does not exist it is automatically created.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(un_dict)
un_dict["new_key"] = "new_val
print(un_dict)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Finally to make life easier with dictionaries there are some tricks to know. For example to get the list of keys in the dictionary

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print( un_dict.keys() )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

To retrieve the set of values stored in the dictionary :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(un_dict.values())
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

And finally to get the set of key, value doublets in a list :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(un_dict.items())
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The use of these methods can be accompanied by the keyword **in** for example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
if "new_key" in un_dict.keys():
    print( un_dict["new_key"] )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### No more? No matrix-vectors a la Matlab ?

So we have just done the tour of the main containers available natively in Python. The question that you must certainly ask yourself is how I can do simulation with Python and therefore manage matrices, vectors, ... Indeed in native Python there is no notion of vectors or matrices as in Matlab which only manages that. 

But don't panic, because people have done the work. We will see later that Python has a number of additional modules and that among these modules there is Numpy which defines the notion of vector and matrix.

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

## Loops --- or how to take advantage of the computer's stupidity

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### What's the point?

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

A large part of computer programs requires the repetitive processing of data, usually stored in lists or tables. In order to do this processing it is necessary to have repetition commands available. Like all programming languages (to my knowledge) Python has two types of commands to repeat a set of instructions: 
* The **for** loop which allows you to repeat a set of instructions N times.
* The **while** loop which allows to repeat a set of statements as long as a certain condition is true.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### *for* loops

The loop, called *for* loop, allows to repeat an operation **N** times with N an integer known before entering the loop. It is therefore a suitable loop when you know in advance the number of times you must repeat the instruction block. 

The Python syntax of the for loop is as follows: 

```python
for i in un_iterable:
    instruction_1
    instruction_2
```

**Note:** the syntax of the for loop is similar to that of the *if*, i.e. the first line ends with the **:** character and then an indented statement block. 

You may notice that the first line involves what I call a **unitable**. These are Python objects that can be iterated on. You are not much further along, I know. In practice they are particular objects that allow you to go through all the elements contained automatically with the help of a *for* loop among others. In this course I will not go into detail about iterators, I will just give you a list of iterables that you can manipulate.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The first iterable, the simplest one, is a list. We can easily browse the elements of a list using the *for* loop. Indeed we can write the following code:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_list = [1,2,3,4,5]

for x in my_list:
    print(x)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The same thing is possible with a tuple of course.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_tuple = (1,2,3,4,5)
for x in my_tuple:
    print(x)
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

Sometimes we don't need to write a loop to go through the elements of a list but just to repeat a given operation N times, with N a positive integer. In this case you have to use the **range** command which will generate an iterable. The syntax of the range command is as follows: 
```python
range(A,B,S)
```

where the parameters are : 
* A : (int) the starting value of the iterable, by default A=0
* B : (int) the final value of the iterable __+1__, no default value
* S : (int) the step between two iterates, default S=1

For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
for i in range(0,5): ## S=1 implicitly
    print(i)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
for i in range(3): ## A=0, S=1 implicitly
    print(i)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
for i in range(0,10,2):
    print(i)
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

Then you could tell me why not use range(len(my_list)) to browse a list? Yes indeed it works as you can see below:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
for i in range(len(my_list)):
    print(my_list[i])
    
    
for x in my_list:
    print(x)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

But this syntax is not recommended at all, it is even to be proscribed for several reasons.
* It is heavy and ugly
* It is not optimized. That is, if len(my_list)>> 1 your code will be slow. 

If you do this to access both the value of your iterable and its index, Python has done everything for you. There is indeed the **enumerate** command whose syntax is the following: 

```python
for i,x in enumerate(un_iterable):
    statement
```
In practice this allows to write :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
for i,x in enumerate(my_list):
    print("my_list[{}] = {}".format(i,x))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

And finally if you want to browse several lists of the same size simultaneously there is also a trick, the **zip** command whose syntax is the following: 

```python
for x,y,z in zip(list_x, list_y, list_z):
    statement
```

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
list_x = [0,1,2,3,4]
list_y = [10,11,12,13,14]
list_z = [20,21,22,23,24]

for x,y,z in zip(list_x, list_y, list_z):
    print("x={}, y={}, z={}".format(x, y, z))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Of course it is possible to combine the **zip** and **enumerate** commands. However, be careful with the syntax (placing the parentheses to the left of the **in**).

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
for i,(x,y,z) in enumerate(zip(list_x, list_y, list_z)):
    print("{} => x={}, y={}, z={}".format(i, x, y, z))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### The keywords *break* and *continue*

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In the Python language there are two particular keywords intended to modify the behavior of a *for* (or *while* as we will see later) loop: 
* __break__ : which allows to interrupt a loop prematurely
* __continue__ : which allows to go to the next iteration without executing the code that follows the continue

Concretely the behavior of these two keywords is the following:

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
my_list = [1,2,3,4,5]

for x in my_list:
    if x == 3:
        break
    print("x = {}".format(x))
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
for x in my_list:
    if x == 3:
        continue
    print("x = {}".format(x))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### A special use of *for* --- The "comprehension lists"

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

The **for** keyword can also be used in a slightly different form to build what we call "comprehension lists". The idea is to define and fill a list in a single command line. The interest is of course to have a better designed code but also to have a syntax which is closer to the one used in mathematics. 

The Python syntax to define a comprehension list is the following: 

```python
list_name = [ expression(x) for x in iterable if condition(x) ]
```

The test with the `if condition(x)` is optional.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

For example, let's say I want to build the list defined by : 
$$ S = \left\lbrace x \in [0,10[ \;\; \backslash \;\; x^2 \;\; \right\rbrace $$
with a comprehension list this translates into the following code:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
the_list = [ x**2 for x in range(10) ]
print(the_list)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

And if we now want to add a condition, for example to build : 
$$ S = x \in [0,10[ ; x^2 < 30 ; $$
It is enough to write this in the following form:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
the_list = [ x**2 for x in range(10) if x**2 < 30 ]
print(the_list) 
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### The *while* loop

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The *while* loop allows in computer science to repeat a series of instructions as long as a certain condition (specified by the developer when writing the loop) is verified. Therefore the *while* loop is suitable when you don't know in advance how many times you will have to repeat the instruction block. A typical example are methods for solving minimization problems where the convergence loop must stop only when the solution is found. 

The Python syntax of the while loop is as follows:    
```python 
while condition:
    statement_1
    statement_2
```

The condition must necessarily be a boolean which will depend on what is done by the instructions. As long as this condition is true then the instructions are repeated and when the condition becomes false the loop stops.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
x = 1.1
n_iter = 0
while x<10:
    x = x**2
    n_iter +=1
    
print("There was {} ( => x={}) execution of the block before the condition became false".format(n_iter, x))
    
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Of course the condition to stop the *while* loop can be as complex as needed and call Python functions. For example

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_list = [100,]
i = 0
while len(my_list)<100 and my_list[i]>0.001:
    my_list.append( my_list[i] / (i+1) )
    i += 1
    
print("The loop is stopped for i={0} with my_list[{0}]={1}".format(i, my_list[i]))
print( "The list is {}".format(my_list))
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

In the same way as for lists, you can use the *break* keyword in a *while* loop to stop its execution prematurely.

```{code-cell} ipython3
---
slideshow:
  slide_type: skip
---
my_list = [100,]
i = 0
while len(my_list)<100 and my_list[i]>0.001:
    my_list.append( my_list[i] / (i+1) )
    i += 1
    if i>5: break
    
print("The loop is stopped for i={0} with my_list[{0}]={1}".format(i, my_list[i]))
print("The list is {}".format(my_list))
```
