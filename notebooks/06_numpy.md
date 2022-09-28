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

```{code-cell} ipython3
---
slideshow:
  slide_type: skip
---
from IPython.display import set_matplotlib_formats
set_matplotlib_formats('svg')
```

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

**Programming Course** - ***Master 1 PSL - Science et Génie des Matériaux / Énergie*** 

---------------

# Introduction to Numpy

**Basile Marchand (Centre des Matériaux- Mines ParisTech / CNRS / PSL University)**

<div>
<a href="https://twitter.com/BasileMarchand?ref_src=twsrc%5Etfw" class="twitter-follow-button" data-size="large" data-text="Follow me on Twitter" data-show-count="false">Follow @BasileMarchand</a><script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

+++ {"lang": "en"}

## Numpy

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

NumPy is a Python module allowing to work with multidimensional arrays. Indeed Python does not have natively notions of arrays and therefore by extension even less notions of matrices. 

It is therefore necessary to use a particular module, which is not a module of the standard Python library. **The** recommended module for multidimensional array manipulation (including matrices) is **NumPy**. 

As a proof of the recognition of this module as well as of its performance it is worth mentioning that it is the module that is used in almost all other scientific modules available in Python. The secret of the NumPy module is that for performance reasons it is not developed in Python but in C++.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Of course the use of this module is done in the classic way: 

```python
import numpy
```

However, for simplicity's sake you will almost always see the import done by giving an alias to numpy :

```python
import numpy as np
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The basic object in NumPy, the one we will manipulate later, is the **np.ndarray**. An **np.ndarray** numpy is a multidimensional array of the same type (you can't mix integer, float and string in the same **np.ndarray** for example). We call *rank* of the **np.ndarray** the number of dimensions of the latter: 
* *rank of 1* : array with 1 dimension thus a line of M columns
* *rank of 2* : array with 2 dimension thus N lines and M columns
* *rank of 3* : array with three dimensions (a paving stone in space) 
* etc 

And the shape of the *array*, *shape* in English, is an N-tuple which characterizes the size of the array according to each of its dimensions. For example:
* A row vector of size **N** corresponds to an **array** with rank=1 and shape=(N,)
* A column vector of size **N** corresponds to an **array** with rank=2 and shape=(1,N)
* A rectangular matrix **NxM** corresponds to an **array** with rank=2 and shape=(N,M)
* A square hypermatrix **NxNxN** corresponds to an **array** with rank=3 and shape=(N,N,N)

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

### Creating an **array**

The definition of an `np.ndarray` from a set of values is done by using `np.array` in the following way:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
import numpy as np
a_matrix_3_3 = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(f"a 3x3 matrix : \n{a_matrix_3_3}")
a_vector_column = np.array([[1,], [2,], [3,]]) 
print(f"a column vector : \n{a_vector_column}")
a_vector_line = np.array([1,2,3])
print(f"a row vector : \n{a_vector_line}")
an_array_3_dimension = np.array( [[[1,2,3],[2,5,6]], [[11,12,13],[14,15,16]]])
print(f"a 3 dimensional array :\n{an_array_3_dimension}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

To know the rank and the shape of a NumPy **array** you just have to proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
shape = a_vector_column.shape 
rank = a_vector_column.ndim 
print("shape = {}".format(shape))
print("rank = {}".format(rank))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Moreover, to know the number of elements contained in a `np.array` you just have to access the size attribute of the latter. For example :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
nElement = a_vector_column.size
print(f"size = {nElement}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

In order to initialize an **array** NumPy has a number of functions to create arrays. 
* `np.zeros` which allows to create an array containing only zeros
* `np.zeros_like` which allows to build a matrix of zeros having the same shape as another matrix given as input.
* `np.ones` which creates an array containing only ones.
* `np.eye` which creates an identity array.
* `np.random.rand` which creates a matrix with random values.

Below are examples of how to use each of these functions.

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
print("np.zeros")
print(np.zeros((2,4)))
print("np.ones")
print(np.ones((5,1)))
print("np.zeros_like")
m = np.ones((2,3))
print(np.zeros_like(m))
print("np.eye")
print(np.eye(4))
print("np.random.rand")
print(np.random.rand(3,5))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### A word about `np.matrix`

There is an object of type `matrix` in numpy. At first sight it would be tempting to think that this is the ideal thing for target applications in pre-prep. Well no, it's a false good idea! Don't use `np.matrix` because it will only introduce weird bugs in the codes.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### A word about what C++ imposes on us behind numpy

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
array = np.random.rand(10)
print(f"array = {array}")
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array[0] = int(10)
print(f"array = {array}")
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
try:
    array[0] = "Hello"
except Exception as e: 
    print(e.args[0])
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

And yes the `np.array` are not like Python lists, they are homogeneous containers. You can't store values of different types in them, `numpy` will always try to convert what you give it into the array type.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

This behavior may seem strange, given the dynamically typed nature of Python ! But I remind you that NumPy is not developed in Python but in C++. But C++ is a statically typed language. This is the price to pay for performance! So each `np.ndarray` is associated with a type. To know the type of the elements you just have to access the `dtype` attribute. For example:

```{code-cell} ipython3
---
lang: fr
slideshow:
  slide_type: fragment
---
array.dtype
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

You can see that the type of values that can be contained in the array is `float64` which corresponds to a double precision float (coded on 64 bits). So all the elements that we want to put in the array will be converted to `float64`. If this conversion is not possible we get an error!

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

It is possible to change the type `np.ndarray` for that it is enough to use the method `astype`. For example if I want to convert the array `tableau` which contains only `float64` into an array containing `int32` it is enough to proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
arrayInt = array.astype(np.int32)
print(f"arrayInt = {arrayInt}")
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
arrayInt.dtype
```

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

Then you notice that most of the values become `0`. This is because converting a float64 to an integer is done by simply truncating!

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Of course it is possible when creating an `np.ndarray` to specify the type of element you want, which bypasses the type deduction mechanism of numpy. For example, if we create an array from a list containing only integers.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_no_type = np.array([1,2,3,4])
print(f"type = {array_no_type.dtype}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Numpy automatically deduces an `int64` type.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

But if I want to have `float64` how do I do it ? The stupid and nasty solution is to put dots in the list that I provide as input, for example :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_no_type = np.array([1.,2.,3.,4.])
array_no_type.dtype
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

By the way a remark, if I put only a dot in the list at the first element for example numpy will still consider `float64`. Because in the presence of a heterogeneous list NumPy will take the highest level type, in this case `float64`.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_no_type = np.array([1.,2,3,4])
array_no_type.dtype
```

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

The other slightly more elegant solution is to specify the type of the `np.ndarray` via the optional `dtype` argument of `np.array`. For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_typed = np.array([1,2,3,4], dtype=np.float64)
array_typed.dtype
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_typed[0] = 10.6
array_typed
```

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

### Mathematical operations and vectorization

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

NumPy allows you to create multidimensional arrays, as we have just seen. But once the table with data is created, it is necessary to be able to apply treatments to these data. Of course NumPy is there for that too!

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

To start with the basic operations `+`, `-`, `*`, `/` are all available in numpy.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

There are two cases to consider: 

1. Operation between two `np.ndarray` : **the operations are term to term, including for `*`**
2. Operation between an `np.ndarray` and a number

+++ {"slideshow": {"slide_type": "subslide"}}

For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = np.array([[1,2,3],[4,5,6]], dtype=np.float64)
b = np.array([[1,2,3],[4,5,6]], dtype=np.float64)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a + b 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a - b 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a * b
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a / b 
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

**Broadcasting** 

NumPy for basic operations has a behavior that may seem strange to you when the two `np.ndarray` do not have matching `shape`. This is called broadcasting! If I sum a `2,3` array and a `3,` array, logically we would say that it must not work. But in reality:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
c = np.array([1,2,3], dtype=np.float64)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(f"{a=}")
print(f"{c=}")
a + c
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Numpy has in effect replaced the array `c=np.array([1,2,3])` by `np.array([[1,2,3], [1,2,3]])`. This behavior works for all basic operations

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
a / c
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
d = np.array([[1.,], [2.,]])
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a + d
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

It is this `broadcasting` that also allows us to do the basic operations between an `np.ndarray` and a number. For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
2. * a 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
2 + a
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
2 / a 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a / 2. 
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

**The special case of the matrix product**

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

The question you are probably asking yourself is but can numpy do a matrix product as we teach it to our prep school students?

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Don't worry, the answer is YES ! It's just that the matrix product between two `np.ndarray` which would have the right sizes is not symbolized by the `*` operator but by `np.dot` or `@`.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = np.random.rand(4,2)
b = np.random.rand(2,5)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a @ b 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
np.dot(a, b)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

In the same way, to make a matrix-vector product, which is nothing else than the product of an array $Ntimes N$ by a matrix $Ntimes 1$, we proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
v = np.random.rand(2,1)

a@v
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

**The transpose of an array 

Another essential element of matrix calculation is the transpose. Of course, Numpy has foreseen everything. To compute the transpose of an `np.ndarray` you just have to proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a = np.random.rand(2,4)
a
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
b1 = a.T
b1
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
b2 = np.transpose(a)
b2 
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Beware the transpositon operation only applies to `np.ndarray` of rank greater than or equal to 2. For example the transpose of a "row vector" does not give a column vector :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
v = np.random.rand(4)
print(f"v = {v}")
vt = v.T
print(f"vt = {vt}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

### More complex operations

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Of course the operations `+`, `-`, `*`, `/` are not the only ones available. All classical mathematical functions are defined in numpy. 

* `np.cos`, `np.sin`, `np.tan`
* `np.arccos`, `np.arcsin`, `np.arctan`
* `np.degrees`, `np.radians`, `np.exp`, `np.arcsin`, `np.arctan`.
* `np.exp`, `np.log`

The interest of these functions, which all exist in the `math` module of Python, is that they are made to work on `np.ndarray`.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

For example if we evaluate the function $\sin x$.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In basic Python we would do something like this

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
import math
nStep = 100
x = [ 2*math.pi*i/nStep for i in range(nStep+1)]
y = [ math.sin(x_i) for x_i in x]

import matplotlib.pyplot as plt 
plt.plot(x,y)
plt.show()
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

While using NumPy we can directly write:

```{code-cell} ipython3
---
lang: en
slideshow:
  slide_type: fragment
---
xNumpy = np.linspace(0, 2*np.pi, nStep)
yNumpy = np.sin(xNumpy)
plt.plot(xNumpy,yNumpy)
plt.show()
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

There are two advantages to the Numpy approach: 

1. It is simpler to code and more pleasant to read afterwards 
2. It is much more powerful

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
%timeit [math.sin(x_i) for x_i in x]
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
%timeit np.sin(xNumpy)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

So there is a factor of 4 between the basic Python version and the NumPy version, and I can assure you that things get much worse when we move on to real problems!

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

You may wonder why it goes 4 times faster!? It's simply because on one side you do the loop in the Python world while on the other side the loop is done in the Numpy world so C++.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In the broad outline hidden behind all this is the fact that the numpy arrays are actually allocated in memory contiguously, it's `double*`. And so c++ does a great job of going through the entire array and applying a function to all the elements. Whereas Python has more trouble because it doesn't presuppose a memory alignment and therefore spends its time doing indirections.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

__The basic rule to remember is that when manipulating numpy arrays you should **never** make loops__.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

If you want to apply a "personal" function to an `np.ndarray` it is possible by using the `np.vectorize` function to vectorize your function.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
def my_function(x):
    if x < 0.5:
        return x 
    else:
        return -x
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Without vectorization you would have to do something like:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data = np.random.rand(10,20,30)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
%%timeit
for i,x in enumerate(data):
    for j, y in enumerate(x): 
        for k, z in enumerate(y): 
            data[i,j,k] = my_function(z)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Whereas if we vectorize the `my_function` function this not very nice triple loop comes down to something much nicer :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
my_function_vect = np.vectorize(my_function)

%timeit my_function_vect(data)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

So we observe a significant gain at runtime and most importantly the code is much more pleasant to read.

+++ {"slideshow": {"slide_type": "slide"}}

### Array manipulation

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

So far we have seen how to define `np.ndarray` and how to use these arrays to make more or less complex evaluations. This is good but it is not enough to cover 100% of the needs. In many cases we need to be able to access particular values of an array.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The manipulation of the NumPy `np.ndarray` and in particular the access to the values contained in the latter is done in the same spirit as the access to the elements of a list with the difference that one must specify for an `np.ndarray` several indexes since it is a multidimensional array. 

> **Attention :**  
> As for lists and tuples, the numbering of indices starts at **0**.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
an_array = np.array([[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15]])
print(f"The array :\n {an_array=}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Accessing the elements of an np.ndarray is done in the same way as accessing the values of a list, namely by using the `[]` operator. The subtlety is that the `[]` operator of an `np.ndarray` can take as input several indices.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a_12 = an_array[1,2]
print(f"Element 1,2 : {a_12}")
```

+++ {"lang": "en", "slideshow": {"slide_type": "fragment"}}

Negative indices can also be used to access values from the end:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
a_24 = an_array[-1,-1]
print(f"Element -1,-1 : {a_24}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

In addition, as for lists, we can use the concept of slicing. As a reminder, the notation is of the form : 

```
start:stop+1:step
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

For example, if I want to extract the first row of the matrix `a_table` we can proceed as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
line_0 = an_array[0,:]
print(f"Line_0 : {line_0}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

We can then use these notations to extract a subarray :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
sub_array = an_array[1:,1:]
print(sub_array)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
sub_array = an_array[0,:]
print(sub_array)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
sub_array = an_array[::2,::2]
print(sub_array)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The subarray we get then is a bit special it's called a view. What particularity? An example will speak for itself:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
an_array
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
sub_array
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
sub_array[0,0] = 10
sub_array
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
an_array
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

And here is the drama, or not, the sub-table being only a view when we modify a value in the view we modify the corresponding box in the original table.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

So be careful with sub-tables, it's very practical, and in terms of computational cost it allows you to make quite elegant optimizations, but on the other hand you must always keep in mind that you are working on a view.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

**A remark on the extraction of sub-table :**

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Thus it is possible to access a sub-table in this way. However, in many applications, it is necessary to have access to a sub-table, often discontinuous, only from a list of row and column indices. If we do this directly, we can see below that the extracted sub-table does not match.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
matrix_a = np.array([[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15]])
print("The complete matrix : \n{}".format(matrix_a))
idx_i = [0,2]
idx_j = [1,4]
sub_matrix = matrix_a[idx_i, idx_j]
print("The submatrix by the wrong approach : \n{}".format(sub_matrix))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

In order to get the desired result it is necessary to use the function `np.ix_`. This function allows to generate from two lists of indices, the **mask** of desired values.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
matrix_a = np.array([[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15]])
print(f"The complete matrix : \n{matrix_a}")
idx_i = [0,2]
idx_j = [1,4]

mask = np.ix_(idx_i, idx_j)
print(f"mask : {mask}")

sub_matrix = matrix_a[mask]
print("The submatrix by np.ix_ : \n{}".format(sub_matrix))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

So we have just seen that we can easily extract sub-tables but obviously with the help of this we can easily insert values by block within a table of greater dimension. For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
big_array = np.zeros((6,6))
little_array = np.eye(3)
print(f"Big array : \n{big_array}")
print(f"Little array : \n{little_array}")
big_array[3:,0:3] = little_array
print(f"Big array after insertion : \n{big_array}")
```

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
little_array = np.random.rand(2,2)
print(f"little_array = {little_array}")
big_array[np.ix_([1,3],[1,3])] = little_array
print(f"Big array after insertion: \n{big_array}")
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Among the other possible manipulations on the **array** NumPy there is the `reshape` operation which allows to change the shape of an array. For example:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_1 = np.array([[1,2,3],[4,5,6]])
print("Array before reshape {} : \n{}".format( array_1.shape, array_1))

array_2 = array_1.reshape((6,1))
print("Array after reshape {} : \n{}".format( array_2.shape, array_2))

array_3 = array_1.reshape((6,))
print("Array after reshape {} : \n{}".format( array_3.shape, array_3))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

> **Caution :**  
> For the reshape operation to work it is imperative that the total number of elements is preserved. That is to say that it is imperative that the product of the sizes following each of the dimensions is equal before and after the `reshape`.

> *Hint :*  
> For more simplicity you can leave one of the sizes free during the reshape operation. This size will be automatically deducted from the others in order to satisfy the condition of conservation of the number of elements. To do this, simply give a size of **-1** to the dimension left free.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
column_vector = array_1.reshape((-1,1))
print("After the reshape((-1,1)) : \n{}".format(column_vector))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

### Boolean operations and mask

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

A key concept of NumPy that allows us to avoid a `for` loop to process the data is the concept of mask. The latter is related to boolean operations.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

What is a `mask`? It is an array, a `np.ndarray` but it contains only booleans. This `mask` will then allow us to isolate parts of `np.ndarray` and thus apply different treatments to different elements of an array.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Because an example is always more meaningful than long sentences:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data = np.random.rand(10,3)
data
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

We can create a `mask` corresponding to values strictly less than `0.5`.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
mask = data < 0.5 
mask 
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

If we apply the `mask` to the data array then we only get the values for which the corresponding box in the `mask` is `True`.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data[ mask ]
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The interest is that we can then apply a particular treatment to these values. For example :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data[ mask ] = 0. 
data 
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

The construction of a mask can involve as many complex operations as you like. For example :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data = np.random.rand(10,3)
print(data)
mask_0_03 = np.logical_and(data > 0., data < 0.3) 
mask_0_03 
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data = np.random.rand(10,3)
print(data)
mask_inf03_or_sup07 = np.logical_or(data<0.3, data>0.7)
mask_inf03_or_sup07
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

And there is also the negation of a `mask

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print(mask_inf03_or_sup07)
np.logical_not(mask_inf03_or_sup07)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

### Reduction operation

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

We saw at the beginning that there are a number of mathematical functions defined in NumPy that allow you to process all the entries in an array simultaneously.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In a similar way you have at your disposal in NumPy some functions, called reduction functions, which allow you to calculate global quantities on an `np.ndarray`.

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

For example to calculate the average of a `np.ndarray` of rank 1. You might want to write :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
values = np.random.rand(10)
print(f"values = {values}")
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
m = 0
for x in values:
    m += x
m /= values.size
print(m)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

This is not optimal, NumPy provides you with the `np.mean` function which is used as follows:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
np.mean(values)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

In the same register here is a non-exhaustive list of reduction functions available in Python : 
    
* `np.sum`
* `np.min`
* `np.mean`
`np.std` * `np.var`

* `np.max`
* `np.min`
* `np.argmax`
* `np.argmin`    

The names are rather explicit

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

There is just a little subtlety to know with these reduction operations. Indeed they work on `np.ndarray` of any rank. For example :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data = np.random.rand(4,3)
data
```

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

If we then use the function `np.max` for example, as is this function will return the maximum value over the entire array.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
np.max(data)
```

+++ {"lang": "en", "slideshow": {"slide_type": "subslide"}}

But this may not be the behavior you want. For example you want the max of each column:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
np.max(data, axis=0)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

Or the max of each row :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
np.max(data, axis=1)
```

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

So you can see that with the `axis` argument you can control the behavior of the reduction functions so that they are not applied globally but more specifically.

+++ {"lang": "fr", "slideshow": {"slide_type": "slide"}}

### Linear algebra

In addition to the usual operations and Boolean operations NumPy implements a number of linear algebra functions. Indeed, since NumPy is the Python module for multi-dimensional arrays and thus in particular matrices and vectors, it was imperative to have these linear algebra functions. To use the linear algebra functions of NumPy, you have to use the sub-module `numpy.linalg`.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
import numpy.linalg as npl
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

First of all there are the functions `norm`, `cond` and `det`, which as their names suggest allow you to calculate the norm, the conditioning and the determinant of a 2-dimensional array respectively.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
array_2d = np.random.rand(5,5)
norm_array = npl.norm( array_2d )
cond_array = npl.cond( array_2d )
det_array = npl.det( array_2d )


print("A = \n{}".format(array_2d))
print("||A|| = {}".format(norm_array))
print("cond(A) = {}".format(cond_array))
print("det(A) = {}".format(det_array))
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Then there are all the methods for matrix decomposition and solving linear systems :
* `solve( A, b )` which finds the solution to the system $Acdot x = b$
* `inv( A )` which allows to calculate $A^{-1}$.
* `pinv( A )` which computes the pseudo-inverse of the matrix $A$.
* `svd` which computes the singular value decomposition of a matrix
* `eig( A )` which computes the eigenvalues and eigenvectors

```{code-cell} ipython3
---
slideshow:
  slide_type: subslide
---
rhs = np.random.rand(5,1)
print("rhs = \n{}".format(rhs))
x = npl.solve( array_2d, rhs )
print("Solution x = \n{}".format(x))
verif = array_2d @ x - rhs
print("A.x-rhs = \n{}".format(verif))
array_inv = npl.inv( array_2d )
verif = array_inv.dot( array_2d )
print("inv(A)*A = \n{}".format( verif ) )
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

### Input-output with NumPy

+++ {"lang": "fr", "slideshow": {"slide_type": "fragment"}}

In addition to providing functionality for creating and manipulating arrays and linear algebra, NumPy allows for simpler IO management for the user than is allowed in Python. 

Among the various IO functions that NumPy offers, the three that will certainly be most useful to you are : 
* `loadtxt` which allows you to load the contents of a text file (well formatted, for example a csv) directly as a NumPy array. 
* `savetxt` allows to save in a text file the content of a `array` numpy. 
* `genfromtxt` similar to `loadtxt` except that here the data file can contain holes, missing data, which will then be automatically replaced by a value specified by the user.

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

Here is an extract of a text file containing tensile test acquisition data.

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
!head data/curves/data.txt
```

+++ {"slideshow": {"slide_type": "subslide"}}

To load this data the first solution would be to parse the file by hand using `open`, `read` and finally the string method `split`. However, `numpy` provides the `loadtxt` method which offers more convenience. For example to load the previous data, it is done in one command:

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data_from_file = np.loadtxt("data/curves/data.txt", comments="#")
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print("Shape: {} ".format(data_from_file.shape))
print( data_from_file[:10,:])
```

+++ {"lang": "fr", "slideshow": {"slide_type": "subslide"}}

We notice that we have specified the optional argument `comments`, this allows us to tell NumPy which lines to ignore. If the first lines do not start with a specific character (comment character) it is still possible to ignore them with the optional argument `skiprosws` which allows to indicate the number to ignore at the beginning of the file. An equivalent use of `loadtxt` to the previous one would be :

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
data_from_file = np.loadtxt("data/curves/data.txt", skiprows=5)
```

```{code-cell} ipython3
---
slideshow:
  slide_type: fragment
---
print("Shape: {} ".format(data_from_file.shape))
print( data_from_file[:10,:])
```
